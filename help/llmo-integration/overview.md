---
title: 整合 [!DNL Adobe Commerce] 與 [!DNL Adobe LLM Optimizer]
description: 連線 [!DNL Adobe Commerce] 至 [!DNL Adobe LLM Optimizer] 以監視LLM中的目錄訊號，並部署核准的目錄最佳化。
role: Admin, User, Leader
recommendations: noCatalog
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案（Adobe管理的PaaS基礎結構）和內部部署專案的Adobe Commerce 。"
source-git-commit: 47348a44ff7c5f890c10594f44cae6e771be046f
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# 將[!DNL Adobe Commerce]與[!DNL Adobe LLM Optimizer]整合

>[!IMPORTANT]
>
>存取此整合受到限制。 如需詳細資訊，請聯絡您的技術客戶經理。

[!DNL Adobe LLM Optimizer]是企業解決方案，可協助品牌監視、分析和最佳化其內容在大型語言模型(LLM)和AI助理的回答中的顯示方式。 隨著購物者越來越多地使用AI工具進行研究和產品探索，LLM Optimizer有助於確保您的品牌和目錄被準確引用並在上下文中浮現。

本指南說明當您的產品目錄儲存在Commerce中時，**[!DNL Adobe Commerce]**&#x200B;如何適應該工作流程。 您將瞭解哪些功能可用、需要哪些設定，以及部署的最佳化在管理員和各個擷取管道中的行為方式。

>[!NOTE]
>
>[!DNL Adobe LLM Optimizer]是獨立的Adobe解決方案。 核心監控和商機工作流程不需要[!DNL Adobe Experience Manager] (AEM)或其他Adobe應用程式。 Commerce專屬部署動作僅適用於您的目錄已連線至LLM Optimizer，且您選擇推送已核准的變更至[!DNL Adobe Commerce]時。

## 整合可讓哪些方面受益 {#what-integration-enables}

將LLM Optimizer連線至您的[!DNL Adobe Commerce]目錄可讓您從廣泛的內容深入分析移至&#x200B;**目錄感知**&#x200B;建議：

- **識別目錄資料（例如標題、說明和結構化訊號）中**&#x200B;的空白和不一致，這些會影響LLM解譯您產品的方式。
- **檢閱**&#x200B;支援內容的建議改進，包括理由和前後比較。
- **將**&#x200B;選取的最佳化（例如產品名稱和說明更新）直接部署到Commerce目錄，確保管理工作流程、網格和店面資料保持一致。

當目錄來源為[!DNL Adobe Commerce]時，Adobe可支援完整的端對端工作流程：自動識別商機、建議變更並套用已核准的修正。 對於源自Commerce外部的目錄，LLM Optimizer仍可分析並提出改進建議，但套用變更取決於您的整合模型（例如，映象目錄或手動更新）。 請參閱[整合限制與界限](boundaries-limits.md)。

## 這是給誰的 {#who-this-is-for}

- **數位行銷人員和銷售人員**&#x200B;想要產品資料在LLM導向的答案中準確且一致，以及需要控制方式以大規模改善目錄複製情形。
- **Commerce管理員**，擁有目錄完整性、管理流程，以及提供產品屬性的整合(API、CSV、PIM)。

## 先決條件 {#prerequisites}

您有&#x200B;**存取權** Adobe Commerce與Adobe LLM Optimizer的整合時，便適用下列必要條件。 如需詳細資訊，請聯絡您的技術客戶經理。

- 您的店面可由LLM導向和代理機器人抓取，其中此抓取功能是LLM Optimizer測量和最佳化策略的一部分（目錄感知深入分析的一般先決條件）。
- 對於Commerce支援的部署工作流程，必要的Commerce服務和目錄連線已啟用且狀況良好。 任務層級設定在[將Adobe Commerce連線至LLM Optimizer](get-started/connect-to-llmo.md)中說明。

您也應該瞭解資料如何在系統之間移動：

### 高階資料流 {#high-level-data-flow}

從概念上來說，目錄最佳化遵循兩種模式（視功能而定，您的專案可能使用其中一種模式或同時使用兩者）：

| 方向 | 用途 |
| --- | --- |
| **Commerce目錄 — > LLM Optimizer** | 目錄和URL訊號為LLM Optimizer UI中的商機與建議提供資訊。 |
| **LLM Optimizer -> Commerce** | 在您核准部署動作後，產品名稱和說明的更新會寫入主要Commerce目錄，讓管理員和店面都能反映最佳化的值。 |

### 與協力廠商目錄比較[!DNL Adobe Commerce] {#commerce-vs-third-party}

| 目錄來源 | 一般LLM Optimizer涵蓋範圍 |
| --- | --- |
| **[!DNL Adobe Commerce]** | 對識別和建議提供強大支援，並部署您設定的已核准目錄欄位更新。 |
| **協力廠商商務** | 支援識別與建議；自動部署到商家系統取決於匯出、映象或合作夥伴工作流程，而不是直接寫入商家的來源目錄。 |

## 目錄代理程式、Storefront MCP和LLM Optimizer {#catalog-agent-and-mcp}

您的[!DNL Adobe Commerce] **產品目錄**&#x200B;是產品資料的記錄系統：名稱、說明、屬性、定價及詳細目錄。 為了支援AI輔助的探索和最佳化，**Adobe Commerce Storefront MCP** （模型內容通訊協定）是您即時Commerce目錄資料與Adobe AI體驗之間的結構化介面。

**目錄代理程式**&#x200B;位於Storefront MCP上方。 目錄代理程式可讓[!DNL Adobe LLM Optimizer]透過找出差距、提出改進專案，並在您核准變更時部署變更，來查詢、擴充目錄及PDP內容並據以執行。 在[搭配Adobe Commerce使用LLM Optimizer](get-started/use-llmo-with-commerce.md)中說明的LLM Optimizer工作流程中，會顯示這些功能。

## 目錄代理程式如何改善LLM的Commerce {#catalog-agent-optimizations}

目錄代理程式會透過兩個互補最佳化來處理可發現性：產品詳細資料頁面擴充和產品目錄擴充。

### 產品詳細資料頁面擴充 {#pdp-enrichment-overview}

**產品詳細資料頁面(PDP)擴充**&#x200B;建議對產品頁面內容進行細分，這樣當購物者透過AI助理和類似工具發現產品時，您的商品就會閱讀得更清楚。 目標是改善清晰度和一致性，同時不變更團隊已銷售店面的版面配置。 您可在LLM Optimizer中檢閱建議，並在準備就緒後進行部署。

部署後，點選檢查即時產品頁面，確認購物體驗仍如您預期般顯示。

### 產品目錄擴充 {#catalog-enrichment-overview}

**產品目錄擴充**&#x200B;建議更清楚的&#x200B;**產品名稱**&#x200B;和&#x200B;**產品說明**，其中副本較細、模糊或不一致。 每個建議都包含內容，讓您的團隊可以決定要變更的內容。 當您核准更新時，更新可套用至您的[!DNL Adobe Commerce]目錄，以便管理員、店面和使用這些欄位的其他體驗反映相同的措辭。

因為這些欄位位於Commerce中，只要改善一次名稱或說明，就能讓每個讀取該產品資料的管道受益（取決於系統重新整理的方式和時間）。

## 相關主題 {#related-topics}

- [將Adobe Commerce連線至LLM Optimizer](get-started/connect-to-llmo.md)
- [搭配Adobe Commerce使用LLM Optimizer](get-started/use-llmo-with-commerce.md)
- [整合限制和邊界](boundaries-limits.md)
