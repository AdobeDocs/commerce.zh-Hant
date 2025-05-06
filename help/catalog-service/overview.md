---
title: '[!DNL Catalog Service]'
description: 適用於Adobe Commerce的[!DNL Catalog Service]提供一種比原生Adobe Commerce GraphQL查詢更快擷取產品顯示頁面和產品清單頁面內容的方法。
role: Admin, Developer
recommendations: noCatalog
exl-id: 525e3ff0-efa6-48c7-9111-d0b00f42957a
source-git-commit: be1c739f3821a5f1e846b3026088e3a3ff45a60f
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 0%

---

# 適用於Adobe Commerce的[!DNL Catalog Service]

Adobe Commerce擴充功能的[!DNL Catalog Service]提供豐富檢視模型（唯讀）目錄資料，以便快速完整地呈現與產品相關的店面體驗，包括：

* 產品詳細資料頁面
* 產品清單和類別頁面
* 搜尋結果頁面
* 產品輪播
* 產品比較頁面
* 轉譯產品資料的任何其他頁面，例如購物車、訂單和願望清單頁面

[!DNL Catalog Service]使用[GraphQL](https://graphql.org/)來要求及接收目錄資料，包括產品、產品屬性、存貨及價格。 GraphQL是一種查詢語言，前端使用者端使用它來與後端(例如Adobe Commerce)上定義的應用程式設計介面(API)通訊。 GraphQL是一種常用的通訊方法，因為它很輕量，可讓系統整合商指定每個回應的內容和順序。

Adobe Commerce擁有兩個GraphQL系統。 核心GraphQL系統提供廣泛的查詢（讀取操作）和變動（寫入操作），讓購物者可以與多種型別的頁面互動，包括產品、客戶帳戶、購物車、結帳等。 但是，傳回產品資訊的查詢沒有針對速度進行最佳化。 GraphQL系統只能對產品和相關資訊執行查詢。 這些查詢比類似的核心查詢效能更高。

「目錄服務」可用的資料由SaaS Data Export擴充功能提供。 此擴充功能會同步Commerce應用程式與連線的Commerce服務之間的資料，以確保對GraphQL API端點的服務查詢會傳回最新的目錄資料。 如需有關管理和疑難排解SaaS資料匯出作業的資訊，請參閱[SaaS資料匯出指南](../data-export/overview.md)。

[!DNL Catalog Service]客戶可以使用[SaaS價格索引器](../price-index/price-indexing.md)，提供更快的價格更新和同步處理時間。

## 架構

下圖顯示兩個GraphQL系統：

![目錄架構圖](assets/catalog-service-architecture.png)

在核心GraphQL系統中，PWA會傳送要求至Commerce應用程式，而應用程式會接收每個要求、處理要求（可能透過多個子系統傳送要求），然後傳回回應至店面。 此往返可能會導致頁面載入時間緩慢，進而降低轉換率。

[!DNL Catalog Service]是店面服務閘道。 此服務會存取個別的資料庫，其中包含產品詳細資料和相關資訊，例如產品屬性、系列品種、價格和類別。 此服務會透過索引來保持資料庫與Adobe Commerce同步。
由於服務會略過與應用程式的直接通訊，因此能夠減少要求的延遲和回應週期。

GraphQL系統的核心和服務不會直接互相通訊。 您從不同的URL存取每個系統，而呼叫需要不同的標題資訊。 這兩個GraphQL系統旨在搭配使用。 [!DNL Catalog Service] GraphQL系統可增強核心系統，讓產品店面體驗更快速。

您可以選擇實作Adobe Developer App Builder[&#128279;](https://developer.adobe.com/graphql-mesh-gateway/)的API Mesh，以使用Adobe Developer將兩個Adobe Commerce GraphQL系統與私人和協力廠商API及其他軟體介面整合。 您可以設定網格，以確保路由到每個端點的呼叫在標題中包含正確的授權資訊。

## 架構詳細資料

以下章節說明這兩個GraphQL系統之間的一些差異。

### 綱要管理

由於目錄服務是以服務的形式運作，整合經銷商不需擔心基礎版本的Commerce。 所有版本的查詢語法都相同。 此外，結構對所有商家都是一致的。 這種一致性可讓您更輕鬆地建立最佳實務，並大幅增加店面Widget的重複使用率。

### 簡化產品型別

結構描述將產品型別的多樣性減少為兩個使用案例：

* 簡單產品是指以單一價格和數量定義的產品。 目錄服務將簡單、虛擬、可下載和禮品卡產品型別對應至`simpleProductViews`。

* 複雜的產品是由多個簡單的產品所組成。 元件簡單產品可以有不同的價格。 也可以定義複雜產品，讓購物者可以指定元件簡單產品的數量。 目錄服務將可設定、套件組合和群組產品型別對應至`complexProductViews`。

複雜的產品選項會根據其行為而非型別進行統一和區分。 每個選項值代表簡單產品。 此選項值可存取簡單產品屬性，包括價格。 當購物者選取複雜產品的所有選項時，所選選項的組合會指向特定的簡單產品。 在購物者為所有可用選項選取值之前，簡單產品會保持模稜兩可。

#### 產品檢視屬性

簡單和複雜的產品都有客戶定義的屬性，可顯示在店面上。 這些屬性會傳回為[ProductViewAttributes](https://developer.adobe.com/commerce/services/graphql/catalog-service/products/#productviewattribute-type)。 在Adobe Commerce中，可用的屬性會在建立產品時定義。 您可以從Adobe Commerce後端或以程式設計方式新增其他屬性。 請參閱[延伸與自訂SaaS資料匯出摘要資料](../data-export/extensibility-and-customizations.md)。

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

僅[!BADGE 個PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案(Adobe管理的PaaS基礎結構)和內部部署專案的Adobe Commerce 。"}

安裝程式需要[Commerce Services Connector](../landing/saas.md)的設定。 完成此操作後，系統整合員下一步將更新店面程式碼以合併[!DNL Catalog Service]查詢。 所有[!DNL Catalog Service]查詢都會路由至GraphQL閘道。 URL會在上線流程中提供。
