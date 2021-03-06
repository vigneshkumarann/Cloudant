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

# 建立簡單的 {{site.data.keyword.cloud_notm}} 應用程式以存取 {{site.data.keyword.cloudant_short_notm}} 資料庫：應用程式環境

指導教學的這一節說明如何設定在建立 {{site.data.keyword.cloud}} 應用程式時必須要有的應用程式環境。
{:shortdesc}

<div id="creating"></div>

## 建立 {{site.data.keyword.cloud_notm}} 應用程式環境

1.  登入 {{site.data.keyword.cloud_notm}} 帳戶。{{site.data.keyword.cloud_notm}} 儀表板位於 [http://bluemix.net ![外部鏈結圖示](../images/launch-glyph.svg "外部鏈結圖示")](http://bluemix.net){:new_window}。在您利用使用者名稱及密碼進行鑑別之後，會出現 {{site.data.keyword.cloud_notm}} 儀表板：</br>
    ![{{site.data.keyword.cloud_notm}} 儀表板](images/img0001.png)
2.  按一下`建立資源`按鈕：<br/>
    ![{{site.data.keyword.cloud_notm}} 建立資源按鈕](images/img0002.png)<br/>
即會出現 {{site.data.keyword.cloud_notm}} 上可用的服務清單。

3.  按一下`運算`種類：<br/>
    ![{{site.data.keyword.cloud_notm}} Cloud Foundry 應用程式](images/img0012.png)<br/>
    即會出現 {{site.data.keyword.cloud_notm}} 上可用的各種服務及應用程式清單。

4.  向下捲動至 `Cloud Foundry` 區段，然後按一下 `Python` 項目：<br/>
    ![{{site.data.keyword.cloud_notm}} Python 應用程式](images/img0013.png)<br/>
    即會出現`建立 Cloud Foundry 應用程式`表單。

5.  使用`建立 Cloud Foundry 應用程式`表單，以指定及建立 Python Cloud Foundry 應用程式的環境。請輸入應用程式的名稱（例如 `Cloudant CF app`）。系統會自動為您產生主機名稱，但您可以進行自訂：</br>
    ![{{site.data.keyword.cloud_notm}} Python Cloud Foundry 應用程式名稱](images/img0014.png)
    
    在 {{site.data.keyword.cloud_notm}} 網域內，主機名稱必須是唯一的。在此範例中，網域為 `mybluemix.net`，完整主機名稱則會是 `Cloudant-CF-app.mybluemix.net`。
    {: tip}

6.  按一下`建立`來建立應用程式環境：</br>
    ![建立 {{site.data.keyword.cloud_notm}} Python Cloud Foundry 應用程式](images/img0015.png)

7.  在短暫暫停之後，會出現新應用程式環境的`開始使用`視窗。
    會在環境內自動建立測試應用程式。將自動啟動應用程式，如綠色圖示及`執行中`狀態所示。
    應用程式是一種「活動訊號」程式，足以顯示新應用程式環境可供您使用。按一下 `Cloud Foundry 應用程式`鏈結，以回到 {{site.data.keyword.cloud_notm}} 儀表板。<br/>
    ![首次執行的新 {{site.data.keyword.cloud_notm}} Python Cloud Foundry 應用程式](images/img0016.png)

8.  您的儀表板現在包含新建立的應用程式環境：<br/>
    ![出現在儀表板中的基本 {{site.data.keyword.cloud_notm}} Python Cloud Foundry 應用程式](images/img0017.png)

您現在有了 {{site.data.keyword.cloud_notm}} Python 應用程式環境可供使用。

若要使用 {{site.data.keyword.cloudant_short_notm}} 資料庫實例，下一步是在應用程式環境與資料庫實例之間建立「連線」。

<div id="connecting"></div>

## 連接 {{site.data.keyword.cloud_notm}} 應用程式與服務

指導教學的這一節說明如何使用應用程式的配置及管理區域，來連接 {{site.data.keyword.cloud_notm}} 應用程式環境與服務。

1.  從 {{site.data.keyword.cloud_notm}} 儀表板，按一下應用程式的項目。<br/>
    ![在 {{site.data.keyword.cloud_notm}} 儀表板上選取應用程式](images/img0018.png)</br>
即會出現應用程式的配置及管理概觀區域。

2.  若要將應用程式環境連接至另一個服務，請按一下`連線`鏈結：<br/>
    ![選取 {{site.data.keyword.cloud_notm}} 應用程式的連線配置](images/img0019.png)<br/>
即會出現一個區域，可用於在應用程式與帳戶內可用的任何其他服務之間配置連線。

3.  本指導教學的[必要條件](create_bmxapp_prereq.html#prerequisites)是要具備現有的 {{site.data.keyword.cloudant_short_notm}} 資料庫實例。按一下`建立連線`，以建立該服務實例與應用程式之間的連線：<br/>
    ![連接至現有資料庫實例](images/img0020.png)<br/>
    即會出現您帳戶中的現有服務實例清單。

4.  按一下您要使用的 {{site.data.keyword.cloudant_short_notm}} 服務實例。
    本指導教學使用 `Cloudant-service` 實例：<br/>
    ![選擇指導教學範例資料庫實例](images/img0021.png)

5.  系統會要求您確認是否真的要將資料庫實例連接至應用程式。按一下`連接`來確認連線：<br>
    ![確認與資料庫實例的連線](images/img0022.png)

6.  繼續之前，系統會要求您自訂服務 ID 及存取角色。按一下`連接`以繼續進行。
    ![確認重新編譯打包應用程式](images/img0022b.png)

6.  修改應用程式的服務連線會影響其整體配置。修改需要「重新編譯打包」應用程式，這也會強制停止執行中應用程式。即會出現一個視窗，讓您確認您已準備好可以繼續「重新編譯打包」。按一下`重新編譯打包`以繼續進行：<br/>
    ![確認重新編譯打包應用程式](images/img0023.png)

7.  即會重新出現服務連線頁面。它現在包含新連接的資料庫實例：<br/>
    ![新連接的資料庫實例](images/img0024.png)

現在已連接應用程式環境及資料庫實例。下一步是確定已為您安裝使用 {{site.data.keyword.cloud_notm}} 應用程式的必要工具。

<div id="toolkits"></div>

## Cloud Foundry 及 {{site.data.keyword.cloud_notm}} 指令工具箱

指導教學的這一節說明要使用 {{site.data.keyword.cloud_notm}} 環境、應用程式及服務時必須安裝的工具箱。

[Cloud Foundry ![外部鏈結圖示](../images/launch-glyph.svg "外部鏈結圖示")](https://en.wikipedia.org/wiki/Cloud_Foundry){:new_window} 工具箱是工具集合，這些工具可用來使用在 Cloud Foundry 相容環境中部署的應用程式。使用這些工具可進行各種作業，例如更新已部署的應用程式，或者啟動及停止執行中的應用程式。

{{site.data.keyword.cloud_notm}} 工具箱提供額外功能，而這些功能是使用在 {{site.data.keyword.cloud_notm}} 環境內所管理及執行之應用程式的必要功能。

請確定您已安裝 Cloud Foundry _及_ {{site.data.keyword.cloud_notm}} 工具箱。
{: tip}

下載及安裝工具箱是單次作業。如果工具箱已安裝並在您的系統中運作，則除非有更新，否則不需要重新予以下載。

[這裡 ![外部鏈結圖示](../images/launch-glyph.svg "外部鏈結圖示")](../getting-started.html#getting-started-with-cloudant){:new_window} 提供工具箱的一般資訊。

### 安裝 Cloud Foundry 工具箱

部分作業系統發行套件已有可用的 Cloud Foundry 工具箱版本。如果支援的版本是 6.11 或更新版本，則與 {{site.data.keyword.cloud_notm}} 相容，並且可以使用。您可以執行[此測試](#checkCFversion)來檢查已安裝的版本。

或者，使用下列步驟，在系統上下載及安裝 Cloud Foundry 工具箱： 

1.  按一下`開始使用`，以查看下載 Cloud Foundry 工具箱的相關資訊。

2.  按一下 `CLI`。此鏈結會帶領您前往 {{site.data.keyword.cloud_notm}} Developer Tools（CLI 及 Dev Tools）文件。

3.  按一下 `Cloud Foundry CLI 外掛程式`，然後按一下 `{{site.data.keyword.cloud_notm}} 管理 CLI`。 

4.  遵循頁面上的指示，以下載及執行您系統的最新版安裝程式。

5.  <div id='checkCFversion'></div>若要確認您有運作中的 Cloud Foundry 工具箱，請在提示執行下列指令：

    ```sh
    cf --version
    ```
    {:pre}
    
    預期結果類似下列輸出：
    
    ```
    cf version 6.20.0+25b1961-2016-06-29
    ```
    {:codeblock}
    
    Cloud Foundry 工具箱版本必須是 6.11 或更新版本，才能與 {{site.data.keyword.cloud_notm}} 相容。
    {: tip}

### 安裝 {{site.data.keyword.cloud_notm}} 工具箱

請使用下列步驟，在系統上下載及安裝 {{site.data.keyword.cloud_notm}} 工具箱。

1.  按一下`開始使用`，以查看下載 {{site.data.keyword.cloud_notm}} 管理 CLI 工具箱的相關資訊。

2.  按一下 `CLI`，以開啟[開始使用 {{site.data.keyword.cloud_notm}} Developer Tools ![外部鏈結圖示](../images/launch-glyph.svg "外部鏈結圖示")](https://console.bluemix.net/docs/cli/reference/bluemix_cli/get_started.html#getting-started){:new_window} 文件。

3.  遵循頁面上的指示，以下載及執行您系統的適當安裝程式。

    安裝程式會確認您已安裝適合的 Cloud Foundry 工具箱版本。如果一切正確，則會在系統上安裝 {{site.data.keyword.cloud_notm}} 工具箱。

4.  若要確認您有運作中的 {{site.data.keyword.cloud_notm}} 工具箱，請在提示執行下列指令：
    
    ```sh
    bluemix --version
    ```
    {:pre}
    
    預期結果類似下列輸出：
    
    ```
    bluemix version 0.4.5+03c29de-2016-12-08T07:01:01+00:00
    ```
    {:codeblock}
    
現在已提供使用 {{site.data.keyword.cloud_notm}} 應用程式的工具。下一步是取得「入門範本」資料，協助您建立 {{site.data.keyword.cloud_notm}} 應用程式。

在您安裝指令行介面之後，請回到儀表板中的`開始使用`標籤，以使用指令行介面來下載、修改及重新部署 Cloud Foundry 應用程式與服務實例。
{: tip}

<div id="starter"></div>

## 「入門範本」應用程式

指導教學的這一節說明 {{site.data.keyword.cloud_notm}} 入門範本應用程式，並解釋如何自訂它以便存取 {{site.data.keyword.cloudant_short_notm}} 資料庫實例。

{{site.data.keyword.cloud_notm}} 入門範本應用程式是建立可運作之 {{site.data.keyword.cloud_notm}} 應用程式所需原始檔及配置檔的最小可能集合。在某些方面，它類似於 ['Hello World' 應用程式 ![外部鏈結圖示](../images/launch-glyph.svg "外部鏈結圖示")](https://en.wikipedia.org/wiki/%22Hello,_World!%22_program){:new_window}；它只足以顯示基本系統及配置在正確地運作中。

{{site.data.keyword.cloud_notm}} 入門範本應用程式是您開發 {{site.data.keyword.cloud_notm}} 應用程式時必須修改或延伸的範例檔案的保存檔。

有三個檔案特別重要：

-   [`Procfile`](#procfile)
-   [`manifest.yml`](#manifest)
-   [`requirements.txt`](#requirements)

<div id="procfile"></div>

### `Procfile` 檔案

`Procfile` 包含 {{site.data.keyword.cloud_notm}} 執行應用程式所需的詳細資料。

更明確地說，`Procfile` 是一種 Cloud Foundry 構件，它會定義應用程式處理程序類型和執行應用程式用的指令。[這裡 ![外部鏈結圖示](../images/launch-glyph.svg "外部鏈結圖示")](https://docs.cloudfoundry.org/buildpacks/prod-server.html#procfile){:new_window} 提供 `Procfile` 的相關資訊。

{{site.data.keyword.cloud_notm}} Python 入門範本應用程式的 `Procfile` 與下列範例類似：

```
web: python server.py
```
{:codeblock}

此範例指出應用程式是一個 Python Web 應用程式，且它是透過執行下列指令來啟動：

```sh
python server.py
```
{:codeblock}

入門範本應用程式保存檔中，包含了入門範本 `server.py` Python 原始檔。`server.py` 檔案已針對您的應用程式修改。您也可以建立全新的 Python 原始檔。然後，更新 `Procfile`，以在啟動應用程式時使用新檔案。

<div id="manifest"></div>

### `manifest.yml` 檔案

`manifest.yml` 檔案是應用程式及其執行所需環境的完整說明。

{{site.data.keyword.cloud_notm}} Python 入門範本應用程式的檔案類似下列範例：

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

有三點值得注意：

-   `domain`、`name` 及 `host` 值對應於[建立](#creating) {{site.data.keyword.cloud_notm}} 應用程式時所輸入的值。
-   Cloud Foundry 工具箱使用 `name` 值來識別您所管理的應用程式。
-   `services` 值確認 `Cloudant Service 2017` {{site.data.keyword.cloudant_short_notm}} 資料庫實例已連接至應用程式環境。

您通常不需要修改 `manifest.yml` 檔案，不過，最好瞭解應用程式為什麼必須要有它才能運作。

<div id="requirements"></div>

### `requirements.txt` 檔案

`requirements.txt` 檔案指定應用程式運作所需的任何其他元件。

在入門範本應用程式中，`requirements.txt` 檔案是空的。

不過，在本指導教學中，Python 應用程式會存取 {{site.data.keyword.cloudant_short_notm}} 資料庫實例。因此，應用程式必須可以使用 [Python 應用程式的 {{site.data.keyword.cloudant_short_notm}} 用戶端程式庫](../libraries/supported.html#python)。

若要啟用 Python 用戶端程式庫，請修改 `requirements.txt` 檔案成為：
```
cloudant==2.3.1
```
{:codeblock}

## 下一步

指導教學中的下一步是[建立應用程式](create_bmxapp_createapp.html)。
