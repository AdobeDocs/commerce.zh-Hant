---
title: 安裝
description: 瞭解如何安裝 [!DNL Catalog Service]
exl-id: 3f8492c3-f76d-49b7-a201-35deace36a1d
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案(Adobe管理的PaaS基礎結構)和內部部署專案的Adobe Commerce 。"
source-git-commit: d07f36a71247a96bc2dd950867c2862205238d88
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---

# 上線和安裝

安裝目錄服務，以使用[目錄服務GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)從Commerce執行個體要求及接收產品資料。 目錄服務是以repo.magento.com存放庫中Composer中繼資料的形式提供。

>[!NOTE]
>
>如果您的Commerce執行個體使用即時搜尋或產品推薦，當您載入或升級這些服務時，目錄服務會自動安裝或更新。 如需詳細資訊，請參閱[即時搜尋](https://experienceleague.adobe.com/zh-hant/docs/commerce/live-search/install)和[產品建議](https://experienceleague.adobe.com/zh-hant/docs/commerce/product-recommendations/getting-started/install-configure)的安裝指示。


## 系統需求

**軟體需求**

- Adobe Commerce 2.4.4+
- PHP 8.1、8.2、8.3、8.4
- Composer： 2.x

**支援的平台**

- 雲端基礎結構上的Adobe Commerce： 2.4.4+
- Adobe Commerce內部部署： 2.4.4+

## 端點

[!DNL Catalog Service]有兩個可用於上線的端點：

- 沙箱(`https://catalog-service-sandbox.adobe.io/graphql`) — 用於上線前的測試和驗證
- 製作(`https://catalog-service.adobe.io/graphql`) — 用於Commerce商家和網站的即時流量

所有Commerce測試執行個體都使用沙箱端點。

在沙箱端點上執行所有載入測試。 開始載入測試之前，請先提交[支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=zh-Hant#submit-ticket)，讓服務團隊可以預期額外的伺服器流量。

## 安裝和設定

若要開始使用Adobe Commerce的[!DNL Catalog Service]，必須執行下列步驟：

- 安裝目錄服務延伸模組(`magento/catalog-service`)
- 設定服務與資料匯出
- 存取服務

### 安裝目錄服務擴充功能

>[!BEGINSHADEBOX]

**先決條件**

- 存取[repo.magento.com](https://repo.magento.com)以安裝擴充功能。 如需金鑰產生與取得必要許可權，請參閱[取得您的驗證金鑰](https://experienceleague.adobe.com/zh-hant/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)。 如需雲端安裝，請參閱[雲端基礎結構上的Commerce指南](https://experienceleague.adobe.com/zh-hant/docs/commerce-cloud-service/user-guide/develop/authentication-keys)

- 存取Adobe Commerce應用程式伺服器的命令列。

>[!ENDSHADEBOX]

在執行Adobe Commerce 2.4.4版或更新版本的Adobe Commerce執行個體上安裝最新版本的目錄服務擴充功能(`magento/catalog-service`)。 目錄服務是以Composer中繼資料的形式從[repo.magento.com](https://repo.magento.com)存放庫傳送。

>[!BEGINTABS]

>[!TAB 雲端基礎結構]

使用此方法來安裝Commerce Cloud執行個體的[!DNL Catalog Service]。

1. 在本機工作站上，變更至雲端基礎結構專案上Adobe Commerce的專案目錄。

   >[!NOTE]
   >
   >如需有關在本機管理Commerce專案環境的資訊，請參閱《雲端基礎結構使用手冊》中[Adobe Commerce的](https://experienceleague.adobe.com/zh-hant/docs/commerce-cloud-service/user-guide/develop/cli-branches)使用CLI管理分支&#x200B;__。

1. 檢視環境分支，以使用Adobe Commerce Cloud CLI進行更新。

   ```shell
   magento-cloud environment:checkout <environment-id>
   ```

1. 新增目錄服務模組。

   ```bash
   composer require magento/catalog-service --no-update
   ```

1. 更新套件相依性。

   ```bash
   composer update "magento/catalog-service"
   ```

1. 認可並推播對`composer.json`和`composer.lock`檔案的程式碼變更。

1. 新增、認可並將`composer.json`和`composer.lock`檔案的程式碼變更推播到雲端環境。

   ```shell
   git add -A
   git commit -m "Add catalog service module"
   git push origin <branch-name>
   ```

   將更新推播到雲端環境會啟動[Commerce雲端部署程式](https://experienceleague.adobe.com/zh-hant/docs/commerce-cloud-service/user-guide/develop/deploy/process)以套用變更。 從[部署記錄](https://experienceleague.adobe.com/zh-hant/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log)檢查部署狀態。

>[!TAB 內部部署]

使用此方法來安裝內部部署執行個體的[!DNL Catalog Service]。

1. 使用Composer將目錄服務模組新增至您的專案：

   ```bash
   composer require magento/catalog-service --no-update
   ```

1. 更新相依性並安裝擴充功能：

   ```bash
   composer update  "magento/catalog-service"
   ```

1. 升級Adobe Commerce：

   ```bash
   bin/magento setup:upgrade
   ```

1. 清除快取：

   ```bash
   bin/magento cache:clean
   ```

   >[!TIP]
   >
   >在某些情況下，特別是部署到生產時，您可能希望避免清除編譯的程式碼，因為可能需要一些時間。 在進行任何變更之前，請務必先備份系統。

>[!ENDTABS]

### 設定服務與資料匯出

安裝[!DNL Catalog Service]之後，請完成下列工作，將目錄服務與您的Adobe Commerce執行個體整合。 此整合可實現Commerce執行個體、目錄服務和其他支援服務之間的資料同步和通訊。 資料同步處理由[SaaS Data Export擴充功能](../data-export/overview.md)處理。

1. 設定[Commerce Services Connector](https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/integration-services/saas)，方法是指定API金鑰並選取SaaS資料空間。

   Commerce服務聯結器設定為使用Adobe Commerce服務（例如目錄服務、即時搜尋和產品建議）所需的一次性程式。 如果您已經為另一個服務設定了聯結器，請略過此步驟。

1. 從[資料管理儀表板](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/systems/data-transfer/data-dashboard)執行初始資料同步。

   視目錄大小而定，初始同步可能需要幾分鐘到幾小時的時間。 您可以從「資料管理」控制面板監視同步化狀態。 初始同步後，「目錄」會持續匯出產品資料，以保持服務在最新狀態。

   >[!NOTE]
   >
   >您也可以使用Commerce CLI從命令列啟動初始同步。 請參閱[SaaS Data Export Guide](../data-export/data-export-cli-commands.md#initial-sync)中的&#x200B;_Initial sync_。

若要確保目錄匯出可正確執行：

- [確認cron工作正在執行](https://experienceleague.adobe.com/zh-hant/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues)。
- 請確認索引子是從[Admin](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/systems/tools/index-management)執行，或使用Commerce CLI命令`bin/magento indexer:info`執行。
- 確認`Catalog Attributes Feed, Product Feed, Product Overrides Feed`和`Product Variant Feed`索引子已設定為`Update by Schedule`。

### 監控資料同步並疑難排解

透過Commerce Admin，您可以使用[資料管理控制面板](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/systems/data-transfer/data-dashboard)來監視同步化程式。 使用[Commerce CLI](../data-export/data-export-cli-commands.md#troubleshooting)和記錄檔來管理和疑難排解程式。
