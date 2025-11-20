---
title: 開始使用 [!DNL Adobe Commerce as a Cloud Service]
description: 瞭解如何開始使用 [!DNL Adobe Commerce as a Cloud Service]。
role: Admin, Developer, User
exl-id: 58d98b9e-b41d-44db-9666-c924a5b005b3
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"
source-git-commit: 69870bc7037bdad5a8d5fa769a06c07f8cd920aa
workflow-type: tm+mt
source-wordcount: '1298'
ht-degree: 0%

---

# 快速入門

[!DNL Adobe Commerce as a Cloud Service]提供大部分的立即可用設定。 完成幾個基本設定程式後，您的存放區將立即啟動並執行。 本指南會逐步引導您建立和使用執行個體。 本指南也可協助您設定組織以取得成功，方法是確保您的團隊有適當許可權存取[!DNL Adobe Commerce as a Cloud Service]以及開始使用所需的工具。

[!DNL Adobe Commerce as a Cloud Service]是雲端原生commerce平台，提供彈性、擴充性和效率，用於提供數位商務體驗。 此SaaS產品是完全受管理、無版本的平台，可提供順暢的升級體驗，無需手動干預。

## 主要元件

[!DNL Adobe Commerce as a Cloud Service]包含下列元件：

* **[Adobe Experience Cloud](https://experience.adobe.com/)** — 您在[!DNL Adobe Commerce]experience.adobe.com[所有](https://experience.adobe.com/)產品的中心進入點
   * 按一下「[!UICONTROL **快速存取**]」底下的「[!UICONTROL **Commerce**]」以開啟「Commerce Cloud管理員」
* **[Commerce Cloud管理員](https://experience.adobe.com/#/commerce/cloud-service)** — 建立和管理執行個體、存取API URL和您的Commerce管理員
* **[Adobe Admin Console](https://adminconsole.adobe.com/)** — 管理使用者和角色
* **Commerce管理員** — 管理產品、訂單、客戶和商店設定
* **[由Edge Delivery Services提供支援的店面](./storefront.md)** — 使用可撰寫的高效能系統，為商家和開發人員提供卓越的速度、SEO和使用者體驗，建立並自訂面對客戶的店面
* **[Adobe Developer App Builder](https://developer.adobe.com/app-builder/)** — 使用App Builder以及其他擴充性工具（例如[整合入門套件](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/)和[API Mesh](https://developer.adobe.com/graphql-mesh-gateway/)）建立自訂整合

## 設定與管理

在[!DNL Adobe Commerce as a Cloud Service]設定程式中，您的系統管理員、商家和開發人員會設定您組織的存取權和資源，包括布建雲端資源，以及根據使用者的職責為其指派適當的角色。

### 設定和管理工作流程

作為合併的群組，系統管理員、商家和開發人員需要遵循以下基本步驟來啟動和執行您的Commerce執行個體：

1. **所有使用者**： [建立執行個體](#create-an-instance)
1. **系統管理員**： [新增使用者並指派角色](user-management.md#add-users-and-admins)
1. **商家**： [存取Commerce Admin](#access-an-instance)並[匯入您的目錄](#import-your-catalog)
1. **開發人員**： [設定您的店面](storefront.md)並探索[開發人員平台](overview.md#developer-platform)

#### AEM Assets和產品視覺效果工作流程

需要下列步驟才能將[!DNL Adobe Experience Manager Assets]或[!DNL Product Visuals powered by AEM Assets]與[!DNL Adobe Commerce as a Cloud Service]整合：

1. **系統管理員**： [將使用者新增至AEM Assets和產品視覺效果產品設定檔](user-management.md#add-a-user-to-aem-assets-or-product-visuals)
1. **開發人員**： [整合AEM Assets和產品視覺效果](../aem-assets-integration/overview.md)
1. **商家**： [存取您的AEM Assets和產品視覺效果](./user-management.md#access-the-experience-manager-interface)

### 角色型設定和管理工作

選取下方的標籤，檢視對應角色的高階工作流程圖形：

>[!BEGINTABS]

>[!TAB 系統管理員與商家工作流程]

此圖表提供系統管理員和商家如何存取及管理[!DNL Adobe Commerce as a Cloud Service]執行個體的概觀。 如需有關管理員工作流程的詳細資訊，請參閱[Adobe Admin Console指南](https://helpx.adobe.com/enterprise/admin-guide.html)。

![[!DNL Adobe Commerce as a Cloud Service]商家流程圖](./assets/merchant-flow.svg){zoomable="yes"}

>[!TAB 開發人員工作流程]

此圖表提供開發人員如何使用App Builder為[!DNL Adobe Commerce as a Cloud Service]建立整合的整體概觀。 如需詳細資訊，請參閱[API檔案](https://developer.adobe.com/commerce/webapi/rest/)。

![[!DNL Adobe Commerce as a Cloud Service]開發人員流程圖](./assets/developer-flow.svg){zoomable="yes"}

>[!ENDTABS]

選取您的角色，尋找開始設定程式的資源：

>[!BEGINTABS]

>[!TAB 系統管理員]

作為系統管理員，您負責設定組織並管理使用者存取權。

| 任務 | 說明 | 資源 |
|------|-------------|----------|
| 瞭解平台 | 瞭解Adobe Commerce as a Cloud Service架構和優點 | [總覽](overview.md) |
| 比較功能 | 瞭解Cloud Service與其他Adobe Commerce方案之間的差異 | [功能比較](feature-comparison.md) |
| 建立執行個體 | 布建沙箱和生產環境 | [建立執行個體](#create-an-instance) |
| 設定使用者管理 | 新增使用者、指派角色及管理許可權 | [使用者管理](user-management.md) |
| 設定AEM Assets和產品視覺效果（選用） | 新增使用者、指派角色及管理許可權 | [使用者管理](user-management.md#add-a-user-to-aem-assets-or-product-visuals) |

>[!TAB 商家]

身為商家，您專注於管理產品、訂單和店面內容。

| 任務 | 說明 | 資源 |
|------|-------------|----------|
| 存取您的執行個體 | 登入Commerce管理員以管理您的存放區 | [存取執行個體](#access-an-instance) |
| 探索使用案例 | 瞭解實用的業務案例和工作流程 | [使用案例](./use-cases.md) |
| 匯入目錄 | 瞭解如何將產品資料匯入平台 | [匯入您的目錄](#import-your-catalog) |
| 存取AEM Assets和產品視覺效果（選用） | 存取Experience Manager以開始使用AEM Assets和產品視覺效果 | [存取Experience Manger介面](./user-management.md#access-the-experience-manager-interface) |

>[!TAB 開發人員]

身為開發人員，您需要瞭解如何建立自訂整合併擴充平台功能。

| 任務 | 說明 | 資源 |
|------|-------------|----------|
| 瞭解架構 | 瞭解平台的擴充功能和API | [概觀 — 開發人員平台](overview.md#developer-platform) |
| 設定開發環境 | 建立沙箱例項以供開發和測試 | [建立執行個體](#create-an-instance) |
| 建立店面 | 瞭解如何設定和自訂Commerce店面 | [店面設定](./storefront.md) |
| 設定您的店面 | 瞭解如何設定您的店面 | [店面設定](./storefront.md) |
| 探索整合選項 | 瞭解關於App Builder、API Mesh和您有權存取的其他擴充工具 | [概觀 — 開發人員平台](overview.md#developer-platform) |
| 整合AEM Assets和產品視覺效果（選用） | 瞭解如何將AEM Assets和產品視覺效果與Adobe Commerce整合 | [AEM Assets整合](../aem-assets-integration/overview.md) |

>[!ENDTABS]

### 後續步驟

完成您的角色特定設定工作後：

* **系統管理員**：檢閱[共擔責任](shared-responsibility.md)指南
* **商家**：探索[使用案例](use-cases.md)以瞭解常見的業務案例
* **開發人員**：檢視[Adobe Commerce開發人員檔案](https://developer.adobe.com/commerce/docs)

## Adobe Commerce as a Cloud Service基本需知

以下小節說明您需要完成的基本流程，才能讓Commerce執行個體正常運作。

### 建立執行個體

>[!NOTE]
>
>在您建立執行個體之前，您組織的產品管理員或系統管理員必須將您新增為[!DNL Adobe Commerce as a Cloud Service]產品的使用者。 如需詳細資訊，請參閱[新增使用者和管理員](./user-management.md#add-users-and-admins)。

[!DNL Adobe Commerce as a Cloud Service]執行個體使用信用型系統。 您可以建立多個執行個體，但每個執行個體都需要可用的學分。 您一開始擁有的積分數目取決於您的訂閱。

1. 登入您的[Adobe Experience Cloud](https://experience.adobe.com/)帳戶。

1. 在[!UICONTROL Quick access]底下，按一下&#x200B;[!UICONTROL **Commerce**]&#x200B;以開啟[!UICONTROL Commerce Cloud Manager]。

   [!UICONTROL Commerce Cloud Manager]會顯示您的Adobe IMS組織中可用的[!DNL Adobe Commerce as a Cloud Service]執行個體清單。

1. 按一下畫面右上角的&#x200B;[!UICONTROL **新增執行個體**]。

   ![建立執行個體](./assets/create-instance.png){width="50%" align="center" zoomable="yes"}

1. 選取&#x200B;[!UICONTROL **Commerce as a Cloud Service**]。

1. 輸入您執行個體的&#x200B;**名稱**&#x200B;和&#x200B;**描述**。

1. 為您的執行個體選擇&#x200B;[!UICONTROL **環境型別**]。 您可以選擇下列選項：

   * [!UICONTROL **沙箱**] — 僅供設計和測試之用。 您應該使用沙箱環境來開始您的[!DNL Adobe Commerce as a Cloud Service]歷程。

   >[!NOTE]
   >
   > 沙箱執行個體僅供設計和測試用途。 您不應在沙箱環境中使用任何生產資料。
   >
   >沙箱例項僅限北美區域使用。

   * [!UICONTROL **生產**] — 用於線上商店和客戶對面的網站。

   >[!NOTE]
   >
   >Adobe Commerce as a Cloud Service的基礎設施可在全球使用。 如需您所在地區生產環境的詳細資訊，請聯絡您的客戶服務代表。

1. 選取您要託管執行個體的區域。

   >[!NOTE]
   >
   >建立執行個體後，您將無法修改區域。

1. 按一下&#x200B;[!UICONTROL **新增執行個體**]。

### 存取例項

建立執行個體後，您可以從[!UICONTROL Commerce Cloud Manager]存取它。

1. 登入您的[Adobe Experience Cloud](https://experience.adobe.com/)帳戶。

1. 在[!UICONTROL Quick access]底下，按一下&#x200B;[!UICONTROL **Commerce**]&#x200B;以開啟[!UICONTROL Commerce Cloud Manager]。

   [!UICONTROL Commerce Cloud Manager]會顯示您的Adobe IMS組織中可用的執行個體清單。

1. 若要開啟執行個體的[!UICONTROL Commerce Admin]，請按一下執行個體名稱。

>[!TIP]
>
>若要檢視執行個體的相關資訊，包括REST和GraphQL端點以及管理員URL，請按一下執行個體名稱旁邊的資訊圖示。

管理員和端點的基礎URL會因地區和環境而異，使用下列模式：

* 管理員
   * 北美生產系統管理員： `https://na1.admin.commerce.adobe.com`
   * 北美沙箱管理員： `https://na1-sandbox.admin.commerce.adobe.com`
   * 歐洲生產系統管理員： `https://eu1.admin.commerce.adobe.com`
* REST和GraphQL
   * 北美生產GraphQL： `https://na1.api.commerce.adobe.com`
   * 北美洲沙箱GraphQL： `https://na1-sandbox.api.commerce.adobe.com`
   * 歐洲生產GraphQL： `https://eu1.api.commerce.adobe.com`

### 匯入您的目錄

根據預設，[!DNL Adobe Commerce as a Cloud Service]執行個體不包含任何產品資料。 在匯入您自己的目錄之前，當您建立例項以進行測試和學習時，可以選擇包含範例產品資料。

有兩種方式可將您的目錄匯入[!DNL Adobe Commerce as a Cloud Service]：

* [**Commerce管理員**](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/import/data-import) — 使用者易記的介面，可讓您按幾下滑鼠即可匯入目錄資料。
* [**匯入JSON API**](https://developer.adobe.com/commerce/webapi/rest/modules/import/#import-json-api) - REST API可讓您以程式設計方式匯入目錄資料。

### 設定店面

現在您已建立執行個體，您已準備好[設定您的店面](storefront.md) (由Edge Delivery Services提供技術支援)。

## 其他資源

* [發行說明](release-notes.md)
* [移轉指南](migration/overview.md)
* [Commerce Storefront檔案](https://experienceleague.adobe.com/developer/commerce/storefront/)
