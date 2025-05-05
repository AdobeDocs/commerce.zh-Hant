---
title: 自訂
description: 瞭解如何自訂您的產品推薦。
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# 自訂

當您安裝產品建議模組時，Adobe Commerce會建立`ProductRecommendationsLayout`目錄。 此目錄包含範本檔案，您可以自訂這些檔案，以變更建議在店面中的顯示方式。 具體來說，您可以修改或覆寫下列範本：

`<your theme>/Magento_ProductRecommendationsLayout/web/template/recommendations.html`

如需有關修改範本檔案的詳細資訊，請參閱前端開發人員指南中的[範本自訂](https://developer.adobe.com/commerce/frontend-core/guide/templates/walkthrough/)。

如果您修改`recommendations.html`檔案，必須在檔案中保留下列標籤，以確保Adobe Commerce可以從您的店面收集建議量度：

| 標籤 | 使用 |
|---|---|
| `<div data-bind="attr : {'data-unit-id' : unitId }"...</div>` | 收集檢視事件。 |
| `<a data-bind="attr : {'data-sku' : sku, 'data-unit-id'}"...</a>` | 收集點選事件。 <br/>**注意：**&#x200B;如果您新增任何錨點標籤，則必須包含這些屬性。 |

除了`recommendations.html`檔案之外，`ProductRecommendationsLayout`目錄還包含下列子目錄：

| 目錄 | 用途 |
|---|---|
| `layout` | 包含每個頁面型別的`*.xml`個檔案 |
| `templates` | 包含呼叫擷取和轉譯器指令碼的檔案 |
| `web/js` | 包含為您的存放區擷取及轉譯建議的JavaScript檔案 |
| `web/template` | 包含`magento/product-recommendations`模組的範本 |

## 推薦單位定位

當您[建立](create.md)建議時，請指定它出現在頁面上的[位置](placement.md)。 建議單位可放置在主要內容容器的頂端或底部。 不過，您可以自訂此位置。 如果您建立「頁面產生器」建議內容型別，請使用「頁面產生器」工具，將建議單位放置在頁面上。 針對所有其他頁面型別，編輯建立建議時產生的`*.xml`檔案。

1. 變更至`layout`目錄：

   ```bash
   cd `<your theme>/Magento_ProductRecommendationsLayout/layout`
   ```

   下表列出此目錄中存在的XML檔案：

   | 檔案名稱 | 頁面 |
   |---|---|
   | `catalog_category_view.xml` | 類別 |
   | `catalog_product_view.xml` | 產品詳細資料 |
   | `checkout_cart_index.xml` | 購物車 |
   | `checkout_onepage_success.xml` | 簽出 |
   | `cms_index_index.xml` | 首頁 |

   >[!NOTE]
   >
   >如果您的存放區使用協力廠商副檔名，`layout`目錄中的檔案名稱可能會不同。

1. 修改`catalog_product_view.xml`檔案，讓建議單位顯示在產品詳細資料頁面上的產品影像之後。 在自訂此XML檔案之前，請先檢視檔案並瞭解您需要修改的區段：

   ```xml
   <?xml version="1.0"?>
   <page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
       <referenceBlock name="page.wrapper">
           <block class="Magento\Framework\View\Element\Template" before="-" name="product_recommendations_fetcher" template="Magento_ProductRecommendationsStorefront::fetcher.phtml" />
       </referenceBlock>
       <body>
           <referenceBlock name="main.content">
               <block class="Magento\ProductRecommendationsStorefront\Block\Renderer" after="-" name="product_recommendations_product_below_content" template="Magento_ProductRecommendationsStorefront::renderer.phtml">
                   <arguments>
                       <argument name="pagePlacement" xsi:type="string">below-main-content</argument>
                   </arguments>
               </block>
           </referenceBlock>
       </body>
   </page>
   ```

   在上述程式碼片段中，`main.content`參考區塊會指出建議單位會放置在與該元素相關的位置。 其`block`元素包含`after="-"`屬性，其指定建議單位將顯示在主要內容區塊之後的頁面上。

1. 讓我們指定不同的內容區塊，以修改此檔案。

   將參考區塊`name`從`main.content`變更為`product.info.media`。

   ```xml
   <?xml version="1.0"?>
   <page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
       <referenceBlock name="page.wrapper">
           <block class="Magento\Framework\View\Element\Template" before="-" name="product_recommendations_fetcher" template="Magento_ProductRecommendationsStorefront::fetcher.phtml" />
       </referenceBlock>
       <body>
           <referenceBlock name="product.info.media">
               <block class="Magento\ProductRecommendationsStorefront\Block\Renderer" after="-" name="product_recommendations_product_below_content" template="Magento_ProductRecommendationsStorefront::renderer.phtml">
                   <arguments>
                       <argument name="pagePlacement" xsi:type="string">below-main-content</argument>
                   </arguments>
               </block>
           </referenceBlock>
       </body>
   </page>
   ```

   此變更會導致您的建議單位出現在產品詳細資料頁面上的產品影像之後。 如果您希望建議單位出現在`product.info.media`之前，請將`after="-"`屬性變更為`before="-"`。 `pagePlacement`引數是不應修改的內部引數。

如需關於頁面上區塊型別的詳細資訊，請參閱[版面概觀](https://developer.adobe.com/commerce/frontend-core/guide/layouts/)。

## 自訂產品屬性

開發人員通常需要存取店面建議單位中的自訂產品屬性值，以便他們可以根據這些屬性為產品新增視覺化處理。

例如，如果您的商店銷售某些有機產品，這些產品上可能會有自訂屬性，將其指定為`Organic = Yes`。 您可能需要存取店面上的這個屬性值，以便在這些產品出現在Recommendations中時為其提供特殊的視覺化處理。 同樣地，存取這些自訂產品屬性值可讓您在網站的展示層中為產品加上徽章或驅動自訂邏輯。

![新增徽章](assets/unit-custom.png)

若要確定當您在頁面上轉譯建議單位時，可以使用自訂產品屬性，請在Admin的[產品屬性](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create.html?lang=zh-Hant)頁面中，將`Used in Product Listing`屬性設定為`Yes`。

設定此屬性時，JSON裝載會包含`attributes`物件，其中包含屬性程式碼和值的陣列。 然後，您可以根據這些屬性值套用自訂店面樣式，例如新增特殊視覺處理或徽章，如之前所述。

>[!NOTE]
>
>產品屬性變更最多需要一小時才能顯示在JSON裝載中。
