---
title: 執行大量資料移轉
description: 瞭解如何使用CLI設定並執行從Adobe Commerce PaaS或內部部署執行個體到Adobe Commerce as a Cloud Service的大量資料移轉。
feature: Cloud
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案（Adobe管理的SaaS基礎結構）。"
role: Developer
level: Intermediate
autotag-review: '2026-07-22T19:19:07.600Z'
TQID: 'https://experienceleague.adobe.com/z9659Vnf2JLxJ4U5p3tEEjurj5Mg3bfKj68Gheq2AXY'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: bd989d82-1e15-4534-88db-f1f51dd77ffaid: c1256247-af4b-46d8-9dca-0c654ecfa157id: c32adafa-ed01-4b31-997e-2413013911b0id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2: id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 670b6214b28be93a16130552a226a8cadb487324
workflow-type: tm+mt
source-wordcount: 2802
ht-degree: 0%

---

# 執行大量資料移轉

{{bulk-data-early-access}}

本指南是使用大量資料移轉工具，從[!DNL Adobe Commerce] PaaS或內部部署安裝執行資料移轉至[!DNL Adobe Commerce as a Cloud Service]的逐步操作參考。 實際設定值和特定環境的詳細資料會因您的設定而異。

開始之前，請確認您已完成[客戶整備檢查清單](readiness-checklist.md)中的每個專案，並透過[移轉服務存取指南](cdms-access.md)驗證API存取。

>[!NOTE]
>
>涵蓋工具架構、內部設計、資料轉換架構和完整性測試架構的完整技術檔案，包含在工具發佈套件中。

## 先決條件

- **[!DNL Docker]**&#x200B;和&#x200B;**[!DNL Docker Compose]**&#x200B;必須安裝在您執行移轉的電腦上。
- 執行移轉的使用者必須有執行`docker`和`docker compose` （或舊版`docker-compose`）命令的許可權。 在[!DNL Linux]，使用者必須屬於`docker`群組。 在[!DNL macOS]和[!DNL Windows]上，[!DNL Docker Desktop]必須正在執行且可存取。 移轉CLI會重複叫用[!DNL Docker]，而許可權錯誤會在此封鎖執行。
- 在執行移轉之前，來源和目標之間的核心設定必須一致。 此工具不會移轉核心設定資料，例如存放區設定和系統設定。 請在目標上單獨設定，並在移轉前與來源對齊。

## 設定工具套件

設定大量資料移轉的環境：

>[!VIDEO](https://video.tv.adobe.com/v/3496121)

1. 擷取`ccsaas-migration-tools.tar.gz`的內容。

1. 從擷取的`ccsaas-migration-tools`資料夾執行`bin/console`所在的所有命令。

1. 請確認資料夾可寫入記錄檔、快取、[!DNL Composer]及產生的檔案。

   將該目錄下所有檔案和子資料夾的所有權變更給執行移轉的作業系統使用者，讓工具可以一致地讀取和寫入。 例如，在[!DNL Linux]： `chown -R <user>:<group> <project-root>`。

1. 複製範例檔案（`.example.env`到`.env`和`.my.cnf.example`到`.my.cnf`），在專案根目錄中建立`.env`和`.my.cnf`檔案，然後填入下列章節中說明的值。

### 組態檔範例

存放庫根目錄中的`.example.env`和`.my.cnf.example`檔案是您設定的起點。 將每個檔案複製到其工作名稱並填入所需的值。

| 範例檔案 | 複製到 | 涵蓋範圍 |
| --- | --- | --- |
| `.example.env` | `.env` | 所有支援的環境變數的附註清單：效能、CDMS、IMS、目標SaaS、來源URL驗證、OAuth，以及選用的PaaS值（當`id=`設定在`.my.cnf`中時，則為`MAGENTO_CLOUD_CLI_TOKEN`）。 `.env`檔案中有完整的變數清單。 |
| `.my.cnf.example` | `.my.cnf` | 參考內部部署[!DNL MySQL]和PaaS (`id=project:environment`)的`[section]`配置。 `[section]`名稱必須符合`.env`中的`SOURCE_CONNECTION_NAME`。 欄位包含PaaS的`user`、`password`、`host`、`port`、`database`和`id=`。 |

## 設定環境檔案

專案根目錄中的`.env`檔案是移轉與擷取組態。 它會驅動CLI管道，包括來源和目標URL、OAuth、遠端CDMS連線、SaaS和IMS驗證，以及其他交換器。

>[!NOTE]
>
>請勿在URL中加入結尾斜線。 例如，使用`https://example.com`而非`https://example.com/`。

編輯`.env`檔案並正確設定至少下列值。 如需支援的變數完整清單，請參閱`.example.env`中的內嵌註解。

```shell-session
SOURCE_INSTANCE_URL=https://<source-host>
SOURCE_INSTANCE_GRAPHQL_URL=https://<source-host>/graphql
SOURCE_INSTANCE_REST_URL=https://<source-host>/rest
SOURCE_INSTANCE_CONSUMER_KEY=<consumer_key>
SOURCE_INSTANCE_CONSUMER_SECRET=<consumer_secret>
SOURCE_INSTANCE_ACCESS_TOKEN=<access_token>
SOURCE_INSTANCE_ACCESS_TOKEN_SECRET=<access_token_secret>
```

### 設定來源OAuth認證

>[!VIDEO](https://video.tv.adobe.com/v/3496142)

這四個值會簽署從移轉工具到來源存放區API的請求。 若要取得這些擴充功能，請開啟來源[!UICONTROL Admin]，並移至&#x200B;[!UICONTROL **系統**] > [!UICONTROL **擴充功能**] > [!UICONTROL **整合**]。 建立或開啟整合，然後將值複製到`.env`：

```shell-session
SOURCE_INSTANCE_CONSUMER_KEY=<consumer_key>
SOURCE_INSTANCE_CONSUMER_SECRET=<consumer_secret>
SOURCE_INSTANCE_ACCESS_TOKEN=<access_token>
SOURCE_INSTANCE_ACCESS_TOKEN_SECRET=<access_token_secret>
```

### 設定雲端CLI權杖

>[!NOTE]
>
>這僅適用於[!DNL Adobe Commerce on Cloud]來源執行個體。 工具會自動從`.my.cnf`偵測來源型別。 如果`SOURCE_CONNECTION_NAME`區段包含`id=`行（例如`id=project:production`），則來源為[!DNL Adobe Commerce on Cloud]，且需要`MAGENTO_CLOUD_CLI_TOKEN`。 對於沒有`id=`的內部部署來源，不需要此Token，並略過通道設定。

1. 前往`https://accounts.magento.cloud`並登入。

1. 按一下您的設定檔影像，然後選取&#x200B;[!UICONTROL **帳戶設定**]。

1. 移至&#x200B;[!UICONTROL **API Token**]&#x200B;區段。

1. 選取&#x200B;[!UICONTROL **建立API權杖**]、提供描述性名稱，並複製產生的權杖。

1. 在`.env`中設定權杖：

   ```text
   MAGENTO_CLOUD_CLI_TOKEN=<your_magento_cloud_api_token>
   ```

>[!NOTE]
>
>如果您是第一次使用Cloud CLI，您也必須將SSH公開金鑰新增至帳戶。 如需指示，請參閱[安全連線指南](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections)。

### 調整Commerce管理設定

在移轉之前，請確定來源和目標之間的下列設定一致。

>[!NOTE]
>
>為確保順利移轉，[!DNL Adobe]建議您讓目標執行個體中的所有核心設定與來源一致。

### 設定目標SaaS和IMS憑證

>[!VIDEO](https://video.tv.adobe.com/v/3496167)

這些是目標的[!DNL Adobe Commerce as a Cloud Service] IMS和API設定。 您需要租使用者ID、組織ID、IMS OAuth伺服器對伺服器認證，以及您環境的正確IMS主機。 與您的Adobe團隊協調，以取得組織、租使用者和設定檔存取權。 請勿嘗試推斷或估計敏感值。

#### 產生IMS認證

使用[Adobe Developer Console](https://developer.adobe.com/console/)。 您需要Adobe組織的[!UICONTROL Developer]或[!UICONTROL Admin]存取權才能建立專案。 基本使用者登入不足以新增API。

1. 建立專案或開啟現有專案，然後選取[!UICONTROL Add API]。

1. 選擇&#x200B;[!UICONTROL **Adobe Commerce as a Cloud Service**]&#x200B;並繼續。

1. 選取&#x200B;[!UICONTROL **OAuth伺服器對伺服器**]&#x200B;做為驗證型別，然後繼續。

1. 選取您的Adobe團隊預期用於此租使用者的產品設定檔，然後選取「[!UICONTROL **儲存已設定的API**]」。

1. 在專案側邊欄中，開啟&#x200B;[!UICONTROL **OAuth伺服器對伺服器**] （或&#x200B;[!UICONTROL **認證**]），然後將使用者端ID和使用者端密碼複製到`.env`中，做為`ADOBE_IMS_CLIENT_ID`和`ADOBE_IMS_CLIENT_SECRET`。

IMS權杖端點(`ADOBE_IMS_URL`)必須符合認證的環境。

| 階層 | 一般`ADOBE_IMS_URL` |
| --- | --- |
| QA或分段 | `https://ims-na1-stg1.adobelogin.com` |
| 預先生產或生產 | `https://ims-na1.adobelogin.com` |

>[!NOTE]
>
>這些URL中的`na1`代表已布建目標執行個體的區域。 如果您的執行個體布建在不同區域，請以適當的區域識別碼取代。

`ADOBE_IMS_META_SCOPES`必須符合在該認證上布建的領域。 `.example.env`檔案包含完整的逗號分隔範圍字串作為參考。 只有在Adobe指示您變更時，才能進行變更。

#### 將[!DNL Adobe I/O]認證對應至環境檔案

在[!DNL Developer Console]中，OAuth伺服器對伺服器的值會顯示為使用者端ID和使用者端密碼，與下列JSON結構相對應：

```json
{
  "client_id": "xxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "client_secret": "xxxxxxxxxxxxxxxxxxxxxxxxxxx"
}
```

將它們對應至`.env` （預留位置範例）：

```shell-session
TARGET_ORG_ID=<org_id>@AdobeOrg
ADOBE_IMS_URL=https://ims-na1.adobelogin.com
ADOBE_IMS_CLIENT_ID=xxxxxxxxxxxxxxxxxxxxxxxxxxx
ADOBE_IMS_CLIENT_SECRET=xxxxxxxxxxxxxxxxxxxxxxxxxxx
ADOBE_IMS_META_SCOPES=AdobeID,openid,additional_info.projectedProductContext
```

SaaS API主機在生產前和生產中有所不同。 `TARGET_INSTANCE_REST_URL`和`TARGET_INSTANCE_GRAPHQL_URL`必須使用與移轉相同的Commerce API環境，無論是生產前還是生產環境。 請勿將一個層級與其他層級的CDMS或租使用者混合。

| 環境 | `TARGET_INSTANCE_*_URL`中的一般主機 |
| --- | --- |
| 預先生產或沙箱 | `https://na1-sandbox.api.commerce.adobe.com/{tenantId}` |
| 生產 | `https://na1.api.commerce.adobe.com/{tenantId}` |

>[!NOTE]
>
>這些URL中的`na1`代表已布建目標執行個體的區域。 如果您的執行個體布建在不同區域，請以適當的區域識別碼取代。

```shell-session
TARGET_TENANT_ID=<tenant_id>
TARGET_ORG_ID=<org_id>@AdobeOrg
ADOBE_IMS_URL=https://ims-na1.adobelogin.com
ADOBE_IMS_CLIENT_ID=<client_id>
ADOBE_IMS_CLIENT_SECRET=<client_secret>
ADOBE_IMS_META_SCOPES=AdobeID,openid,additional_info.projectedProductContext
TARGET_INSTANCE_REST_URL=https://na1-sandbox.api.commerce.adobe.com/{tenantId}
TARGET_INSTANCE_GRAPHQL_URL=https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql
```

對於生產SaaS主機，請在兩個`TARGET_INSTANCE_*`個URL中將`na1-sandbox`取代為`na1`。 如上表所示，對該層使用相符的`ADOBE_IMS_URL`。

### 設定CDMS端點

將移轉工具指向符合您要移轉目標環境的CDMS API主機。 在`.env`中設定`CDMS_HOST` （通常是`CDMS_PORT=443`）。 使用單一主機（生產前或生產中），而非同時使用兩者。

| 環境 | 使用時機 | `CDMS_HOST` |
| --- | --- | --- |
| 預先生產 | 生產前或沙箱式執行，非生產CDMS | `https://commerce-data-migration-service-preprod-external.adobe.io` |
| 生產 | 即時生產移轉或切換 | `https://commerce-data-migration-service-prod-external.adobe.io` |

設定或取消註解符合您執行的區塊：

```shell-session
# Pre-production CDMS
CDMS_HOST=https://commerce-data-migration-service-preprod-external.adobe.io
CDMS_PORT=443

# Production CDMS (use for prod cutover only)
# CDMS_HOST=https://na1.api.commerce.adobe.com
# CDMS_PORT=443
```

### 設定商店代碼

`STORE_CODE`是移轉工具用於來源執行個體REST API呼叫、綜合測試客戶建立和資料清理的存放區檢視程式碼。 它也會在載入階段以`x-store-code`標頭的形式傳送。

在`.example.env`中，`STORE_CODE`預設為`default`。 確認這符合您來源執行個體的預設存放區檢視代碼。 若要檢視，請在來源[!UICONTROL Admin]中移至&#x200B;[!UICONTROL **商店**] > [!UICONTROL **所有商店**]，並檢視&#x200B;[!UICONTROL **代碼**]&#x200B;資料行以瞭解應該使用的商店檢視。 如果顯示的程式碼沒有`default`，請更新`.env`中的`STORE_CODE`以符合。

## 設定資料庫連線檔案

>[!VIDEO](https://video.tv.adobe.com/v/3496152)

`.my.cnf`檔案為移轉工具的擷取端提供[!DNL MySQL]個連線設定。 將`.my.cnf.example`複製到專案根目錄中的`.my.cnf`以建立它。 區段名稱必須符合`.env`中的`SOURCE_CONNECTION_NAME`。

對於內部部署或自行託管的來源：

```ini
[<connection-name>]
user=<db_user>
password='<db_password>'
host=<db_host>
port=3306
database=<db_name>
```

>[!NOTE]
>
>執行移轉工具的電腦必須具備來源資料庫的直接網路存取權。 此工具不會自動建立或驗證內部部署連線。 在執行任何移轉命令之前，請確認可從移轉機器存取主機、連線埠和認證。

針對[!DNL Adobe Commerce on Cloud]來源：

```ini
[<connection-name>]
id=<project_id>:<environment>
```

`id=`欄位告訴工具來源是PaaS，並使用`MAGENTO_CLOUD_CLI_TOKEN`觸發通道設定。 `project_id`和`environment`值可在[!DNL Cloud Console]中使用，或透過`magento-cloud project:list`和`magento-cloud environment:list`命令使用。

## 準備網路和執行個體

商店前面的HTTP基本驗證可以封鎖API和工具流量。 請確定移轉所使用的來源URL已停用此功能，或允許工具的路徑，因此REST和GraphQL請求可以到達存放區。

### 在擷取期間維護來源資料庫穩定性

雖然工具會從來源資料庫擷取資料，但其他程式都不應寫入來源資料庫。 同時寫入可能會導致不一致的快照。

- 停止來源上的cron，以及針對擷取視窗執行`bin/magento`或其他寫入器的任何作業系統排程器，或確保它們無法在擷取期間執行。
- 檢閱其他整合，例如ERP、OMS、PIM、自訂工作，以及寫入相同資料庫的第三方API。 暫停或封鎖擷取視窗的寫入，以便在擷取執行時沒有任何專案會變更表格。
- 這補充了維護模式以及通道或資料庫存取。 它們一起減少店面和API流量。 Cron和整合是不同的寫入來源，您必須明確控制這些來源。

### 目標

如果必須在移轉前清除目標目錄，請以小批次（例如一次刪除200個）刪除[!UICONTROL Admin]中的產品，以避免重複目錄衝突和大量刪除逾時。

## 建立並執行移轉

從擷取的專案目錄使用寫入許可權。

### 透過SSH保持工作階段作用中

如果您透過SSH連線，中斷的網路可能會中止殼層，並中斷長時間的移轉。 GNU `screen`命令讓工作階段在伺服器上持續運作：

```bash
screen -S migration          # new session named "migration"
# run ./bin/console commands here; when you want to disconnect without stopping work:
# press Ctrl+A, release, then press d   # detach
screen -ls                   # list sessions
screen -x migration          # reattach to "migration"
```

如果伺服器上有`tmux`，您也可以使用。

### 構建Docker映像

建置`bin/console`使用的[!DNL Docker]影像，包含PHP、CLI和相依性。 在第一次執行之前，或在Dockerfile或基本影像變更之後執行此動作。

```bash
./bin/console build
```

### 啟動支援服務

啟動工具的[!DNL Docker Compose]支援服務，例如本機測試資料庫，以及在`.env`中啟用的選擇性本機服務。 確切的服務取決於您的設定。 在成功建置之後以及殼層、移轉或分階段命令之前執行此命令。

```bash
./bin/console start
```

### 初始化CLI容器

啟動一次CLI容器，讓入口點可以針對已掛載的專案完成安裝，例如視需要進行[!DNL Composer]安裝。 在新的環境中首次執行移轉之前，請執行此工作流程一次。

```bash
./bin/console shell
exit
```

### 執行移轉

此工具支援兩種移轉方法。 選擇適合您使用案例的專案。

#### 單階段移轉

來源執行個體不需要維護模式。 使用單一命令執行完整的移轉管道：

```bash
./bin/console migration
```

指令會依下列順序自動執行所有配管步驟，端對端。

1. **組態檢查** — 驗證環境變數和工具設定。
1. **環境初始化** — 啟動[!DNL Docker]服務、開啟雲端通道（如果適用），以及執行單元測試。
1. **整合測試與CDMS初始化** — 執行整合測試並初始化CDMS API連線。
1. **建立移轉** — 向CDMS註冊移轉並等待目標結構描述分析。 移轉識別碼已儲存至`.migration_id`。
1. **功能測試和測試資料產生** — 執行功能測試並在來源上產生綜合測試資料以進行完整性驗證（如果已啟用）。
1. **資料擷取** — 從來源執行個體擷取資料。
1. **載入目標** — 將擷取的資料載入目標[!DNL Adobe Commerce as a Cloud Service]執行個體。 在來源上清理中繼檢視，並透過REST與載入同時移除來源測試資料。
1. **資料完整性驗證** — 觸發總和檢查碼驗證並執行本機API驗證測試。 結果會記錄下來，失敗不會停止管道。
1. **目標**&#x200B;上的測試資料清理 — 從目標執行個體移除綜合測試資料。
1. **處理結果** — 產生移轉摘要，並可選擇從儲存裝置下載成品。

當不需要維護時段時（這是端對端練習、開發或沙箱環境的典型情況，或任何在擷取期間來源可以保持即時狀態的移轉），即可使用此選項。

>[!WARNING]
>
>當需要凍結的來源時（例如任何在擷取期間不得發生新訂單或資料變更的生產移轉），請勿使用此選項。 請改用分階段移轉。 請勿在分階段維護工作流程內將此命令當做步驟使用。

#### 使用維護模式進行多階段移轉

來源例項需要維護模式，以確保提取期間的資料一致性。 移轉會分成不同的階段，您必須依順序執行。

>[!NOTE]
>
>涉及兩個不同的CLI。 `./bin/console`命令從移轉工具專案根目錄執行。 `bin/magento maintenance:*`命令會在來源[!DNL Adobe Commerce]應用程式伺服器上執行，透過SSH連線至安裝根目錄，或透過[!UICONTROL Admin]。 工具不會代表您發出[!DNL Magento]個維護命令。

| 階段 | 執行者 | Source州別 |
| --- | --- | --- |
| 1. `migration:before-maintenance` | 工具 | 即時 — 尚未啟用維護 |
| &#x200B;2. 啟用維護模式 | 手動 | 轉換為凍結 |
| 3. `migration:during-maintenance` | 工具 | 凍結 — 在此階段不要停用維護 |
| &#x200B;4. 停用維護模式 | 手動（視條件而定） | 轉換來源執行個體回到即時狀態 |
| &#x200B;5. `migration:cleanup` （選擇性） | 工具 | 已上線 — 必須已停止維護 |

**階段1 — 維護之前（來源已上線）**

在來源執行個體上線並接受流量時執行。 來源的REST和GraphQL存取權必須完整可用。 請勿在此階段完成之前啟用維護模式。

返回伺服器根目錄並執行：

```bash
./bin/console migration:before-maintenance
```

1. **組態檢查** — 驗證環境變數和工具設定。
1. **環境初始化** — 啟動[!DNL Docker]服務、開啟PaaS雲端通道（如果適用）並執行單元測試。
1. **整合測試與CDMS初始化** — 執行整合測試並初始化CDMS API連線。
1. **建立移轉** — 向CDMS註冊移轉並等待目標結構描述分析。 移轉識別碼已儲存至`.migration_id`。
1. **功能測試** — 針對即時來源執行功能測試。
1. **測試資料產生** — 在來源上建立綜合測試客戶和訂單以進行完整性驗證（如果已啟用）。

**階段2 — 啟用維護模式（手動）**

在來源上啟用維護模式，並暫停寫入或影響資料庫的所有活動，包括排程工作、協力廠商整合、訂單處理和媒體資產同步。

在來源Commerce伺服器（安裝根目錄）上，執行：

```bash
bin/magento maintenance:enable
```

**階段3 — 維護期間（來源已凍結）**

在維護模式下使用來源執行個體執行。 來源必須在此階段的整個期間保持凍結。 在&#x200B;**階段3**&#x200B;成功完成之前，請勿停用維護模式。

```bash
./bin/console migration:during-maintenance
```

1. **雲端通道設定** — 針對[!DNL Adobe Commerce on Cloud]來源執行個體，重新開啟雲端通道並驗證資料庫連線。 已針對內部部署執行個體自動略過。
1. **資料擷取** — 從凍結的來源執行個體擷取資料。
1. **臨時檢視清理** — 使用直接資料庫連線（在維護模式下安全）從來源移除臨時檢視。
1. **載入目標** — 將擷取的資料載入目標[!DNL Adobe Commerce as a Cloud Service]執行個體並等待完成。
1. **資料完整性驗證** — 觸發CDMS總和檢查碼驗證並執行本機API驗證測試。 結果會記錄下來，失敗不會停止管道。
1. **目標**&#x200B;上的測試資料清理 — 從目標執行個體移除綜合測試資料。
1. **處理結果** — 產生移轉摘要，並可選擇從儲存裝置下載成品。

**階段4 — 停用維護模式（手動，條件式）**

此階段會停用維護模式，並重新啟用來源執行個體的流量。 在執行清除階段之前需要此步驟，因為清除會透過REST與來源通訊，如果維護模式仍在作用中，則失敗為`HTTP 503`。

在來源Commerce伺服器上，執行：

```bash
bin/magento maintenance:disable
```

**階段5 — 清除（選擇性，來源必須為即時）**

透過REST從來源執行個體移除在&#x200B;**階段1**&#x200B;中建立的綜合測試客戶和訂單。 此階段只能在停用維護模式後執行。

>[!NOTE]
>
>如果`SKIP_TEST_DATA_CREATION=true`設定在`.env`中，則跳過此階段，因為未建立任何測試資料。

返回伺服器根目錄並執行：

```bash
./bin/console migration:cleanup
```

1. **資料庫連線設定** — 針對[!DNL Adobe Commerce on Cloud]個來源執行個體，重新開啟雲端通道。 對於內部部署執行個體，建立並驗證直接的資料庫連線。
1. **Source REST清理** — 透過REST API從來源移除綜合測試客戶和訂單。

## 繼續或重新執行移轉

移轉工具使用專案根目錄中的`.migration_id`檔案來追蹤進度。 此檔案會在新的移轉開始時自動建立，並記錄目前的移轉識別碼。

### 失敗後繼續

如果移轉執行失敗或中斷，請重新執行相同的命令以從上一個成功的步驟（擷取、載入或驗證）繼續，而不是從頭開始重新啟動。 已完成的步驟會自動跳過。

>[!IMPORTANT]
>
>當您繼續`migration:during-maintenance`階段時，來源必須始終保持維護模式。 如果來源已停止維護，或資料在執行之間變更，則繼續移轉可能會產生不一致的結果。

### 開始全新的移轉

若要捨棄先前執行並啟動全新的移轉，請在開始下一次移轉之前刪除`.migration_id`檔案：

```bash
rm .migration_id
```

如果`.migration_id`存在且前一個移轉已經完成，工具會列印一則訊息，指出移轉已經完成，並建議您刪除檔案。

## 檢閱記錄檔並偵錯

所有移轉記錄檔都會寫入專案根目錄中的`logs/`目錄，並組織成時間戳記子目錄：

```text
logs/
  2026-03-23_14-30-00/     ← one directory per run
    index.log              ← main pipeline log (start here)
    ...
```

- `index.log`是主要管道協調流程記錄檔。 如果步驟失敗，會顯示哪個指令碼以非零程式碼結束，以及原因。
- 每個步驟的記錄，例如`09b_run_load.log`和`11_verify_data_integrity_local.log`，包含每個階段的詳細輸出。
