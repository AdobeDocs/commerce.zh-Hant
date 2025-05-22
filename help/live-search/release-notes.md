---
title: '[!DNL Live Search]發行說明'
description: Adobe Commerce中 [!DNL Live Search] 的最新發行資訊。
feature: Services, Search, Release Notes
exl-id: 099cf79c-968c-4381-b66d-7f6141ad2db3
source-git-commit: 773b5f703ce608a54f691defcc2a3ad3f49b755c
workflow-type: tm+mt
source-wordcount: '2500'
ht-degree: 0%

---

# [!DNL Live Search]發行說明

以下版本說明說明[!DNL Live Search]的最新版本。
支援目前的主要發行版本。 舊版的發行說明僅供參考。
更新包括：

![新](../assets/new.svg)新功能
![修正](../assets/fix.svg)修正和改良
![錯誤](../assets/bug.svg)已知問題

## 託管服務更新

這些附註會說明在版本設定發行之外發佈的更新，或託管服務的改進。

_2025年4月29日_

![修正](../assets/fix.svg)修正&#x200B;[**效能**](./performance.md)&#x200B;索引標籤上的&#x200B;**匯出至CSV**&#x200B;報告未包含日期範圍中指定之所有資料的問題。
![修正](../assets/fix.svg)修正使用搜尋查詢篩選時，無法儲存[銷售規則](./rules.md)的問題。
![修正](../assets/fix.svg)修正[釘選產品](./facets-manage.md#pinunpin-facet)未列在結果頁面頂端的問題。

_2025年4月21日_

![修正](../assets/fix.svg)修正價格範圍篩選器的問題，以免結果中包含等於上限範圍的產品。 此變更會與Facet價格範圍的定義方式一致。

_2025年4月3日_

![修正](../assets/fix.svg)已更新SaaS Data Export擴充功能，針對B2B商家移除「產品必須指派至根類別」[限制](boundaries-limits.md#b2b-and-category-permissions)。 請參閱[管理資料匯出擴充功能](../data-export/manage-extension.md)，瞭解如何將SaaS Data Export擴充功能更新至103.4.0+版。

_2025年2月20日_

![新](../assets/new.svg) Commerce支援多字同義字。 [深入瞭解](synonyms-type.md#multi-word-synonym-behavior)。 2月20日正式發行後，才能支援多字同義字。 任何現有的多字同義字都需要完整重新索引才能運作，您可以透過[建立支援票證](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide)來要求這樣做。

_2025年1月31日_

![新](../assets/new.svg)測試環境中未查詢的目錄資料有新的資料保留原則。 [了解更多](overview.md#catalog-data-retention-policy)。

_2024年9月19日_

![新](../assets/new.svg)已發行支援三種新搜尋功能的測試版：分層、開頭為和包含。 [了解更多](install.md#install-the-live-search-beta)。

_2024年9月4日_

![修正](../assets/fix.svg)將Facet[&#128279;](boundaries-limits.md#facets)內可傳回的最大值區數增加到100。

_2024年8月7日_

![修正](../assets/fix.svg)將[價格刻面](settings.md#price-faceting)的最大間隔值或價格範圍從10,000增加到40,000,000。

_2024年2月13日_

![新的](../assets/new.svg) [!DNL Live Search]現在支援設定[搜尋銷售](rules.md)的預設規則。

_2023年10月12日_

![新](../assets/new.svg) Commerce管理員現在可以指定[!DNL Live Search]的索引語言。 請參閱[設定](settings.md)。
![修正](../assets/fix.svg) 「搜尋規則」標籤已重新命名為「搜尋銷售」。

_2023年6月13日_

![修正](../assets/fix.svg)修正某些字元（如引號或縮寫符號）造成排名問題的問題。 重新索引可解決這些問題。

_2023年4月25日_

![新](../assets/new.svg) [!DNL Live Search]客戶現在可以利用新的[SaaS價格索引子](../price-index/price-indexing.md)。

### PLP Widget

_2025年5月22日_

![Fix](../assets/fix.svg)修正地區設定變更為法文、德文、義大利文或西班牙文時，「加入購物車」按鈕仍為英文的問題。
![修正](../assets/fix.svg)修正無存貨產品顯示「加入購物車」按鈕的問題。

_2024年5月31日_

![新增](../assets/new.svg)已發行PLP Widget 2.0.0版，其中新增支援下列功能：

- 加入購物車按鈕 — 僅適用於簡單產品。
- 每個產品有多個影像 — 為可設定產品選擇不同顏色時，影像可能會變更。

_2023年10月27日_

![新](../assets/new.svg) [!DNL Live Search] PLP Widget現在支援色票。

## [!DNL Live Search] 4.3.0

_2025年3月11日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![修正](../assets/fix.svg) [!DNL Live Search]現在支援執行Adobe Commerce 2.4.8-beta2的PHP 8.4安裝。
![修正](../assets/fix.svg)修正搜尋配接器與`psr/http-message:2.0`不相容的問題。

## [!DNL Live Search] 4.2.3

_2025年2月13日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![修正](../assets/fix.svg)修正訂單詳細資料頁面遺失訂單編號、日期及&#x200B;**[!UICONTROL Reorder]**&#x200B;按鈕的問題。

## [!DNL Live Search] 4.2.2

_2025年1月6日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![修正](../assets/fix.svg)已修正Adobe Commerce 2.4.5版和更舊版本上`categoryList` GraphqL查詢發生錯誤的問題。

## [!DNL Live Search] 4.2.1

_2024年7月31日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![修正](../assets/fix.svg)修正某些指令碼未在結帳頁面上載入的問題。
![修正](../assets/fix.svg)修正`composer.json`檔案中的相依性版本。

## [!DNL Live Search] 4.2.0

_2024年5月31日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)已更新Live Search擴充功能以使用PLP Widget 2.0.0版。

## [!DNL Live Search] 4.1.2

_2024年5月16日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

### 更新

![修正](../assets/fix.svg)已修正[`productSearch`](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#filtering-by-categories) GraphQL查詢，以根據類別的`categoryPath`和`categoryList`正確篩選。

## [!DNL Live Search] 4.1.1

_2024年3月19日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

### 新功能

![New](../assets/new.svg)已新增波蘭文的語言支援。
![New](../assets/new.svg) [!DNL Live Search]現在支援執行Adobe Commerce 2.4.4的PHP 8.3安裝。

## [!DNL Live Search] 4.1.0

_2024年2月22日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

### 新功能

![新增](../assets/new.svg) [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard)現已可用。 此改版後的儀表板提供[!DNL Product Recommendations]、[!DNL Live Search]和[!DNL Catalog Service]的資料串流的深入分析。

### 更新

![修正](../assets/fix.svg)修正當訪客使用者在非預設商店檢視中將產品新增到購物車時發生錯誤的問題。
![修正](../assets/fix.svg)修正搜尋彈出視窗一律在價格值前面顯示貨幣符號（不論地區設定為何）的問題。
![修正](../assets/fix.svg)已移除已停用核心外掛程式不必要的型別定義，以修正安裝時的相容性問題。

## [!DNL Live Search] 4.0.0

_2023年11月13日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

### 新功能

![新](../assets/new.svg) [!DNL Live Search]現在支援PLP Widget中的色票。
![新](../assets/new.svg) [!DNL Live Search]現在會顯示類別名稱，而非類別識別碼。
![新的](../assets/new.svg) [!DNL Live Search]現在支援PLP Widget中的刪除線價格。
![新](../assets/new.svg)推出「隱藏篩選器」按鈕以隱藏篩選器面板。


### 更新

![修正](../assets/fix.svg) [!DNL Live Search] PLP Widget現在已預設為新安裝啟用。
![修正](../assets/fix.svg)已棄用搜尋配接器。 日後，搜尋配接卡只會更新以解決安全性問題。
![修正](../assets/fix.svg)已重新設定CSS樣式，以便更妥善地隔離Widget類別。
![修正](../assets/fix.svg)微幅錯誤修正

安裝3.1.1版或更新版本後，啟用新的索引子：

- 產品價格摘要
- 範圍網站資料摘要
- 範圍客戶群組資料摘要

升級之後，在將變更推送至生產環境之前，請先在QA或測試環境中測試已更新的設定。

+++3.1.1和舊版

### [!DNL Live Search] 3.1.1

_2023年9月15日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

已新增![新](../assets/new.svg)新類別銷售標籤。 使用者現在可以為每個類別新增智慧型排名和手動排名（釘選、提升、隱藏、隱藏）
![新](../assets/new.svg)使用者可以新增具有智慧型或手動排名的單一類別規則
![新](../assets/new.svg)使用者現在可以將智慧型排名規則新增到子類別
![新](../assets/new.svg)刪除具有智慧型排名之子類別時，提供詳細資訊
![新](../assets/new.svg)已新增刪除繼承排名策略規則的功能
![新](../assets/new.svg)已新增刪除單一類別之規則的功能
![新](../assets/new.svg)使用者現在可以在新增規則時依類別名稱搜尋
![新的](../assets/new.svg)使用類別樹狀檢視，使用者現在可以檢視哪個類別已套用規則。
![新](../assets/new.svg)類別預覽只會顯示選取的類別。
![新的](../assets/new.svg) AEM CIF [Pover Widget](https://github.com/adobe/aem-cif-guides-venia/pull/319)和[PLP Widget](https://github.com/adobe/aem-cif-guides-venia/pull/320)元件可讓AEM網站充分利用[!DNL Live Search]。

#### 更新

![修正](../assets/fix.svg)產品與價格摘要的資料表大小已大幅縮減。 資料表`catalog_data_exporter_products`和`catalog_data_exporter_product_prices`應該會大幅縮減大小。
![修正](../assets/fix.svg)「規則」索引標籤已重新命名為「搜尋規則」
![修正](../assets/fix.svg)依「趨勢」排名時，您現在可以選擇：
- 3天（預設）
- 14天
- 30天
![修正](../assets/fix.svg) 「事件」（提升/釘選/隱藏）已重新命名為「手動排名」
![修正](../assets/fix.svg)「排名型別」已重新命名為「智慧型排名」
![修正](../assets/fix.svg)微幅錯誤修正

### [!DNL Live Search] 3.1.0

_2023年9月1日_

[!BADGE 支援]{type="Informative" tooltip="支援"} Adobe Commerce 2.4.4或更新版本

#### 更新

![修正](../assets/fix.svg)產品清單Widget已更新為使用[目錄服務API](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/)。

### [!DNL Live Search] 3.0.2

_2023年8月7日_

[!BADGE 支援]{type="Informative" tooltip="支援"} Adobe Commerce 2.4.4或更新版本

#### 新功能

![新](../assets/new.svg)下列值已新增至`storeDetails`物件：

- &quot;允許每頁所有產品&quot;
- 匯率
- 「網格上每頁產品允許值」
- 「網格上每頁產品預設值」
- 存放區語言

#### 更新

已將![Fix](../assets/fix.svg)目錄服務模組新增至中繼封裝，以支援進階資料擷取。
![修正](../assets/fix.svg)使用產品清單頁面Widget時，**我的帳戶**&#x200B;頁面導覽不再消失。

商家必須升級[!DNL Live Search]擴充功能版本>= 3.0.2才能存取這些功能。

建議先升級並測試，再推送至生產環境。 確認測試環境結果後，請考慮在非尖峰時段升級生產環境。

#### 限制

使用即時搜尋產品清單頁面Widget會導致Google Tag Manager失敗。 如果需要Google Tag Manager，請使用預設的「搜尋轉接器」。

### [!DNL Live Search] 3.0.1

_2023年3月14日_

[!BADGE 支援]{type="Informative" tooltip="支援"} Adobe Commerce 2.4.4或更新版本

#### 新功能

規則預覽中的![新](../assets/new.svg)產品專案卡
![新增](../assets/new.svg) [產品清單頁面Widget](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-storefront/plp-styling)
![新](../assets/new.svg) [類別篩選選項](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#facets)
![新](../assets/new.svg)已新增拖放以建立Pin事件的功能
![新](../assets/new.svg)個新的Pin動作：
 — 釘選到地點 — 按一下即可建立釘選事件的釘選按鈕
 — 釘選到頂端 — 將產品放在第一個位置
 — 釘選到底部 — 將產品放置在結果的底部
 — 按一下即可取消釘選事件
![新](../assets/new.svg) [規則的智慧型排名](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/rules/rules-add)
![新](../assets/new.svg) [!DNL Live Search]現在支援Commerce中的完整[Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction)功能(先前稱為多Source詳細目錄，或MSI)。 若要啟用完整支援，您必須[將](install.md#update)相依性模組`commerce-data-export`更新為102.2.0+版。

#### 更新

![修正](../assets/fix.svg)設定規則現在會自動以唯一方式排序職位
![修正](../assets/fix.svg)刪除現有事件現在會更新預覽
可以儲存沒有事件的![修正](../assets/fix.svg)規則
![修正](../assets/fix.svg)移除多面向「選取型別」選取器
![修正](../assets/fix.svg)已新增未儲存規則的新「編輯」狀態

#### 修正

![修正](../assets/fix.svg)儲存期間發生未完成的事件時修復伺服器錯誤
![修正](../assets/fix.svg)修正當有多個事件時，正確刪除特定事件的問題
![修正](../assets/fix.svg)已修正當新增新事件時現有規則事件未更新的問題
![修正](../assets/fix.svg)已修正來自詳細資料的第二個「編輯」點選，[!DNL Live Search]個頁面需要重新載入
![修正](../assets/fix.svg)同義字：修正使用者按一下退出輸入時，無法將焦點傳回欄位的問題
![修正](../assets/fix.svg)其他微幅錯誤修正與效能更新
![錯誤](../assets/bug.svg) — 僅在「即時搜尋」Widget中支援「為您推薦」的排名。 預設的Luma和PWA搜尋功能不支援此功能。
![錯誤](../assets/bug.svg) — 自訂價格屬性Facet無法在Luma中正確轉譯，但API已正確篩選它們。

商家必須升級[!DNL Live Search]擴充功能版本>= 3.0.1才能存取這些功能。

建議先升級並測試，再推送至生產環境。 確認測試環境結果後，請考慮在非尖峰時段升級生產環境。

### [!DNL Live Search] 2.0.5

[!BADGE 支援]{type="Informative" tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![修正](../assets/fix.svg) — 當SDK資源因網路問題而無法使用時，即時搜尋會擲回錯誤。 此錯誤已修正。

商家必須升級Live Search擴充功能>= 2.0.5版才能存取這些功能。

建議先升級並測試，再推送至生產環境。 確認測試環境結果後，請考慮在非尖峰時段升級生產環境。

### [!DNL Live Search] 2.0.4

[!BADGE 支援]{type="Informative" tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)「即時搜尋」現在支援以管理員中的「顯示無庫存產品」設定進行篩選。 如果「顯示無庫存產品」設為false，則會將`inStock = true`新增至篩選器。
![修正](../assets/fix.svg)為了改善效能，「建議」區塊已從「即時搜尋」快顯視窗中移除。 如果您想要取代功能，資料仍會透過GraphQL傳遞。
![修正](../assets/fix.svg) `categories`和`categoryPath`已取代`categoryIds`進行類別篩選。 閱讀[productSearch](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/)主題中的詳細資訊。
![修正](../assets/fix.svg)之前，繫結至B2B公司的使用者在執行搜尋時會收到錯誤的客戶群組代碼。 即時搜尋現在會傳回正確的值。
![修正](../assets/fix.svg)先前，當搜尋不存在的辭彙時，即時搜尋會傳回錯誤。 此錯誤現已修正。

商家必須升級[!DNL Live Search]擴充功能版本>= 2.0.4才能存取這些功能。

建議使用者在推送至生產環境前，先升級並測試。 確認測試環境結果後，請考慮在非尖峰時段升級生產環境。

### [!DNL Live Search] 2.0.3

[!BADGE 支援]{type="Informative" tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新的](../assets/new.svg) Live Search現在藉由遵循類別許可權、共用類別目錄和客戶群組特定定價，支援B2B功能。

商家必須升級[!DNL Live Search]擴充功能版本>= 2.0.3才能存取這些功能。

建議使用者在推送至生產環境前，先升級並測試。 確認測試環境結果後，請考慮在非尖峰時段升級生產環境。

### [!DNL Live Search] 2.0

[!BADGE 支援]{type="Informative" tooltip="支援"} Adobe Commerce 2.4.4或更新版本

現有的[!DNL Live Search]安裝必須升級至[!DNL Live Search] 2.0.0，才能使用下列新功能、修正和改良：

![New](../assets/new.svg) [!DNL Live Search]現在支援執行Adobe Commerce 2.4.4的PHP 8.1安裝。
![新增](../assets/new.svg) `Magento_ElasticsearchCatalogPermissionsGraphQl`模組已新增至安裝期間停用的模組清單。
![新](../assets/new.svg) [[!DNL storefront popover]](overview.md)中的可用行數可以從&#x200B;*管理員*設定。
[!DNL Live Search]支援的![新](../assets/new.svg) Beta [PWA](https://developer.adobe.com/commerce/pwa-studio/)。
![新增](../assets/new.svg) [!DNL Live Search]安裝程式已更新，其中包含進階程式變更。
![修正](../assets/fix.svg) [進階搜尋](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search)連結已從店面頁尾移除。
![錯誤](../assets/bug.svg) [Commerce GraphQL API](https://developer.adobe.com/commerce/services/graphql/live-search/)不支援與PWA測試版相關的下列產品屬性： `description`、`name`、`short_description`
![錯誤](../assets/bug.svg) [!DNL Live Search]的PWA測試版不支援[事件處理](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/)。

### [!DNL Live Search] 1.3.1

[!BADGE 支援]{type="Informative" tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![修正](../assets/fix.svg) [自訂價格屬性](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types)在設定為[Facet](facets-add.md)時不再傳回錯誤。
![修正](../assets/fix.svg)修正無法使用[貨幣符號](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration#step-5-customize-currency-symbols-optional) (`data-currency-symbol`)時，發生錯誤的問題。
![修正](../assets/fix.svg) [[!DNL Storefront popover]](storefront-popover.md)現在會顯示[特別價格](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-special) （最低最終價格）（可用時）。

### [!DNL Live Search] 1.3.0

[!BADGE 支援]{type="Informative" tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新](../assets/new.svg) [效能](performance.md)報告儀表板可提供insight以供購物者使用搜尋字詞。
![新](../assets/new.svg) [!DNL Live Search] [店面事件SDK](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/)提供對一般資料層的存取權，其中包含事件發佈和訂閱服務以及量度。
![修正](../assets/fix.svg) [[!DNL Storefront popover]](storefront-popover.md)具有控制可見性的`.search-autocomplete`容器的新`active`類別。
![修正](../assets/fix.svg)在店面中，[搜尋詞](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-terms)頁尾連結已移除，且已針對[!DNL Live Search]個安裝停用其快取。
搜尋配接器的![錯誤](../assets/bug.svg)修補程式會處理重複的產品。
![錯誤](../assets/bug.svg) [!DNL Live Search]支援[單一來源](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/sources/sources-manage) （實體）清查位置，其中包含多個（虛擬） [庫存](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/stocks/stocks-manage)。 目前不支援多個清查來源。

### [!DNL Live Search] 1.2.0

[!BADGE 支援]{type="Informative" tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新](../assets/new.svg) [[!DNL Storefront popover]](storefront-popover.md)在購物者將查詢輸入搜尋方塊時，顯示建議的產品和最上層搜尋結果的縮圖影像。
![新](../assets/new.svg) Commerce *管理員*工作階段在鍵盤長時間不活動期間保持開啟
![新](../assets/new.svg) [!DNL Live Search]在上線後自動啟用
![修正](../assets/fix.svg)初始索引時間不到一小時
![修正](../assets/fix.svg)近乎即時的增量產品更新（安裝及設定後）
同義字編輯器中的![修正](../assets/fix.svg)可排序的欄
如果搜尋條件包含空白的排序順序值，![修正](../assets/fix.svg) [!DNL Live Search]不再擲回錯誤
如果屬性程式碼包含字串「to」或「from」，則![修正](../assets/fix.svg)範圍篩選不再中斷

### [!DNL Live Search] 1.1.0

[!BADGE 支援]{type="Informative" tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![錯誤](../assets/bug.svg) [!DNL Live Search]服務只支援Adobe Commerce安裝的[基本貨幣](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration)。
![錯誤](../assets/bug.svg)新增Facet時，產品屬性摘要設定為`Update on Save`時未正確更新。 若要避免此問題，請移至[索引管理](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management)，並將產品屬性摘要設定為`Update by Schedule`。
![錯誤](../assets/bug.svg) [!DNL Live Search]同義字是依商店檢視定義，但目前是依網站儲存，並以`environmentId`與`storeViewCode`的組合識別。 因此，Adobe Commerce安裝中的所有網站和商店檢視會共用同義字。 存放區檢視最近建立的同義字集優先。
![錯誤](../assets/bug.svg)如果同義字詞包含多個字詞，每個字詞都會被視為個別的同義字。 例如，如果您將「time piece」定義為「watch」的同義字，則「time」和「piece」都會被視為監視的同義字。

+++

## 檔案

若要深入瞭解：

- [Adobe Commerce開發人員檔案](https://developer.adobe.com/commerce/docs)
- [Adobe Commerce使用手冊](https://experienceleague.adobe.com/en/docs/commerce)
- Marketplace[&#128279;](https://commercemarketplace.adobe.com/magento-live-search.html)上的[!DNL Live Search] 
