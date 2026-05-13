---
title: '[!DNL Commerce Storefront Catalog Service Release Notes]'
description: 適用於Adobe Commerce的 [!DNL Catalog Service] 的最新發行資訊。
feature: Services, Catalog Service, Release Notes
exl-id: 74f2e46a-5592-4857-a6d7-b95b85d8b4cc
TQID: https://experienceleague.adobe.com/-yxW4sTuk7LPjGy5YsQ65phtkBLiByg8SmBaQPHMevM
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: e1e0219c-f879-479f-8427-888ed2a6e9c2id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 22f44afb7221c735785b6e9a38fb70c733cf0942
workflow-type: tm+mt
source-wordcount: 2742
ht-degree: 0%

---

# [!DNL Commerce Storefront Catalog Service]發行說明

下列發行說明涵蓋最新的Commerce Catalog Service更新，包括：

- **[店面目錄服務發行版本](#storefront-catalog-service)**

   - 目錄服務API結構描述增強功能可改善資料擷取
   - 目錄服務API和基礎基礎結構的安全性、效能和可靠性改善。

  如需這些API的詳細資訊，請參閱Commerce開發人員檔案中的[Storefront Services結構描述](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)。

- **[目錄服務中繼套件發行版本](#catalog-service-metapackage)**

   - 更新相依性，以提升效能、穩定性以及與其他Adobe Commerce元件的相容性。

- **[目錄服務安裝程式版本](#catalog-service-installer)**

   - 更新相依性，以維護目錄服務與Commerce棧疊之間的相容性。

>[!NOTE]
>
>如果您的Commerce專案使用Adobe Commerce Optimizer將目錄資料傳送至Commerce Edge Delivery Service或Headless店面，請參閱[Adobe Commerce Optimizer發行說明](../optimizer/release-notes.md)以瞭解最新的API更新。

更新會依型別分類：

![新](../assets/new.svg)新功能
![修正](../assets/fix.svg)修正和改良
![錯誤](../assets/bug.svg)已知問題

支援最新版本。 隨附舊版發行說明以供參考。

## 店面目錄服務

### 2026年5月

**發行日期**： 2026年5月13日
<!--v1.54-->

![新的](../assets/new.svg) **GraphQL中的類別排序順序** — 現在`CategoryView` GraphQL型別包含位置欄位，所以店面可以顯示目錄階層中商戶設定的順序類別。
<!--DATA-7166-->

**發行日期**：2026年5月4日
<!-- v1.53 -->

![Fix](../assets/fix.svg)店面產品價格現在會顯示所有產品型別的正確貨幣代碼（例如USD）。 之前，部分產品顯示`NONE`而非預期的貨幣，導致價格遺失。 此更新可確保跨店面一致且精確的價格呈現。<!--DATA-7115-->

### 2026年4月

**發行日期**： 2026年4月29日
<!--v1.52-->

![新](../assets/new.svg)Adobe Commerce Optimizer和Adobe Commerce as a Cloud Service的每個請求強制限制，最多100個SKU
根據[記錄的限制和邊界](https://experienceleague.adobe.com/en/docs/commerce/optimizer/boundaries-limits)的使用者端。<!--DATA-7156-->

**發行日期**： 2026年4月17日
<!--v1.51-->

![新](../assets/new.svg)已新增新的`searchCategory` GraphQL查詢，讓使用者端能依名稱搜尋具有分頁結果的類別。 查詢接受必要的`searchTerm` （至少3個字元）以及選用的`family`、`pageSize`和`currentPage`引數。 結果包含比對具有完整類別中繼資料的`CategoryTreeView`物件、`totalCount`以及分頁的`pageInfo`。<!--COMOPT-1819-->

此查詢僅適用於使用Adobe Commerce Optimizer銷售服務的客戶。 請參閱[searchCategory](https://developer.adobe.com/commerce/services/reference/graphql/)。

### 2026年3月

**發行日期**： 2026年3月24日
<!--v1.49-->

![新增](../assets/new.svg)新增支援，可計算並傳回動態套裝的價格範圍。
<!--DATA-7115-->

### 2025年12

**發行日期**：2025年12月11日
<!-- v1.46 -->

![修正](../assets/fix.svg)系統層級和基礎建設的改善，以強化效能和穩定性。
<!--DATA-6852, DATA-6864-->

### 2025年11月

**發行日期**： 2025年11月17日
<!-- v1.45 -->

![新的](../assets/new.svg) **依名稱篩選屬性**- `productSearch` GraphQL查詢現在支援使用`names`欄位篩選產品屬性。<!--DATA-6831--> 使用此篩選器，您可以：

- 僅要求特定屬性，以減少回應裝載大小
- 與現有的`roles`篩選器結合，以依據可見性角色和屬性名稱來縮小
- 範例：

  **僅依屬性名稱篩選**

  ```graphql
  query {
    products(skus: ["SKU-001"]) {
      attributes(names: ["color", "size", "material"]) {
        name
        label
        value
      }
    }
  }
  ```

  **同時依角色和名稱篩選：**

  ```graphql
  query {
    products(skus: ["SKU-001"]) {
      attributes(roles: ["visible in PDP"], names: ["eco_collection", "new"]) {
        name
        label
        value
        roles
      }
    }
  }
  ```

>[!NOTE]
>
>若要擷取所有屬性而不進行篩選，請省略`names`引數或提供空陣列。

**發行日期**：2025年11月6日
<!-- v1.44 -->

![修正](../assets/fix.svg)系統層級和基礎建設的改善，以強化效能和穩定性。<!--DATA-6852, DATA-6864-->

![修正](../assets/fix.svg)當父項沒有訂價時，現在可以查詢已分組的產品；子項產品會傳回自己的可見性角色。<!--DATA-6779-->

![修正](../assets/fix.svg)系統層級和基礎建設的改善，以強化效能和穩定性。<!--DATA-6721, DATA-6864-->

### 2025年9月

**發行日期**：2025年9月8日
<!-- v1.42 -->

![新](../assets/new.svg) **已新增層級定價支援**&#x200B;以查詢磁碟區定價：<!--DATA-6643-->

若要擷取階層訂價，請執行下列步驟：

1. 搭配您想要的SKU使用`products`查詢
2. 針對&#x200B;**SimpleProductView**，存取`price.tiers`
3. 針對&#x200B;**ComplexProductView**，存取`priceRange.minimum.tiers`和`priceRange.maximum.tiers`
4. 每個層級都包含折扣的`tier`價格和`quantity`條件
5. 使用`gte` （大於或等於）和`lt` （小於）定義數量臨界值

**範例：**

```graphql
query {
  products(skus: ["SKU-001"]) {
    ... on SimpleProductView {
      price {
        regular { amount { value currency } }
        tiers {
          tier { amount { value currency } }
          quantity {
            ... on ProductViewTierRangeCondition { gte lt }
          }
        }
      }
    }
  }
}
```

![修正](../assets/fix.svg) **依最低最終價格篩選的層級價格** <!--DATA-6643-->

此API現在只會傳回折扣價格比產品最低最終價格&#x200B;**低**&#x200B;的階層。 省略較高層級，因為店面將改為適用最低最終價格。

套用至：

- **簡單產品**： `price.tiers`僅包含具有`tier.amount.value` &lt; `price.final.amount.value` （最小最終值）的層級。
- **複雜產品**： `priceRange.minimum.tiers`和`priceRange.maximum.tiers`在建立價格範圍時使用相同的規則。

**發行日期**： 2025年9月2日
<!-- v1.41 -->

![修正](../assets/fix.svg) **已改善遺失價格資訊的錯誤處理** — 尚未收到價格資料時，API會傳回價格欄位的`null`，而非擲回錯誤，讓使用者端能夠妥善處理遺失的資料。<!--DATA-6612-->

![修正](../assets/fix.svg)系統層級和基礎建設的改善，以強化效能和穩定性。<!--DATA-6671-->

### 2025年7月

**發行日期**： 2025年7月30日
<!-- v1.40 -->

![修正](../assets/fix.svg)系統層級和基礎建設改善專案，以強化安全性、效能和穩定性。<!--DATA-6619-->

**發行日期**： 2025年7月24日
<!-- v1.39 -->

![新的](../assets/new.svg) **依單位ID擷取建議單位** — 新的GraphQL端點`recommendationsByUnitIds`會依其唯一的ID擷取建議單位，以獲得更靈活、目標明確的存取。

- 需要`unitIds` （要擷取的recId清單）。
- 內容引數(`currentSku`， `cartSkus`， `userViewHistory`， `userPurchaseHistory`， `category`)的行為與現有建議查詢中的相同。

- **範例**

  ```graphql
  query {
    recommendationsByUnitIds(
      unitIds: ["11ee89d1-bfae-4582-a921-2ced44ff6bf7"]
      currentSku: "24-MB01"
      cartSkus: ["24-MB01"]
    ) {
      totalResults
      results {
        unitId
        unitName
        totalProducts
        productsView {
          sku
        }
        pageType
        typeId
        storefrontLabel
        displayOrder
      }
    }
  }
  ```

![修正](../assets/fix.svg)系統層級和基礎建設改善專案，以強化安全性、效能和穩定性。<!--DATA-6316-->

**發行日期**： 2025年7月15日
<!-- v1.38 -->

![新的](../assets/new.svg) **禮卡產品型別** — 目錄店面服務現在支援產品屬性為JSON物件或陣列，可彈性管理複雜型別，例如禮卡。<!--DATA-6573-->

+++舊版

### 2025年6月

**發行日期**： 2025年6月20日
<!-- v1.37 -->

![新的](../assets/new.svg) **階層式價格簿組態** — 上下階價格簿的精確價格範圍。 計算會遵循階層與繼承的規則；當連結多重價格簿時，可減少訂價錯誤。 僅限Adobe Commerce Optimizer。 檢視[價格手冊](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/pricebooks)。

![新](../assets/new.svg) **不區分大小寫的索引鍵** — 查詢中的索引鍵查閱現在不區分大小寫，可減少因索引鍵大小寫造成的錯誤。<!--DATA-6494, DCAT-2495-->

**發行日期**： 2025年6月20日
<!-- v1.36 -->

![新](../assets/new.svg) **目錄店面的公用IO事件** — 已新增公用IO事件，以便即時整合和可觀察性（CSS和EDS）。<!--DATA-6329-->

![新的](../assets/new.svg) **伺服器端轉譯(SSR)** — 支援SSR的架構改進，可在大型目錄上提供更優異的效能、SEO和UX。<!--DATA-6278, DATA-6280-->

![新](../assets/new.svg) **基礎架構和安全性** — 事件服務的新AWS角色、ServiceNow整合和CI/CD管道。

![新](../assets/new.svg) **事件格式和可觀察性** — 簡化裝載、增強監控、改善變體事件資料。<!--DATA-6332, DATA-6402, -->

![修正](../assets/fix.svg)系統層級和基礎建設改善專案，以強化安全性、效能和穩定性。<!--DATA-6404, DATA-6410, -->

**發行日期**： 2025年6月13日
<!-- v1.35 -->

![新的](../assets/new.svg) **擷取未快取的資料** — 啟用`Magento-Is-Preview`標頭以將未快取的資料從目錄端點傳遞至搜尋服務。<!--DATA-6345-->

![新的](../assets/new.svg) **多重選取產品選項**-GraphQL API現在會公開產品選項是否允許多重選取（例如，套件組合「選擇多個專案」）。<!--DATA-6487-->

![新的](../assets/new.svg)資料擷取已更新價格驗證，以支援沒有價格的產品。<!--DATA-6098-->

![修正](../assets/fix.svg)已改善Adobe Commerce Optimizer中簡單套件定價的錯誤處理。<!--DATA-6541-->

![修正](../assets/fix.svg)系統層級和基礎建設改善專案，以強化安全性、效能和穩定性。<!--DATA-6273, DATA-6485, -->

### 2025年4月

**發行日期**： 2025年4月8日
<!-- v1.34 -->

![修正](../assets/fix.svg)系統層級和基礎建設改善專案，以強化安全性、效能和穩定性。<!--DATA-5732-->

<!-- v1.33 -->
![Fix](../assets/fix.svg)基礎架構現在支援超大型目錄（最多約4.4億SKU），不會影響現有的工作負載。

### 2025年3月

**發行日期**： 2025年3月28日
<!-- v1.32 -->

![修正](../assets/fix.svg)沒有角色的屬性預設不再為可撰寫的目錄編制索引，因此可縮短編制索引的時間並減少儲存空間。 舊版行為可透過功能標幟重新啟用。

![修正](../assets/fix.svg)系統層級和基礎建設改善，以強化安全性、效能和穩定性。
<!--DATA-6348, DATA-6440, DATA-6446, DATA-6641-->

### 2025年2月

**發行日期**： 2025年2月18日
<!-- v1.31 -->

![修正](../assets/fix.svg)系統層級和基礎建設改善專案，以強化安全性、效能和穩定性。<!--DATA-6389, DATA-6367, DATA-6373-->

### 2024年12

**發行日期**： 2024年12月9日
<!-- v1.30 -->

主要版本： Headless店面、標題管理和產品資料處理的[可撰寫目錄資料模型](https://developer.adobe.com/commerce/services/optimizer/)。

![新的](../assets/new.svg) **可撰寫的目錄資料模型(CCDM)** — 支援客戶將Composable目錄用於Headless店面。 新端點接受目錄檢視和原則ID （向後相容）。 可設定的產品詳細資料和價格（內建分頁）。<!--DATA-6018, DATA-6288-->

針對可撰寫的目錄API作業，![New](../assets/new.svg) **標題管理**-`AC-Locale`已重新命名為`AC-Scope-Locale`；已指定標題對應和預設值。<!--DATA-6303, DATA-6078-->

![新的](../assets/new.svg) **產品資料與價格** — 支援可撰寫的目錄資料模型，並改善可設定產品價格處理。<!--DATA-6279-->

已更新`CurrencyEnum`以支援`NONE`產品搜尋查詢，與同盟邏輯一致。<!--DATA-6285-->

![修正](../assets/fix.svg) **基礎結構和升級** — 安全性、效能和穩定性的系統層級改善。

![修正](../assets/fix.svg)套件組合產品選項現在只會顯示啟用的產品。<!--DATA-6347-->

**發行日期**： 2024年12月9日
<!-- v1.29 -->

![新](../assets/new.svg) **產品查詢中的影像訂購**—GraphQL `images`欄位中的產品影像現在會遵循目錄匯出`sortOrder`，以取得一致的店面和API行為。<!--DATA-6258-->

![修正](../assets/fix.svg)系統層級和基礎建設改善專案，以強化安全性、效能和穩定性。<!--DATA-6619-->

**發行日期**： 2024年12月
<!-- v1.28 -->

![修正](../assets/fix.svg)系統層級和基礎建設改善，以強化安全性、效能和穩定性。
<!--DATA-6180, DATA-6230, DATA-6254, DATA-6257-->

### 2024年10

**發行日期**：2024年10月22日
<!-- v1.26 -->

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新的](../assets/new.svg) GraphQL結構描述現在在產品資訊中包含`lastModifiedAt`，以取得精確的Sitemap和搜尋引擎重新索引（例如Google）。
<!--DATA-6209-->

### 2024年9月

**發行日期**： 2024年9月26日
<!-- v1.27 -->

![修正](../assets/fix.svg)系統層級和基礎建設改善，以強化安全性、效能和穩定性。
<!--DATA-6243-->

### 2024年8月

**發行日期**： 2024年8月22日
<!-- v1.23 -->

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![修正](../assets/fix.svg)現在可以擷取產品資訊，而不需要產品覆寫（價格）資料。 以前，這些查詢會傳回： `The following sku does not have product override data in the DB: <SKU value>. Make sure data is synced.`
<!--DATA-6121-->

**發行日期**：2024年8月13日
<!-- v1.22 -->

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![New](../assets/new.svg)已新增支援，以依據產品SKU擷取所有變體。 請參閱[目錄服務API參考](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)。
<!--DATA-6067-->

### 2024年5月

**發行日期**： 2024年5月23日
<!-- v1.19 -->

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本


![修正](../assets/fix.svg)選項值的`InStock`旗標現在會遵守產品變體的領域`enabled`狀態。

<!--DATA-5033-->

![Fix](../assets/fix.svg)已新增對產品價格的支援，最多可包含16位數和4位小數。 從[資料管理儀表板](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)或[CLI](../data-export/data-export-cli-commands.md)重新同步以套用更新。
<!--DATA-5033-->

#### 已知限制

尚未支援下列功能：

- 動態屬性承載的大小上限為9 MB。
- 本集團產品價格可用簡單產品價格計算。
- 在影像陣列中，只有第一個影像包含角色。

將API Mesh和核心GraphQL API用於：

- 最低廣告價格
- 層級定價
- 捆綁固定價格的產品

如需詳細資訊和範例，請參閱[目錄服務和API Mesh](mesh.md)。

### 2024年4月

**發行日期**： 2024年4月11日
<!-- v1.18 -->

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)已新增對PHP 8.3的支援。

![新的](../assets/new.svg) [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/)與[`refineProduct`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/)查詢現在會傳回簡單與複雜產品的可自訂選項資料。<!--DATA-5538-->

### 2024年2月

**發行日期**： 2024年2月22日
<!-- v1.17 -->

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新增](../assets/new.svg) [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html)現在可用於資料串流（產品推薦、即時搜尋、目錄服務）。 需要`catalog-service`個中繼封裝v3.1.0+。

**發行日期**： 2024年2月13日
<!-- v1.16 -->

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

目錄服務API現在支援![新](../assets/new.svg)產品影片。
![Fix](../assets/fix.svg)無存貨的選項現在顯示在PDP Widget中。

#### 已知限制

尚未支援這些功能：

- 動態屬性承載的大小上限為9 MB。
- 群組產品價格。 此值可使用簡單產品價格計算。
- 在影像陣列中，只有第一個影像包含角色。

將API Mesh和核心GraphQL API用於：

- 最低廣告價格
- [層級定價](mesh.md)

### 2023年10

**發行日期**： 2023年10月12日
<!-- v1.13 -->

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)目錄服務支援產品變體的`inStock`旗標。
![新](../assets/new.svg) `urlKey`和`externalId`欄位已新增至GraphQL結構描述。
現在支援![新](../assets/new.svg)可下載的產品和禮品卡。

### 2023年9月

**發行日期**： 2023年9月19日
<!-- v1.12 -->

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)目錄服務現在使用[SaaS價格索引](../price-index/price-indexing.md)。
![修正](../assets/fix.svg)此版本包含服務端的錯誤修正和改善。

### 2023年7月

**發行日期**： 2023年7月18日
<!-- v1.11 -->

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)目錄服務現在支援產品推薦的[`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) GraphQL查詢。

### 2023年6月

**發行日期**： 2023年6月27日
<!-- v1.10 -->

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)目錄服務API現在支援`related products`。

### 2023年4月

**發行日期**： 2023年4月12日
<!-- v1.7 -->

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)目錄服務現在會清除已刪除的產品變體。
![修正](../assets/fix.svg)基礎架構擴充性與效能的改善。

### 2023年3月

**發行日期**： 2023年3月28日
<!-- v1.6 -->

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)已新增色票至[`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/)查詢。
![新](../assets/new.svg)已新增使用[API Mesh](mesh.md)取得`entityId`的功能。

**發行日期**： 2023年3月6日
<!-- v1.5 -->

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)已新增[`categories`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) GraphQL功能。
![修正](../assets/fix.svg)已改善效能和API擴充性。

### 2023年2月

**發行日期**： 2023年2月7日
<!-- v1.4 -->

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新增](../assets/new.svg)已發佈的目錄服務中繼資料以簡化安裝步驟。
![修正](../assets/fix.svg) API擴充性和效能改善。

### 2023年1月

**發行日期**： 2023年1月17日
<!-- v1.3 -->

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新](../assets/new.svg)簡化並改善入門體驗。
![新的](../assets/new.svg)新客戶沙箱端點可用於生產前測試。
已新增虛擬產品的![新](../assets/new.svg)支援。
![修正](../assets/fix.svg) API擴充性和效能改善。

### 2022年11月

**發行日期**： 2022年11月18日
<!-- v1.1 -->

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新](../assets/new.svg)目錄服務現在支援Adobe的[API Mesh](https://developer.adobe.com/graphql-mesh-gateway/)。
![修正](../assets/fix.svg)已改善API擴充性和整體效能。

### 2022年10

**發行日期**： 2022年10月4日
<!-- v1.0 -->

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

套件和群組產品的![新](../assets/new.svg)支援。
![新](../assets/new.svg)已新增B2B可見性覆寫。 產品現在可供搜尋，並可新增至特定客戶群組的購物車。
![Fix](../assets/fix.svg)服務現在更穩定且效能更佳。

### 2022年9月

**發行日期**： 2022年9月12日
<!-- v0.3 -->

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新](../assets/new.svg)變體影像：根據選取的選項傳回產品影像。
![新](../assets/new.svg)價格角色：只有特定客戶群組的成員才能看到產品價格。
![修正](../assets/fix.svg)已改善服務的穩定性和效能。
從目錄中刪除產品時，會收到![新的](../assets/new.svg)更新。

### 2022年8月

**發行日期**： 2022年8月9日
<!-- Beta -->

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新](../assets/new.svg) `products`和`refineProduct`查詢傳回下列資料：

- 預先定義的（系統）產品屬性。
- 動態產品屬性，並依角色（產品顯示頁面/產品清單頁面）篩選。
- 產品選項。
- 產品影像並依角色(PDP/PLP)篩選。
- 簡單產品的特定價格，以及可設定產品的價格範圍。
- 客戶群組價格和價格範圍。 這類優惠會針對沒有客戶群組的購物者傳回遞補預設價格。
- 使用B2B客戶特定定價的產品型別。

+++

## 目錄服務中繼資料

目錄服務PHP中繼套件(`magento/catalog-service`)的更新。

- 針對Adobe Commerce as a Cloud Service客戶，您的環境中已安裝最新版本。

- 針對雲端或內部部署的Adobe Commerce，Adobe建議使用撰寫器，將雲端環境中的目錄服務中繼資料升級為最新版本。

### v3.3.0版本

**發行日期**：2025年10月14日

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg) **資料服務升級**—`magento/data-services`相依性已更新為^8.0.0。 升級之前，請先驗證環境與自訂資料服務API的使用情況，以符合8.x版本。

![新](../assets/new.svg)已更新3.3.0版的版本和中繼資料。

### v3.2.0版本

**發行日期**： 2024年4月12日

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

已針對3.2.0更新![新](../assets/new.svg)版本和中繼資料。 沒有其他相依性變更。

### v3.1.0版本

**發行日期**： 2024年1月26日

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)已新增新的套件相依性：

- **類別許可權資料匯出工具** (`magento/module-category-permission-data-exporter`)，用於匯出目錄服務使用的類別許可權資料。
- **目錄同步管理員** `magento/module-catalog-sync-admin`，用於與目錄同步相關的管理員UI和設定。

![新](../assets/new.svg)已更新3.1.0版的版本和中繼資料。

## 目錄服務安裝程式

安裝程式隨目錄服務擴充功能提供，並會處理安裝和環境檢查，使目錄服務符合您的Commerce棧疊。

- 針對&#x200B;**Adobe Commerce as a Cloud Service**&#x200B;客戶，您的環境中已安裝最新安裝程式版本。

- 針對雲端基礎結構上的&#x200B;**Adobe Commerce**&#x200B;或&#x200B;**內部部署**，請讓安裝程式與[目錄服務中繼資料](#catalog-service-metapackage)保持一致。

每當您使用Composer升級`magento/catalog-service`時，安裝程式套件都會自動更新至最新版本。 在這些發行說明描述您需要的變更時（例如，支援新的PHP版本），您也可以使用Composer個別升級`magento/catalog-service-installer`。 如此一來，您的安裝工具就會與您執行的目錄服務版本相容。

### v1.0.6版本

**發行日期**： 2026年3月25日

![New](../assets/new.svg) **PHP 8.5** — 確保目錄服務在PHP 8.5上運作時的相容性。

## 相關檔案

- 對於部署在**Adobe Commerce雲端、內部部署或Adobe Commerce as a Cloud Service上的專案，請參閱下列檔案：

   - [目錄服務指南](overview.md)
   - [目錄服務GraphQL API參考](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)
   - [Adobe Commerce管理指南](https://experienceleague.adobe.com/en/docs/commerce-admin/)
   - [Adobe Commerce as a Cloud Service指南](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/)
   - [雲端上的Adobe Commerce指南](https://experienceleague.adobe.com/en/docs/commerce-cloud/)

- 對於使用&#x200B;**Adobe Commerce Optimizer**&#x200B;或&#x200B;**Adobe Commerce Optimizer Connector**&#x200B;的專案，請參閱下列檔案：

   - [Merchandising Services開發人員指南](https://developer.adobe.com/commerce/services/optimizer/)
   - [銷售GraphQL API參考](https://developer.adobe.com/commerce/services/reference/graphql/)
   - [Adobe Commerce Optimizer指南](../optimizer/overview.md)
