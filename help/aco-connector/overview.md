---
title: Adobe Commerce Optimizer聯結器
description: 瞭解如何將資料從Commerce雲端或內部部署專案連線到Adobe Commerce Optimizer
feature: Personalization, Integration, Configuration
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案(Adobe管理的PaaS基礎結構)和內部部署專案的Adobe Commerce 。"
source-git-commit: 380d2c91a17a3e6b84d435774de1b05ada7d3a52
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---


# Adobe Commerce Optimizer聯結器

Adobe Commerce Optimizer Connector是整合橋接器，可在雲端基礎結構或內部部署上的Adobe Commerce與[!DNL Adobe Commerce Optimizer]之間同步目錄和定價資料。 將資料同步至Adobe Commerce Optimizer可啟用如動態AI 搜尋、建議、快速載入Headless店面等功能，包括Edge Delivery Services上的Adobe Commerce店面，以及即時效能分析。

## 架構與體驗

Adobe Commerce Optimizer Connector的運作方式是將應Commerce網站和商店檢視至Commerce Optimizer專案，如下圖所示：

![將Commerce資料對應至Adobe Commerce Optimizer](./assets/storeview-to-catalogview-mapping.svg){width="600" zoomable="yes"}

將資料從Commerce匯出至Commerce Optimizer時：

* Commerce存放區檢視已對應至目錄來源
* 網站對應至價格手冊

會匯出關聯的目錄和價格資料，稍後再用來建立目錄檢視，以及選擇性地定義原則，以篩選特定業務使用案例的目錄和價格資料。

您不必透過Commerce Admin設定和管理Commerce服務（即時搜尋和產品建議），而是使用[[!DNL Adobe Commerce Optimizer] 銷售工具](../optimizer/merchandising/overview.md)來管理產品探索（即時搜尋）和建議（產品建議）規則設定。 Adobe Commerce例項會成為目錄和價格資料的資料來源。 在Commerce中更新資料時，更新會同步至[!DNL Adobe Commerce Optimizer]執行個體。

## 工作流程

聯結器可啟用數個關鍵工作流程：

* **將Commerce目錄資料匯出至[!DNL Adobe Commerce Optimizer]** — 在網站和客戶群組層級匯出價格和價格簿資料。 產品和產品屬性資料會匯出至`store view`層級。 依預設，所有Commerce範圍（網站和商店檢視）的目錄資料同步已啟用。

  若要啟用此工作流程，請安裝`adobe-commerce/commerce-data-export-aco-adapter` PHP擴充功能、檢閱匯出程式設定，然後從Commerce管理員啟用Commerce與Commerce Optimizer之間的整合。 如需詳細指示，請參閱[開始使用](#get-started)。

* **對應Commerce網站並儲存檢視資料以匯出至[!DNL Adobe Commerce Optimizer]**

  或者，自訂匯出設定，以僅同步特定網站或商店檢視的資料。 例如，您可以選擇只匯出一個商店檢視的目錄資料以用於特定使用案例，例如最佳化特定市場或區域的搜尋和探索體驗。

* **銷售規則組態與管理**

  聯結器啟用時，產品探索和建議的銷售規則會從[!DNL Adobe Commerce Optimizer] UI定義和管理，而非從Commerce管理員的[!UICONTROL Live Search]和[!UICONTROL Product Recommendations]頁面定義和管理。

* **在Edge Delivery Services上部署您的Commerce店面**

  在設定與[!DNL Adobe Commerce Optimizer]的整合後，您可以在Edge Delivery Services上設定並部署Commerce店面，以透過[!DNL Adobe Commerce Optimizer]提供的可組合、API導向的架構和模組化元件，提供超快速的效能、擴充能力、順暢的內容製作、整合式個人化，並降低營運成本。

如需有關如何設定整合及啟用這些工作流程的詳細資訊，請參閱[開始使用](get-started.md)。
