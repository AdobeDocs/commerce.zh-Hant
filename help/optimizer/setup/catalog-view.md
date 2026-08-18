---
title: 目錄檢視
description: 瞭解什麼是目錄檢視，以及如何建立檢視，以依業務結構、原則和定價組織您的產品目錄。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 專案（Adobe管理的SaaS基礎結構）。"
exl-id: 76c1b81c-b456-4334-89bd-6027308cbc47
TQID: https://experienceleague.adobe.com/Jmze0Pq3kSNMIXqkkML-hmmlZnv-XKgeEgRB8Q8NZ6s
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
nudge: true
source-git-commit: 42c252f70f6ed1d7a5c1fd2832324308294da264
workflow-type: tm+mt
source-wordcount: 1317
ht-degree: 0%

---

# 銷售服務的目錄檢視

目錄檢視會定義使用者端可擷取的產品和定價。 它結合目錄來源、目錄層、原則和價格手冊，以支援不同的品牌、地區、業務單位或管道。

## 什麼是目錄檢視？

目錄檢視會定義產品目錄的組織和顯示方式。 它們作為篩選條件來判斷：

- 根據業務結構（品牌、地區、經銷商）**可看見哪些產品**
- **透過連結的價格手冊顯示哪些價格**
- **如何使用原則（品牌、模型、類別等屬性）篩選產品**
- **使用哪些[目錄來源](catalog-sources.md)**，根據地區設定等屬性
- **誰可以透過[目錄保護](private-catalog-view.md)和[受限制的存取金鑰](restricted-access-keys.md)存取檢視的資料**

例如，您可以為以下專案建立個別的目錄檢視：

- 品牌或業務單位
- 地理區域
- 經銷商或合作夥伴管道
- 具有特定定價的客戶區段

## 建立目錄檢視

在建立目錄檢視之前，請視需要準備下列專案：

- [目錄來源](catalog-sources.md)
- 定義產品篩選器的[原則](policies.md)
- 如果您需要覆寫產品屬性，請[目錄層](catalog-layer.md)
- 針對檢視中顯示的定價，[價格簿](pricebooks.md)
- 如果要建立私人目錄檢視，請[受限制的存取金鑰](restricted-access-keys.md)

### 設定

在此區段中，您建立目錄檢視、選取[原則](policies.md)以及[價格手冊](pricebooks.md)。

1. 從左側功能表移至&#x200B;**[!UICONTROL Store setup]**，然後按一下&#x200B;**[!UICONTROL Catalog views]**。

1. 按一下&#x200B;**[!UICONTROL Create catalog view]**。 &#x200B;

1. 設定目錄檢視詳細資料：

   - **名稱** — 輸入目錄檢視的名稱，例如`Celport`。 &#x200B;
   - **目錄來源** — 選取[目錄來源](catalog-sources.md)，例如`en-US`。
   - **目錄圖層** — 檢閱擷取的圖層和優先順序。
   - **原則** — 使用下拉式功能表選取相關原則。 例如，「品牌」、「型號」。 請&#x200B;確定您已[建立原則](policies.md)。

1. 選取要連結至型錄檢視表的價格簿。

   - **使用所有可用的價格簿** — 此選項會從所有可用的價格簿提取價格資料。
   - **僅允許選取的價格簿** — 此選項會顯示&#x200B;**新增允許的價格簿**&#x200B;對話方塊。 使用此對話方塊來選取目錄檢視要使用的特定價格簿。
   - **僅限單一價格簿** — 如果只套用一份價格簿，請選取此選項。 如果您想要設定僅能參考一個價格簿的私人型錄檢視表，則需要使用此選項。 檢視私人目錄檢視的[價格簿限制](private-catalog-view.md#price-book-restriction-on-private-catalog-views)。
   - **停用定價** — 目前無法使用此選項。

   >[!NOTE]
   >
   >價格簿ID可控制請求哪個訂價。 它不會限制對目錄檢視的存取權。 若要限制存取，請啟用目錄保護以建立[私人目錄檢視](private-catalog-view.md)。

1. （選用）將&#x200B;**[!UICONTROL Catalog Protection]**&#x200B;切換為&#x200B;**[!UICONTROL Enabled]**，以限制此目錄檢視的資料只能由具有有效簽署權杖的使用者端使用。 如需設定步驟，請參閱[保護目錄檢視](private-catalog-view.md#protect-a-catalog-view)。

1. 按一下&#x200B;**[!UICONTROL Add]**&#x200B;以建立包含連結價格手冊和原則的目錄檢視。

目錄檢視頁面會更新以顯示新的目錄檢視&#x200B;。

完成這些步驟後，目錄檢視現在會設定為根據您選取的來源和原則顯示產品和定價。

### 指定建議和產品探索規則的目錄檢視

當您[建立建議單位](../merchandising/recommendations/create.md)或[銷售規則](../merchandising/rules/add.md)時，您可以指定目錄檢視。

## 目錄圖層

目錄層可讓您覆寫所選的產品屬性，而不變更來源目錄資料。 使用圖層可自訂目錄檢視的名稱、說明、影像、連結或中繼資料。

請參閱[目錄圖層](catalog-layer.md)。

## 將目錄檢視設為私人

依預設，目錄檢視是可供可存取GraphQL Merchandising API的使用者端應用程式公開使用。 若要限制存取，請啟用&#x200B;**[!UICONTROL Catalog Protection]**&#x200B;以設定私人目錄檢視。

若要瞭解如何保護目錄檢視並驗證存取權是否已強制執行，請參閱[私人目錄檢視](private-catalog-view.md)。

## 管理目錄檢視

若要更新或檢視現有目錄檢視的屬性，請遵循下列指示。

### 編輯目錄檢視

1. 在&#x200B;**[!UICONTROL Catalog views]**&#x200B;工作區中，找出目錄檢視。
1. 若要開啟動作功能表，請選取(**[!UICONTROL ...]**)。
1. 選取&#x200B;**[!UICONTROL Edit]**&#x200B;以存取目錄檢視編輯器。
1. 視需要更新名稱、目錄來源、原則、價格簿資訊，以及&#x200B;**[!UICONTROL Catalog Protection]**&#x200B;設定（包括指派的限制存取金鑰）。
1. 按一下&#x200B;**[!UICONTROL Save]**。

### 刪除目錄檢視

1. 在&#x200B;**[!UICONTROL Catalog views]**&#x200B;工作區中，找出目錄檢視。
1. 若要開啟動作功能表，請選取(**[!UICONTROL ...]**)。
1. 選取&#x200B;**[!UICONTROL Delete]**。
1. 確認刪除。

   當確認對話方塊出現時，按一下&#x200B;**[!UICONTROL Delete]**。

### 檢視目錄檢視詳細資料

此選項提供快速檢視所有目錄檢視引數的方法，同時保留在&#x200B;**[!UICONTROL Catalog views]**&#x200B;表格上。

在&#x200B;**[!UICONTROL Catalog views]**&#x200B;工作區中，選取目錄檢視的![資訊圖示](../assets/info-icon.png)以檢視其設定詳細資料。

![目錄檢視詳細資料](../assets/catalog-view-details.png)

您可以在此處檢視目錄檢視設定詳細資料，例如：

- 檢視ID
- 名稱
- 目錄來源
- 原則
- 建立日期
- 資料已修改

當您設定店面或使用資料擷取API時，需要用到其中的一些組態設定。

## 架構概覽

目錄檢視是Merchandising Services架構的一部分，其使用更彈性的模型取代Adobe Commerce基礎中使用的網站、商店、商店評論架構：

![[!DNL Merchandising Services]架構](../assets/merchandising-svcs-architecture.png)

### 運作方式

**1. 資料擷取**
來自PIM、ERP和其他系統的目錄資料會擷取至「銷售服務」架構。 每個SKU都包含對應至目錄檢視、原則及區域設定的區域設定資訊與產品屬性。 如需資料擷取的詳細資訊，請參閱[開發人員檔案](https://developer.adobe.com/commerce/services/optimizer/)。

**2. 統一基礎目錄**
內嵌的資料會在目錄服務資料管道中建立統一的基本目錄。 此單一來源可消除業務單位間的資料重複。

**3. 目錄檢視**
多個目錄檢視代表不同的業務單位（例如，「Texas Retail」、「Texas Retail Secondural」）。 您可以跨目錄檢視共用地區、原則和價格簿，以取得彈性。

**4. 多頻道傳送**
經篩選的目錄資料會傳送至Edge Delivery Services、行銷場所、廣告平台和自訂微型店面等目的地。 如需目錄資料傳遞的詳細資訊，請參閱[開發人員檔案](https://developer.adobe.com/commerce/services/optimizer/)。

當目錄檢視啟用&#x200B;**[!UICONTROL Catalog Protection]**&#x200B;時，傳遞至該目的地需要指派的[受限制存取金鑰](restricted-access-keys.md)中的有效已簽署權杖；未獲授權的請求會遭拒，而非接收目錄資料。

### 主要元件

| 元件 | 用途 | 範例 |
|---|---|---|
| **目錄檢視** | 業務單位或分銷管道 | 經銷商網路、地區商店 |
| **原則** | 根據屬性的產品篩選器 | 品牌、型號、類別 |
| **地區設定** | 語言/地區設定 | en-US、fr-CA、es-MX |
| **價格簿** | 定價結構 | 零售、批發、員工 |
| **受限制的存取金鑰** | 可閘道受保護目錄檢視存取權的已簽署Token認證 | 合作夥伴入口網站金鑰、B2B定價金鑰 |

### 資料流程

1. **擷取** — 來自PIM/ERP系統的產品資料
2. **處理序** — 套用目錄檢視、原則和定價
3. **傳遞** — 將篩選的目錄提供給店面、市場等。

## 主要功能

| 功能 | 優點 |
|---|---|
| **單一基底目錄** | 消除業務單位之間的資料重複 |
| **彈性定價** | 針對不同客戶區段，每個SKU有多個價格簿 |
| **可擴充** | 有效管理200M以上的SKU |
| **多頻道** | 將目錄提供給店面、市集和廣告平台 |
| **即時更新** | 快速更新促銷活動和行銷活動的目錄資料 |
| **私人目錄檢視** | 使用已簽署的權杖驗證將目錄檢視限製為授權使用者端 |

## 使用案例

### 多品牌企業集團

**挑戰**：管理多個品牌、國家/地區和語言<br>
**解決方案**：每個品牌/地區組合的單一目錄包含目錄檢視

### 汽車零件經銷商

**挑戰**： 3,000個產品相同但價格不同的經銷商<br>
**解決方案**：一個目錄，包含經銷商特定的目錄檢視和價格簿

### 多位置retailer

**挑戰**：每個地點的不同定價和詳細目錄<br>
**解決方案**：以位置為基礎的目錄檢視具有區域特定原則

>[!NOTE]
>
>如需目錄資料擷取與傳遞的詳細資訊，請參閱[開發人員檔案](https://developer.adobe.com/commerce/services/optimizer/)。

## 更多相關資訊

- [目錄來源](catalog-sources.md) — 定義搜尋、篩選和排序行為的產品、屬性和類別的權威範圍
- [目錄圖層](catalog-layer.md) — 瞭解如何修改產品資料而不變更原始來源
- [私人目錄檢視](private-catalog-view.md) — 建立私人目錄檢視以限制授權使用者端的存取權
- [受限制的存取金鑰](restricted-access-keys.md) — 建立、指派及旋轉用於簽署目錄保護權杖的金鑰
- [原則](policies.md) — 建立原則以篩選目錄檢視中的產品
- [價格手冊](pricebooks.md) — 管理不同客戶區段的定價結構
