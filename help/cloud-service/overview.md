---
title: '[!DNL Adobe Commerce as a Cloud Service] 概覽'
description: 瞭解 [!DNL Adobe Commerce as a Cloud Service]的主要功能和優點。
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
exl-id: 1b7e2731-4a10-4c2b-9bfc-8945729ed523
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"
source-git-commit: d46526db56dad08a8f865664c92d1214bbf063d8
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 0%

---


# [!DNL Adobe Commerce as a Cloud Service] 概覽

[!DNL Adobe Commerce as a Cloud Service]可讓企業提供並快速擴充數位作業，加速創新，進而提供彈性、擴充性和效率。 Adobe的雲端原生基礎結構會自動調整資源，以符合流量、訂單和目錄管理的高峰需求。

下表著重說明[!DNL Adobe Commerce as a Cloud Service]的支援產品：

<table style="table-layout:auto">
  <tr>
    <td align="left">
      <img src="../assets/icon-checkmark-circle-outline.svg" alt="核取記號" align="center"> <strong>Commerce店面</strong>
    </td>
    <td align="left">
      顧客導向的介面，購物者可在此瀏覽及購買產品
    </td>
  </tr>
  <tr>
    <td align="left">
      <img src="../assets/icon-checkmark-circle-outline.svg" alt="核取記號" align="center"> <strong>銷售服務</strong>
    </td>
    <td align="left">
      管理產品目錄、定價和存貨的後端服務
    </td>
  </tr>
  <tr>
    <td align="left">
      <img src="../assets/icon-checkmark-circle-outline.svg" alt="核取記號" align="center"> <strong>產品視覺效果</strong>
    </td>
    <td align="left">
      產品影像和媒體的數位資產管理
    </td>
  </tr>
  <tr>
    <td align="left">
      <img src="../assets/icon-checkmark-circle-outline.svg" alt="核取記號" align="center"> <strong>開發人員平台</strong>
    </td>
    <td align="left">
      建置自訂功能的核心開發工具和API
    </td>
  </tr>
</table>

## 架構

請參閱下列影片，瞭解[!DNL Adobe Commerce as a Cloud Service]架構的簡介。 說明此架構的圖表會顯示在影片下方。

>[!VIDEO](https://video.tv.adobe.com/v/3443278?captions=chi_hant&learn=on)

此圖表說明[!DNL Adobe Commerce as a Cloud Service]與所有Adobe Experience Cloud解決方案之間的資料流程。

![[!DNL Adobe Commerce as a Cloud Service]架構圖表](./assets/data-flow.svg){zoomable="yes"}

## Commerce店面

使用Adobe的[Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront?lang=zh-Hant) (由Edge Delivery Services提供技術支援)，透過Storefront Builder的簡單檔案式撰寫或視覺化編輯，在幾分鐘內建立豐富的體驗。

Commerce Storefront採用完全無周邊的分離式架構，可透過GraphQL API層提供所有銷售服務和資料。 此架構讓團隊可獨立於Commerce Foundation開發他們的前端，提供使用新興技術建立和測試新接觸點的靈活性。

>[!NOTE]
>
>[!DNL Adobe Commerce as a Cloud Service]不支援Luma店面。 如果您要從雲端或內部部署上的Adobe Commerce進行移轉，請參閱[現有店面](https://experienceleague.adobe.com/developer/commerce/storefront/discovery/?lang=zh-Hant#existing-storefronts)以取得移轉指南。

## 銷售服務與付款服務

Adobe提供豐富的智慧型可撰寫銷售服務，協助您支援關鍵業務目標。 這些服務也提供對大規模最佳化效能至關重要的應用程式開發介面。

- [即時搜尋](../live-search/overview.md) — 使用此AI支援的搜尋工具，為購物者提供更聰明、更快速且相關的結果。
- [產品推薦](../optimizer/merchandising/recommendations/overview.md) — 根據購物者行為、熱門趨勢、產品相似性等新增AI輔助推薦。
- [目錄服務](../catalog-service/guide-overview.md) — 提供客戶最佳化的產品體驗，同時提升效能、改善擴充能力，並提高轉換率。
- [付款服務](../payment-services/guide-overview.md) — 提供多種付款方式，包括免息分期付款，以及付款處理、訂單和發票的單一檢視，以提升客戶滿意度。

## 由AEM Assets支援的產品視覺效果

產品視覺效果使用數位資產管理(DAM)系統協助簡化資產管理，此系統與Adobe Experience Manager整合以管理多媒體內容。

整合可根據SKU或其他關鍵屬性，確保數位資產（例如產品影像或行銷內容）動態連結至適當的銷售實體，包括Adobe Commerce中的產品和類別。

產品視覺效果現成可與[!DNL Adobe Commerce as a Cloud Service]搭配使用，提供AEM Assets的部分功能。

另外，[!DNL Adobe Commerce as a Cloud Service]中的原生功能可提供儲存和管理數位資產的基本資產管理工具。

檢視[AEM Assets整合](../aem-assets-integration/overview.md)指南，深入瞭解如何將AEM Assets支援的產品視覺效果與[!DNL Adobe Commerce as a Cloud Service]整合。

### 產品視覺效果或AEM Assets

以下比較可協助您選取最符合內容supply chain需求的選項：

<table>
  <tr>
    <td align="left">
      <strong>由AEM Assets支援的產品視覺效果</strong>
      <ul>
        <li>整合式自動化產品影像和視訊數位資產管理器(DAM)</li>
        <li>調整大小、裁切和轉換影像</li>
        <li>高速影像和視訊傳送</li>
        <li>根據使用者端瀏覽器功能最佳化影像格式、大小和品質</li>
        <li>存取Adobe Express和Adobe Firefly</li>
        <li>影像/視訊傳遞容量和使用者存取的使用量限制</li>
        <li>整合式資產選擇器</li>
      </ul>
    </td>
    <td align="center">
      <br><br><br><br><br><br><br><br><br><br><br>
      <img src="../assets/icon-double-chevron-right.svg" alt="V形" width="100">
    </td>
    <td align="left">
      <strong>AEM Assets</strong>
      <ul>
        <li>產品視覺效果的所有功能</li>
        <li>Full Marketing Digital Asset Manager (DAM)</li>
        <li>無限制的使用者（依使用者付費）</li>
        <li>影像和視訊傳遞無限制</li>
        <li>進階資產管理功能：</li>
        <ul>
          <li>360°迴轉集與互動式檢視器</li>
          <li>3D模型支援和沈浸式內容</li>
          <li>PDF支援</li>
          <li>AI支援的智慧型裁切</li>
          <li>動態影像範本</li>
          <li>智慧標籤</li>
          <li>追蹤及分析資產績效</li>
        </ul>
      </ul>
    </td>
  </tr>
    <tr>
    <td align="center" colspan="3">
      <strong>Adobe品牌整合可讓您在不同方案之間輕鬆進行移轉。</strong>
    </td>
  </tr>
</table>

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

使用[!UICONTROL Commerce Cloud Manager]自助布建入口網站，在幾分鐘內啟動沙箱和生產執行個體。 您所需的一切功能(包括銷售服務、Headless Commerce執行個體和App Builder)都會自動設定，並與執行個體整合。

請參閱[快速入門](getting-started.md)，瞭解如何建立和管理Commerce執行個體。

### 順暢的升級

存取最新功能和增強功能，無需手動升級。 持續提供新功能和更新後，您不再需要手動修補，確保您能夠以低廉的總體擁有成本隨時存取最新功能。

雲端上Adobe Commerce的典型升級程式包含建立備份、複製執行個體、執行相容性工具以及修正程式碼衝突。 [!DNL Adobe Commerce as a Cloud Service]不再需要該專案。 新功能和安全性更新發行後，Adobe會傳送應用程式內通知給您。 您有30天的時間評估沙箱執行個體中的新功能，之後更新會自動套用至您的生產環境。

>[!NOTE]
>
>Adobe可保證所有更新的回溯相容性。 這表示套用更新時，不會破壞符合[API優先擴充性](https://developer.adobe.com/commerce/extensibility/)模型的現有功能或自訂。

### 協力廠商整合

開發人員可以使用完整的[GraphQL](https://developer.adobe.com/commerce/webapi/graphql/)和[REST API](https://developer.adobe.com/commerce/webapi/rest/)，將Commerce Foundation與協力廠商系統整合，並延伸Commerce功能。

<!-- ## Experience Cloud integration

[!DNL Adobe Commerce as a Cloud Service] integrates with all Experience Cloud solutions to deliver [personalized commerce experiences at scale](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/customers/customers-menu/personalize-scale#customers-menu).

[Data Connection](../data-connection/overview.md) unlocks insights about your shoppers' buying behavior so that you can create personalized shopping experiences across all channels with other Adobe Digital Experience products. -->

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
