---
title: '[!DNL Catalog Service]發行說明'
description: 適用於Adobe Commerce的 [!DNL Catalog Service] 的最新發行資訊。
feature: Services, Catalog Service, Release Notes
exl-id: 74f2e46a-5592-4857-a6d7-b95b85d8b4cc
source-git-commit: 93adab667d1d8ed40c9d5668db376493bd8ae684
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 0%

---

# [!DNL Catalog Service]發行說明

以下版本說明說明[!DNL Catalog Service]的最新版本。
支援目前的主要發行版本。 舊版的發行說明僅供參考。
更新包括：

![新](../assets/new.svg)新功能
![修正](../assets/fix.svg)修正和改良
![錯誤](../assets/bug.svg)已知問題

## 目前的主要版本

### V1.26版本

_2024年10月22日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg) GraphQL結構描述現在在產品資訊中包含`lastModifiedAt`屬性。 此精確的時間戳記可協助客戶確保Sitemap準確反映其產品的最新更新。 此外，它還有助於Google等搜尋引擎判斷何時需要重新索引、最佳化編目流程，以及在無法取得精確資訊時，防止與使用的積極上次修改日期相關的問題。<!--DATA-6209-->

## 舊版

+++ 舊版

### V1.23版本

_2024年8月22日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![修正](../assets/fix.svg)您現在可以擷取產品資訊，而不需要產品覆寫（價格）資料。 在舊版中，這些查詢傳回下列錯誤：
`The following sku does not have product override data in the DB: <SKU value>. Make sure data is synced.` <!--DATA-6121-->

### V1.22版本

_2024年8月13日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![New](../assets/new.svg)已新增支援，以依據產品SKU擷取所有變體。 檢視[目錄服務API參考](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)。<!--DATA-6067-->

### V1.22版本

_2024年8月13日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![New](../assets/new.svg)已新增支援，以依據產品SKU擷取所有變體。 檢視[目錄服務API參考](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)。<!--DATA-6067-->

### V1.19版本

_2024年5月23日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本


![修正](../assets/fix.svg) <!--DATA-5033-->選項值的`InStock`旗標現在會考量產品變體的領域`enabled`狀態。

![修正](../assets/fix.svg) <!--DATA-5888-->新增支援需要大數字（最多16位數）和更高小數位數（最多4位小數）的產品價格。 若要將價格設定更新套用至您現有的目錄，請從[資料管理儀表板](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)重新同步目錄資料，或使用[Adobe Commerce命令列介面](../landing/catalog-sync.md#command-line-interface)。

#### 已知限制

尚未支援下列功能：

* 動態屬性承載的大小上限為9 MB。
* 本集團產品價格可用簡單產品價格計算。
* 在影像陣列中，只有第一個影像包含角色。

使用API Mesh和核心GraphQL API解決下列限制：

* 最低廣告價格
* 層級定價
* 捆綁固定價格的產品

如需詳細資訊和範例，請參閱[目錄服務和API Mesh](mesh.md)

### V1.18版本

_2024年4月11日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)已新增對PHP 8.3的支援。

![新的](../assets/new.svg) [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/)與[`refineProduct`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/)查詢現在會傳回簡單與複雜產品的可自訂選項資料。<!--DATA-5538-->

### V1.17版本

_2024年2月22日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新增](../assets/new.svg) [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html)現已可用。 此改版後的儀表板提供[!DNL Product Recommendations]、[!DNL Live Search]和[!DNL Catalog Service]的資料串流的深入分析。 `catalog-service`中繼套件3.1.0版已引進對此功能的支援。

### V1.16版本

_2024年2月13日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

目錄服務API現在支援![新](../assets/new.svg)產品影片。
![Fix](../assets/fix.svg)無存貨的選項現在顯示在PDP Widget中。

#### 已知限制

尚未支援這些功能：

* 動態屬性承載的大小上限為9 MB。
* 群組產品價格。 此值可使用簡單產品價格計算。
* 在影像陣列中，只有第一個影像包含角色。

下列限制可使用API Mesh和核心GraphQL API來解決：

* 最低廣告價格
* [層級定價](mesh.md)

### V1.13版本

_2023年10月12日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)目錄服務支援產品變體的`inStock`旗標。
![新](../assets/new.svg) `urlKey`和`externalId`欄位已新增至GraphQL結構描述。
現在支援![新](../assets/new.svg)可下載的產品和禮品卡。

### V1.12版本

_2023年9月19日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)目錄服務現在使用[SaaS價格索引](../price-index/price-indexing.md)。
![修正](../assets/fix.svg)此版本包含服務端的錯誤修正和改善。

### V1.11版本

_2023年7月18日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)目錄服務現在支援產品推薦的[`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) GraphQL查詢。

### V1.10版本

_2023年6月27日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)目錄服務API現在支援`related products`。

### V1.7版本

_2023年4月12日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)目錄服務現在會清除已刪除的產品變體。
![修正](../assets/fix.svg)基礎架構擴充性與效能的改善。

### V1.6版本

_2023年3月28日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)已新增色票至[`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/)查詢。
![新](../assets/new.svg)已新增使用`entityId`API Mesh[取得](mesh.md)的功能。

### V1.5版本

_2023年3月6日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)已新增[`categories`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) GraphQL功能。
![修正](../assets/fix.svg)已改善效能和API擴充性。

### V1.4版本

_2023年2月7日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新增](../assets/new.svg)已發佈的目錄服務中繼資料以簡化安裝步驟。
![修正](../assets/fix.svg) API擴充性和效能改善。

### V1.3版本

_2023年1月17日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新](../assets/new.svg)簡化並改善入門體驗。
![新的](../assets/new.svg)新客戶沙箱端點可用於生產前測試。
已新增虛擬產品的![新](../assets/new.svg)支援。
![修正](../assets/fix.svg) API擴充性和效能改善。

### V1.1版本

_2022年11月18日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新](../assets/new.svg)目錄服務現在支援Adobe的[API Mesh](https://developer.adobe.com/graphql-mesh-gateway/)。
![修正](../assets/fix.svg)已改善API擴充性和整體效能。

### V1.0版本

_2022年10月4日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新](../assets/new.svg)現在支援套件和分組的產品。
![新](../assets/new.svg)已新增B2B可見性覆寫。 產品現在可供搜尋，並可新增至特定客戶群組的購物車。
![Fix](../assets/fix.svg)服務現在更穩定且效能更佳。

### 0.3版 — Beta+

_2022年9月12日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新](../assets/new.svg)支援變體的影像：根據選取的選項傳回產品影像
![新的](../assets/new.svg)價格支援角色：僅允許特定客戶群組的成員檢視產品價格
![修正](../assets/fix.svg)已改善服務的穩定性和效能
從目錄中刪除產品時收到![新的](../assets/new.svg)更新

### Beta版本

_2022年8月9日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新](../assets/new.svg) `products`和`refineProduct`查詢傳回下列資料：

* 預先定義的（系統）產品屬性。
* 動態產品屬性，並依角色（產品顯示頁面/產品清單頁面）篩選。
* 產品選項。
* 產品影像並依角色(PDP/PLP)篩選。
* 簡單產品的特定價格，以及可設定產品的價格範圍。
* 客戶群組價格和價格範圍。 這類優惠會針對沒有客戶群組的購物者傳回遞補預設價格。
* 使用B2B客戶特定定價的產品型別。
