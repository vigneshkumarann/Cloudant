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

# Création d'une application {{site.data.keyword.cloud_notm}} simple permettant d'accéder à une base de données {{site.data.keyword.cloudant_short_notm}} : l'environnement d'application

Cette section du tutoriel décrit comment configurer l'environnement d'application dont vous devez disposer pour créer une application {{site.data.keyword.cloud}}.
{:shortdesc}

<div id="creating"></div>

## Création d'un environnement d'application {{site.data.keyword.cloud_notm}}

1.  Connectez-vous à votre compte {{site.data.keyword.cloud_notm}}.
    Le tableau de bord {{site.data.keyword.cloud_notm}} est disponible à l'adresse :
    [http://bluemix.net ![Icône de lien externe](../images/launch-glyph.svg "Icône de lien externe")](http://bluemix.net){:new_window}.
    Une fois que vous vous êtes authentifié avec votre nom d'utilisateur et votre mot de passe, le tableau de bord {{site.data.keyword.cloud_notm}} apparaît :</br>
    ![Tableau de bord {{site.data.keyword.cloud_notm}}](images/img0001.png)
2.  Cliquez sur le bouton `Créer une ressource` :<br/>
    ![Bouton Créer une ressource de {{site.data.keyword.cloud_notm}}](images/img0002.png)<br/>
    La liste des services disponibles sur {{site.data.keyword.cloud_notm}} s'affiche.

3.  Cliquez sur la catégorie `Calcul` :<br/>
    ![Applications {{site.data.keyword.cloud_notm}} Cloud Foundry](images/img0012.png)<br/>
    Une liste des divers services et applications disponibles sur {{site.data.keyword.cloud_notm}} s'affiche.

4.  Faîtes défiler l'écran jusqu'à la section `Cloud Foundry` et cliquez sur l'entrée `Python` :<br/>
    ![Application Python {{site.data.keyword.cloud_notm}}](images/img0013.png)<br/>
    Le formulaire `Créez une application Cloud Foundry` s'affiche.

5.  Utilisez le formulaire `Créez une application Cloud Foundry` pour spécifier et créer l'environnement de votre application Python Cloud Foundry. Entrez un nom pour votre application, par exemple `Application Cloudant CF`. Le nom d'hôte est automatiquement généré pour vous, même si vous avez la possibilité de le personnaliser.</br>
    ![Noms d'application {{site.data.keyword.cloud_notm}} Python Cloud Foundry](images/img0014.png)
    
    Le nom d'hôte doit être unique au sein du domaine {{site.data.keyword.cloud_notm}}. Dans cet exemple, le domaine est `mybluemix.net`, ce qui donne le nom d'hôte complet `Cloudant-CF-app.mybluemix.net`.
    {: tip}

6.  Cliquez sur `Créer` pour créer l'environnement d'application :</br>
    ![Créer l'application {{site.data.keyword.cloud_notm}} Python Cloud Foundry](images/img0015.png)

7.  Après une courte pause,
    la fenêtre `Initiation` du nouvel environnement d'application s'affiche.
    Une application de test est automatiquement créée dans l'environnement.
    L'application est démarrée automatiquement,
    comme le montre l'icône verte et le statut `En cours d'exécution`.
    L'application est un programme à 'pulsations' suffisant pour montrer que le nouvel environnement d'application est prêt à être utilisé.
    Cliquez sur le lien `Applications Cloud Foundry` pour retourner à votre tableau de bord {{site.data.keyword.cloud_notm}}.<br/>
    ![La nouvelle application {{site.data.keyword.cloud_notm}} Python Cloud Foundry exécutée pour la première fois](images/img0016.png)

8.  Votre tableau de bord inclut désormais l'environnement d'application nouvellement créé :<br/>
    ![Application {{site.data.keyword.cloud_notm}} Python Cloud Foundry de base apparaissant dans le tableau de bord](images/img0017.png)

Vous disposez maintenant d'un environnement d'application {{site.data.keyword.cloud_notm}} Python prêt à être utilisé.

Si vous souhaitez utiliser une instance de base de données {{site.data.keyword.cloudant_short_notm}}, vous devez maintenant créer une 'connexion' entre l'environnement d'application et l'instance de base de données.

<div id="connecting"></div>

## Connexion des applications et des services {{site.data.keyword.cloud_notm}}

Cette section du tutoriel explique comment connecter des services et des environnements d'application {{site.data.keyword.cloud_notm}} en utilisant la zone de configuration et de gestion de votre application.

1.  A partir de votre tableau de bord {{site.data.keyword.cloud_notm}}, cliquez sur l'entrée correspondant à votre application.<br/>
    ![Sélection de votre application sur le tableau de bord {{site.data.keyword.cloud_notm}}](images/img0018.png)</br>
    La zone d'aperçu de la configuration et de la gestion de votre application s'affiche.

2.  Pour connecter l'environnement d'application à un autre service, cliquez sur le lien `Connexions` :<br/>
    ![Sélection de la configuration de connexion de votre application {{site.data.keyword.cloud_notm}}](images/img0019.png)<br/>
    Une zone permettant de configurer une connexion entre votre application et tout autre service disponible dans votre compte apparaît.

3.  Ce tutoriel [requiert](create_bmxapp_prereq.html#prerequisites) une instance de base
de données {{site.data.keyword.cloudant_short_notm}} existante.
    Cliquez sur `Créer une connexion` pour établir une connexion entre cette instance de service et votre application :<br/>
    ![Connexion à une instance de base de données existante](images/img0020.png)<br/>
    La liste des instances de service existantes de votre compte s'affiche.

4.  Cliquez sur l'instance de service {{site.data.keyword.cloudant_short_notm}} que vous souhaitez utiliser.
    Ce tutoriel utilise l'instance `Cloudant-service` :<br/>
    ![Sélection de l'instance de base de données exemple du tutoriel](images/img0021.png)

5.  Vous êtes invité à confirmer que vous souhaitez réellement connecter l'instance de base de données à votre application.
    Cliquez sur `Connecter` pour confirmer la connexion :<br>
    ![Confirmation de la connexion à l'instance de base de données](images/img0022.png)

6.  Avant de continuer, vous êtes invité à personnaliser l'ID de service et le rôle d'accès. Cliquez sur `Connecter` pour continuer.
    ![Confirmation de la reconstitution de l'application](images/img0022b.png)

6.  La modification des connexions de service d'une application affecte sa configuration globale. Une modification requiert une 'reconstitution' de l'application, ce qui entraîne
l'arrêt forcé de l'application en cours d'exécution. Une fenêtre s'affiche et vous invite à confirmer que vous êtes prêt à effectuer le
processus de 'reconstitution'.
    Cliquez sur `Reconstituer` pour continuer :<br/>
    ![Confirmation de la reconstitution de l'application](images/img0023.png)

7.  La page des connexions de service apparaît à nouveau.
    Elle inclut désormais l'instance de base de données nouvellement connectée :<br/>
    ![Instance de base de données nouvellement connectée](images/img0024.png)

L'environnement d'application et l'instance de base de données sont maintenant connectés.
L'étape suivante consiste à vérifier que les outils requis sont installés et prêts à fonctionner avec les applications {{site.data.keyword.cloud_notm}}.

<div id="toolkits"></div>

## Kits d'outils de ligne de commande Cloud Foundry et {{site.data.keyword.cloud_notm}}

Cette section du tutoriel décrit les kits d'outils qui doivent être installés pour fonctionner avec votre environnement {{site.data.keyword.cloud_notm}}, vos applications et vos services.

Le kit d'outils [Cloud Foundry ![Icône de lien externe](../images/launch-glyph.svg "Icône de lien externe")](https://en.wikipedia.org/wiki/Cloud_Foundry){:new_window} est une collection d'outils destinés à
être utilisés avec des applications déployées dans un environnement compatible avec Cloud Foundry.
Employez ces outils pour effectuer des tâches telles que la mise à jour d'une application
déployée, ou pour démarrer et arrêter une application en cours d'exécution.

Le kit d'outils {{site.data.keyword.cloud_notm}} offre des fonctions
supplémentaires requises pour une utilisation avec des applications hébergées et exécutées dans un environnement {{site.data.keyword.cloud_notm}}.

Vérifiez que vous installez bien à la fois Cloud Foundry _et_ les kits d'outils {{site.data.keyword.cloud_notm}}.
{: tip}

Le téléchargement et l'installation des kits d'outils est une tâche ponctuelle.
S'ils sont déjà installés et en fonctionnement sur votre système, il n'est pas nécessaire
de les télécharger à nouveau, sauf s'ils ont fait l'objet d'une mise à jour.

Des informations générales sur les kits d'outils sont disponibles [ici ![Icône de lien externe](../images/launch-glyph.svg "Icône de lien externe")](../getting-started.html#getting-started-with-cloudant){:new_window}.

### Installation du kit d'outils Cloud Foundry

Certaines distributions de système d'exploitation disposent déjà d'une version disponible du kit d'outils Cloud Foundry.
S'il s'agit de la version 6.11 ou ultérieure, la version prise en charge est compatible avec {{site.data.keyword.cloud_notm}} et peut être utilisée.
Pour vérifier le niveau de la version installée, exécutez [ce test](#checkCFversion).

Vous pouvez également suivre les étapes ci-après pour télécharger et installer le kit d'outils Cloud Foundry sur votre système : 

1.  Cliquez sur `Initiation` pour afficher les informations sur le téléchargement du kit d'outils Cloud Foundry.

2.  Cliquez sur `Interface de ligne de commande`. Le lien vous renvoie à la documentation de {{site.data.keyword.cloud_notm}} Developer Tools (CLI et Dev Tools).

3.  Cliquez sur `Plug-in de l'interface de ligne de commande Cloud Foundry`, puis sur `Interface de ligne de commande d'administration {{site.data.keyword.cloud_notm}}`. 

4.  Suivez les instructions sur la page à télécharger et exécutez la dernière version du programme d'installation de votre système.

5.  <div id='checkCFversion'></div>Pour vérifier que vous disposez d'un kit d'outils Cloud Foundry compatible, exécutez la commande suivante à l'invite :

    ```sh
    cf --version
    ```
    {:pre}
    
    Vous devez obtenir un résultat similaire à la sortie suivante :
    
    ```
    cf version 6.20.0+25b1961-2016-06-29
    ```
    {:codeblock}
    
    La version du kit d'outils Cloud Foundry doit être 6.11 ou une version plus récente pour être compatible avec {{site.data.keyword.cloud_notm}}.
    {: tip}

### Installation du kit d'outils {{site.data.keyword.cloud_notm}}

Procédez comme suit pour télécharger et installer l' kit d'outils {{site.data.keyword.cloud_notm}} sur votre système.

1.  Cliquez sur `Initiation` pour afficher des informations sur le téléchargement du kit d'outils de l'interface de ligne de commande d'administration de {{site.data.keyword.cloud_notm}}.

2.  Cliquez sur `Interface de ligne de commande` pour ouvrir le document [Getting started with {{site.data.keyword.cloud_notm}} developer tools ![Icône de lien externe](../images/launch-glyph.svg "Icône de lien externe")](https://console.bluemix.net/docs/cli/reference/bluemix_cli/get_started.html#getting-started){:new_window}.

3.  Suivez les instructions sur la page pour télécharger et exécuter le programme d'installation adapté à votre système.

    Le programme d'installation vérifie que la version installée du kit d'outils Cloud Foundry est appropriée.
    Si tout est correct, le kit d'outils {{site.data.keyword.cloud_notm}} est installé sur votre système.

4.  Pour vérifier que vous disposez d'un kit d'outils {{site.data.keyword.cloud_notm}} approprié, exécutez la commande suivante à l'invite :
    
    ```sh
    bluemix --version
    ```
    {:pre}
    
    Vous devez obtenir un résultat similaire à la sortie suivante :
    
    ```
    bluemix version 0.4.5+03c29de-2016-12-08T07:01:01+00:00
    ```
    {:codeblock}
    
Les outils destinés à être utilisés avec les applications {{site.data.keyword.cloud_notm}} sont désormais disponibles.
L'étape suivante consiste à obtenir les éléments de démarrage pour créer une application {{site.data.keyword.cloud_notm}}.

Après avoir installé l'interface de ligne de commande, retournez à l'onglet `Initiation` du tableau de bord, pour télécharger, modifier et redéployer vos instances de service et applications Cloud Foundry avec l'interface de ligne de commande.
{: tip}

<div id="starter"></div>

## Application de démarrage

Cette section du tutoriel décrit une application de démarrage {{site.data.keyword.cloud_notm}} et explique comment la personnaliser afin qu'elle accède à une instance de base de données {{site.data.keyword.cloudant_short_notm}}.

Une application de démarrage {{site.data.keyword.cloud_notm}} est la
collection la plus petite possible de fichiers source et de configuration nécessaires à la
création d'une application {{site.data.keyword.cloud_notm}} pouvant être exécutée.
Par certains aspects, elle est similaire à une [application 'Hello World' ![Icône de lien externe](../images/launch-glyph.svg "Icône de lien externe")](https://en.wikipedia.org/wiki/%22Hello,_World!%22_program){:new_window} ; elle suffit à montrer que le système et la configuration de base fonctionnent correctement.

Une application de démarrage {{site.data.keyword.cloud_notm}} est une archive de fichiers exemples que vous devez modifier ou étendre au fur et à mesure que vous développez votre application {{site.data.keyword.cloud_notm}}.

Trois fichiers en particulier sont essentiels :

-   [`Procfile`](#procfile)
-   [`manifest.yml`](#manifest)
-   [`requirements.txt`](#requirements)

<div id="procfile"></div>

### Le fichier `Procfile` 

Le fichier `Procfile` contient les informations
dont {{site.data.keyword.cloud_notm}} a besoin pour exécuter votre application.

Plus spécifiquement,
un fichier `Procfile` est un artefact Cloud Foundry qui
définit un type de processus applicatif et la commande permettant d'exécuter l'application.
Vous trouverez plus d'informations sur `Procfile`
[ici ![Icône de lien externe](../images/launch-glyph.svg "Icône de lien externe")](https://docs.cloudfoundry.org/buildpacks/prod-server.html#procfile){:new_window}.

Le fichier `Procfile` d'une application de démarrage {{site.data.keyword.cloud_notm}} Python est similaire à l'exemple suivant :

```
web: python server.py
```
{:codeblock}

Cet exemple indique que l'application est une application Web Python et qu'elle est démarrée via la commande :

```sh
python server.py
```
{:codeblock}

Un fichier source Python de démarrage `server.py` est inclus dans l'archive de l'application de démarrage.
Le fichier `server.py` est modifié pour votre application.
Vous pouvez également créer un fichier source Python entièrement nouveau.
Vous devez alors mettre à jour le fichier `Procfile` de telle sorte qu'il utilise le nouveau fichier au démarrage de votre application.

<div id="manifest"></div>

### Le fichier `manifest.yml` 

Le fichier `manifest.yml` est une description complète de l'application et de l'environnement dont elle a besoin pour s'exécuter.

Le fichier d'une application de démarrage {{site.data.keyword.cloud_notm}} Python ressemble à l'exemple suivant :

```
applications:
- path: .
  memory: 128M
  instances: 1
  domain: mybluemix.net
  name: Cloudant Python
  host: Cloudant-Python
  disk_quota: 1024M
  services:
  - Cloudant Service 2017
```
{:codeblock}

Il est important de noter les trois points suivants :

-   Les valeurs de `domain`, `name` et `host` correspondent aux valeurs saisies lors de la [création](#creating) de votre application {{site.data.keyword.cloud_notm}}.
-   La valeur de `name` est utilisée par le kit d'outils Cloud Foundry pour identifier l'application que vous administrez.
-   La valeur de `services` confirme que l'instance de base de données {{site.data.keyword.cloudant_short_notm}} `Cloudant Service 2017` est connectée à l'environnement d'application.

Il n'est normalement pas nécessaire de modifier le fichier `manifest.yml`. Il est cependant utile de comprendre la raison de sa présence et son utilité au fonctionnement de votre application.

<div id="requirements"></div>

### Le fichier `requirements.txt`

Le fichier `requirements.txt` spécifie les éventuels composants supplémentaires requis pour le fonctionnement de votre application.

Dans l'application de démarrage, le fichier `requirements.txt` est vide.

Toutefois, dans ce tutoriel, l'application Python accède à une instance de base de données {{site.data.keyword.cloudant_short_notm}}.
L'application doit donc pouvoir utiliser la [bibliothèque client {{site.data.keyword.cloudant_short_notm}} pour les applications Python](../libraries/supported.html#python).

Pour activer la bibliothèque client Python, modifiez le fichier `requirements.txt` de la manière suivante :
```
cloudant==2.3.1
```
{:codeblock}

## Etape suivante

L'étape suivante du tutoriel consiste à [créer l'application](create_bmxapp_createapp.html).
