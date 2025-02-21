---
title: 索引
description: 瞭解 [!DNL Live Search] 如何索引產品屬性屬性。
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 0%

---

# 索引

[!DNL Live Search]索引程式會讀取目錄中的產品屬性並建立索引，以便快速搜尋、篩選和展示產品。

產品屬性屬性（中繼資料）會決定：

* 如何在目錄中使用屬性
* 其在存放區中的外觀和行為
* 資料傳輸作業中包含的資料

屬性中繼資料的範圍是`website/store/store view`。

[!DNL Live Search] API允許使用者端在Adobe Commerce管理中，依任何具有[storefront屬性](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes) `Use in Search`設定為`Yes`的產品屬性來排序。 啟用時，可以為屬性設定`Search Weight`。

[!DNL Live Search]未索引已刪除的產品或設定為`Not Visible Individually`的產品。

>[!NOTE]
>
> 擁有[!DNL Live Search]的Commerce客戶可透過[SaaS價格索引器](../price-index/price-indexing.md)，利用其網站上更快速的價格變更更新和同步處理時間。

## 索引管道

使用者端從店面呼叫搜尋服務以擷取（可篩選、可排序）索引中繼資料。 搜尋服務只能呼叫具有層次導覽中&#x200B;*使用*&#x200B;屬性設定為`Filterable (with results)`且&#x200B;*產品清單中用於排序*&#x200B;設定為`Yes`的可搜尋產品屬性。

若要建構動態查詢，搜尋服務必須知道哪些屬性可搜尋，以及它們的[權重](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-results)。 [!DNL Live Search]遵循Adobe Commerce搜尋權重（1-10，其中10是最高優先順序）。 您可以在結構描述中找到已同步並與目錄服務共用的資料清單，其定義如下：

`vendor/magento/module-catalog-data-exporter/etc/et_schema.xml`

![[!DNL Live Search]索引使用者端搜尋圖表](assets/indexing-pipeline.svg)

1. 檢查商家是否有[!DNL Live Search]權益。
1. 取得含屬性中繼資料變更的存放區檢視。
1. 儲存索引屬性。
1. 重新索引搜尋索引。

### 完整索引

當[!DNL Live Search]已設定並在上線期間同步時，最多可能需要60分鐘才能建立初始索引。 大型目錄可能需要更長的時間來編列索引。 處理程式會在`cron`提交摘要後開始，並完成執行。

以下事件會觸發完整同步和索引建置：

* 正在上線[目錄資料同步](install.md#synchronize-catalog-data)
* 屬性中繼資料的變更

例如，將`color`屬性的`Use in Search`屬性從`No`變更為`Yes`會將屬性中繼資料變更為`searchable=true`，並觸發完全同步和重新索引。 下列屬性中繼資料在變更時觸發完整同步和重新索引：

* `filterableInSearch`
* `searchable`
* `sortable`
* `visibleInSearch`

### 串流產品更新

在[上線](install.md#synchronize-catalog-data)期間建立初始索引後，將會持續同步下列增量產品更新並重新編制索引：

* 新增至目錄的新產品
* 產品屬性值的變更

例如，將新的色票值新增至`color`屬性會作為串流產品更新處理。

串流更新工作流程：

1. 更新的產品會從Adobe Commerce執行個體同步至目錄服務。
1. 索引服務會持續從目錄服務尋找產品更新。 更新的產品在到達目錄服務時會編制索引。
1. 產品更新最多可能需要15分鐘的時間才能在[!DNL Live Search]中提供。

#### 影響產品可見性的更新

當您更新[!DNL Live Search]管理員組態設定、Adobe Commerce管理員組態設定或目錄資料時，這些變更可能會延遲出現在店面上。

下表說明各種變更，以及它們出現在店面前的等待時間。

| 更新 | 延遲至店面可見 |
|---|---|
| [!DNL Live Search]管理員變更多面向、價格設定、搜尋或類別銷售規則。 | 15-20分鐘。 |
| [!DNL Live Search]個需要重新索引的管理變更：語言設定或同義字。 | 在重新索引完成之後最多15分鐘。 |
| 需要完整重新索引的Adobe Commerce管理變更：可搜尋、可排序或可篩選的屬性中繼資料 | 在重新索引完成之後最多15分鐘。 |
| 目錄資料中不需要重新索引的增量變更：產品詳細目錄、價格、名稱等。 | 彈性搜尋索引更新後最多15分鐘提供最新資料。 |

## 使用者端搜尋

[!DNL Live Search] API可讓使用者端藉由將[storefront屬性](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes)，*產品清單中用於排序的*&#x200B;設定為`Yes`，依任何可排序的產品屬性排序。 根據主題，此設定會導致在目錄頁面上的[排序依據](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/navigation/navigation)分頁控制項中包含屬性作為選項。 [!DNL Live Search]最多可為200個產品屬性編制索引，其中有[可搜尋且可篩選的店面屬性](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes)。

索引中繼資料儲存在索引管道中，並可由搜尋服務存取。

![[!DNL Live Search]索引中繼資料API圖表](assets/index-metadata-api.svg)

### 可排序的屬性工作流程

1. 使用者端呼叫搜尋服務。
1. 搜尋服務會呼叫Search Admin服務。
1. 搜尋服務會呼叫索引管道。

## 已針對所有產品編制索引

此清單中的欄位順序反映了匯出產品資料中欄的一般順序。

* `environment_id`
* `website_code`
* `store_code`
* `store_view_code`
* `product_id`
* `sku`
* `name`
* `type`
* `displayable`
* `deleted`
* `url`
* `currency`
* `meta_description`
* `meta_keyword`
* `meta_title`
* `description`
* `short_description`
* `weight`
* `image`
* `small_image`
* `thumbnail_image`
* `prices`
* `in_stock`
* `low_stock`

下列欄位會針對所有可設定的產品編制索引：

* `childrenSkus`
