---
title: 管理 [!DNL Live Search]中無庫存的產品
description: 瞭解如何在 [!DNL Live Search] 中為Adobe Commerce管理無庫存產品。 設定詳細目錄顯示、inStock篩選器和GraphQL API篩選。
feature: Services, Search
role: Admin, Developer
level: Intermediate
source-git-commit: bc8f35434c9f01f1a920745fe42617df2003ca60
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# 管理無庫存產品

您可以使用庫存組態、查詢時間篩選和選用的後端功能標幟，控制缺貨產品在[!DNL Live Search]搜尋和類別結果中的顯示方式。 這些選項有重要的限制，本主題將對此進行說明。

## 庫存狀態篩選器

Adobe Commerce stock屬性`quantity_and_stock_status`不支援作為Facet，而且不會出現在&#x200B;**[!UICONTROL Add Facet]**&#x200B;對話方塊中。 但是，[!DNL Live Search]會公開您可在查詢時作為篩選器使用的`inStock`欄位。

## 隱藏無庫存產品

使用下列其中一種方法來隱藏無庫存的產品。

### Commerce設定

1.從&#x200B;*管理員*，前往&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**>**[!UICONTROL Catalog]**>**[!UICONTROL Inventory]**。

1.將&#x200B;**[!UICONTROL Display Out of Stock Products]**&#x200B;設為&#x200B;**[!UICONTROL No]**。

1. 按一下&#x200B;**[!UICONTROL Save Config]**。

當&#x200B;**[!UICONTROL Display Out of Stock Products]**&#x200B;設定為`No`時，[!DNL Live Search]會透過PLP Widget將`inStock = 'no`新增至店面查詢，因此不會傳回無存貨的產品。

### API篩選器

當您直接呼叫[!DNL Live Search] API （GraphQL或REST）時，請明確篩選無庫存的產品，例如：

```graphql
query productSearchInStockOnly {
  productSearch(
    phrase: ""
    filter: [
      { attribute: "inStock", eq: "true" }
    ]
  ) {
    total_count
    items {
      productView {
        sku
        name
        inStock
      }
    }
  }
}
```

當您不透過[即時搜尋PLP Widget](plp-styling.md)路由傳送請求時，請使用此方法。

### 在庫存結果後顯示無庫存

為了保留結果集中的缺貨產品，但在依相關性排序時始終在缺貨產品之後，Adobe可以為您的環境啟用內部功能標幟。

- [!DNL Live Search]管理UI中未公開此功能標幟。
- 若要請求，請[聯絡Adobe支援](https://experienceleague.adobe.com/zh-hant/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide){target="_blank"}並參考該功能，以將無庫存產品移至搜尋結果的結尾。

>[!NOTE]
>
>啟用標幟後，依&#x200B;*關聯性*&#x200B;排序時，結果集中任何剩餘的缺貨產品都會移至底部。 其他排序訂單（例如，*價格*&#x200B;或&#x200B;*產品名稱*）不受影響。

### 搜尋銷售規則和庫存

搜尋銷售規則是以查詢為基礎，並鎖定個別產品，而非依庫存狀態或Facet值鎖定整個群組：

- 規則條件僅取決於購物者的搜尋片語(`Query is`， `Query contains`， `Query starts with`， `Query ends with`)。
- 規則事件（提升、隱藏、釘選、隱藏）適用於每個事件一個SKU。

由於這些限制：

- 您無法單獨根據庫存狀態來建立埋藏或隱藏所有無庫存產品的規則。
- 您可以手動隱藏或隱藏您新增為規則中事件的特定SKU （每個規則最多50個規則和25個事件）。

若要隱藏或取消所有目錄中的無庫存產品優先順序，請使用本主題中說明的詳細目錄設定和`inStock`篩選器（以及選用功能標幟），而不要使用「搜尋銷售」規則。

>[!MORELIKETHIS]
>
> - [搜尋銷售規則](rules.md)
> - [設定Inventory management全域選項](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/inventory/configuration/configuration)
