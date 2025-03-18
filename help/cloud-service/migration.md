---
title: 移轉至Adobe Commerce as a Cloud Service
description: 瞭解如何移轉至Adobe Commerce as a Cloud Service。
source-git-commit: 19c49b2b9d630898353addd778e062d3208505c1
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 0%

---


# 移轉至Adobe Commerce as a Cloud Service

Adobe Commerce as a Cloud Service提供大部分的立即可用設定。 不過，如果您要從雲端或內部部署執行個體上的現有Adobe Commerce移轉，則需根據您的特定設定執行不同的移轉動作。

## 移轉路徑

Adobe Commerce as a Cloud Service支援多個移轉路徑，實際取決於您的時間軸、店面和自訂。

除了完整移轉外，Adobe Commerce as a Cloud Service也支援使用Commerce Optimizer或增量方式的分階段移轉。

* **累加移轉** — 此方法包含分階段移轉資料、自訂和整合。 此方法適用於有許多自訂專案的大型商戶，這些商戶想要根據自己的步調，將其複雜的自訂專案和資料逐步轉換至Adobe Commerce as a Cloud Service。

![增量移轉](./assets/incremental.png){width="600" zoomable="yes"}

* **Commerce Optimizer** — 此方法可讓您重複移轉，方法是使用Commerce Optimizer作為轉換階段，以您自己的步調將複雜的自訂專案和資料移至Adobe Commerce as a Cloud Service。 Commerce Optimizer可讓您存取由目錄管道和原則支援的銷售服務、由Edge Delivery支援的Commerce店面，以及由AEM Assets支援的產品視覺效果。

![反複移轉](./assets/optimizer.png){width="600" zoomable="yes"}

* **完整移轉** — 此方法需要一次移轉所有資料、自訂和整合。 此方法非常適合需要快速轉換至Adobe Commerce as a Cloud Service、且僅有少量自訂內容的小型商家。

下表提供不同店面及設定的移轉程式概覽：

|                    | LUMA店面 | PWA店面 | 由Edge Delivery提供支援的Commerce店面 | Headless |
|--------------------|----------------------------------------|----------------------------------------|------------------------------------------------------|----------------------------------------|
| 資料移轉 | 必填 | 必填 | 必填 | 必填 |
| 店面 | 移轉至Edge Delivery支援的Commerce店面 | 移轉至Edge Delivery支援的Commerce店面或維護 | 沒有影響 | 沒有影響 |
| API網格 | 建立新網格 | 建立新網格或重新設定現有網格 | 建立新網格或重新設定現有網格 | 建立新網格或重新設定現有網格 |
| 整合 | 善用整合入門套件 | 善用整合入門套件 | 善用整合入門套件 | 善用整合入門套件 |
| 自訂 | 移至App Builder &amp; API Mesh | 移至App Builder &amp; API Mesh | 移至App Builder &amp; API Mesh | 移至App Builder &amp; API Mesh |
| Assets管理 | 使用OOTB時需要移轉 | 使用OOTB時需要移轉 | 使用OOTB時需要移轉 | 使用OOTB時需要移轉 |
| 擴充功能 | 移轉至App Builder | 移轉至App Builder | 移轉至App Builder | 移轉至App Builder |

如表所示，每次移轉的緩解措施將包含：

* **資料移轉** — 使用提供的移轉工具，將資料從您現有的執行個體移轉到Adobe Commerce as a Cloud Service。
* **店面** — 現有的EDS和Headless店面不需要減輕影響，但LUMA店面需要移轉至Edge Delivery支援的Commerce店面。 PWA Studio店面可移轉至Edge Delivery支援的Commerce店面，或維持其目前狀態。 Adobe將提供加速器來協助店面遷移。
* **[API網格](https://developer.adobe.com/graphql-mesh-gateway)** — 建立新網格或修改現有網格。 Adobe將提供預先設定的網格，以協助進行此程式。
* **整合** — 所有整合都需要運用[整合入門套件](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/)或[Adobe Commerce as a Cloud Service REST API](https://developer.adobe.com/commerce/services/reference/cloud-service/core-admin/)。
* **自訂** — 所有自訂都必須移至App Builder和API Mesh。
* **Assets管理** — 所有資產管理都需要移轉。 如果您已在使用AEM Assets，則不需要移轉。
* **擴充功能** — 任何處理中的擴充功能都必須重新建立為程式外擴充功能。 到2025年底，Adobe將提供100個最熱門的擴充功能，這些擴充功能已預先載入並準備使用，以將建置時間縮到最短。

## 移轉階段

從您目前的Adobe Commerce例項移轉至新的Adobe Commerce as a Cloud Service例項主要涉及下列階段：

* **[整備](#readiness-phase)** — 首先判斷您的部署是否已準備好移至ACCS。 在這個階段中，您也應該熟悉ACCS所做的變更&#x200B;。
* **[實作](#implementation-phase)** — 接下來，準備好您的程式碼、店面、擴充功能和整合以進行移轉。 為了簡化轉換，Adobe同時允許[短期和長期反複方法](#migration-paths)&#x200B;。
* **[上線](#go-live-phase)** — 測試並確認一切準備就緒，然後執行資料移轉。
* **[上線後](#post-go-live-phase)** — 與Adobe合作，在移轉完成後監視問題並視需要改善效能。

### 整備階段

1. 首先，請檢閱Adobe Commerce as a Cloud Service架構、擴充性架構和店面功能：

   * [雲端服務架構上的Adobe Commerce](./overview.md) — 檢閱平台架構，以及它與您目前的Adobe Commerce執行個體有何不同。
   * [Adobe Commerce擴充性架構](https://developer.adobe.com/commerce/extensibility/) — 識別您要如何轉換目前的自訂專案。
   * [由Edge Delivery提供支援的Commerce店面](https://experienceleague.adobe.com/developer/commerce/storefront/) — 檢閱建議的店面解決方案。

1. 稽核您的自訂相容性：

   * 識別您目前的自訂模組和協力廠商整合。
   * 使用App Builder評估需要重新實作的自訂。
   * 將您目前的自訂對應至其App Builder擴充功能的同等專案。

1. 確認您的店面需求，並確保其符合Adobe Edge交付功能。

1. 檢閱您目前的第三方整合，並確認與Adobe Commerce as a Cloud Service平台的API相容性。

### 實作階段

下列步驟概述移轉的開發和執行程式：

1. 在[Adobe Commerce Manager](./getting-started.md#create-an-instance)中建立新的Commerce Cloud as a Cloud Service執行個體。

1. 安裝必要的應用程式和自訂。 Adobe Commerce as a Cloud Service已預先載入100個最受歡迎的應用程式。 如果您需要其他應用程式或自訂，可以使用App Builder重新實作。

1. 設定下列其中一個GraphQL型店面：

   * [建立Commerce店面](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/)
   * [使用PWA Studio建立自訂GraphQL型店面](https://developer.adobe.com/commerce/pwa-studio/)

1. 將資料從先前的Commerce執行個體移轉至ACCS：

   * 使用資料遷移工具遷移原生Adobe Commerce資料。
   * 移轉協力廠商擴充功能與自訂
   * 移轉設定和整合資料：
      * 使用[Adobe Commerce Integration Starter Kit](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/)傳輸API Mesh設定、協力廠商服務和系統整合。

### 上線階段

在啟動之前，請先驗證並測試新的Adobe Commerce as a Cloud Service執行個體：

* **功能測試** — 確保移轉的資料、店面功能與自訂作業順利運作。

* **效能測試** — 評估儲存區的速度和擴充能力，以確保全球最佳效能。

* **安全性稽核** — 檢閱安全性措施，包括API存取控制和任何可能的漏洞。

### 上線後階段

一旦您已驗證並測試新的Adobe Commerce as a Cloud Service沙箱執行個體，您就可以啟動生產執行個體：

1. 上線

   * 將流量重新導向至新平台並監控效能。
   * 停用您的舊Adobe Commerce執行個體。

1. 啟動後監視

   * 使用監控工具確保穩定運作，並解決任何上市後問題。
