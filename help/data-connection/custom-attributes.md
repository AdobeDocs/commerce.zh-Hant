---
title: 新增自訂屬性至訂單
description: 瞭解如何將自訂訂單屬性新增至您的後台資料，並將這些屬性傳送至Experience Platform。
role: Admin, Developer
feature: Personalization, Integration
exl-id: dcd0b9e7-8d36-4bde-b226-ac19e83f00e4
source-git-commit: 5b1387e18e059c938aca600cc31951a3f5289e7e
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 2%

---

# 新增自訂屬性至訂單

在本文中，您將瞭解如何新增自訂屬性至後台事件。 透過自訂屬性，您可以擷取豐富的資料深入解析來增強分析，並進一步為購物者建立個人化體驗。

>[!NOTE]
>
>瞭解如何[新增自訂身分](custom-identities.md)至設定檔。

自訂屬性支援兩個層級：

- 訂單層級
- 訂單料號層次

>[!NOTE]
>
>Adobe [!DNL Commerce]支援資料型別為字串、布林值或日期的自訂屬性。

將自訂屬性新增至後端辦公室事件需要您：

1. 在您的[!DNL Commerce]安裝中建立專案。
1. 更新您的結構描述，以便新的自訂屬性可以正確擷取到Experience Platform中。
1. 在Admin中，確認正在擷取自訂屬性並傳送至Experience Platform。

>[!IMPORTANT]
>
>以下目錄結構和程式碼範例說明如何實作自訂屬性。 所需的實際目錄結構和程式碼取決於存放區設定和環境。

## 步驟1：建立目錄結構

1. 導覽至`app/code`安裝中的[!DNL Commerce]目錄，並建立模組目錄。 例如： `Magento/AepCustomAttributes`。 此目錄包含自訂屬性所需的檔案。
1. 在模組目錄中，建立名為`etc`的子目錄。 `etc`目錄包含`module.xml`、`query.xml`、`di.xml`和`et_schema.xml`檔案。

## 步驟2：定義相依性和設定版本

建立定義相依性和安裝程式版本的`module.xml`檔案。 例如：

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="Magento_AepCustomAttributes">
        <sequence>
            <module name="Magento_SalesOrderDataExporter"/>
        </sequence>
    </module>
</config>
```

## 步驟3：擷取銷售訂單資料

建立可擷取銷售訂單資料的`query.xml`檔案。 例如：

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:Module:Magento_QueryXml:etc/query.xsd">
  <query name="salesOrdersV2">
    <source name="sales_order">
      <link-source name="sales_order_inventory_source" link-type="inner">
        <attribute name="inventory_source_code" alias="inventory_source" />
        <using glue="and">
          <condition attribute="order_id" operator="eq" type="identifier">entity_id</condition>
         </using> 
        </link-source>
    </source>
  </query>
  </config>
```

## 步驟4：設定相依性插入

建立設定相依性插入的`di.xml`檔案。 例如：

```xml
  <?xml version="1.0"?>
  <config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
      <type name="Magento\AepCustomAttributes\Model\Provider\CustomAttribute">
          <arguments>
              <argument name="usingField" xsi:type="string">commerceOrderId</argument>
          </arguments>
      </type>
      <type name="Magento\AepCustomAttributes\Model\Provider\OrderItemCustomAttribute">
          <arguments>
              <argument name="usingField" xsi:type="string">entityId</argument>
          </arguments>
      </type>
      <type name="Magento\DataServices\Model\ProductContext">
          <plugin name="product-context-plugin" type="Magento\AepCustomAttributes\Plugin\Model\ProductContext"/>
      </type>
  </config>
```

## 步驟5：定義用於相依性插入的服務

建立`et_schema.xml`檔案，定義用於相依性插入的服務。 例如：

```xml
  <?xml version="1.0"?>
  <config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_DataExporter:etc/et_schema.xsd">
      <record name="OrderV2">
          <field name="additionalInformation" type="CustomAttribute" repeated="true" provider="Magento\AepCustomAttributes\Model\Provider\CustomAttribute">
              <using field="commerceOrderId"/>
          </field>
      </record>
      <record name="OrderItemV2">
          <field name="additionalInformation" type="CustomAttribute" repeated="true" provider="Magento\AepCustomAttributes\Model\Provider\OrderItemCustomAttribute">
              <using field="entityId"/>
          </field>
      </record>
  </config>
```

## 步驟6：建立PHP檔案的目錄

在與`etc`目錄相同的層級，建立名為`Module/Provider`的目錄。 此目錄包含`OrderCustomAttributes`和`OrderItemCustomAttributes` PHP檔案。

## 步驟7：定義OrderCustomAttribute

建立定義順序自訂屬性的`OrderCustomAttributes.php`檔案。 例如：

```php
declare(strict_types=1);

namespace Magento\AepCustomAttributes\Model\Provider;

use Magento\Framework\Serialize\Serializer\Json;

class CustomAttribute
{
  /**
   * @var Json
   */
  private Json $jsonSerializer;

  /**
   * @var string
   */
  private string $usingField = '';

  /**
   * @param string $usingField
   * @param Json $jsonSerializer
   */
  public function __construct(
      string $usingField,
      Json $jsonSerializer
  ) {
      $this->usingField = $usingField;
      $this->jsonSerializer = $jsonSerializer;
  }

  /**
   * @param array $values
   * @return array
   */
  public function get(array $values): array
  {
      $output = [];

      /**
       * Entity IDs
       */
      $ids = array_column($values, $this->usingField);

      foreach ($this->flatten($values) as $row) {
          $info = \is_string($row['additionalInformation']) ? $row['additionalInformation'] : '{}';
          $unserializedData = $this->jsonSerializer->unserialize($info) ?? [];

          if (isset($row)) {
              $unserializedData['order_channel'] = 'order_channel';
              $unserializedData['order_status'] = 'order_status';

              $additionalInformation = [];
              foreach ($unserializedData as $name => $value) {
                  $additionalInformation[] = [
                      'name' => $name,
                      'value' => \is_string($value) ? $value : $this->jsonSerializer->serialize($value)
                  ];
              }
              foreach ($additionalInformation as $information) {
                  $output[] = [
                      'additionalInformation' => $information,
                      $this->usingField => $row[$this->usingField],
                  ];
              }
          }
      }
      return $output;
  }

  /**
   * @param $values
   * @return array
   */
  private function flatten($values): array
  {
      if (isset(current($values)[0])) {
          return array_merge([], ...array_values($values));
      }
      return $values;
  }
}
```

## 步驟8：定義OrderItemCustomAttribute

建立定義訂單專案自訂屬性的`OrderItemCustomAttributes.php`檔案。 例如：

```php
declare(strict_types=1);

namespace Magento\AepCustomAttributes\Model\Provider;

use Magento\Framework\Serialize\Serializer\Json;

class OrderItemCustomAttribute
{
  /**
   * @var Json
   */
  private Json $jsonSerializer;

  /**
   * @var string
   */
  private string $usingField = '';

  /**
   * @param Json $jsonSerializer
   * @param string $usingField
   */
  public function __construct(
      Json $jsonSerializer,
      string $usingField
  ) {
      $this->jsonSerializer = $jsonSerializer;
      $this->usingField = $usingField;
  }

  /**
   * Getting additional attributes data.
   *
   * @param array $values
   * @return array
   */
  public function get(array $values): array
  {
      $output = [];
      $values = $this->flatten($values);

      foreach ($values as $row) {
          $info = \is_string($row['additionalInformation']) ? $row['additionalInformation'] : '{}';
          $unserializedData = $this->jsonSerializer->unserialize($info) ?? [];
          $unserializedData['product_brand'] = implode(',', ['label 1', 'label 2']);

          $additionalInformation = [];
          foreach ($unserializedData as $name => $value) {
              $additionalInformation[] = [
                  'name' => $name,
                  'value' => \is_string($value) ? $value : $this->jsonSerializer->serialize($value)
              ];
          }
          foreach ($additionalInformation as $information) {
              $output[] = [
                  'additionalInformation' => $information,
                  $this->usingField => $row[$this->usingField],
              ];
          }
      }
      return $output;
  }

  /**
   * @param $values
   * @return array
   */
  private function flatten($values): array
  {
      if (isset(current($values)[0])) {
          return array_merge([], ...array_values($values));
      }
      return $values;
  }
}
```

## 步驟9：建立productContext檔案的目錄

在與`etc`目錄相同的層級，建立名為`Plugin/Module`的目錄。 此目錄包含`ProductContext.php`檔案。

## 步驟10：定義ProductContext類別

建立名為`ProductContext.php`的檔案來定義`ProductContext`類別。 例如：

```php
<?php>
namespace Magento\AepCustomAttributes\Plugin\Model;
use Magento\Catalog\Model\Product;
use Magento\DataServices\Model\ProductContext as Subject;
use Magento\Framework\App\ResourceConnection;

class ProductContext
{
    private ?array $brandCache = [];
    public function __construct(
        private ResourceConnection $resourceConnection ) {
    }  

    public function afterGetContextData(Subject $subject, array $result Product $product)
    {
        $brand = $product->getCustomAttribute('cust_attr1');
        if (!empty($brand) && $brand->getValue()) {
            $result['brands'] = ['brand_label_1', 'brand_label_2'];
            }
            return $result;
      }
  }
```

## 步驟11：註冊模組

在與`etc`目錄相同的層級，建立登入模組的`registration.php`檔案。 例如：

```php
<?php>
declare(strict_types=1);

use \Magento\Framework\Component\ComponentRegistrar;

ComponentRegistrar::register(
    ComponentRegistrar::MODULE,
    'Magento_AepCustomAttributes',
    __DIR__
);
```

## 步驟12：擴充您現有的XDM結構

為了確保您的[!DNL Commerce]結構描述可以在Experience Platform中擷取新的自訂訂單屬性，您需要擴充結構描述以包含這些自訂欄位。

若要瞭解如何擴充現有的XDM結構描述以包含這些自訂欄位，請參閱Experience Platform檔案中的[在UI中建立和編輯結構描述](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/ui/resources/schemas#custom-fields-for-standard-groups)一文。 租使用者ID欄位是動態產生的；但是，欄位結構應類似於Experience Platform檔案中提供的範例。

>[!IMPORTANT]
>
>XDM自訂屬性必須符合從[!DNL Commerce]傳送的屬性。

至`commerce.order`，新增訂單層級的欄位：

![訂單層級](assets/order-level.png)

至`productListItems`，新增訂單專案層級的欄位：

![訂單專案層級](assets/order-item-level.png)

## 步驟12：確認正在擷取資料

檢視Admin中的[資料自訂](connect-data.md#data-customization)索引標籤，以確認正在擷取自訂屬性資料並傳送至Experience Platform。

### 疑難排解

如果您在`No custom order attributes found.`標籤上看到訊息&#x200B;**[!UICONTROL Data Customization]**，請確認下列事項：

1. 您已完成啟用[Data Connector擴充功能](overview.md#prerequisites)的必要條件。
1. 您已設定[自訂訂單屬性](#add-custom-order-attributes)。
1. 至少已產生一個訂購事件。
