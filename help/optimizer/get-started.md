---
title: 開始使用
description: 瞭解如何開始使用 [!DNL Adobe Commerce Optimizer]。
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"
source-git-commit: f49a86b8793e2d91413acfbc0b922cb94db67362
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 0%

---

# 開始使用

本文會逐步引導您瞭解[!DNL Adobe Commerce Optimizer]的最新資訊。 雖然本指南的重點是銷售人員和管理員角色，它確實包括開發人員將執行的簡短高層級任務。 如需開發人員特定內容的詳細資訊，請參閱[開發人員檔案](https://developer-stage.adobe.com/commerce/services/composable-catalog/)。

## 您的角色為何？

成功設定[!DNL Adobe Commerce Optimizer]通常涉及下列團隊成員：

- 管理員
- 開發人員
- 銷售商

每個專案團隊成員都有各自的一組角色和職責，如下表所述：

| 角色 | 任務 |
|---|---|
| 管理員 | 使用Admin Console來建立管理員、使用者群組、使用者和開發人員&#x200B;。 |
|  | 在Commerce Cloud管理員中建立新的[!DNL Adobe Commerce Optimizer]執行個體&#x200B;。 |
|  | 設定您的原則和目錄檢視。 |
| 開發人員 | 使用Developer Console建立專案、授予開發人員API存取權，以及安裝必要的應用程式和自訂。 |
|  | 使用API Mesh和App Builder連線至您的後台系統（購物車、結帳）&#x200B;。 |
|  | 使用Merchandising Services資料擷取API，從您現有的商務解決方案擷取目錄資料&#x200B;。 |
|  | 設定您的店面 |
| 銷售商 | 設定產品探索&#x200B;。 |
|  | 設定產品推薦。 |

每個角色都是成功上線和啟動[!DNL Adobe Commerce Optimizer]環境的必要部分。 下圖顯示貴組織中每個角色的高階開始至完成工作流程：

![高階工作流程](./assets/high-level-workflow.png){zoomable="yes"}

### 管理員

管理員負責設定執行個體，管理組織的使用者、群組和權益。

- **[存取Adobe Admin Console](https://helpx.adobe.com/tw/enterprise/admin-guide.html)** — 管理整個組織的Adobe權益。 請參閱[使用者管理](./user-management.md)，瞭解您或您組織的產品管理員或系統管理員如何新增使用者至[!DNL Adobe Commerce Optimizer]產品。

- **建立執行個體** - [!DNL Adobe Commerce Optimizer]執行個體使用信用型系統。 您可以建立多個沙箱和生產執行個體，每個執行個體都需要一個對應的評分。 您最初的退款金額取決於您的訂閱。 [了解更多](#create-an-instance)。

- **存取執行個體** — 建立執行個體後，您可以從[!UICONTROL Commerce Cloud Manager]存取它。 [了解更多](#access-an-instance)。

- **設定目錄檢視和原則** — 瞭解如何[定義您的目錄檢視和原則](./setup/catalog-view.md)。 目錄不僅包含您的產品資料，也可協助您定義業務結構。

### 開發人員

開發人員建立專案和認證、安裝擴充功能、擷取目錄資料，以及執行一般平台架構工作。 如需開發人員特定內容的詳細資訊，請參閱[開發人員檔案](https://developer-stage.adobe.com/commerce/services/composable-catalog/)。

- **存取Developer Console** — 存取[Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started)以建立[!DNL Adobe Commerce Optimizer]的專案、產生存取權杖並安裝必要的應用程式和自訂。

- **擷取目錄資料** — 請參閱[資料擷取API](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/)檔案，瞭解如何將目錄資料匯入[!DNL Adobe Commerce Optimizer]。

  內嵌的目錄資料會顯示在[資料同步](./setup/data-sync.md)頁面中。

- **設定店面** — 在設定店面之前，您必須先建立執行個體，這項工作通常由您組織的[管理員](#administrator)執行。 建立執行個體後，您就可以繼續[設定](./storefront.md)由Edge Delivery Services支援的Commerce店面。

### 銷售商

該銷售人員會使用購物者資料和分析，針對店面的產品放置、定價和促銷活動進行策略決策，同時透過產品探索和建議最佳化購物體驗。

- **設定產品探索和建議** — 瞭解如何透過產品探索和建議[為您的購物者](./merchandising/overview.md)建立個人化體驗。

## 建立執行個體

1. 登入您的[Adobe Experience Cloud](https://experience.adobe.com/)帳戶。

1. 在[!UICONTROL Quick access]底下，按一下&#x200B;[!UICONTROL **Commerce**]&#x200B;以開啟[!UICONTROL Commerce Cloud Manager]。

   [!UICONTROL Commerce Cloud Manager]會顯示您的Adobe IMS組織中可用的[!DNL Adobe Commerce]執行個體清單，包括為[!DNL Adobe Commerce Optimizer]和[!DNL Adobe Commerce as a Cloud Service]布建的執行個體。

1. 按一下畫面右上角的&#x200B;[!UICONTROL **新增執行個體**]。

   ![建立執行個體](./assets/create-aco-instance.png){width="100%" align="center" zoomable="yes"}

1. 選取&#x200B;[!UICONTROL **Commerce Optimizer**]。

1. 輸入您執行個體的&#x200B;**名稱**&#x200B;和&#x200B;**描述**。

1. 選取您要託管執行個體的區域。

   >[!NOTE]
   >
   >建立例證之後，便無法變更區域。

1. 為您的執行個體選擇下列&#x200B;[!UICONTROL **環境型別**]&#x200B;之一：

   - [!UICONTROL **沙箱**] — 適用於設計和測試用途。 您應該使用沙箱環境來開始您的[!DNL Adobe Commerce Optimizer]歷程。
   - [!UICONTROL **生產**] — 用於線上商店和客戶對面的網站。

   >[!NOTE]
   >
   >沙箱例專案前僅限北美區域使用。

1. 按一下&#x200B;[!UICONTROL **新增執行個體**]。

   新執行個體現在可在Cloud Manager中使用。

1. 若要檢視執行個體詳細資訊(包括GraphQL和目錄服務端點、存取Adobe Commerce Optimizer應用程式的URL，以及執行個體ID （租使用者ID）)，請按一下執行個體名稱旁的資訊圖示。

   ![建立執行個體](./assets/aco-instance-details.png){width="100%" align="center" zoomable="yes"}

## 存取例項

1. 登入您的[Adobe Experience Cloud](https://experience.adobe.com/)帳戶。

1. 在[!UICONTROL Quick access]底下，按一下&#x200B;[!UICONTROL **Commerce**]&#x200B;以開啟[!UICONTROL Commerce Cloud Manager]。

   [!UICONTROL Commerce Cloud Manager]會顯示您的Adobe IMS組織中可用的執行個體清單。

1. 若要開啟與執行個體相關聯的[!UICONTROL Commerce Optimizer]應用程式，請按一下執行個體名稱。


