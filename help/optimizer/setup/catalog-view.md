---
title: 目錄檢視
description: 瞭解什麼是目錄檢視，以及如何建立檢視，以依業務結構、原則和定價組織您的產品目錄。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和[!DNL Adobe Commerce Optimizer]個專案（Adobe管理的SaaS基礎結構）。"
exl-id: 76c1b81c-b456-4334-89bd-6027308cbc47
TQID: https://experienceleague.adobe.com/Jmze0Pq3kSNMIXqkkML-hmmlZnv-XKgeEgRB8Q8NZ6s
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
nudge: true
last-update: 2026-11-12
source-git-commit: 44918d5b636f0577c75010def79737acee1ffe0b
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 0%
---
# 銷售服務的目錄檢視

{{$include /help/_includes/ccdm-shared/setup/catalog-view.md}}

## 管理目錄檢視

使用這些指示來管理目錄檢視：

- [建立目錄檢視](#create-a-catalog-view) — 設定名稱、目錄來源、原則和價格簿。 然後[指定建議和產品探索規則的目錄檢視](#specify-catalog-views-for-recommendations-and-product-discovery-rules)、檢閱覆寫產品屬性的[目錄層](#catalog-layers)，或[將目錄檢視設為私人](#make-a-catalog-view-private)。
- [編輯目錄檢視](#edit-a-catalog-view) — 更新其來源、原則、價格手冊和保護設定。
- [刪除目錄檢視](#delete-a-catalog-view) — 移除您不再需要的目錄檢視。
- [檢視目錄檢視詳細資料](#view-catalog-view-details) — 從目錄檢視表格檢視目錄檢視的組態。

### 建立目錄檢視

在建立目錄檢視之前，請視需要準備下列專案：

- [目錄來源](catalog-sources.md)
- 定義產品篩選器的[原則](policies.md)
- 如果您需要覆寫產品屬性，請[目錄層](catalog-layer.md)
- 針對檢視中顯示的定價，[價格簿](pricebooks.md)
- 如果要建立私人目錄檢視，請[受限制的存取金鑰](restricted-access-keys.md)

#### 設定

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

#### 指定建議和產品探索規則的目錄檢視

當您[建立建議單位](../merchandising/recommendations/create.md)或[銷售規則](../merchandising/rules/add.md)時，您可以指定目錄檢視。

#### 目錄圖層

目錄層可讓您覆寫所選的產品屬性，而不變更來源目錄資料。 使用圖層可自訂目錄檢視的名稱、說明、影像、連結或中繼資料。

請參閱[目錄圖層](catalog-layer.md)。

#### 將目錄檢視設為私人

依預設，目錄檢視是可供可存取GraphQL Merchandising API的使用者端應用程式公開使用。 若要限制存取，請啟用&#x200B;**[!UICONTROL Catalog Protection]**&#x200B;以設定私人目錄檢視。

若要瞭解如何保護目錄檢視並驗證存取權是否已強制執行，請參閱[私人目錄檢視](private-catalog-view.md)。

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

在&#x200B;**[!UICONTROL Catalog views]**&#x200B;工作區中，選取目錄檢視的![資訊圖示](/help/assets/ccdm-shared/recommendations/info-icon.png)以檢視其設定詳細資料。

![目錄檢視詳細資料](../assets/catalog-view-details.png)

您可以在此處檢視目錄檢視設定詳細資料，例如：

- 檢視ID
- 名稱
- 目錄來源
- 原則
- 建立日期
- 資料已修改

當您設定店面或使用資料擷取API時，需要用到其中的一些組態設定。
