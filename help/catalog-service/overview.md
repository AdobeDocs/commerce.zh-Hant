---
title: '[!DNL Catalog Service]'
description: 透過 [!DNL Catalog Service] 加速Adobe Commerce店面 — 高效能的GraphQL API減少產品頁面、類別頁面和搜尋結果的頁面載入時間。
role: Admin, Developer
recommendations: noCatalog
exl-id: 525e3ff0-efa6-48c7-9111-d0b00f42957a
source-git-commit: e582bff6ee8ee7c4213f04bdab984efa94333fb6
workflow-type: tm+mt
source-wordcount: '1323'
ht-degree: 0%

---

# 適用於Adobe Commerce的[!DNL Catalog Service]

Adobe Commerce擴充功能的[!DNL Catalog Service]透過專用的GraphQL API提供最佳化的唯讀目錄資料，以改善店面載入時間。 此服務是專為增強產品相關頁面體驗所設計，可加快頁面載入速度並改善轉換率。

[!DNL Catalog Service]提供的豐富檢視模型資料包括產品詳細資料、屬性、存貨和價格，可快速呈現與產品相關的店面體驗，例如：

- 產品詳細資料頁面
- 產品清單和類別頁面
- 搜尋結果頁面
- 產品輪播
- 產品比較頁面
- 轉譯產品資料的任何其他頁面，例如購物車、訂單和願望清單頁面


## 主要優點和功能

- **頁面載入速度更快**：最佳化的查詢，與核心GraphQL系統相比，目錄資料擷取速度加快10倍
- **轉換率改善**：載入時間越快，使用者體驗越好
- **簡化的產品型別**：以簡單而複雜的產品型別為基礎的統一結構描述，可降低開發人員的複雜性
- **進階價格精確度**：支援16位數的值和4位小數
- **分離式架構**：目錄資料的獨立GraphQL系統可確保高效能，而不會影響Commerce的核心作業
- **即時資料同步**：目錄服務會透過SaaS Data Export擴充功能與Adobe Commerce應用程式保持同步，確保查詢會傳回最新的目錄資料
- **資料管理儀表板**：從Adobe Commerce管理介面監視和管理資料同步作業
- **API Mesh整合**：可選擇與Adobe Developer App Builder的[API Mesh整合](https://developer.adobe.com/graphql-mesh-gateway/)，以結合Adobe Commerce GraphQL系統與其他內部和第三方API，以擴充目錄服務GraphQL結構描述並新增自訂資料或功能


## 架構概覽

[!DNL Catalog Service]使用[GraphQL](https://graphql.org/)來要求及接收目錄資料，包括產品、產品屬性、存貨及價格。 GraphQL是一種查詢語言，前端使用者端使用它來與後端(例如Adobe Commerce)上定義的應用程式設計介面(API)通訊。 GraphQL是一種常用的通訊方法，因為它很輕量，可讓系統整合商指定每個回應的內容和順序。

Adobe Commerce提供兩種GraphQL系統，其用途不同：

### 核心GraphQL系統

- **用途**：適用於所有Commerce作業的完整功能API
- **功能**：產品、客戶、購物車、結帳等的查詢（讀取）和變動（寫入）
- **限制**：產品查詢未針對速度最佳化
- **使用案例**：一般Commerce作業和寫入作業

### 目錄服務GraphQL系統

- **用途**：僅限高效能產品目錄查詢
- **功能**：產品、屬性、詳細目錄和價格的唯讀查詢
- **優勢**：產品資料比核心系統快很多
- **使用案例**：速度至關重要的店面產品體驗

「目錄服務」可用的資料由SaaS Data Export擴充功能提供。 此擴充功能會同步Commerce應用程式與連線的Commerce服務之間的資料，以確保對GraphQL API端點的服務查詢會傳回最新的目錄資料。 如需有關管理和疑難排解SaaS資料匯出作業的資訊，請參閱[SaaS資料匯出指南](../data-export/overview.md)。

[!DNL Catalog Service]客戶可以使用[SaaS價格索引器](../price-index/price-indexing.md)，提供更快的價格更新和同步處理時間。

## 架構詳細資料

下圖說明核心GraphQL系統與目錄服務GraphQL系統之間的架構差異，說明兩者如何共同運作以最佳化店面效能：

![目錄架構圖](assets/catalog-service-architecture.png)

### 系統運作方式

**核心GraphQL系統（傳統方法）：**
漸進式網頁應用程式(PWA)會直接將要求傳送至Commerce應用程式，而應用程式會在傳回回應前，透過多個子系統處理每個要求。 此多步驟來回行程可能會導致頁面載入時間緩慢，進而降低轉換率。

**目錄服務（最佳化方法）：**
目錄服務可做為存取專屬最佳化資料庫的Storefront Services閘道，其中包含產品詳細資訊、屬性、變體、價格和類別。 此服務會透過自動化索引來維持與Adobe Commerce的同步，略過傳統的請求 — 回應週期，以大幅減少延遲。

GraphQL系統的核心和服務不會直接互相通訊。 您從不同的URL存取每個系統，而呼叫需要不同的標題資訊。 這兩個GraphQL系統旨在搭配使用。 [!DNL Catalog Service] GraphQL系統可增強核心系統，讓產品店面體驗更快速。

您可以選擇實作Adobe Developer App Builder[的](https://developer.adobe.com/graphql-mesh-gateway/)API Mesh，以使用Adobe Developer將兩個Adobe Commerce GraphQL系統與私人和協力廠商API及其他軟體介面整合。 您可以設定網格，以確保路由到每個端點的呼叫在標題中包含正確的授權資訊。

## 架構詳細資料

以下章節說明這兩個GraphQL系統之間的一些差異。

### 綱要管理

由於目錄服務是以服務的形式運作，整合經銷商不需擔心基礎版本的Commerce。 所有版本的查詢語法都相同。 此外，結構對所有商家都是一致的。 這種一致性可讓您更輕鬆地建立最佳實務，並大幅增加店面Widget的重複使用率。

### 簡化產品型別

結構描述將產品型別的多樣性減少為兩個使用案例：

- **簡單產品** — 目錄服務將Adobe Commerce簡單、虛擬、可下載和禮品卡產品型別對應至`simpleProductViews`。 此型別具有：
   - 單一、固定的價格和數量
   - 一般價格（折扣前）與最終價格（折扣後）
   - 支援產品屬性，例如顏色、大小和其他特性

- **複雜產品** — 目錄服務將Adobe Commerce可設定、套件組合和群組產品型別對應至`complexProductViews`。 複雜的產品是多個簡單產品的集合，可以設定或捆綁在一起。
   - 每個元件簡單產品可以有自己的價格。
   - 購物者可以指定個別元件產品的數量。
   - 產品選項（例如大小、顏色、材質）統一且運作方式相同，無論產品型別為何。 每個選項選項選項都指向特定的簡單產品，並具有其自己的屬性和價格。 最終產品會保持未定義狀態，直到購物者選取所有必要選項為止。

#### 產品檢視屬性

簡單和複雜的產品都有客戶定義的屬性，可顯示在店面上。 這些屬性會傳回為[ProductViewAttributes](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#productviewattribute-type)。 在Adobe Commerce中，可用的屬性會在建立產品時定義。 您可以從Adobe Commerce後端或以程式設計方式新增其他屬性。 請參閱[延伸與自訂SaaS資料匯出摘要資料](../data-export/extensibility-and-customizations.md)。

>[!TIP]
>
>您可以將[API Mesh與目錄服務](mesh.md)搭配使用，擴充目錄服務GraphQL結構描述，以新增資料或設定現有的目錄資料，以啟用新功能，而不將資料型別新增到Commerce後端。

### 價格

簡單產品代表有價格的基本銷售單位。 [!DNL Catalog Service]計算折扣前的一般價格以及折扣後的最終價格。 定價計算可包含固定產品稅捐。 他們會排除個人化促銷活動。

複雜的產品沒有設定價格。 相反地，目錄服務會傳回連結的簡單專案的價格。 例如，商家一開始可以為可設定產品的所有變體指定相同的價格。 如果某些尺寸或顏色不受歡迎，商家可以降低這些系列產品的價格。 因此，複雜（可設定）產品的價格一開始會顯示價格範圍，反映標準及不受歡迎的變體的價格。 購物者為所有可用選項選取值後，店面會顯示單一價格。

目錄服務支援大值（最多16位數）和高小數精確度（最多4位小數）的價格，確保價格更新與計算準確無誤。

>[!NOTE]
>
> 擁有[!DNL Catalog Service]的Commerce客戶可透過[SaaS價格索引器](../price-index/price-indexing.md)，利用其網站上更快速的價格變更更新和同步處理時間。

## 實施

實作程式涉及：

1. 僅[!BADGE PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案(Adobe管理的PaaS基礎結構)和內部部署專案的Adobe Commerce 。"} **[安裝並設定目錄服務](installation.md)** — 安裝並設定目錄服務延伸功能，並使用[!DNL Commerce Services Connector]設定SaaS連線。
2. **更新店面程式碼**：將目錄服務GraphQL查詢整合至您的店面。
3. **路由查詢**：所有目錄服務查詢都會透過GraphQL閘道（上線期間提供的URL）
4. **監視和疑難排解資料同步處理**：驗證已改善的效能並監視結果


