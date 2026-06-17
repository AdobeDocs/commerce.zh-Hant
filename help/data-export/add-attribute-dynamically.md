---
title: 動態新增產品屬性
description: 瞭解如何在資料同步程式進行期間，以動態方式將自訂產品屬性新增至資料匯出摘要。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: d5ed7497-4be1-440a-a567-81b64fdc54fc
TQID: https://experienceleague.adobe.com/SZWtLSvxb-w-968f4wqWrPTBn1c9IEuthvhIv86Pvss
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 267
ht-degree: 0%

---

# 動態新增產品屬性

您可以在資料同步處理過程中建立外掛程式來新增屬性，而不需在[!DNL Adobe Commerce]中註冊產品屬性。

>[!NOTE]
>
>擴充產品屬性的最佳方式是使用 [!DNL Catalog Service]](../catalog-service/mesh.md)將這些屬性[新增至 [!DNL Adobe Commerce]](extensibility-and-customizations.md#add-product-attributes-to-adobe-commerce) where you can configure and manage them from the Commerce Admin. Only add them dynamically if you need them solely for Commerce storefront services and do not want to register them in [!DNL Adobe Commerce]. You also have the option to manage custom attributes using [[!DNL API Mesh] ，以擴充[!DNL Catalog Service] [!DNL GraphQL]結構描述。

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

   ```shell
   bin/magento saas:resync --feed=products
   ```

## 宣告自訂產品屬性中繼資料

如果您動態建立自訂產品屬性，並想要將其用於店面服務中的顯示、搜尋或篩選，請新增產品屬性中繼資料以設定店面行為。

1. 更新[相依性插入組態檔](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`)以定義產品屬性中繼資料的外掛程式。

   ```xml
   <type name="Magento\CatalogDataExporter\Model\Provider\ProductMetadata">
     <plugin name="product_customer_attributes_metadata" type="Vendor\CatalogDataExporter\Model\Plugin\AddAttributeMetadata"/>
   </type>
   ```

1. 為下列提供者`Magento\CatalogDataExporter\Model\Provider\ProductMetadata`建立外掛程式。

   檢查`vendor/magento/module-catalog-data-exporter/etc/et_schema.xml`中的`ProductAttributeMetadata`以取得必要欄位。

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

   ```shell
   bin/magento saas:resync --feed=productAttributes
   ```

>[!MORELIKETHIS]
>
> * [延伸與自訂SaaS資料匯出摘要](extensibility-and-customizations.md)
> * [使用Commerce CLI同步摘要](data-export-cli-commands.md)
> * [同步如何運作](sync-overview.md) — 瞭解同步模式，以及排程與手動重新同步。
> * [檢閱記錄檔並進行疑難排解](troubleshooting/logging.md)
