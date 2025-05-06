---
title: 開始使用 [!DNL Live Search]
description: 從Adobe Commerce瞭解 [!DNL Live Search] 的系統需求和安裝步驟。
role: Admin, Developer
exl-id: 45b985f1-9afb-4a07-93e8-f2fe231c5400
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案(Adobe管理的PaaS基礎結構)和內部部署專案的Adobe Commerce 。"
source-git-commit: be1c739f3821a5f1e846b3026088e3a3ff45a60f
workflow-type: tm+mt
source-wordcount: '3139'
ht-degree: 0%

---

# 設定以透過[!DNL Live Search]成功

Adobe Commerce [!DNL Live Search]與[[!DNL Catalog Service]](../catalog-service/guide-overview.md)共同合作，提供效能、相關且直覺式的搜尋解決方案，讓您的客戶快速找到他們所需的專案。 具體來說，[!DNL Catalog Service]會呈現您的目錄資料以供SaaS服務使用，例如[!DNL Live Search]。

本文提供了使用 [!DNL Catalog Service]進行實施[!DNL Live Search]的分步說明。

>[!IMPORTANT]
>
>在網站搜尋方面，Adobe Systems商務為您提供了多種選擇。 請務必在實施之前閱讀 [邊界和限制](boundaries-limits.md) ，以確保這 [!DNL Live Search] 符合您的業務需求。

## 對象

本文適用於團隊上負責安裝和配置 Adobe Systems Commerce 執行個體的開發人員或系統集成商。

## 需求

- [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) 2.4.4+
- PHP 8.1、8.2或8.3版
- [!DNL Composer]

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

已從[Adobe Marketplace](https://commercemarketplace.adobe.com/magento-live-search.html)透過[Composer](https://getcomposer.org/)將[!DNL Live Search]安裝為擴充功能。 安裝並設定[!DNL Live Search]後，Adobe [!DNL Commerce]會開始與SaaS服務共用搜尋和目錄資料。 此時，*管理員*&#x200B;使用者可以設定、自訂及管理搜尋Facet、同義字及銷售規則。

>[!NOTE]
>
>截至[!DNL Live Search] 3.0.2，[!DNL Catalog Service]擴充功能已與[!DNL Live Search]安裝整合。

>[!IMPORTANT]
>
>自[!DNL Live Search] 4.0.0起，已棄用搜尋配接器。 日後，搜尋配接卡只會更新以解決安全性問題。

1. 確認[cron工作](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs)和[索引子](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management)正在執行。

   >[!IMPORTANT]
   >
   >鑑於Elasticsearch 7於2023年8月宣佈終止支援，建議所有Adobe Commerce客戶移轉至OpenSearch 2.x搜尋引擎。 如需在產品升級期間移轉搜尋引擎的相關資訊，請參閱&#x200B;_升級指南_&#x200B;中的[移轉至OpenSearch](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/prepare/opensearch-migration)。

1. 從[Adobe Marketplace](https://commercemarketplace.adobe.com/magento-live-search.html)下載`live-search`套件。

1. 從命令列執行以下命令：

   ```bash
   composer require magento/live-search
   ```

   如果您正在將[!DNL Live Search]擴充功能新增至&#x200B;**新的** Adobe Commerce安裝，請執行以下命令以暫時停用[!DNL OpenSearch]和相關模組，並安裝[!DNL Live Search]。 然後，繼續步驟4。

   ```bash
      bin/magento module:disable Magento_Elasticsearch Magento_Elasticsearch7 Magento_OpenSearch Magento_ElasticsearchCatalogPermissions Magento_InventoryElasticsearch Magento_ElasticsearchCatalogPermissionsGraphQl
   ```

   如果您正在將[!DNL Live Search]擴充功能新增至&#x200B;**現有** Adobe Commerce安裝，請執行以下動作以停用提供店面搜尋結果的[!DNL Live Search]模組。 然後，繼續步驟4：

   ```bash
      bin/magento module:disable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover Magento_LiveSearchProductListing 
   ```

   [!DNL Elasticsearch]會繼續從店面管理搜尋要求，而[!DNL Live Search]服務會在背景同步目錄資料和索引產品。

1. 執行下列動作：

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

1. 如果您正在新的Commerce執行個體上安裝[!DNL Live Search]，則您已完成，可以跳至[2。 設定API金鑰](#2-configure-api-keys)區段。 如果您要將即時搜尋安裝至現有的Commerce執行個體，請繼續進行下一個步驟。

1. 執行以下命令以啟用[!DNL Live Search]延伸、停用[!DNL OpenSearch]並執行`setup`。

   ```bash
   bin/magento module:enable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover  Magento_LiveSearchProductListing 
   ```

   ```bash
   bin/magento module:disable Magento_Elasticsearch Magento_Elasticsearch6 Magento_Elasticsearch7 Magento_ElasticsearchCatalogPermissions Magento_InventoryElasticsearch 
   Magento_ElasticsearchCatalogPermissionsGraphQl
   ```

   ```bash
   bin/magento setup:upgrade
   ```

### 安裝[!DNL Live Search]測試版

>[!IMPORTANT]
>
>以下功能為測試版。 若要參與測試版，請傳送電子郵件要求給[commerce-storefront-services](mailto:commerce-storefront-services@adobe.com)。

此Beta版支援[`productSearch`查詢](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/)的三個新功能：

- **分層搜尋** — 在另一個搜尋內容中搜尋 — 使用此功能，您最多可以執行兩個層級的搜尋來搜尋您的搜尋查詢。 例如：

   - **第1層搜尋** — 搜尋&quot;product_attribute_1&quot;上的&quot;motor&quot;。
   - **第2層搜尋** — 搜尋「product_attribute_2」上的「零件編號123」。 此範例會在結果中搜尋「馬達」的「零件編號123」。

  分層搜尋可用於`startsWith`搜尋索引和`contains`搜尋索引，如下所述：

- **startsWith搜尋索引** — 使用`startsWith`索引搜尋。 這項新功能可讓：

   - 搜尋屬性值以特定字串開頭的產品。
   - 設定「結尾為」搜尋，讓購物者可以搜尋屬性值結尾為特定字串的產品。 若要啟用「結尾為」搜尋，產品屬性需要反向擷取，且API呼叫也應該為反向字串。

- **包含搜尋索引** — 使用包含索引來搜尋屬性。 這項新功能允許：

   - 在較大的字串中搜索查詢。 例如，如果購物者在字符串“HAPE-123”中搜索產品編號“PE-123”。

      - 注意：此搜尋類型不同于執行自動填充搜尋的現有 [短語搜尋](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#phrase)。 例如，如果您的商品屬性值為「戶外褲子」，則詞組搜尋返回“out pan”的回應，但不返回“oor ants”的回應。 但是，包含搜尋確實返回“oor ants”的回應。

這些新條件會增強搜尋查詢篩選機制，以縮小搜尋結果。 這些新條件不會影響主要搜尋查詢。

您可以在搜尋結果頁面上實作這些新條件。 例如，您可以在頁面上新增區段，讓購物者可以進一步縮小搜尋結果。 您可以允許購物者選取特定產品屬性，例如「製造商」、「零件編號」和「說明」。 從該位置，他們使用`contains`或`startsWith`條件在這些屬性中搜尋。 如需可搜尋的[屬性](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types)清單，請參閱管理員指南。

1. 若要安裝測試版，請在專案中新增下列相依性：

   ```bash
   composer require magento/module-live-search-search-types:"^1.0.0-beta1"
   ```

1. 認可並將變更推送至您的`composer.json`和`composer.lock`檔案至雲端專案。 [了解更多](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/extensions#upgrade-an-extension)。

   此Beta版在Admin中新增&#x200B;**[!UICONTROL Autocomplete]**、**[!UICONTROL Contains]**&#x200B;和&#x200B;**[!UICONTROL Starts with]**&#x200B;的&#x200B;**[!UICONTROL Search types]**&#x200B;核取方塊。 它也會更新[`productSearch`](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#filtering-using-search-capability) GraphQL API，以包含這些新搜尋功能。

1. 在Admin中，[將產品屬性](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes-add#step-5-describe-the-storefront-properties)設定為可搜尋，並指定該屬性的搜尋功能，例如&#x200B;**包含** （預設）或&#x200B;**開頭為**。 您最多可以為&#x200B;**Contains**&#x200B;指定6個要啟用的屬性，並為&#x200B;**Starts with**&#x200B;指定6個要啟用的屬性。 若為測試版，請注意，管理員不會強制執行此限制，但會在API搜尋中強制執行。

   ![指定搜尋功能](./assets/search-filters-admin.png)

1. 請參閱[開發人員檔案](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#filtering-using-search-capability)，瞭解如何使用新的`contains`和`startsWith`搜尋功能更新您的[!DNL Live Search] API呼叫。

### 欄位說明

| 欄位 | 說明 |
|--- |--- |
| `Autocomplete` | 預設為啟用，無法修改。 透過`Autocomplete`，您可以在[搜尋篩選器](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#filtering)中使用`contains`。 此處，`contains`中的搜尋查詢會傳回自動完成型別搜尋回應。 Adobe建議您使用此型別的搜尋來搜尋說明欄位，這些欄位通常超過50個字元。 |
| `Contains` | 啟用真正的「字串中包含的文字」搜尋，而非自動完成搜尋。 在[搜尋篩選器](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#filtering-using-search-capability)中使用`contains`。 如需詳細資訊，請參閱[限制](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#limitations)。 |
| `Starts with` | 可讓您查詢以特定值開頭的字串。 在[搜尋篩選器](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#filtering-using-search-capability)中使用`startsWith`。 |

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
> 當資料已編制索引並同步時，店面中無法使用搜尋和類別瀏覽操作。 根據目錄的大小，從`cron`執行開始，程式至少可能需要一小時才能將您的資料同步到SaaS服務。

### 監視同步處理進度

您可以使用[資料管理控制面板](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard)檢視已同步處理和共用的資料。 此儀表板提供您店面產品資料可用性的寶貴見解，確保可及時向購物者顯示。

![資料管理儀表板](assets/data-management-dashboard.png)

您也可以使用[Commerce CLI](../data-export/data-export-cli-commands.md#troubleshooting)和資料匯出擴充功能記錄檔，執行同步處理命令並疑難排解同步處理程式。

#### 未來的產品更新

初始同步後，增量產品更新最多可能需要15分鐘才能用於店面搜尋。 若要深入瞭解，請參閱索引檔案中的[串流產品更新](indexing.md)。

## 4. 驗證數據是否已匯出

若要檢查目錄數據是否已從 Commerce 匯出Adobe Systems並與 同步， [!DNL Live Search]您有幾個選項可以選擇：

- 下表中的條目Look：

   - `cde_products_feed`
   - `cde_product_attributes_feed`

  >[!NOTE]
  >
  >如果收到 `table does not exist` 錯誤，請在 和 `catalog_data_exporter_products` `catalog_data_exporter_product_attributes` 表中查找條目。 這些表名在 [!DNL Live Search] 4.2.1 之前的版本中使用。

- [使用具有預設查詢的 GraphQL場](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/graphql)（有關更多詳細信息，請參閱 [GraphQL 參考](https://developer.adobe.com/commerce/services/graphql/live-search/)）來驗證以下內容：

   - 傳回的產品計數接近您對商店檢視的預期。
   - 會傳回多面向。

如需其他說明，請參閱支援知識庫中的[[!DNL Live Search] 目錄未同步](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-catalog-data-sync)。

## 5.設定資料

正確設定您的產品資料可確保為您的客戶帶來良好的搜尋結果。 您可以在此區段中啟用產品清單Widget並指派類別。

### 啟用產品清單Widget

安裝[!DNL Live Search] 4.0.0+時，預設會啟用產品清單Widget。 Widget啟用時，搜尋結果頁面和類別瀏覽產品清單頁面會使用不同的UI元件。 此UI元件會直接呼叫[目錄服務API](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/)，如此可加快回應時間。

如果您的[!DNL Live Search]版本早於4.0.0+，則必須手動啟用產品清單Widget。

1. 從&#x200B;*管理員*，前往&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在下 **[!UICONTROL Live Search]**，選擇 **[!UICONTROL Storefront Features]**。
1. 設為 **[!UICONTROL Enable Product Listing Widgets]** `Yes`。

   ![啟用產品清單介面工具集](assets/ls-admin-enable-widget.png)

更改此配置時，將顯示該消息 `Page cache is invalidated` 。 您需要清空 Magento 快取以儲存變更。

1. [通過執行以下作之一訪問緩存管理](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/cache-management)頁面：

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

確保部署到您網站的店面事件可正常運作。 這對Headless實作尤其重要。

- 檢閱[!DNL Live Search]所需的[事件](events.md)。
- 確定[即時搜尋儀表板](performance.md)顯示的是來自非生產環境的資料。
- [驗證事件集合](../product-recommendations/verify.md)。 此頁面位於[!DNL Product Recommendations]指南中，驗證步驟也適用於[!DNL Live Search]。

## 8.為您的店面量身打造

您已安裝[!DNL Live Search]擴充功能、同步處理、驗證及設定您的資料。 下一步是確保[!DNL Live Search] Widget符合您商店的外觀與風格。

您可以視需要定義自訂CSS規則，以設定彈出視窗和PLP Widget的樣式。 請參閱[樣式彈出視窗元素](storefront-popover.md#styling-popover-example)和[產品清單頁面Widget](plp-styling.md#styling-example)。

如果您想要擴充Widget的功能，每個元件的原始碼都可在公用存放庫中取得。
在這種情況下，您可以根據自己的需求自訂JavaScript，然後在CDN上託管自訂程式碼。 此自訂指令碼會與[!DNL Live Search]服務通訊，並傳回正常的結果，讓您控制Widget的功能。

- [PLP Widget存放庫](https://github.com/adobe/storefront-product-listing-page)
- [搜尋列存放庫](https://github.com/adobe/storefront-search-as-you-type)

## 更新 [!DNL Live Search]

在更新 Live Search 之前，請從命令行運行以下命令以檢查已安裝的 Live Search 版本：

```bash
composer show magento/module-live-search | grep version
```

要更新 [!DNL Live Search]，請從命令行運行以下命令：

```bash
composer update magento/live-search --with-dependencies
```

要更新到主要版本（例如從 3.1.1 到 4.0.0），請按如下所示編輯專案的根[!DNL Composer]`.json`檔：

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

## 正在卸載 [!DNL Live Search]

要卸載 [!DNL Live Search]，請參閱 [卸載模組](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/uninstall-modules)。

## [!DNL Live Search] 包

該 [!DNL Live Search] 擴展由以下包組成：

| 包 | 說明 |
|--- |--- |
| `module-live-search` | 允許商戶設定其面向、同義字、查詢規則等的搜尋設定，並提供唯讀GraphQL遊樂場的存取權，以測試來自&#x200B;*Admin*&#x200B;的查詢。 |
| `module-live-search-adapter` | 將搜尋要求從店面路由到[!DNL Live Search]服務，並在店面中呈現結果。 <br /> — 類別瀏覽 — 將要求從店面[上層導覽](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/navigation/navigation-top)路由到搜尋服務。<br /> — 全域搜尋 — 將要求從店面右上角的[快速搜尋](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search)方塊路由到[!DNL Live Search]服務。 |
| `module-live-search-storefront-popover` | 「依輸入方式搜尋」彈出視窗會取代標準快速搜尋，並傳回熱門搜尋結果的資料和縮圖。 |

## [!DNL Live Search]相依性

安裝[!DNL Live Search]擴充功能的[!DNL Composer]中繼套件包含下列模組相依性。

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

由於無權訪問完整的產品資料庫，[!DNL Live Search]因此 [!DNL Live Search] GraphQL 和 Commerce 核心 GraphQL API 不具有完全奇偶校驗。

Adobe Systems建議直接調用 SaaS API，特別是目錄服務終端節點。

- 通過繞過商務資料庫/Graphql進程獲得性能並減少處理器負載
- 利用聯合[!DNL Live Search]身份驗證從[!DNL Catalog Service]單個終結點調用、 [!DNL Catalog Service]和[!DNL Product Recommendations]。

對於某些用例，最好調用 [!DNL Catalog Service] 產品詳細資訊和類似案例。 有關詳細資訊，請參閱 [優化產品](https://developer.adobe.com/commerce/services/graphql/catalog-service/refine-product/) 。

如果您有自訂Headless實作，請檢視[!DNL Live Search]參考實作：

- [PLP WIDGET](https://github.com/adobe/storefront-product-listing-page)
- [即時搜尋欄位](https://github.com/adobe/storefront-search-as-you-type)

若您未使用搜尋配接器、Luma Widget或AEM CIF Widget等標準元件，預設無法自動收集使用者互動資料。 Adobe Sensei會使用這項收集到的資料進行智慧型銷售與效能追蹤。 若要解決此問題，您需要開發自訂解決方案，以透過Headless方式實施此資料收集。

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
| 德語 | 德國 | de_DE | de_DE |
| 希臘語 | 希臘 | el_GR | el_GR |
| 英文 | 英國 | en_GB | en_GB |
| 英語 | 美國 | en_US | en_US |
| 西班牙文 | 西班牙 | es_ES | es_ES |
| 愛沙尼亞文 | 愛沙尼亞 | et_EE | et_EE |
| 巴斯克語 | 西班牙 | eu_ES | eu_ES |
| 波斯語 | 伊朗 | fa_IR | fa_IR |
| 芬蘭文 | 芬蘭 | fi_FI | fi_FI |
| 法文 | 法國 | fr_FR | fr_FR |
| 加利西亞語 | 西班牙 | gl_ES | gl_ES |
| 北印度文 | 印度 | hi_IN | hi_IN |
| 匈牙利文 | 匈牙利 | hu_HU | hu_HU |
| 印尼文 | 印尼 | id_ID | id_ID |
| 義大利文 | 義大利 | it_IT | it_IT |
| 朝鮮語 | 韓國 | ko_KR | ko_KR |
| 立陶宛語 | 立陶宛 | lt_LT | lt_LT |
| 拉脫維亞文 | 拉脫維亞 | lv_LV | lv_LV |
| 挪威文 | 挪威博克瑪律 | nb_NO | nb_NO |
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

如果小組件檢測到「商務管理員語言」設置與支持的語言匹配，則預設為該語言。 否則，介面工具集預設為 英文。 在“管理”中，通過導航到 _[!UICONTROL Stores]_>> [!UICONTROL Settings]_[!UICONTROL Configuration]_ > _[!UICONTROL General]_> [!UICONTROL Country Options]來配置語言設置。

管理員還可以設置搜尋索引[&#128279;](settings.md#language)的語言，以幫助確保獲得更好的搜尋結果。

### Widget代碼存放庫

產品列表 頁面 接口工具集和即時Search字段介面工具集的代碼可從 GitHub 下載。

有權訪問代碼的開發人員可以完全自定義代碼的工作方式和外觀。 他們在自己的伺服器上主機代碼，但仍使用該 [!DNL Live Search] 服務。

- [PLP WIDGET](https://github.com/adobe/storefront-product-listing-page)
- [搜尋列](https://github.com/adobe/storefront-search-as-you-type)

### Data Export擴充功能

啟用「即時搜尋」後，「資料匯出」擴充功能會將Commerce資料在Commerce應用程式和「即時搜尋」之間同步。 此程式可確保店面上有最新的Commerce資料。 在Admin中，您可以使用「資料管理」控制面板檢查同步狀態。 您可以使用Commerce CLI和記錄檔來管理和疑難排解資料匯出程式。 如需詳細資訊，請參閱[資料匯出指南](../data-export/overview.md)。

### 庫存管理

[!DNL Live Search] 支持 [商務中的庫存管理](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction) 功能（以前稱為多來源庫存或 MSI）。 若要啟用完全支持，必須[將依賴項模組`commerce-data-export`更新](install.md#updating-live-search)到版本 102.2.0+。

[!DNL Live Search]傳回布林值，指出產品是否可在Inventory management中使用，但不包含有關哪個來源有庫存的資訊。

### 價格索引器

Live Search客戶可以使用[SaaS價格索引器](../price-index/price-indexing.md)，提供更快的價格變更更新和同步處理時間。

### 價格支援

即時搜尋Widget支援大多數（但不是所有）Adobe Commerce支援的價格型別。

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
1. 在`storeDetails`物件中設定`environmentId`。

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
