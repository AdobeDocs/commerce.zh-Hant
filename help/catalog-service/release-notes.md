---
title: '[!DNL Commerce Storefront Catalog Service Release Notes]'
description: 適用於Adobe Commerce的 [!DNL Catalog Service] 的最新發行資訊。
feature: Services, Catalog Service, Release Notes
exl-id: 74f2e46a-5592-4857-a6d7-b95b85d8b4cc
source-git-commit: 9ba7a964243c616cc7e40fb180a855b839cd4597
workflow-type: tm+mt
source-wordcount: '2252'
ht-degree: 0%

---

# [!DNL Commerce Storefront Catalog Service]發行說明

下列發行說明涵蓋最新的Commerce Catalog Service更新，包括：

- **店面目錄服務發行版本**

   - 目錄服務API結構描述增強功能，可改善資料擷取。
   - 目錄服務API和基礎基礎結構的安全性、效能和可靠性改善。

- **目錄服務中繼套件發行版本**

   - 更新相依性，以提升效能、穩定性以及與其他Adobe Commerce元件的相容性。

更新會依型別分類：

![新](../assets/new.svg)新功能
![修正](../assets/fix.svg)修正和改良
![錯誤](../assets/bug.svg)已知問題

支援最新版本。 隨附舊版發行說明以供參考。

## 店面目錄服務

### v1.48版本

_2025年2月19日_

![新增](../assets/new.svg) GraphQL API中的`categoryTree`查詢現在會傳回類別說明、影像和SEO中繼標籤。 此更新提供店面開發人員顯示類別影像所需的資料，並透過適當的中繼標題、說明和關鍵字改善搜尋引擎最佳化。 僅支援針對Headless店面&lt;[使用](https://developer.adobe.com/commerce/services/optimizer/)可撰寫目錄資料模型<!--DATA-6933-->的Commerce實作

### v1.47版本

_2025年2月12日_

![新](../assets/new.svg) API服務現在支援`CategoryProductView`型別，可依類別啟用產品的增強型檢視和查詢。 此更新可讓開發人員根據類別有效率地擷取及篩選產品資料，改善類別導向使用案例的彈性和效能。 如需詳細資訊，請參閱[實作店面](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/categories-storefront-implementation/)上的類別。 僅支援針對Headless店面[使用](https://developer.adobe.com/commerce/services/optimizer/)可撰寫目錄資料模型<!--DATA-6949-->的Commerce實作

### v1.46版本

_2025年12月11日_

![修正](../assets/fix.svg)系統層級和基礎建設的改善，以強化效能和穩定性。<!--DATA-6852, DATA-6864-->

### v1.45版本

_2025年11月17日_

![新的](../assets/new.svg) **依名稱篩選屬性**- `productSearch` GraphQL查詢現在支援使用`names`欄位篩選產品屬性。 <!--DATA-6831-->使用此篩選器，您可以：

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

### v1.44版本

_2025年11月6日_

![修正](../assets/fix.svg)系統層級和基礎建設的改善，以強化效能和穩定性。<!--DATA-6852, DATA-6864-->

### v1.43版本

_2025年11月3日_

![新增](../assets/new.svg) **多維度產品自訂的產品層** — 已針對Adobe Commerce Optimizer實作新增通道特定、地區設定感知的內容傳遞支援。<!--DATA-6632-->

- 為不同的客戶區段提供不同的產品內容
- 套用地區特定自訂而不複製基本資料
- 使用圖層遮色片控制欄位層級覆寫
- 支援優質、季節和行動最佳化內容層

  使用現有`products`查詢擷取圖層、從請求標頭套用至伺服器端，且不需要變更結構描述。 請參閱[Adobe Commerce Optimizer指南](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/catalog-layer)中的&#x200B;_目錄層_。

![修正](../assets/fix.svg)當父項沒有訂價時，現在可以查詢已分組的產品；子項產品會傳回自己的可見性角色。<!--DATA-6779-->

![修正](../assets/fix.svg)系統層級和基礎建設的改善，以強化效能和穩定性。<!--DATA-6721, DATA-6864-->

### v1.42版本

_2025年9月8日_

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

### v1.41版本

_2025年9月2日_

![修正](../assets/fix.svg) **已改善遺失價格資訊的錯誤處理** — 尚未收到價格資料時，API會傳回價格欄位的`null`，而非擲回錯誤，讓使用者端能夠妥善處理遺失的資料。<!--DATA-6612-->

![修正](../assets/fix.svg)系統層級和基礎建設的改善，以強化效能和穩定性。<!--DATA-6671-->

### v1.40版本

_2025年7月30日_

![修正](../assets/fix.svg)系統層級和基礎建設改善專案，以強化安全性、效能和穩定性。<!--DATA-6619-->

### v1.39版本

_2025年7月24日_

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

### v1.38版本

_2025年7月15日_

![新的](../assets/new.svg) **禮卡產品型別** — 目錄店面服務現在支援產品屬性為JSON物件或陣列，可彈性管理複雜型別，例如禮卡。<!--DATA-6573-->


### v1.37版本

_2025年6月20日_

![新的](../assets/new.svg) **階層式價格簿組態** — 上下階價格簿的精確價格範圍。 計算會遵循階層與繼承的規則；當連結多重價格簿時，可減少訂價錯誤。 僅限Adobe Commerce Optimizer。 檢視[價格手冊](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/pricebooks)。

![新](../assets/new.svg) **不區分大小寫的索引鍵** — 查詢中的索引鍵查閱現在不區分大小寫，可減少因索引鍵大小寫造成的錯誤。<!--DATA-6494, DCAT-2495-->

### v1.36版本

_2025年6月20日_

![新](../assets/new.svg) **目錄店面的公用IO事件** — 已新增公用IO事件，以便即時整合和可觀察性（CSS和EDS）。<!--DATA-6329-->

![新的](../assets/new.svg) **伺服器端轉譯(SSR)** — 支援SSR的架構改進，可在大型目錄上提供更優異的效能、SEO和UX。<!--DATA-6278, DATA-6280-->

![新](../assets/new.svg) **基礎架構和安全性** — 事件服務的新AWS角色、ServiceNow整合和CI/CD管道。

![新](../assets/new.svg) **事件格式和可觀察性** — 簡化裝載、增強監控、改善變體事件資料。<!--DATA-6332, DATA-6402, -->

![修正](../assets/fix.svg)系統層級和基礎建設改善專案，以強化安全性、效能和穩定性。<!--DATA-6404, DATA-6410, -->

+++ 舊版

## v1.35版本

_2025年6月13日_

![新的](../assets/new.svg) **擷取未快取的資料** — 啟用`Magento-Is-Preview`標頭以將未快取的資料從目錄端點傳遞至搜尋服務。<!--DATA-6345-->

![新的](../assets/new.svg) **多重選取產品選項**-GraphQL API現在會公開產品選項是否允許多重選取（例如，套件組合「選擇多個專案」）。<!--DATA-6487-->

![新的](../assets/new.svg)資料擷取已更新價格驗證，以支援沒有價格的產品。<!--DATA-6098-->

![修正](../assets/fix.svg)已改善Adobe Commerce Optimizer中簡單套件定價的錯誤處理。<!--DATA-6541-->

![修正](../assets/fix.svg)系統層級和基礎建設改善專案，以強化安全性、效能和穩定性。<!--DATA-6273, DATA-6485, -->

## v1.34版本

_2025年3月23日_

![修正](../assets/fix.svg)系統層級和基礎建設改善專案，以強化安全性、效能和穩定性。<!--DATA-5732-->

## v1.33版本

_2025年4月29日_

![修正](../assets/fix.svg)系統層級和基礎建設改善。 基礎架構現在支援超大型的目錄（最多達4.4億SKU），不會影響現有的工作負載。

### v1.32版本

_2025年3月28日_

![修正](../assets/fix.svg)沒有角色的屬性預設不再為可撰寫的目錄編制索引，因此可縮短編制索引的時間並減少儲存空間。 舊版行為可透過功能標幟重新啟用。

![修正](../assets/fix.svg)系統層級和基礎建設改善，以強化安全性、效能和穩定性。<!--DATA-6348, DATA-6440, DATA-6446, DATA-6641-->

### v1.31版本

_2025年2月18日_

![修正](../assets/fix.svg)系統層級和基礎建設改善專案，以強化安全性、效能和穩定性。<!--DATA-6389, DATA-6367, DATA-6373-->

### v1.30版本

_2024年12月9日_

主要版本： Headless店面、標題管理和產品資料處理的[可撰寫目錄資料模型](https://developer.adobe.com/commerce/services/optimizer/)。

![新的](../assets/new.svg) **可撰寫的目錄資料模型(CCDM)** — 支援客戶將Composable目錄用於Headless店面。 新端點接受目錄檢視和原則ID （向後相容）。 可設定的產品詳細資料和價格（內建分頁）。<!--DATA-6018, DATA-6288-->

針對可撰寫的目錄API作業，![New](../assets/new.svg) **標題管理**-`AC-Locale`已重新命名為`AC-Scope-Locale`；已指定標題對應和預設值。<!--DATA-6303, DATA-6078-->

![新的](../assets/new.svg) **產品資料與價格** — 支援可撰寫的目錄資料模型，並改善可設定產品價格處理。<!--DATA-6279-->

已更新`CurrencyEnum`以支援`NONE`產品搜尋查詢，與同盟邏輯一致。<!--DATA-6285-->

![修正](../assets/fix.svg) **基礎結構和升級** — 安全性、效能和穩定性的系統層級改善。

![修正](../assets/fix.svg)套件組合產品選項現在只會顯示啟用的產品。<!--DATA-6347-->

### v1.29版本

_2024年12月9日_

![新](../assets/new.svg) **產品查詢中的影像訂購**—GraphQL `images`欄位中的產品影像現在會遵循目錄匯出`sortOrder`，以取得一致的店面和API行為。<!--DATA-6258-->

![修正](../assets/fix.svg)系統層級和基礎建設改善專案，以強化安全性、效能和穩定性。<!--DATA-6619-->

### v1.28版本

![修正](../assets/fix.svg)系統層級和基礎建設改善專案，以強化安全性、效能和穩定性。<!--DATA-6180, DATA-6230, DATA-6254, DATA-6257-->

### v1.27版本

_2024年9月26日_

![修正](../assets/fix.svg)系統層級和基礎建設改善專案，以強化安全性、效能和穩定性。<!--DATA-6243-->

### v1.26版本

_2024年10月22日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新的](../assets/new.svg) GraphQL結構描述現在在產品資訊中包含`lastModifiedAt`，以取得精確的Sitemap和搜尋引擎重新索引(例如Google)。<!--DATA-6209-->

### v1.23版本

_2024年8月22日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![修正](../assets/fix.svg)現在可以擷取產品資訊，而不需要產品覆寫（價格）資料。 以前，這些查詢會傳回： `The following sku does not have product override data in the DB: <SKU value>. Make sure data is synced.` <!--DATA-6121-->

### v1.22版本

_2024年8月13日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![New](../assets/new.svg)已新增支援，以依據產品SKU擷取所有變體。 檢視[目錄服務API參考](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)。<!--DATA-6067-->

### v1.19版本

_2024年5月23日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本


![修正](../assets/fix.svg) <!--DATA-5033-->選項值的`InStock`旗標現在會遵守產品變體的領域`enabled`狀態。

![修正](../assets/fix.svg) <!--DATA-5888-->已新增對產品價格的支援，最多可包含16位數和4位小數。 從[資料管理儀表板](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)或[CLI](../landing/catalog-sync.md#command-line-interface)重新同步以套用更新。

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

### v1.18版本

_2024年4月11日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)已新增對PHP 8.3的支援。

![新的](../assets/new.svg) [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/)與[`refineProduct`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/)查詢現在會傳回簡單與複雜產品的可自訂選項資料。<!--DATA-5538-->

### v1.17版本

_2024年2月22日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新增](../assets/new.svg) [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html)現在可用於資料串流（產品推薦、即時搜尋、目錄服務）。 需要`catalog-service`個中繼封裝v3.1.0+。

### v1.16版本

_2024年2月13日_

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

### v1.13版本

_2023年10月12日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)目錄服務支援產品變體的`inStock`旗標。
![新](../assets/new.svg) `urlKey`和`externalId`欄位已新增至GraphQL結構描述。
現在支援![新](../assets/new.svg)可下載的產品和禮品卡。

### v1.12版本

_2023年9月19日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)目錄服務現在使用[SaaS價格索引](../price-index/price-indexing.md)。
![修正](../assets/fix.svg)此版本包含服務端的錯誤修正和改善。

### v1.11版本

_2023年7月18日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)目錄服務現在支援產品推薦的[`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) GraphQL查詢。

### v1.10版本

_2023年6月27日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)目錄服務API現在支援`related products`。

### v1.7版本

_2023年4月12日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)目錄服務現在會清除已刪除的產品變體。
![修正](../assets/fix.svg)基礎架構擴充性與效能的改善。

### v1.6版本

_2023年3月28日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)已新增色票至[`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/)查詢。
![新](../assets/new.svg)已新增使用`entityId`API Mesh[取得](mesh.md)的功能。

### v1.5版本

_2023年3月6日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)已新增[`categories`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) GraphQL功能。
![修正](../assets/fix.svg)已改善效能和API擴充性。

### v1.4版本

_2023年2月7日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新增](../assets/new.svg)已發佈的目錄服務中繼資料以簡化安裝步驟。
![修正](../assets/fix.svg) API擴充性和效能改善。

### v1.3版本

_2023年1月17日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新](../assets/new.svg)簡化並改善入門體驗。
![新的](../assets/new.svg)新客戶沙箱端點可用於生產前測試。
已新增虛擬產品的![新](../assets/new.svg)支援。
![修正](../assets/fix.svg) API擴充性和效能改善。

### v1.1版本

_2022年11月18日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新](../assets/new.svg)目錄服務現在支援Adobe的[API Mesh](https://developer.adobe.com/graphql-mesh-gateway/)。
![修正](../assets/fix.svg)已改善API擴充性和整體效能。

### v1.0版本

_2022年10月4日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

套件和群組產品的![新](../assets/new.svg)支援。
![新](../assets/new.svg)已新增B2B可見性覆寫。 產品現在可供搜尋，並可新增至特定客戶群組的購物車。
![Fix](../assets/fix.svg)服務現在更穩定且效能更佳。

### 0.3版 — Beta+

_2022年9月12日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新](../assets/new.svg)變體影像：根據選取的選項傳回產品影像。
![新](../assets/new.svg)價格角色：只有特定客戶群組的成員才能看到產品價格。
![修正](../assets/fix.svg)已改善服務的穩定性和效能。
從目錄中刪除產品時，會收到![新的](../assets/new.svg)更新。

### Beta版本

_2022年8月9日_

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

- 針對雲端內部部署的Adobe Commerce，Adobe建議使用撰寫器，將雲端環境中的目錄服務中繼資料升級為最新版本。

### v3.3.0版本

_2025年10月14日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg) **資料服務升級**—`magento/data-services`相依性已更新為^8.0.0。升級之前，請先驗證環境與自訂資料服務API的使用情況，以符合8.x版本。
ea
![新](../assets/new.svg)已更新3.3.0版的版本和中繼資料。

### v3.2.0版本

_2024年4月12日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

已針對3.2.0更新![新](../assets/new.svg)版本和中繼資料。沒有其他相依性變更。

### v3.1.0版本

_2024年1月26日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)已新增新的套件相依性：

- **類別許可權資料匯出工具** (`magento/module-category-permission-data-exporter`)，用於匯出目錄服務使用的類別許可權資料。
- **目錄同步管理員** `magento/module-catalog-sync-admin`，用於與目錄同步相關的管理員UI和設定。

![新](../assets/new.svg)已更新3.1.0版的版本和中繼資料。

## 相關檔案

- 對於部署在雲端、內部部署或Adobe Commerce as a Cloud Service上的**Adobe Commerce上的專案，請參閱以下檔案：

   - [目錄服務指南](overview.md)
   - [目錄服務GraphQL API參考](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)
   - [Adobe Commerce管理指南](https://experienceleague.adobe.com/en/docs/commerce-admin/)
   - [Adobe Commerce as a Cloud Service指南](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/)
   - [雲端上的Adobe Commerce指南](https://experienceleague.adobe.com/en/docs/commerce-cloud/)

- 對於使用&#x200B;**Adobe Commerce Optimizer**&#x200B;或&#x200B;**Adobe Commerce Optimizer Connector**&#x200B;的專案，請參閱下列檔案：

   - [Merchandising Services開發人員指南](https://developer.adobe.com/commerce/services/optimizer/)
   - [銷售GraphQL API參考](https://developer.adobe.com/commerce/services/reference/graphql/)
   - [Adobe Commerce Optimizer指南](../optimizer/overview.md)
