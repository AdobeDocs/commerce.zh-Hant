---
title: 擴充及自訂SaaS資料匯出摘要資料
description: 瞭解如何擴充及自訂 [!DNL SaaS Data Export] 摘要資料。
role: Admin, Developer
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# 擴充及自訂SaaS資料匯出摘要資料

[!DNL Commerce Data Export]擴充功能可讓您將資料從[!DNL Commerce]應用程式匯出至Commerce服務，例如即時搜尋、目錄服務和產品建議。 如有需要，您可以擴充及自訂摘要資料，以包含其他屬性資料或修改收集的資料。

新增屬性資料後，可從GraphQL結構描述中的[屬性欄位](https://developer.adobe.com/commerce/services/graphql/catalog-service/products/#productviewattribute-type)存取店面服務。

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

開發人員可以使用下列其中一種方法，新增可從[產品屬性欄位](https://developer.adobe.com/commerce/services/graphql/catalog-service/products/#output-fields)存取的產品屬性：

- 將屬性新增至Adobe Commerce，以包含在匯出至Commerce店面服務的`products`摘要資料中。
- 在摘要同步程式期間，使用外掛程式動態新增屬性。

### 將屬性新增至Adobe Commerce

您可以從「Commerce管理員」新增產品屬性，或以程式設計方式使用自訂PHP模組來定義屬性及更新Adobe Commerce。 這是新增產品屬性最簡單的方法，因為您可以新增屬性和所有必要的中繼資料。 在下次排定的同步處理期間，新屬性及其中繼資料屬性會自動匯出至SaaS服務。

#### 從管理員建立產品屬性

1. 從Commerce Admin，從產品屬性設定頁面([!UICONTROL Stores] > *[!UICONTROL Attributes]* > [!UICONTROL Product])建立屬性。

1. 視需要新增屬性至屬性集。

請參閱&#x200B;*Adobe Commerce管理指南*&#x200B;中的[建立產品屬性](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create)。

#### 以程式設計方式建立產品屬性

建立實作`DataPatchInterface`的資料修補程式，以程式設計方式新增產品屬性，並在建構函式中具現化`EavSetup Factory`類別的復本，以設定屬性選項。

當您定義屬性選項時，除了`type`、`label`和`input`以外的所有屬性引數都是選用的。 定義下列其他選項以及與預設設定不同的任何其他選項。

- 透過設定`user_defined` = `1`，確保屬性在資料同步處理期間匯出至storefront services
- 若要確保在產品清單資料庫查詢中可存取屬性，請設定`used_in_product_listing` = `1`。

如需有關建立資料修補程式的資訊，請參閱&#x200B;*PHP Developer Guide*&#x200B;中的[開發資料與結構描述修補程式](https://developer.adobe.com/commerce/php/development/components/declarative-schema/patches/)。

### 動態新增產品屬性

如需有關動態建立產品屬性而不引入新Eav屬性的詳細資訊，請參閱[動態新增屬性](add-attribute-dynamically.md)。
