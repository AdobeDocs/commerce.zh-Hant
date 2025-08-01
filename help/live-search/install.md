---
title: 開始使用 [!DNL Live Search]
description: 從Adobe Commerce瞭解 [!DNL Live Search] 的系統需求和安裝步驟。
role: Admin, Developer
exl-id: 45b985f1-9afb-4a07-93e8-f2fe231c5400
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案(Adobe管理的PaaS基礎結構)和內部部署專案的Adobe Commerce 。"
source-git-commit: b1cf82f09c934dd585c350f82cbf258d8c1d002c
workflow-type: tm+mt
source-wordcount: '3147'
ht-degree: 0%

---

# 設定以透過[!DNL Live Search]成功

Adobe Commerce [!DNL Live Search]與[[!DNL Catalog Service]](../catalog-service/guide-overview.md)共同合作，提供效能、相關且直覺式的搜尋解決方案，讓您的客戶快速找到他們所需的專案。 具體來說，[!DNL Catalog Service]會呈現您的目錄資料以供SaaS服務使用，例如[!DNL Live Search]。

本文提供使用[!DNL Live Search]實作[!DNL Catalog Service]的逐步指示。

## 對象

本文適用於負責安裝和設定Adobe Commerce執行個體的開發人員或團隊中的系統整合商。

## 需求

- [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) 2.4.4+
- PHP 8.1、8.2或8.3
- [!DNL Composer]
- 執行cron工作和索引子

>[!IMPORTANT]
>
>在實作[!DNL Live Search]之前，請參閱[界限和限制](boundaries-limits.md)區段以確保[!DNL Live Search]符合您的業務需求。

## 重要更新

- 截至[!DNL Live Search] 3.0.2，[!DNL Catalog Service]擴充功能已隨安裝一併提供。

- 鑑於Elasticsearch 7於2023年8月宣佈終止支援，Adobe建議所有Adobe Commerce客戶移轉至OpenSearch 2.x搜尋引擎。 如需在產品升級期間移轉搜尋引擎的相關資訊，請參閱[升級指南](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/prepare/opensearch-migration)中的&#x200B;_移轉至OpenSearch_。

## 支援平台

- 雲端上的Adobe Commerce (ECE) ： 2.4.4+
- Adobe Commerce內部部署(EE) ： 2.4.4+

## 工作流程概觀

從高層面來看，上線[!DNL Live Search]需要您：

1. [安裝](#1-install-the-live-search-extension) [!DNL Live Search]延伸模組
1. [設定](#2-configure-api-keys) API金鑰
1. [同步處理](#3-sync-your-catalog-data)您的目錄資料
1. [驗證](#4-verify-that-the-data-was-exported)目錄資料是否已匯出
1. [設定](#5-configure-the-data)資料
1. [測試](#6-test-the-connection)連線
1. [驗證](#7-validate-events-are-capturing-data)事件正在擷取資料
1. [自訂](#8-customize-for-your-storefront)您的店面

## 1.安裝[!DNL Live Search]擴充功能

已從[!DNL Live Search]Adobe Marketplace[透過](https://commercemarketplace.adobe.com/magento-live-search.html)Composer[將](https://getcomposer.org/)安裝為擴充功能。 安裝並設定[!DNL Live Search]後，Adobe [!DNL Commerce]會開始與SaaS服務共用搜尋和目錄資料。 此時，*管理員*&#x200B;使用者可以設定、自訂及管理搜尋Facet、同義字及銷售規則。

>[!BEGINTABS]

>[!TAB 新Commerce執行個體]

如果您在新的Commerce執行個體上安裝[!DNL Live Search]，請依照這些指示操作。

1. 確認[cron工作](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs)和[索引子](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management)正在執行。

1. 使用Composer將「即時搜尋」模組新增至您的專案：

   ```bash
   composer require magento/live-search --no-update
   ```

1. 更新相依性並安裝擴充功能：

   ```bash
   composer update magento/live-search --with-dependencies
   ```

1. 暫時停用[!DNL OpenSearch]和相關模組，並安裝[!DNL Live Search]。

   ```bash
   bin/magento module:disable Magento_ Magento_Elasticsearch8 Magento_Elasticsearch7 Magento_OpenSearch Magento_ElasticsearchCatalogPermissions Magento_InventoryElasticsearch Magento_ElasticsearchCatalogPermissionsGraphQl
   ```

   [!DNL Elasticsearch]會繼續從店面管理搜尋要求，而[!DNL Live Search]服務會在背景同步目錄資料和索引產品。

1. 安裝更新。

   ```bash
   bin/magento setup:upgrade
   ```

1. 確認下列[索引子](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management)已設定為「依排程更新」：

   - 產品摘要
   - 產品變體摘要
   - 目錄屬性摘要
   - 產品價格摘要
   - 範圍網站資料摘要
   - 範圍客戶群組資料摘要
   - 類別摘要
   - 類別許可權摘要

驗證索引器後，下一步是[設定API金鑰](#2-configure-api-keys)。

>[!TAB 現有的Commerce執行個體]

如果您要在現有的Commerce執行個體上安裝[!DNL Live Search]，請依照這些指示操作。

1. 確認[cron工作](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs)和[索引子](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management)正在執行。

1. 使用Composer將「即時搜尋」模組新增至您的專案：

   ```bash
   composer require magento/live-search --no-update
   ```

1. 更新相依性並安裝擴充功能：

   ```bash
   composer update magento/live-search --with-dependencies
   ```

1. 停用提供店面搜尋結果的[!DNL Live Search]模組。

   ```bash
   bin/magento module:disable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover Magento_LiveSearchProductListing
   ```

   [!DNL Elasticsearch]會繼續從店面管理搜尋要求，而[!DNL Live Search]服務會在背景同步目錄資料和索引產品。

1. 安裝更新。

   ```bash
   bin/magento setup:upgrade
   ```

1. 確認下列[索引子](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management)已設定為「依排程更新」：

   - 產品摘要
   - 產品變體摘要
   - 目錄屬性摘要
   - 產品價格摘要
   - 範圍網站資料摘要
   - 範圍客戶群組資料摘要
   - 類別摘要
   - 類別許可權摘要

1. 啟用[!DNL Live Search]擴充功能，並停用[!DNL OpenSearch] (Magento Elasticsearch和OpenSearch模組)。

   ```bash
   bin/magento module:enable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover  Magento_LiveSearchProductListing
   ```

   ```
   bin/magento module:disable Magento_Elasticsearch Magento_Elasticsearch6 Magento_Elasticsearch7 Magento_Elasticsearch8 Magento_OpenSearch Magento_ElasticsearchCatalogPermissions Magento_InventoryElasticsearch Magento_ElasticsearchCatalogPermissionsGraphQl
   ```

   >[!NOTE]
   >
   >disable命令包含支援OpenSearch的Commerce模組清單。 如果您的Commerce執行個體未安裝模組，您將會看到`module does not exist`錯誤。

1. 安裝更新。

   ```bash
   bin/magento setup:upgrade
   ```

驗證索引器後，下一步是[設定API金鑰](#2-configure-api-keys)。

>[!ENDTABS]

### 安裝[!DNL Live Search]測試版

>[!IMPORTANT]
>
>以下功能為測試版。 若要參與測試版，請傳送電子郵件要求給[commerce-storefront-services](mailto:commerce-storefront-services@adobe.com)。

此Beta版支援[`productSearch`查詢](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/)的三個新功能：

- **分層搜尋** — 在另一個搜尋內容中搜尋 — 使用此功能，您最多可以執行兩個層級的搜尋來搜尋您的搜尋查詢。 例如：

   - **第1層搜尋** — 搜尋&quot;product_attribute_1&quot;上的&quot;motor&quot;
   - **第2層搜尋** — 搜尋「product_attribute_2」上的「零件編號123」。 此範例會在結果中搜尋「馬達」的「零件編號123」。

  分層搜尋可用於`startsWith`搜尋索引和`contains`搜尋索引，如下所述：

- **startsWith搜尋索引** — 使用`startsWith`索引搜尋。 這項新功能可讓：

   - 搜尋屬性值以特定字串開頭的產品。
   - 設定「結尾為」搜尋，讓購物者可以搜尋屬性值結尾為特定字串的產品。 若要啟用「結尾為」搜尋，需要反向擷取產品屬性，且API呼叫也應是反向字串。

- **包含搜尋索引** — 使用包含索引來搜尋屬性。 這項新功能可讓：

   - 在較大的字串中搜尋查詢。 例如，如果購物者搜尋字串「HAPE-123」中的產品編號「PE-123」。

     >[!NOTE]
     >
     >此搜尋型別與執行自動完成搜尋的現有[片語搜尋](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#phrase)不同。 例如，如果您的產品屬性值是&quot;outdoor pants&quot;，則短語搜尋會傳回&quot;out pan&quot;的回應，但不會傳回&quot;oor ants&quot;的回應。 但是，「包含搜尋」會傳回「或螞蟻」的回應。

這些新條件會增強搜尋查詢篩選機制，以縮小搜尋結果。 這些新條件不會影響主要搜尋查詢。

您可以在搜尋結果頁面上實作這些新條件。 例如，您可以在頁面上新增區段，讓購物者可以進一步縮小搜尋結果。 您可以允許購物者選取特定產品屬性，例如「製造商」、「零件編號」和「說明」。 從該位置，他們使用`contains`或`startsWith`條件在這些屬性中搜尋。 如需可搜尋的[屬性](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types)清單，請參閱管理員指南。

1. 若要安裝測試版，請在專案中新增下列相依性：

   ```bash
   composer require magento/module-live-search-search-types:"^1.0.0-beta1"
   ```

1. 認可並將變更推送至您的`composer.json`和`composer.lock`檔案至雲端專案。 [了解更多](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/extensions#upgrade-an-extension)。

   此Beta版在Admin中新增&#x200B;**[!UICONTROL Search types]**、**[!UICONTROL Autocomplete]**&#x200B;和&#x200B;**[!UICONTROL Contains]**&#x200B;的&#x200B;**[!UICONTROL Starts with]**&#x200B;核取方塊。 它也會更新[`productSearch`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability) GraphQL API，以包含這些新搜尋功能。

1. 在Admin中，[將產品屬性](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes-add#step-5-describe-the-storefront-properties)設定為可搜尋，並指定該屬性的搜尋功能，例如&#x200B;**包含** （預設）或&#x200B;**開頭為**。 您最多可以為&#x200B;**Contains**&#x200B;指定6個要啟用的屬性，並為&#x200B;**Starts with**&#x200B;指定6個要啟用的屬性。 若為測試版，請注意，管理員不會強制執行此限制，但會在API搜尋中強制執行。

   ![指定搜尋功能](./assets/search-filters-admin.png)

1. 請參閱[開發人員檔案](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability)，瞭解如何使用新的[!DNL Live Search]和`contains`搜尋功能更新您的`startsWith` API呼叫。

### 欄位說明

| 欄位 | 說明 |
|--- |--- |
| `Autocomplete` | 預設為啟用，無法修改。 透過`Autocomplete`，您可以在`contains`搜尋篩選器[中使用](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering)。 此處，`contains`中的搜尋查詢會傳回自動完成型別搜尋回應。 Adobe建議您使用此型別的搜尋來搜尋說明欄位，這些欄位通常超過50個字元。 |
| `Contains` | 啟用真正的「字串中包含的文字」搜尋，而非自動完成搜尋。 在`contains`搜尋篩選器[中使用](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability)。 如需詳細資訊，請參閱[限制](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#limitations)。 |
| `Starts with` | 以特定值開頭的查詢字串。 在`startsWith`搜尋篩選器[中使用](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability)。 |

## 2.設定API金鑰

必須有Adobe Commerce API金鑰及其相關的私密金鑰，才能將[!DNL Live Search]連線至Adobe Commerce的安裝。 API金鑰是在[!DNL Commerce]授權持有者的帳戶中產生和維護的，該帳戶可與開發人員或系統整合商共用。 開發人員可以代表授權持有人建立和管理SaaS資料空間。 如果您已經有一組API金鑰，則不需要重新產生。

在[Commerce Services Connector](../landing/saas.md)文章中瞭解如何設定您的API金鑰。

## 3.同步處理您的目錄資料

[!DNL Live Search]將目錄資料移動到Adobe的SaaS基礎結構。 資料會編制索引，而搜尋結果會從此索引直接傳送到店面。 根據大小和複雜性，索引可能需要30分鐘到數小時的時間。

若要開始將目錄資料初始同步至SaaS服務，請依此順序執行下列命令：

```bash
bin/magento saas:resync --feed productattributes
bin/magento saas:resync --feed products
bin/magento saas:resync --feed scopesCustomerGroup
bin/magento saas:resync --feed scopesWebsite
bin/magento saas:resync --feed prices
bin/magento saas:resync --feed productoverrides
bin/magento saas:resync --feed variants
bin/magento saas:resync --feed categories
bin/magento saas:resync --feed categoryPermissions
```

當您執行這些命令時，會開始將目錄資料與SaaS服務進行初始同步。

>[!WARNING]
>
>同步期間無法使用搜尋和類別瀏覽操作。 視目錄大小而定，此程式可能需要1小時以上的時間。

### 監視同步處理進度

使用[資料管理儀表板](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard)監視同步處理進度。 此儀表板提供您店面產品資料可用性的寶貴見解，確保可及時向客戶顯示。

![資料管理儀表板](assets/data-management-dashboard.png)

您也可以使用[Commerce CLI](../data-export/data-export-cli-commands.md#troubleshooting)和資料匯出擴充功能記錄檔，執行同步處理命令並疑難排解同步處理程式。

#### 未來的產品更新

初始同步後，增量產品更新最多可能需要15分鐘才能用於店面搜尋。 若要深入瞭解，請參閱索引檔案中的[串流產品更新](indexing.md)。

## 4.確認資料已匯出

若要檢查您的目錄資料是否已從Adobe Commerce匯出並與[!DNL Live Search]同步，您有幾個選擇：

- 在下清單格中尋找專案：

   - `cde_products_feed`
   - `cde_product_attributes_feed`

  >[!NOTE]
  >
  >如果您收到`table does not exist`錯誤，請尋找`catalog_data_exporter_products`和`catalog_data_exporter_product_attributes`表格中的專案。 這些資料表名稱用於4.2.1之前的[!DNL Live Search]版本。

- 搭配預設查詢使用[GraphQL遊樂場](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/graphql) (如需詳細資訊，請參閱[GraphQL參考資料](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/))以驗證下列專案：

   - 傳回的產品計數接近您對商店檢視的預期。
   - 會傳回多面向。

如需其他說明，請參閱支援知識庫中的[[!DNL Live Search] 目錄未同步](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-catalog-data-sync)。

## 5.設定資料

正確設定您的產品資料可確保為您的客戶帶來良好的搜尋結果。 您可以在此區段中啟用產品清單Widget並指派類別。

### 啟用產品清單Widget

安裝[!DNL Live Search] 4.0.0+時，預設會啟用產品清單Widget。 Widget啟用時，搜尋結果和類別瀏覽產品清單頁面會使用不同的UI元件。 此UI元件會直接呼叫[目錄服務API](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/)，如此可加快回應時間。

如果您的[!DNL Live Search]版本早於4.0.0+，則必須手動啟用產品清單Widget。

1. 從&#x200B;*管理員*，前往&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在&#x200B;**[!UICONTROL Live Search]**&#x200B;下，選取&#x200B;**[!UICONTROL Storefront Features]**。
1. 將&#x200B;**[!UICONTROL Enable Product Listing Widgets]**&#x200B;設為`Yes`。

   ![啟用產品清單Widget](assets/ls-admin-enable-widget.png)

當您變更此設定時，會出現訊息`Page cache is invalidated`。 您需要清除Magento快取以儲存變更。

1. 執行下列其中一項作業來存取[快取管理](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/cache-management)頁面：

   - 按一下工作區上方訊息中的&#x200B;**[!UICONTROL Cache Management]**&#x200B;連結。
   - 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL System]** > _[!UICONTROL Tools]_>**[!UICONTROL Cache Management]**。

1. 選取&#x200B;**組態** [!UICONTROL Cache Type]並按一下&#x200B;**[!UICONTROL Flush Magento Cache]**。

   排清快取後，立即變更店面。

### 指派類別

在[!DNL Live Search]中傳回的產品必須指派給[類別](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/categories)。 例如，在Luma中，產品分為「男性」、「女性」和「齒輪」等類別。 也會為「Top」、「Bottoms」和「Watch」設定子類別。 這些類別指派可改善篩選時的精細度。

## 6.測試連線

現在，如果您的目錄資料在SaaS中，請進行測試以確保在以下情況下傳回產品資料：

- [!UICONTROL Search]方塊正確傳回結果
- 類別瀏覽正確傳回結果
- Facet在搜尋結果頁面上可作為篩選使用

如果一切正常運作，[!DNL Live Search]已安裝、連線且隨時可使用。

如果在店面發生問題，請檢查`var/log/system.log`檔案中的API通訊失敗或服務端發生錯誤。

若要允許[!DNL Live Search]通過防火牆，請新增`commerce.adobe.io`至允許清單。

## 7.確認事件正在擷取資料

確保部署到您網站的店面事件可正常運作。 此檢查對Headless實施尤其重要。

- 檢閱[所需的](events.md)事件[!DNL Live Search]。
- 確定[[!DNL Live Search] 儀表板](performance.md)顯示的是來自非生產環境的資料。
- [驗證事件集合](../product-recommendations/verify.md)。 此頁面位於[!DNL Product Recommendations]指南中，驗證步驟也適用於[!DNL Live Search]。

## 8.為您的店面量身打造

您已安裝[!DNL Live Search]擴充功能、同步處理、驗證及設定您的資料。 下一步是確保[!DNL Live Search] Widget符合您商店的外觀與風格。

您可以視需要定義自訂CSS規則，以設定彈出視窗和PLP Widget的樣式。 請參閱[樣式彈出視窗元素](storefront-popover.md#styling-popover-example)和[產品清單頁面Widget](plp-styling.md#styling-example)。

如果您想要擴充Widget的功能，每個元件的原始碼都可在公用存放庫中取得。
在這種情況下，您可以根據自己的需求自訂JavaScript，然後在CDN上託管自訂程式碼。 此自訂指令碼會與[!DNL Live Search]服務通訊，並傳回正常的結果，讓您控制Widget的功能。

- [PLP Widget存放庫](https://github.com/adobe/storefront-product-listing-page)
- [搜尋列存放庫](https://github.com/adobe/storefront-search-as-you-type)

## 正在更新[!DNL Live Search]

更新[!DNL Live Search]之前，請檢查使用撰寫器安裝的[!DNL Live Search]版本。

```bash
composer show magento/module-live-search | grep version
```

若要更新[!DNL Live Search]，請從命令列執行下列動作：

```bash
composer update magento/live-search --with-dependencies
```

若要更新至主要版本，例如從3.1.1到4.0.0，請編輯專案的根[!DNL Composer] `.json`檔案，如下所示：

1. 如果您目前安裝的`magento/live-search`版本是`3.1.1`或更低，而且您正在升級至版本`4.0.0`或更新版本，請在升級之前執行下列命令：

   ```bash
   bin/magento module:enable Magento_AdvancedSearch
   ```

   如需目前所安裝`magento/live-search`版本的相關資訊，請執行以下命令：

   ```bash
   composer show magento/live-search
   ```

1. 開啟根`composer.json`檔案並搜尋`magento/live-search`。

1. 在`require`區段中，更新版本號碼，如下所示：

   ```json
   "require": {
      ...
      "magento/live-search": "^4.0",
      ...
    }
   ```

1. 儲存`composer.json`。 然後，從命令列執行下列動作：

   ```bash
   composer update magento/live-search --with-dependencies
   ```

## 正在解除安裝[!DNL Live Search]

若要解除安裝[!DNL Live Search]，請參閱[解除安裝模組](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/uninstall-modules)。

## [!DNL Live Search]個套件

[!DNL Live Search]擴充功能包含下列封裝：

| 封裝 | 說明 |
|--- |--- |
| `module-live-search` | 允許商戶設定其面向、同義字、查詢規則等的搜尋設定，並提供唯讀GraphQL遊樂場的存取權，以測試來自&#x200B;*Admin*&#x200B;的查詢。 |
| `module-live-search-adapter` | 將搜尋要求從店面路由到[!DNL Live Search]服務，並在店面中呈現結果。 <br /> — 類別瀏覽 — 將要求從店面[上層導覽](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/navigation/navigation-top)路由到搜尋服務。<br /> — 全域搜尋 — 將要求從[快速搜尋](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search)欄位路由到[!DNL Live Search]服務。 快速搜尋欄位位於店面頁面的右上角。 |
| `module-live-search-storefront-popover` | 「依輸入方式搜尋」彈出視窗會取代標準快速搜尋，並傳回熱門搜尋結果的資料和縮圖。 |

## [!DNL Live Search]相依性

安裝[!DNL Composer]擴充功能的[!DNL Live Search]中繼套件包含下列模組相依性。

- `magento/module-saas-catalog`
- `magento/module-saas-category`
- `magento/module-saas-category-permissions`
- `magento/module-saas-product-override`
- `magento/module-saas-product-variant`
- `magento/module-saas-price`
- `magento/module-saas-scopes`
- `magento/module-bundle-product-data-exporter`
- `magento/module-catalog-inventory-data-exporter`
- `magento/module-catalog-url-rewrite-data-exporter`
- `magento/module-configurable-product-data-exporter`
- `magento/module-parent-product-data-exporter`
- `magento/module-gift-card-product-data-exporter`
- `magento/module-bundle-product-override-data-exporter`
- `data-services`
- `services-id`

## 進階概念

下列章節提供使用[!DNL Live Search]和[!DNL Catalog Service]時更進階的主題。

### 端點

[!DNL Live Search]透過`https://catalog-service.adobe.io/graphql`的端點通訊。

由於[!DNL Live Search]沒有完整產品資料庫的存取權，[!DNL Live Search] GraphQL與Commerce核心GraphQL API沒有完整的同位檢查。

Adobe建議直接呼叫SaaS API，尤其是目錄服務端點。

- 略過Commerce資料庫/Graphql程式，獲得效能並降低處理器負載
- 利用[!DNL Catalog Service]同盟從單一端點呼叫[!DNL Live Search]、[!DNL Catalog Service]和[!DNL Product Recommendations]。

對於某些使用案例，最好是呼叫[!DNL Catalog Service]以取得產品詳細資料和類似案例。 如需詳細資訊，請參閱[refineProduct](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/)。

如果您有自訂Headless實作，請檢視[!DNL Live Search]參考實作：

- [PLP WIDGET](https://github.com/adobe/storefront-product-listing-page)
- [[!DNL Live Search] 欄位](https://github.com/adobe/storefront-search-as-you-type)

如果您未使用標準元件(例如搜尋轉接器、Luma Widget或AEM CIF Widget)，預設將無法自動收集使用者互動資料。 Adobe Sensei會使用這項收集到的資料進行智慧型銷售與效能追蹤。 若要解決此問題，您需要開發自訂解決方案，以透過Headless方式實施此資料收集。

[!DNL Live Search]的最新版本已使用[!DNL Catalog Service]。

### 語言支援

[!DNL Live Search] Widget支援下列語言：

|  |  |  |  |
|--- |--- |--- |--- |
| 語言 | 地區 | 語言代碼 | Magento地區設定 |
| 保加利亞文 | 保加利亞 | bg_BG | bg_BG |
| 加泰隆尼亞文 | 西班牙 | ca_ES | ca_ES |
| 捷克文 | 捷克共和國 | cs_CZ | cs_CZ |
| 丹麥文 | 丹麥 | da_DK | da_DK |
| 德文 | 德國 | de_DE | de_DE |
| 希臘文 | 希臘 | el_GR | el_GR |
| 英文 | 英國 | en_GB | en_GB |
| 英文 | 美國 | en_US | en_US |
| 西班牙文 | 西班牙 | es_ES | es_ES |
| 愛沙尼亞文 | 愛沙尼亞 | et_EE | et_EE |
| 巴斯克語 | 西班牙 | eu_ES | eu_ES |
| 波斯文 | 伊朗 | fa_IR | fa_IR |
| 芬蘭文 | 芬蘭 | fi_FI | fi_FI |
| 法文 | 法國 | fr_FR | fr_FR |
| 加利西亞語 | 西班牙 | gl_ES | gl_ES |
| 北印度文 | 印度 | hi_IN | hi_IN |
| 匈牙利文 | 匈牙利 | hu_HU | hu_HU |
| 印尼文 | 印尼 | id_ID | id_ID |
| 義大利文 | 義大利 | it_IT | it_IT |
| 韓文 | 南韓 | ko_KR | ko_KR |
| 立陶宛文 | 立陶宛 | lt_LT | lt_LT |
| 拉脫維亞文 | 拉脫維亞 | lv_LV | lv_LV |
| 挪威文 | 挪威巴克摩 | nb_NO | nb_NO |
| 荷蘭文 | 荷蘭 | nl_NL | nl_NL |
| 波蘭文 | 波蘭 | pl_PL | pl_PL |
| 葡萄牙文 | 巴西 | pt_BR | pt_BR |
| 葡萄牙文 | 葡萄牙 | pt_PT | pt_PT |
| 羅馬尼亞文 | 羅馬尼亞 | ro_RO | ro_RO |
| 俄文 | 俄羅斯 | ru_RU | ru_RU |
| 瑞典文 | 瑞典 | sv_SE | sv_SE |
| 泰文 | 泰國 | th_TH | th_TH |
| 土耳其文 | 土耳其 | tr_TR | tr_TR |
| 中文 | 中國 | zh_CN | zh_Hans_CN |
| 中文 | 台灣 | zh_TW | zh_Hant_TW |

如果Widget偵測到Commerce管理語言設定符合支援的語言，則會預設為該語言。 否則，Widget會預設為英文。 在Admin中，語言設定是透過導覽至&#x200B;_[!UICONTROL Stores]_> [!UICONTROL Settings] >_[!UICONTROL Configuration]_ > _[!UICONTROL General]_> [!UICONTROL Country Options]來設定。

管理員也可以設定[搜尋索引](settings.md#language)的語言，以協助確保更好的搜尋結果。

### Widget程式碼存放庫

產品清單頁面Widget和[!DNL Live Search]欄位Widget的程式碼可從GitHub下載。

有權存取程式碼的開發人員可完全自訂其運作和外觀方式。 他們在自己的伺服器上代管程式碼，但仍使用[!DNL Live Search]服務。

- [PLP WIDGET](https://github.com/adobe/storefront-product-listing-page)
- [搜尋列](https://github.com/adobe/storefront-search-as-you-type)

### Data Export擴充功能

啟用[!DNL Live Search]後，資料匯出擴充功能會在Commerce應用程式和[!DNL Live Search]之間同步Commerce資料。 此程式可確保店面上有最新的Commerce資料。 在Admin中，您可以使用「資料管理」控制面板檢查同步狀態。 您可以使用Commerce CLI和記錄檔來管理和疑難排解資料匯出程式。 如需詳細資訊，請參閱[資料匯出指南](../data-export/overview.md)。

### Inventory management

[!DNL Live Search]在Commerce中支援[Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction)功能(先前稱為多Source詳細目錄，或MSI)。 若要啟用完整支援，您必須[將](install.md#updating-live-search)相依性模組`commerce-data-export`更新為102.2.0+版。

[!DNL Live Search]傳回布林值，指出產品是否可在Inventory management中使用，但不包含有關哪個來源有庫存的資訊。

### 價格索引器

[!DNL Live Search]客戶可以使用[SaaS價格索引器](../price-index/price-indexing.md)，提供更快的價格變更更新和同步處理時間。

### 價格支援

[!DNL Live Search] Widget支援大部分（但不是所有）Adobe Commerce支援的價格型別。

目前支援基本價格。 不支援的進階價格為：

- 成本
- 最低廣告價格

檢視[API Mesh](../catalog-service/mesh.md)，瞭解更複雜的價格計算。

價格格式支援Commerce執行個體中的地區設定設定： *商店* >設定> *設定* >一般> *一般* >本機選項>地區設定。

### Headless店面支援

您可以選擇安裝`module-data-services-graphql`模組，該模組會擴充應用程式的現有GraphQL涵蓋範圍，以包含店面行為資料收集所需的欄位。

```bash
composer require magento/module-data-services-graphql
```

此模組會將其他內容新增至GraphQL查詢：

- `dataServicesStorefrontInstanceContext`
- `dataServicesMagentoExtensionContext`
- `dataServicesStoreConfigurationContext`

### B2B支援

[!DNL Live Search]支援[B2B功能](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/guide-overview)及其他[限制](boundaries-limits.md#b2b-and-category-permissions)。

### PWA支援

[!DNL Live Search]可與PWA Studio搭配使用，但使用者在其他Commerce實作中可能會看到細微的差異。 在Venia中，基本功能（例如搜尋和產品清單頁面）可正常運作，但Graphql的某些排列可能無法正常運作。 可能也會有效能差異。

- 目前[!DNL Live Search]的PWA實作需要比[!DNL Live Search]更長的處理時間才能傳回搜尋結果(使用原生Commerce店面)。
- PWA中的[!DNL Live Search]不支援[事件處理](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/)。 因此，搜尋報告和智慧型銷售無法在PWA商店上運作。
- 使用[PWA Studio](https://developer.adobe.com/commerce/pwa-studio/)時，GraphQL不支援直接篩選`description`、`name`、`short_description`，但這些欄位可透過較一般的篩選傳回。

若要搭配PWA Studio使用[!DNL Live Search]，整合經銷商也必須：

1. 安裝[livesearch-storefront-utils](https://www.npmjs.com/package/@magento/ds-livesearch-storefront-utils)。
1. 在`environmentId`物件中設定`storeDetails`。

   ```javascript
   const storeDetails: StoreDetailsProps = {
       environmentId: <Storefront_ID>,
       websiteCode: "base",
       storeCode: "main_website_store",
       storeViewCode: "default",
       searchUnitId: searchUnitId,
       config: {
           minQueryLength: 5,
           pageSize: 8,
           currencySymbol: "$",
           },
       };
   ```

### Cookie

[!DNL Live Search]會收集使用者互動資料，作為其基本功能的一部分，而Cookie是用來儲存此資料。 收集任何使用者資訊時，使用者必須同意儲存Cookie。 [!DNL Live Search]和[!DNL Product Recommendations]共用資料流，因此使用相同的Cookie機制。 在[控制代碼Cookie限制](https://experienceleague.adobe.com/en/docs/commerce/product-recommendations/developer/setting-cookie)中閱讀更多相關資訊。
