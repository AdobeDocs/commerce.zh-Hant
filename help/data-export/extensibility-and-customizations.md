---
title: 擴充及自訂SaaS資料匯出摘要資料
description: 瞭解如何擴充及自訂 [!DNL SaaS Data Export] 摘要資料。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 694bd281-12c5-415c-a251-b4251e2edea7
TQID: https://experienceleague.adobe.com/T71zNl7WOrqzEsz4H8A8arx--q6w1B0h33CF2Q0VI4A
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 815
ht-degree: 0%

---

# 擴充及自訂SaaS資料匯出摘要資料

[!DNL Commerce Data Export]擴充功能可讓您將資料從[!DNL Commerce]應用程式匯出至Commerce服務，例如即時搜尋、目錄服務和產品建議。 如有需要，您可以擴充及自訂摘要資料，以包含其他屬性資料或修改收集的資料。

新增屬性資料後，可從GraphQL結構描述中的[屬性欄位](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#productviewattribute-type)存取店面服務。

>[!NOTE]
>
>新增或修改摘要資料可能會影響Commerce後端的效能和處理邏輯。 在合併到生產環境之前測試自訂的程式碼。 使用API Mesh擴充目錄服務GraphQL架構，而不將資料新增到後端。 如需設定詳細資料，請參閱[目錄服務與API Mesh](../catalog-service/mesh.md)。

## 擴充產品摘要中的系統屬性資料

產品摘要包含產品處理所需或消費者常用的預設系統屬性。 您可以將其他系統屬性新增至摘要，以將其納入產品摘要中。

若要完成此工作，請更新`magento/catalog-data-exporter`模組以將其他系統屬性新增到[相依性插入組態檔](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`)。

將屬性新增至產品屬性查詢(`Magento\CatalogDataExporter\Model\Query\ProductAttributeQuery`)。

**範例**

```xml
    <type name="Magento\CatalogDataExporter\Model\Query\ProductAttributeQuery">
        <arguments>
            <argument name="systemAttributes" xsi:type="array">
                <item name="news_from_date" xsi:type="string">news_from_date</item>
                ...
                <item name="some_system_attribute_code">some_system_attribute_code</item>
            </argument>
        </arguments>
    </type>
```

## 將產品屬性新增至Adobe Commerce

開發人員可以使用下列其中一種方法，新增可從[產品屬性欄位](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#output-fields)存取的產品屬性：

- 將屬性新增至Adobe Commerce，以包含在匯出至Commerce店面服務的`products`摘要資料中。
- 在摘要同步程式期間，使用外掛程式動態新增屬性。

### 將屬性新增至Adobe Commerce

您可以從「Commerce管理員」新增產品屬性，或以程式設計方式使用自訂PHP模組來定義屬性及更新Adobe Commerce。 從「Commerce管理員」新增屬性是最簡單的方法，因為您可以一次新增屬性和所有必要的中繼資料。 在下次排定的同步處理期間，新屬性及其中繼資料屬性會自動匯出至SaaS服務。

#### 從管理員建立產品屬性

1. 從Commerce Admin，從產品屬性設定頁面([!UICONTROL Stores] > *[!UICONTROL Attributes]* > [!UICONTROL Product])建立屬性。

1. 視需要新增屬性至屬性集。

請參閱&#x200B;*Adobe Commerce管理指南*&#x200B;中的[建立產品屬性](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create)。

#### 以程式設計方式建立產品屬性

建立實作`DataPatchInterface`的資料修補程式，以程式設計方式新增產品屬性，並在建構函式中具現化`EavSetup Factory`類別的復本，以設定屬性選項。

當您定義屬性選項時，除了`type`、`label`和`input`以外的所有屬性引數都是選用的。 定義下列其他引數以及與預設設定不同的其他任何引數。

- **`user_defined`=`1`** — 在資料同步處理期間，將屬性匯出至storefront services
- **`used_in_product_listing`=`1`** — 讓屬性可在產品清單資料庫查詢中存取

如需有關建立資料修補程式的資訊，請參閱&#x200B;*PHP Developer Guide*&#x200B;中的[開發資料與結構描述修補程式](https://developer.adobe.com/commerce/php/development/components/declarative-schema/patches/)。

### 動態新增產品屬性

如需有關動態建立產品屬性而不引入新EAV屬性的詳細資訊，請參閱[動態新增產品屬性](add-attribute-dynamically.md)。

## 摘要結構描述概述(`et_schema.xml`) {#feed-schema-overview}

每個摘要資料結構都是使用簡單的XML DSL在`etc/et_schema.xml`中宣告。 架構會讀取此檔案，以決定要收集哪些欄位以及要呼叫哪些PHP提供者類別。

```xml
<record name="Product">
  <field name="sku" type="ID" />
  <field name="name" type="String" />
  <field name="attributes" type="Attribute" repeated="true"
         provider="Magento\CatalogDataExporter\Model\Provider\Product\Attributes">
    <using field="productId" />
    <using field="storeViewCode" />
  </field>
</record>
```

關鍵元素：

- `<record>` — 定義摘要實體
- `<field>` — 宣告資料欄位；`provider`屬性指向實作`DataProcessorInterface`的PHP類別以擷取資料
- `repeated="true"` — 欄位是物件陣列
- `<using>` — 從父記錄內容傳遞至提供者的輸入引數

>[!IMPORTANT]
>
>新增欄位至`et_schema.xml`只會變更[!DNL Adobe Commerce]在本機收集的內容。 接收SaaS服務也必須更新，以接受和處理新欄位，才能對店面產生任何影響。

## 提交後觀察資料 {#observe-data-after-submission}

每次成功將批次提交至SaaS服務後，[!DNL SaaS Data Export]都會傳送`data_sent_outside`事件。 使用此事件來稽核記錄、webhook觸發程式或量度集合。

**事件：** `data_sent_outside`

**可用資料：**

| 索引鍵 | 說明 |
|---|---|
| `timestamp` | 提交的Unix時間戳記 |
| `type` | 摘要名稱（例如，`products`、`prices`） |
| `data` | 已提交的摘要裝載 |

**觀察者範例：**

```php
<?php
namespace My\Module\Observer;

use Magento\Framework\Event\Observer;
use Magento\Framework\Event\ObserverInterface;

class DataSentOutsideObserver implements ObserverInterface
{
    public function execute(Observer $observer): void
    {
        $feedName = $observer->getData('type');
        $timestamp = $observer->getData('timestamp');
        $data = $observer->getData('data');

        // Custom logic: audit logging, webhook, metrics
    }
}
```

在`etc/events.xml`中註冊觀察者：

```xml
<event name="data_sent_outside">
    <observer name="my_module_data_sent_outside"
              instance="My\Module\Observer\DataSentOutsideObserver" />
</event>
```

如需有關活動和觀察者的一般資訊，請參閱Adobe Commerce開發人員檔案中的[活動和觀察者](https://developer.adobe.com/commerce/php/development/components/events-and-observers){target="_blank"}。

## 提交前篩選資料

使用`Magento\SaaSCommon\Model\DataFilter`延伸點來標籤敏感性欄位，或在將資料傳送至SaaS服務之前略過特定實體。 這對GDPR或PCI等法規遵循要求非常有用，因為某些欄位不得離開Commerce執行個體。

實作介面並透過`etc/di.xml`中的DI喜好設定連線：

```xml
<preference for="Magento\SaaSCommon\Model\DataFilter"
            type="My\Module\Model\MyDataFilter" />
```

>[!NOTE]
>
>篩選會在資料收集後套用。 如果設定`PERSIST_EXPORTED_FEED=1`，則摘要表格會在進行篩選之前儲存未篩選的裝載。

>[!MORELIKETHIS]
>
> - [動態新增產品屬性](add-attribute-dynamically.md)
> - [新增稅捐類別、屬性集及存貨中繼資料](add-tax-attribute-set-inventory-attributes.md)
> - [同步化的運作方式](sync-overview.md)
