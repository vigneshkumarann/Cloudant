---

copyright:
  years: 2017, 2018
lastupdated: "2018-10-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

<!-- Acrolinx: 2017-05-10 -->

# Configurando o {{site.data.keyword.cloudant_short_notm}} para recuperação de desastre de região cruzada

O [Guia de recuperação de desastre do {{site.data.keyword.cloudant_short_notm}}](disaster-recovery-and-backup.html)
explica que uma maneira de ativar a recuperação de desastre é usar
a replicação do {{site.data.keyword.cloudantfull}} para criar redundância entre as regiões.

É possível configurar a replicação no {{site.data.keyword.cloudant_short_notm}} usando uma topologia
ativa/ativa ou ativa/passiva entre os data centers.

O diagrama a seguir mostra uma configuração típica que
usa duas contas do {{site.data.keyword.cloudant_short_notm}},
uma em cada região:

![Exemplo de arquitetura ativa/ativa](../images/active-active.png)

É útil lembrar-se de que:

* Dentro de cada data center, o
{{site.data.keyword.cloudant_short_notm}} já oferece alta disponibilidade
ao armazenar dados em triplicidade nos três servidores.
* A replicação ocorre no banco de dados, em vez de no nível de conta
e deve ser configurada explicitamente.
* O {{site.data.keyword.cloudant_short_notm}} não fornece nenhum Acordo de Nível de Serviço (SLA)
ou certezas sobre a latência de replicação.
* O {{site.data.keyword.cloudant_short_notm}} não monitora as replicações individuais.
  É aconselhável sua própria estratégia para detectar replicações com falha e reiniciá-las.

## Antes de iniciar

> **Nota**: para uma implementação ativa/ativa,
uma estratégia para gerenciar conflitos deverá estar em vigor.
  Portanto, certifique-se de entender como a [replicação](../api/replication.html) e
os [conflitos](mvcc.html#distributed-databases-and-conflicts) funcionam
antes de considerar essa arquitetura.

Entre em contato com o [suporte do {{site.data.keyword.cloudant_short_notm}} ![Ícone de link externo](../images/launch-glyph.svg "Ícone de link externo")](mailto:support@cloudant.com){:new_window}
se precisar de ajuda com a modelagem de dados para manipular conflitos efetivamente.

## Visão geral

No material a seguir,
será criada uma replicação bidirecional.
Essa configuração permite que dois bancos de dados trabalhem em uma topologia ativa/ativa.

A configuração supõe que você tenha duas contas em regiões diferentes:

* `myaccount-dc1.cloudant.com`
* `myaccount-dc2.cloudant.com`

Quando essas contas estiverem em vigor,
as etapas básicas serão como a seguir:

1. [Criar](#step-1-create-your-databases) um par de bancos de dados peer dentro das contas.
2. [Configurar](#step-2-create-an-api-key-for-your-replications) chaves API
a serem usadas para as replicações entre esses bancos de dados.
3. Conceder permissões apropriadas.
4. Configurar replicações.
5. As replicações de teste estão funcionando conforme o esperado.
6. Configurar o aplicativo e a infraestrutura para uso ativo/ativo
ou ativo/passivo dos bancos de dados.

## Etapa 1: criar seus bancos de dados

[Crie os bancos de dados](../api/database.html#create) que desejar replicar
dentro de cada conta.

Neste exemplo,
um banco de dados chamado `mydb` é criado.

Os nomes usados para os bancos de dados nesse exemplo não são importantes,
mas usar o mesmo nome é mais adequado.

```sh
curl https://myaccount-dc1.cloudant.com/mydb -XPUT -u myaccount-dc1
curl https://myaccount-dc2.cloudant.com/mydb -XPUT -u myaccount-dc2
```
{:codeblock}

## Etapa 2: criar uma chave de API para suas replicações

É uma boa ideia usar uma [chave de API](../api/authorization.html#api-keys) para replicações contínuas.
A vantagem é que, se os detalhes de sua conta primária mudarem,
por exemplo, após uma reconfiguração de senha,
suas replicações poderão continuar inalteradas.

As chaves API não são ligadas a uma única conta.
Essa característica significa que uma única chave de API pode ser criada e,
em seguida, receber permissões adequadas do banco de dados para ambas as contas.

Por exemplo,
o comando a seguir solicita uma chave de API para a conta `myaccount-dc1`:

```sh
$ curl -XPOST https://myaccount-dc1.cloudant.com/_api/v2/api_keys -u myaccount-dc1
```
{:codeblock}

Uma resposta bem-sucedida será semelhante ao exemplo abreviado a seguir:

```json
{
  "password": "YPN...Tfi",
  "ok": true,
  "key": "ble...igl"
}
```
{:codeblock}

> **Nota**: observe atentamente a senha.
  Não será possível recuperar a senha mais tarde.

### Etapa 3: conceder permissão de acesso

[Forneça à chave de API permissão](../api/authorization.html#modifying-permissions)
para ler e gravar nos bancos de dados.

Se você também desejar replicar índices,
designe permissões de administrador.

Use o Painel do {{site.data.keyword.cloudant_short_notm}}
ou, como alternativa, veja as informações de [autorização](../api/authorization.html)
para obter detalhes sobre como conceder permissões programaticamente.

### Etapa 4: configurar replicações

As replicações no {{site.data.keyword.cloudant_short_notm}} são sempre unidirecionais:
de um banco de dados para outro banco de dados.
Portanto,
para replicar os dois modos entre dois bancos de dados,
são necessárias duas replicações,
uma para cada direção.

É criada uma replicação em cada conta,
que usa a Chave de API criada [anteriormente](#step-2-create-an-api-key-for-your-replications).

Primeiramente,
crie uma replicação do banco de dados `myaccount-dc1.cloudant.com/mydb` para
o banco de dados `myaccount-dc2.cloudant.com/mydb`.

```sh
curl -XPOST 'https://myaccount-dc1.cloudant.com/_replicator'
	-u myaccount-dc1
	-H 'Content-type: application/json'
	-d '{ "_id": "mydb-myaccount-dc1-to-myaccount-dc2",
	"source": "https://ble...igl:YPN...Tfi@myaccount-dc1.cloudant.com/mydb",
	"target": "https://ble...igl:YPN...Tfi@myaccount-dc2.cloudant.com/mydb",
	"continuous": true
}'
```
{:codeblock}

Em seguida,
crie uma replicação do banco de dados `myaccount-dc2.cloudant.com/mydb` para
o banco de dados `myaccount-dc1.cloudant.com/mydb`.

```sh
curl -XPOST 'https://myaccount-dc2.cloudant.com/_replicator'
	-u myaccount-dc2
	-H 'Content-type: application/json'
	-d '{ "_id": "mydb-myaccount-dc2-to-myaccount-dc1",
	"source": "https://ble...igl:YPN...Tfi@myaccount-dc2.cloudant.com/mydb",
	"target": "https://ble...igl:YPN...Tfi@myaccount-dc1.cloudant.com/mydb",
	"continuous": true
}'
```
{:codeblock}

> **Nota:** se essa etapa falhar porque o banco de dados `_replicator` não existe,
crie-o.

### Etapa 5: testar sua replicação

Teste os processos de replicação criando,
modificando
e excluindo documentos em um dos bancos de dados.

Após cada mudança em um banco de dados,
verifique se também será possível ver a mudança refletida no outro banco de dados.

### Etapa 6: configurar seu aplicativo

Neste ponto,
os bancos de dados são configurados para permanecer sincronizados entre si.

A próxima decisão é se os bancos de dados serão usados de uma
maneira [ativa/ativa](#active-active) ou [ativa/passiva](#active-passive).

#### Ativa/ativa

Em uma configuração ativa/ativa,
as diferentes instâncias de aplicativo podem gravar em
bancos de dados diferentes.

Por exemplo,
o aplicativo 'A' pode gravar no banco de dados `myaccount-dc1.cloudant.com/mydb`,
enquanto o aplicativo 'B' pode gravar no banco de dados `myaccount-dc2.cloudant.com/mydb`.

Essa configuração oferece vários benefícios:

- O carregamento pode ser difundido por várias contas.
- Os aplicativos podem ser configurados para acessar uma conta com
latência inferior (nem sempre a mais próxima geograficamente).

Um aplicativo pode ser configurado para se comunicar com a conta 'mais próxima'
do {{site.data.keyword.cloudant_short_notm}}.
Para aplicativos hospedados no DC1,
é apropriado configurar suas URLs do {{site.data.keyword.cloudant_short_notm}}
como `"https://myaccount-dc1.cloudant.com/mydb"`.
Da mesma forma,
para aplicativos que são hospedados no DC2,
você configuraria sua URL do {{site.data.keyword.cloudant_short_notm}} para `"https://myaccount-dc2.cloudant.com/mydb"`.

#### Ativa/Passiva

Em uma configuração ativa/passiva,
todas as instâncias de um aplicativo são configuradas para usar um banco de dados principal.
No entanto,
poderá ocorrer failover do aplicativo no outro banco de dados de backup,
se as circunstâncias o fizerem necessário.
O failover pode ser implementado dentro da lógica do aplicativo em si,
usando um balanceador de carga
ou usando algum outro meio.

Um teste simples de se um failover é necessário seria
usar o terminal do banco de dados principal como uma 'pulsação'.
Por exemplo,
uma simples solicitação `GET` enviada para o terminal de banco de dados principal normalmente retorna
[detalhes sobre o banco de dados](../api/database.html#getting-database-details).
Se nenhuma resposta for recebida,
isso pode indicar que um failover será necessário.

#### Outras configurações

É possível considerar outras abordagens híbridas para sua configuração.

Por exemplo,
em uma configuração 'Gravação principal, Réplica de leitura',
todas as gravações vão para um banco de dados,
mas a carga de leitura é difundida entre as réplicas.

### Etapa 7: próximas etapas

* Considere monitorar as [replicações](../api/advanced_replication.html) entre os bancos de dados.
  Use os dados para determinar se a sua configuração pode ser otimizada ainda mais.
*	Considere como seus documentos e índices de design são implementados e atualizados.
  Talvez você ache mais eficiente automatizar essas tarefas.

## Executando failover entre regiões do {{site.data.keyword.cloudant_short_notm}}

Em geral,
o processo de gerenciamento de um failover entre regiões ou data centers é manipulado mais alto dentro da pilha de aplicativos,
por exemplo, configurando mudanças de failover do servidor de aplicativos
ou balanceando a carga.

O {{site.data.keyword.cloudant_short_notm}} não fornece um recurso para você
gerenciar explicitamente qualquer failover ou rotear novamente solicitações entre as regiões.
Essa restrição é em parte por razões técnicas
e em parte porque as condições em que pode acontecer tendem a ser específicas do aplicativo.
Por exemplo,
talvez você queira forçar um failover em resposta a uma métrica de desempenho customizada.

No entanto,
se você decidir que realmente precisa de uma capacidade para gerenciar failover,
algumas opções possíveis incluirão:

* Coloque seu próprio [proxy HTTP na frente do {{site.data.keyword.cloudant_short_notm}} ![Ícone de link externo](../images/launch-glyph.svg "Ícone de link externo")](https://github.com/greenmangaming/cloudant-nginx){:new_window}.
  Configure seu aplicativo para falar com o proxy, em vez de com a instância do {{site.data.keyword.cloudant_short_notm}}.
  Essa configuração significa que a tarefa de mudar as instâncias do {{site.data.keyword.cloudant_short_notm}}
usadas pelos aplicativos pode ser manipulada por meio de uma modificação na configuração de proxy,
em vez de uma modificação nas configurações do aplicativo.
  Muitos proxies têm a capacidade de balancear a carga,
com base nas verificações de funcionamento definidas pelo usuário.
* Use um balanceador de carga global, como o [Diretor de tráfego ![Ícone de link externo](../images/launch-glyph.svg "Ícone de link externo")](http://dyn.com/traffic-director/){:new_window} para rotear para o {{site.data.keyword.cloudant_short_notm}}.
  Essa opção requer uma definição `CNAME` que roteie para
diferentes contas do {{site.data.keyword.cloudant_short_notm}},
com base em uma verificação de funcionamento ou uma regra de latência.

## Recuperando-se de failover

Se uma única instância do {{site.data.keyword.cloudant_short_notm}} estiver inacessível,
evite redirecionar tráfego de volta para ele assim que ele se tornar acessível novamente.
O motivo é a necessidade de algum tempo para tarefas intensivas,
como sincronizar o estado do banco de dados de quaisquer peers
e assegurar que os índices sejam atualizados.

É útil ter um mecanismo para monitorar essas tarefas
para ajudar a decidir quando um banco de dados estará em um estado adequado para atender seu tráfego de produção.

Como um guia,
uma lista típica de verificações a serem aplicadas inclui:

* [Replicações](#replications)
* [Índices](#indexes)

> **Nota:** se você implementar novo roteamento de solicitação ou de failover com base em um teste de funcionamento,
talvez desejará incorporar verificações correspondentes para evitar novo roteamento prematuro de volta para
uma instância de serviço que ainda está se recuperando.

### Replicações

* Tem alguma replicação em estado de erro?
* Alguma replicação precisa ser reiniciada?
* Quantas mudanças pendentes ainda estão esperando replicação no banco de dados?

Mais informações sobre o [status de replicação de monitoramento](../api/advanced_replication.html#replication-status)
estão disponíveis.

> **Nota:** se um banco de dados estiver sendo mudado continuamente,
é improvável que o status de replicação seja 0.
  Deve-se decidir qual limite de status é aceitável
ou que represente um estado de erro.

### Índices

* Os índices estão suficientemente atualizados?
  Verifique isso usando o terminal de [tarefas ativas](../api/active_tasks.html).
* Teste o nível de 'prontidão do índice' enviando uma consulta para o índice
e decidindo se ele é retornado em um tempo aceitável.
