---
title: 目錄配接器擴充功能
description: 使用目錄配接器從Commerce Services呈現價格
seo-title: Catalog Adapter Extension
seo-description: Using Catalog Adapter to render prices from Commerce Services
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 0%

---

# 目錄配接器

`[!DNL Catalog Adapter]`擴充功能會停用Commerce應用程式中包含的預設產品價格索引器，並改用[目錄服務](../catalog-service/overview.md)提供的價格。

介面卡設計來搭配[SaaS資料匯出](../data-export/overview.md)和Adobe Commerce服務使用。 SaaS資料匯出負責提交價格，而[!DNL Catalog Adapter]會從Adobe Commerce服務擷取所有價格。

當您啟用[!DNL Catalog Adapter]時，價格索引和作業會以下列方式受到影響：

- Adobe Commerce應用程式中包含的價格索引器已停用。
- 使用SaaS資料匯出和[SaaS價格索引器](price-indexing.md)來管理價格。
- 當客戶開啟產品、類別或其他顯示產品價格的頁面時，價格會從Adobe Commerce服務擷取。
- 價格會透過同步處理[SaaS資料匯出](../data-export/overview.md)的資料來傳送至Adobe Commerce服務。
- 結帳會動態重新計算價格。

您可以移除或停用目錄轉接器擴充功能，以在Commerce應用程式中重新啟用價格索引。

## 需求

- Adobe Commerce 2.4.4+
- 已安裝下列Commerce服務之一：

   - [即時搜尋](../live-search/install.md)
   - [產品推薦](../product-recommendations/install-configure.md)
   - [目錄服務](../catalog-service/installation.md)

## 安裝

Catalog Adapter擴充功能是Composer中繼套件，可安裝下列模組：

- **價格索引器停用程式** — 此模組會停用Commerce應用程式中的價格索引，以便透過SaaS價格索引來傳遞價格。 安裝SaaS價格索引擴充功能時，無法開啟Commerce應用程式中的產品價格索引器。
- **價格提供者** — 此模組提供來自Adobe Commerce服務的產品價格。 它會形成搜尋查詢並取得前端產品的價格。
- **目錄服務搜尋配接器** — 此模組會回應產品搜尋要求，將價格從Adobe Commerce應用程式傳輸至Adobe Commerce服務。

## 安裝步驟

>[!BEGINTABS]

>[!TAB 雲端基礎結構]

使用此方法來安裝Commerce Cloud執行個體的[!DNL Catalog Adapter]。

1. 在本機工作站上，變更至雲端基礎結構專案上Adobe Commerce的專案目錄。

   >[!NOTE]
   >
   >如需有關在本機管理Commerce專案環境的資訊，請參閱《雲端基礎結構使用手冊》中&#x200B;_Adobe Commerce的[使用CLI管理分支](https://experienceleague.adobe.com/zh-hant/docs/commerce-cloud-service/user-guide/develop/cli-branches)_。

1. 檢視環境分支，以使用Adobe Commerce Cloud CLI進行更新。

   ```shell
   magento-cloud environment:checkout <environment-id>
   ```

1. 新增目錄配接器模組。

   ```bash
   composer require magento/catalog-adapter --no-update
   ```

1. 更新套件相依性。

   ```bash
   composer update "magento/catalog-adapter"
   ```

1. 認可並推播對`composer.json`和`composer.lock`檔案的程式碼變更。

1. 新增、認可並將`composer.json`和`composer.lock`檔案的程式碼變更推播到雲端環境。

   ```shell
   git add -A
   git commit -m "Add catalog adapter module"
   git push origin <branch-name>
   ```

   將更新推播到雲端環境會啟動[Commerce雲端部署程式](https://experienceleague.adobe.com/zh-hant/docs/commerce-cloud-service/user-guide/develop/deploy/process)以套用變更。 從[部署記錄](https://experienceleague.adobe.com/zh-hant/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log)檢查部署狀態。

>[!TAB 內部部署]

使用此方法來安裝內部部署執行個體的[!DNL Catalog Adapter]。

1. 使用Composer將目錄轉接器新增到您的專案：

   ```bash
   composer require magento/catalog-adapter --no-update
   ```

1. 更新相依性並安裝擴充功能：

   ```bash
   composer update  "magento/catalog-adapter"
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


## 重新啟用Adobe Commerce產品價格索引器

如果您有協力廠商應用程式依賴預設的Adobe Commerce產品價格索引器，則可以使用下列命令將其重新啟用：

```bash
# re-enable Product Price indexer
bin/magento module:disable Magento_PriceIndexerDisabler
# re-index Product Price indexer
bin/magento index:reindex catalog_product_price
```

## 停用Headless店面案例的產品價格索引器

如果您有Headless Commerce執行個體，您可能需要停用Adobe Commerce產品價格索引器，以減少Adobe Commerce執行個體的負載。 您可以透過安裝`magento/module-price-indexer-disabler`模組來完成此工作：

```bash
composer require magento/module-price-indexer-disabler
```

## 使用案例

以下是一些常見的`[!DNL Catalog Adapter]`案例。

### Adobe Commerce產品價格索引器沒有相依性

- 您是已安裝必要服務（即時搜尋、產品推薦、目錄服務）的Luma或Adobe Commerce Core GraphQL商家
- 沒有與依賴Adobe Commerce產品價格索引器的第三方擴充功能整合

1. 安裝[!DNL Catalog Adapter]。

### 依賴於Adobe Commerce產品價格索引器

- 您是Luma或Adobe Commerce Core GraphQL商家，已安裝支援服務（即時搜尋、產品推薦、目錄服務）
- 您使用依賴Adobe Commerce產品價格索引器的第三方擴充功能

1. 安裝[!DNL Catalog Adapter]。
1. 重新啟用預設的Adobe Commerce產品價格索引器。

### Headless Commerce執行個體

- 具有已安裝所需服務（即時搜尋、產品推薦、目錄服務）的Headless Commerce執行個體的商家
- 不依賴預設的Adobe Commerce產品價格索引器

1. 從[!DNL Catalog Adapter]封裝安裝`magento/module-price-indexer-disabler`模組。

