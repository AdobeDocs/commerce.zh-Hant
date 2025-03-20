---
title: '[!DNL Adobe Commerce as a Cloud Service]總覽'
description: 瞭解 [!DNL Adobe Commerce as a Cloud Service]的主要功能和優點。
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Architect, Developer, User
exl-id: 1b7e2731-4a10-4c2b-9bfc-8945729ed523
source-git-commit: d38066b6db7da5bb029391716063ed098be1f519
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 0%

---

# [!DNL Adobe Commerce as a Cloud Service]總覽

{{accs-early-access}}

[!DNL Adobe Commerce as a Cloud Service]可讓企業提供並快速擴充數位作業，加速創新，進而提供彈性、擴充性和效率。 Adobe的雲端原生基礎結構會自動調整資源，以符合流量、訂單和目錄管理的高峰需求。

下圖會強調支援[!DNL Adobe Commerce as a Cloud Service]的產品：

![[!DNL Adobe Commerce as a Cloud Service]產品棧疊](./assets/product-stack.svg){align="center" zoomable="yes"}

>[!BEGINSHADEBOX]

![資訊](assets/Smock_InfoOutline_18_N.svg)如果您要參與[!DNL Adobe Commerce as a Cloud Service]搶先存取計畫，請完成[此表單](https://forms.office.com/pages/responsepage.aspx?id=Wht7-jR7h0OUrtLBeN7O4WOxhjY2doZPikS2hIbfmL5URFZXTE5TUk9PMUw0OFdOWTBNNlI3UTlNMS4u&amp;route=shorturl)。

>[!ENDSHADEBOX]

## 架構

請參閱下列影片，瞭解[!DNL Adobe Commerce as a Cloud Service]架構的簡介。 說明此架構的圖表會顯示在影片下方。

>[!VIDEO](https://video.tv.adobe.com/v/3443232?learn=on)

此圖表說明[!DNL Adobe Commerce as a Cloud Service]與所有Adobe Experience Cloud解決方案之間的資料流程。

![[!DNL Adobe Commerce as a Cloud Service]架構圖表](./assets/data-flow.svg){zoomable="yes"}

## Commerce店面

使用Adobe的[Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront) (由Edge Delivery Services提供技術支援)，透過Storefront Builder的簡單檔案式撰寫或視覺化編輯，在幾分鐘內建立豐富的體驗。

Commerce Storefront採用完全無周邊的分離式架構，可透過GraphQL API層提供所有銷售服務和資料。 此架構讓團隊可獨立於Commerce Foundation開發他們的前端，提供使用新興技術建立和測試新接觸點的靈活性。

>[!NOTE]
>
>[!DNL Adobe Commerce as a Cloud Service]不支援Luma店面。 如果您要從雲端或內部部署上的Adobe Commerce進行移轉，請參閱[現有店面](https://experienceleague.adobe.com/developer/commerce/storefront/discovery/#existing-storefronts)以取得移轉指南。

## 銷售服務與付款服務

Adobe提供豐富的智慧型可撰寫銷售服務，協助您支援關鍵業務目標。 這些服務也提供對大規模最佳化效能至關重要的應用程式開發介面。

- [即時搜尋](../live-search/overview.md) — 使用此AI支援的搜尋工具，為購物者提供更聰明、更快速且相關的結果。
- [產品推薦](../product-recommendations/overview.md) — 根據購物者行為、熱門趨勢、產品相似性等新增AI輔助推薦。
- [由管道和原則支援的銷售服務](../merchandising-services/overview.md) — 透過彈性的資料模型管理大型且複雜的產品目錄，以提供符合業務結構和上市策略的高效能、彈性的商業目錄。 搭配[Commerce Optimizer](../optimizer/overview.md)使用以最佳化目錄效能並改善轉換率。
- [付款服務](../payment-services/overview.md) — 提供多種付款方式，包括免息分期付款，以及付款處理、訂單和發票的單一檢視，以提升客戶滿意度。

## 產品視覺效果

使用與Adobe Experience Manager整合的健全數位資產管理(DAM)系統，以管理多媒體內容，藉此簡化資產管理。 或者，原生mini-DAM提供基本資產管理工具，用於儲存和管理數位資產。

請參閱[資產管理](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/aem-asset-management/aem-assets-integration)以瞭解更多資訊。

## 開發人員平台

Adobe為開發人員提供全方位的擴充點和工具，以便建立可擴充Commerce Foundation功能並與協力廠商系統（例如CRM、ERPS和PIMS）整合的應用程式。 這些工具可透過下列方式降低平台的總體擁有成本：

- **擴充性** — 應用程式可與核心軟體分開擴充，以提升效率並簡化升級。
- **隔離** — 隔離的環境表示開發人員可以自行升級或修改其擴充功能，而不需依賴核心版本。
- **技術獨立性** — 開發人員可以選擇任何符合其需求的技術棧疊和程式碼語言。

>[!TIP]
>
>廠商建置的應用程式也可在[Adobe Exchange](https://exchange.adobe.com/)上安裝。

Adobe提供下列開發人員工具，用於建立整合與自訂：

- 適用於Adobe Developer App Builder的&#x200B;[**API Mesh**](https://developer.adobe.com/graphql-mesh-gateway/) — 協調多個API、GraphQL、REST和其他來源並將其合併為單一、可查詢的GraphQL端點。
- [**App Builder**](https://developer.adobe.com/app-builder/docs/overview/) — 建置並部署安全且可擴充的Web應用程式，這些應用程式可擴充Commerce功能並與協力廠商解決方案整合。
- [**事件**](https://developer.adobe.com/commerce/extensibility/events/) — 使用自訂事件觸發程式與其他可擴充的開發工具互動。
- [**Webhooks**](https://developer.adobe.com/commerce/extensibility/webhooks/) — 使用Webhook自動觸發Commerce與協力廠商系統之間的互動。
- [**管理UI SDK**](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/) — 使用商戶的新頁面和功能，自訂並增強Commerce管理。
- [**整合入門套件**](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) — 透過參考整合、入門指令碼和標準化架構，加速您的後台整合。

## Commerce Foundation

Commerce Foundation提供安全的自動化託管平台和自助服務功能，可在雲端原生環境中管理您的Commerce應用程式。

主要功能包括：

- 簡化入門
- 順暢的升級
- 協力廠商整合

### 簡化入門

使用Commerce Cloud Manager自助布建入口網站，在幾分鐘內啟動沙箱和生產執行個體。 您所需的一切(包括銷售服務、Commerce Storefront和App Builder)都會自動設定，並與您的執行個體整合。

請參閱[快速入門](getting-started.md)，瞭解如何建立和管理Commerce執行個體。

### 順暢的升級

存取最新功能和增強功能，無需手動升級。 持續提供新功能和更新後，您不再需要手動修補，確保您能夠以低廉的總體擁有成本隨時存取最新功能。

雲端上Adobe Commerce的典型升級程式包含建立備份、複製執行個體、執行相容性工具以及修正程式碼衝突。 [!DNL Adobe Commerce as a Cloud Service]不再需要該專案。 新功能和安全性更新發行後，Adobe會傳送應用程式內通知給您。 您有30天的時間評估沙箱執行個體中的新功能，之後更新會自動套用至您的生產環境。

>[!NOTE]
>
>Adobe可保證所有更新的回溯相容性。 這表示套用更新時，不會破壞符合[API優先擴充性](https://developer.adobe.com/commerce/extensibility/)模型的現有功能或自訂。

### 協力廠商整合

開發人員可以使用完整的[GraphQL和REST API](https://developer.adobe.com/commerce/services/cloud/guides/)，將Commerce Foundation與協力廠商系統整合，並延伸Commerce功能。

## Experience Cloud整合

[!DNL Adobe Commerce as a Cloud Service]與所有Experience Cloud解決方案整合，以大規模提供[個人化的商務體驗](https://experienceleague.adobe.com/en/docs/commerce-admin/customers/customers-menu/personalize-scale#customers-menu)。

[Data Connection](../data-connection/overview.md)可解鎖有關購物者購買行為的深入分析，以便您可以使用其他Adobe Digital Experience產品跨所有管道建立個人化購物體驗。

## 優點

下列章節提供有關[!DNL Adobe Commerce as a Cloud Service]為業務和IT主管提供的權益資訊。

### 業務領導者

- **增加收入**：透過可提升SEO的高效能店面，促進自然流量。 建立個人化體驗，使用豐富的資料推動轉換。
- **擴充營運**：自動擴充服務可提供99.9%的可用性，滿足您業務的高峰需求。 轉出多個品牌和區域，並從單一執行個體支援B2B和B2C。 透過彈性的資料模型支援大型且複雜的產品目錄。
- **提升銷售商生產力**：使用AI支援的銷售服務來改善轉換。 原生實驗，直接在店面中。 管理店面體驗，透過簡單的檔案式撰寫或視覺化編輯器，在幾分鐘內建立豐富的體驗。
- **降低總體擁有成本(TCO)並加速創新**：隨時更新服務可讓您立即使用新功能。 從市集輕鬆安裝應用程式，啟動新功能。 將資源從繁瑣的維護中釋出，以專注於建立新功能。

### 資訊科技(IT)領導者

- **快速布建**：快速開始自助布建，只需幾分鐘即可完成。 所有服務皆已預先設定為緊密合作，以更快開始。 視需要布建沙箱以供開發人員實驗使用。
- **低廉的擁有成本**：永遠最新的服務不再升級。 使用自動套用的最新安全性修補程式，確保安全無虞並符合規範。 自動擴充，以因應最繁重的工作負荷。
- **高效能店面**：使用簡單的檔案式撰寫或視覺化編輯器，在幾分鐘內建立豐富的體驗。 使用AI支援的銷售服務來改善轉換。 店面內建的原生實驗。
- **更快速的創新**：將資源從繁瑣的維護中釋出，專注於建立提供商業價值的新功能。 使用全方位的擴充能力和以標準為基礎的技術(JavaScript、HTML、CSS和低程式碼工具)，建置差異化的體驗。 按一下以安裝協力廠商應用程式，將新功能新增至您的Commerce平台。

## 新功能解決方案

[管理員UI](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/guide-overview)是存取功能的主要介面，可管理後端商店作業、庫存、定價、促銷和客戶互動。 但是，[!DNL Adobe Commerce as a Cloud Service]提供獨特的解決方案，取代了Adobe Commerce雲端和內部部署專案中某些著名的功能。 下表說明[!DNL Adobe Commerce as a Cloud Service]中可用的功能和取代解決方案：

| 功能 | 解決方案 | 可用性 | 詳細資料 |
|---------|----------|--------------|--------|
| [數位資產管理](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/wysiwyg/gallery/media-gallery-asset-management) | [產品視覺效果](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/aem-asset-management/aem-assets-integration)或迷你DAM | 可用 | 健全的數位資產管理(DAM)系統與Adobe Experience Manager整合，用於管理多媒體內容。 或者，mini-DAM提供儲存和管理數位資產的基本資產管理工具。 |
| [內容管理系統(CMS)](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/guide-overview) | [Commerce店面](https://www.aem.live/) | 可用 | 基本的CMS可讓使用者使用檔案式撰寫輕鬆建立和管理檔案和網站內容。 此外，通用編輯器也允許跨多個平台進行更進階的內容管理和自訂。 |
| [內容暫存](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/staging/content-staging) | [目錄服務](../catalog-service/overview.md) | 藍圖 | 繫結至Adobe Experience Platform的目錄管理工具，可管理大型目錄。 |
| [頁面產生器](https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/guide-overview) | [Commerce店面](https://www.aem.live/) | 可用 | 基本的CMS可讓使用者使用檔案式撰寫輕鬆建立和管理檔案和網站內容。 此外，通用編輯器也允許跨多個平台進行更進階的內容管理和自訂。 |
| [付款](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/payments/payments) | [Adobe Commerce的付款服務](../payment-services/overview.md) | 可用 | 整合的支付服務，可促進安全且有效率的交易。 |
| [共用的目錄](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared) | [價格索引服務](../price-index/price-indexing.md) | 藍圖 | 分析定價資料，並根據各種因素建議產品的最佳定價策略。 |
| [URL重寫](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite) | [Commerce店面](https://www.aem.live/) | 可用 | 基本的CMS可讓使用者使用檔案式撰寫輕鬆建立和管理檔案和網站內容。 此外，通用編輯器也允許跨多個平台進行更進階的內容管理和自訂。 |
| [Visual Merchandiser](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/merchandising/visual-merch/visual-merchandiser) | [目錄服務](../catalog-service/overview.md) | 藍圖 | 繫結至Adobe Experience Platform的目錄管理工具，可管理大型目錄。 |
