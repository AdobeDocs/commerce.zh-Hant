---
title: 使用者管理
description: 瞭解如何建立及管理 [!DNL Adobe Commerce Optimizer]的使用者並指派使用者角色。
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"
exl-id: 9ab2118d-b7e3-4e2e-adac-8f3950fe1824
source-git-commit: 36a953d4fb0e1e14c7cb88a80f3b59d6fe8eb49e
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# 使用者管理

若要啟用[!DNL Adobe Commerce Optimizer]的存取權，請從[Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"}新增使用者，並確定他們有權存取Commerce產品。

您可以將使用者指派給下列任何角色：

- **使用者** — 使用者可以存取[!DNL Adobe Commerce Optimizer] UI，以檢視及管理目錄檢視與銷售規則，以及追蹤效能度量。

- [**開發人員**](https://helpx.adobe.com/tw/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"} — 開發人員擁有使用者許可權和存取Adobe Developer Console的許可權。 這表示他們可以建立專案並設定認證，以使用[!DNL Adobe Commerce Optimizer] API和SDK等開發人員工具，以及App Builder和API Mesh等Adobe擴充性工具。

- **管理員** — 有三種不同型別的管理員角色：
   - [系統管理員](https://helpx.adobe.com/tw/enterprise/using/admin-roles.html){target="_blank"} — 系統管理員可以透過Adobe Admin Console存取組織中的所有產品和產品設定檔。
   - [產品管理員](#add-a-product-admin) — 產品管理員可以在[中](#add-users-and-admins)管理產品[!DNL Adobe Admin Console]的使用者、角色和許可權。
   - [產品設定檔管理員](#add-users-developers-and-product-profile-admins) — 產品設定檔管理員可以在[!DNL Adobe Admin Console]中管理產品的使用者。

## 新增產品管理員

>[!BEGINTABS]

>[!NOTE]
>
>將產品管理員新增為產品管理員之前，請先指派給[使用者角色](#add-users)。 基本Commerce許可權需要使用者角色。

>[!TAB GA （在2025年10月13日之後布建）]

1. 導覽至<https://adminconsole.adobe.com>並使用您的Adobe ID登入。

1. 選取您的組織。

1. 選取&#x200B;[!UICONTROL **使用者**]&#x200B;索引標籤。

1. 選取&#x200B;[!UICONTROL **管理員**]&#x200B;標籤。

1. 按一下&#x200B;[!UICONTROL **新增管理員**]。

1. 輸入您要新增為管理員之使用者的使用者名稱或電子郵件地址，然後按一下&#x200B;[!UICONTROL **下一步**]。

1. 選取&#x200B;[!UICONTROL **產品設定檔管理員**]&#x200B;角色。

1. 按一下&#x200B;**+**&#x200B;以新增產品。

1. 選取要新增管理員的現有Commerce Optimizer執行個體。 Commerce Optimizer執行個體使用以下格式： `Adobe Commerce - <instance-name> - ACO - <environment-type> - <tenant-id>`。

1. 選取產品設定檔。

1. 按一下&#x200B;[!UICONTROL **套用**]。

1. 按一下&#x200B;[!UICONTROL **儲存**]。

>[!TAB 搶先使用（2025年10月13日之前布建）]

1. 導覽至<https://adminconsole.adobe.com>並使用您的Adobe ID登入。

1. 選取您的組織。

1. 在「[!UICONTROL **產品**]」標籤的「[!UICONTROL **產品和服務**]」下，選取「[!UICONTROL **Adobe Commerce - Commerce Cloud管理員**]」產品。

   ![選取產品](/help/cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. 選取「[!UICONTROL **管理員**]」標籤。

1. 按一下&#x200B;[!UICONTROL **新增管理員**]。

1. 輸入您要新增為管理員的使用者使用者名稱或電子郵件地址，然後按一下[儲存]。[!UICONTROL **&#x200B;**]

>[!ENDTABS]

## 新增使用者

下列指示提供如何將使用者新增到[!DNL Commerce Cloud Manager]和Commerce Optimizer的資訊。 [!DNL Commerce Cloud Manager]介面可讓您建立和管理Commerce Optimizer執行個體。 所有使用者（包括開發人員和管理員）都必須進行此程式。

>[!NOTE]
>
>只有產品管理員和系統管理員可以將使用者和開發人員新增到Adobe Commerce Optimizer產品。

>[!BEGINTABS]

>[!TAB GA （在2025年10月13日之後布建）]

1. 導覽至<https://adminconsole.adobe.com>並使用您的Adobe ID登入。

1. 選取您的組織。

1. 選取「[!UICONTROL **產品**]」標籤。

1. 選取&#x200B;[!UICONTROL **Adobe Commerce**]&#x200B;產品。

1. 如果您想要將使用者新增到Commerce Cloud Manager介面(他們可以在此建立和管理Commerce Optimizer執行個體)，請選取Manager產品，或選取要新增使用者的現有Commerce Optimizer執行個體。 Commerce Optimizer執行個體使用以下格式： `Adobe Commerce - <instance-name> - ACO - <environment-type> - <tenant-id>`。

1. 選取&#x200B;[!UICONTROL **使用者**]&#x200B;索引標籤，然後按一下&#x200B;[!UICONTROL **新增使用者**]。

1. 輸入要新增的使用者使用者名稱或電子郵件地址，然後按一下[儲存]。[!UICONTROL **&#x200B;**]

1. 選取所需的產品設定檔。

1. 按一下&#x200B;[!UICONTROL **套用**]。

1. 按一下&#x200B;[!UICONTROL **儲存**]。

>[!TAB 搶先使用（2025年10月13日之前布建）]

1. 導覽至<https://adminconsole.adobe.com>並使用您的Adobe ID登入。

1. 選取您的組織。

1. 在「[!UICONTROL **產品**]」標籤的「[!UICONTROL **產品和服務**]」下，選取「[!UICONTROL **Adobe Commerce - Commerce Cloud管理員**]」產品。

   ![選取產品](/help/cloud-service//assets/backend.png){width="600" zoomable="yes"}

1. 按一下&#x200B;[!UICONTROL **預設 — Cloud Manager**]&#x200B;產品設定檔。

1. 選取&#x200B;[!UICONTROL **使用者**]&#x200B;索引標籤，然後按一下&#x200B;[!UICONTROL **新增使用者**]。

   ![索引標籤選取](/help/cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

1. 輸入要新增的使用者使用者名稱或電子郵件地址，然後按一下[儲存]。[!UICONTROL **&#x200B;**]

>[!ENDTABS]

### 新增開發人員和產品設定檔管理員

若要新增開發人員和產品設定檔管理員，請重複[新增使用者](#add-users)程式，但選取&#x200B;[!UICONTROL **開發人員**]&#x200B;或&#x200B;[!UICONTROL **管理員**]&#x200B;標籤，而非&#x200B;[!UICONTROL **使用者**]&#x200B;標籤。

>[!NOTE]
>
>將開發人員新增為開發人員之前，先為其指派使用者角色。 基本Commerce許可權需要使用者角色。

![索引標籤選取](/help//cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

## 大量使用者管理

您可以使用下列其中一種方法來更有效率地新增多個使用者：

- 使用Adobe Admin Console中的&#x200B;**透過CSV新增使用者**&#x200B;功能來執行[大量CSV上傳](https://helpx.adobe.com/tw/enterprise/using/bulk-upload-users.html){target="_blank"}。
- 建立[使用者群組](https://helpx.adobe.com/tw/enterprise/using/user-groups.html){target="_blank"}，將多位使用者新增至角色。 接著，將&#x200B;[!UICONTROL **Adobe Commerce - Commerce Cloud Manager**]&#x200B;產品新增至使用者群組。

