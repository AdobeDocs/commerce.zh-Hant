---
title: 動態新增產品屬性
description: 瞭解如何在資料同步程式進行期間，以動態方式將自訂產品屬性新增至資料匯出摘要。
role: Admin, Developer
exl-id: d5ed7497-4be1-440a-a567-81b64fdc54fc
source-git-commit: 37d5699315e34f1504602090fae5201ee51cf470
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# 在資料同步期間動態新增產品屬性

您可以在資料同步過程中建立外掛程式來新增屬性，以擴充產品屬性而不需在Adobe Commerce中註冊它們。

>[!NOTE]
>
>擴充產品屬性的最佳方式是[將它們新增至Adobe Commerce](extensibility-and-customizations.md#add-product-attributes-to-adobe-commerce)，您可以在其中從Commerce管理員設定和管理這些屬性。 只有在您僅需要Commerce店面服務才能動態新增這些值，且不想在Adobe Commerce中註冊這些值時，才可動態新增。 您也可以選擇搭配目錄服務[使用](../catalog-service/mesh.md)API Mesh來管理自訂屬性，以擴充目錄服務GraphQL結構描述。

## 新增產品屬性

建立將`customer_attribute`新增至`Magento\CatalogDataExporter\Model\Provider\Product\Attributes`類別的外掛程式。

1. 更新[相依性插入組態檔](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`)以定義外掛程式。

   ```xml
   <type name="Magento\CatalogDataExporter\Model\Provider\Product\Attributes">
     <plugin name="product_customer_attributes" type="Vendor\CatalogDataExporter\Model\Plugin\AddAttribute"/>
   </type>
   ```

1. 建立外掛程式。

   ```php
    <?php
    declare(strict_types=1);
   
    namespace Vendor\CatalogDataExporter\Model\Plugin;
   
    use Magento\CatalogDataExporter\Model\Provider\Product\Attributes;
   
    class AddAttribute {
   
         /**
          * @param Attributes $subject
          * @param array $result
          * @param $arguments
          * @return array
          * @throws \Zend_Db_Statement_Exception
          */
          public function afterGet(Attributes $subject, array $result, $arguments): array
          {
              $additionalAttributes = [];
              $attributeCode = 'customer_attribute';
              foreach ($result as $product) {
                  if (!isset($product['productId']) || !isset($product['storeViewCode'])) {
                      continue;
                  }
                  // HINT: if needed, do filtration by "storeViewCode" and or "productId"
   
                  $productId = $product['productId'];
                  $storeViewCode = $product['storeViewCode'];
   
                  $newKey = \implode('-', [$product['storeViewCode'], $product['productId'], $attributeCode]);
                  if (isset($additionalAttributes[$newKey])) {
                      continue;
                  }
                  $additionalAttributes[$newKey] = [
                      'productId' => $productId,
                      'storeViewCode' => $storeViewCode,
                      'attributes' => [
                          'attributeCode' => $attributeCode,
                          // provide single or multiple values for the attribute
                          'value' => [
                              rand(1, 42)
                          ]
                      ]
                  ];
   
              }
   
              return array_merge($result, $additionalAttributes);
          }
    }
   ```

   新增外掛程式後，在下次排定的同步處理期間，變更會同步處理至已連線的店面服務。 若要立即傳送更新，請使用下列CLI命令手動啟動同步化程式。

   ```
   bin/magento saas:resync --feed=products
   ```

## 宣告自訂產品屬性中繼資料

如果您動態建立自訂產品屬性，並想要將其用於店面服務中的顯示、搜尋或篩選，請新增產品屬性中繼資料以設定店面行為。

1. 更新[相依性插入組態檔](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`)以定義產品屬性中繼資料的外掛程式。

   ```xml
   <type name="\Magento\CatalogDataExporter\Model\Provider\ProductMetadata">
     <plugin name="product_customer_attributes_metadata" type="Vendor\CatalogDataExporter\Model\Plugin\AddAttributeMetadata"/>
   </type>
   ```

1. 建立下列提供者`\Magento\CatalogDataExporter\Model\Provider\ProductMetadata`的外掛程式。

   檢查`ProductAttributeMetadata`中的`vendor/magento/module-catalog-data-exporter/etc/et_schema.xml`以取得必要欄位。

   ```php
    <?php
    declare(strict_types=1);
   
    namespace Vendor\CatalogDataExporter\Model\Plugin;
   
    use Magento\CatalogDataExporter\Model\Provider\ProductMetadata;
   
    class AddAttributeMetadata {
   
         /**
          * @param ProductMetadata $subject
          * @param array $result
          * @param $arguments
          * @return array
          * @throws \Zend_Db_Statement_Exception
          */
         public function afterGet(ProductMetadata $subject, array $result, $arguments): array
         {
              $result[] = [
                'id' => '123',
                // provide storeCode, websiteCode and storeViewCode applicable for your AC instance
                'storeCode' => 'default',
                'websiteCode' => 'base',
                'storeViewCode' => 'default',
                // specify the customer attribute code - should be the same as used in the products attributes plugin
                'attributeCode' => 'customer_attribute',
                // only product attributes are supported
                'attributeType' => 'catalog_product',
                // specify the data type
                'dataType' => 'int',
                'multi' => false,
                'label' => 'Customer Attribute',
                'frontendInput' => 'select',
                'required' => false,
                'unique' => false,
                'global' => true,
                'visible' => true,
                'searchable' => true,
                'filterable' => true,
                // This value must be set to true to export it to the storefront services
                'visibleInCompareList' => true,
                'visibleInListing' => true,
                'sortable' => true,
                'visibleInSearch' => true,
                'filterableInSearch' => true,
                'searchWeight' => 1.0,
                'usedForRules' => true,
                'boolean' => false,
                'systemAttribute' => false,
                'numeric' => false,
                // specify the list of attribute options
                'attributeOptions' => [
                    'option1',
                    'option2',
                    'option3'
                ]
             ];
   
              return $result;
         }
      }
   ```

   新增外掛程式後，在下次排定的同步處理期間，變更會同步處理至已連線的店面服務。 若要立即傳送更新，請使用下列CLI命令手動啟動同步化程式。

   ```
   bin/magento saas:resync --feed=productattributes
   ```

