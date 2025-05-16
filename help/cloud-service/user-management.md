---
title: 使用者管理
description: 瞭解如何在 [!DNL Adobe Commerce as a Cloud Service]中管理使用者。
exl-id: 9bc80fe6-6dfd-4bb3-8dc5-d5efd8a8d90c
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"
source-git-commit: 34057c1e55ff117ea7aab4407f31548ce826691b
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---

# 使用者管理

{{accs-early-access}}

如果您希望使用者在[!DNL Adobe Commerce as a Cloud Service]中存取Admin，您需要將他們新增為您組織中的使用者，並確保他們有權在[Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"}中存取Cloud Service產品。

此程式需要IMS組織才能存取[!DNL Adobe Commerce as a Cloud Service]。 只有組織的系統管理員或產品管理員可以執行這些流程。

>[!TIP]
>
>若要同時新增多個使用者，您可以執行[大量CSV上傳](https://helpx.adobe.com/tw/enterprise/using/bulk-upload-users.html){target="_blank"}。
> 
> 您也可以建立[使用者群組](https://helpx.adobe.com/tw/enterprise/using/user-groups.html){target="_blank"}，將多位使用者新增至角色。 然後您可以將&#x200B;[!UICONTROL **Adobe Commerce as a Cloud Service — 後端**]&#x200B;產品新增到使用者群組。

## 瞭解角色

下列角色適用於[!DNL Adobe Commerce as a Cloud Service]。 若要檢視或編輯這些角色，請在Commerce管理員中導覽至&#x200B;**系統** > **許可權** > **使用者角色**。

* **使用者** — 使用者擁有Commerce管理員的管理員存取權，但無法在Admin Console中管理產品層級的存取權。 使用者也可以使用積分在[!DNL Commerce Cloud Manager]中[建立執行個體](./getting-started.md#create-an-instance)。

* [**開發人員**](https://helpx.adobe.com/tw/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"}開發人員擁有使用者許可權，並新增至Commerce執行個體作為開發人員使用者。 這表示他們可以使用[Admin UI SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/){target="_blank"}、[設定事件](https://developer.adobe.com/commerce/extensibility/events/){target="_blank"}和[建立Webhook](https://developer.adobe.com/commerce/extensibility/webhooks/){target="_blank"}。

* 管理員 — 管理員分為三種型別：
   * [系統管理員](https://helpx.adobe.com/tw/enterprise/using/admin-roles.html){target="_blank"} — 系統管理員可以透過Admin Console存取組織中的所有產品和產品設定檔。
   * [產品管理員](#add-a-product-admin) — 產品管理員可以在[!DNL Adobe Admin Console]中[管理產品的使用者、角色和許可權](#add-users-and-admins)，並在Commerce管理員中[管理使用者](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/systems/user-accounts/permissions-users-all#create-a-user){target="_blank"}。
   * [產品設定檔管理員](#add-users-developers-and-product-profile-admins) — 產品設定檔管理員無法存取Adobe Commerce管理員，但可以在[!DNL Adobe Admin Console]中管理產品的使用者。

如需授與Adobe Commerce中每個角色的許可權的詳細資訊，請參閱[使用者許可權](#user-permissions)。

## 新增產品管理員

1. 導覽至https://adminconsole.adobe.com並使用您的Adobe ID登入。

1. 選取您的組織。

1. 在「[!UICONTROL **產品**]」標籤的「[!UICONTROL **產品和服務**]」下，選取「[!UICONTROL **Adobe Commerce as a Cloud Service — 後端**]」產品。

   ![選取產品](./assets/backend.png){width="600" zoomable="yes"}

1. 選取「[!UICONTROL **管理員**]」標籤。

1. 按一下&#x200B;[!UICONTROL **新增管理員**]。

1. 輸入您要新增為管理員的使用者使用者名稱或電子郵件地址，然後按一下[儲存]。[!UICONTROL **&#x200B;**]

## 新增使用者、開發人員和產品設定檔管理員

下列指示提供如何將使用者和開發人員新增到[!DNL Commerce Cloud Manager]和Commerce管理員的資訊。 [!DNL Commerce Cloud Manager]介面可讓您建立和管理Commerce執行個體。

>[!NOTE]
>
>只有產品管理員和系統管理員可以將使用者和開發人員新增到Adobe Commerce as a Cloud Service產品。

1. 導覽至https://adminconsole.adobe.com並使用您的Adobe ID登入。

1. 選取您的組織。

1. 在「[!UICONTROL **產品**]」標籤的「[!UICONTROL **產品和服務**]」下，選取「[!UICONTROL **Adobe Commerce as a Cloud Service — 後端**]」產品。

   ![選取產品](./assets/backend.png){width="600" zoomable="yes"}

1. 按一下&#x200B;[!UICONTROL **預設 — Cloud Manager**]&#x200B;產品設定檔。

1. 選取「[!UICONTROL **使用者**]」、「[!UICONTROL **開發人員**]」或「[!UICONTROL **管理員**]」標籤，然後按一下「[!UICONTROL **新增使用者**]」、「[!UICONTROL **新增開發人員**]」或「[!UICONTROL **新增管理員**]」。

   >[!NOTE]
   >
   >從此畫面新增的管理員是[產品設定檔管理員](#understanding-roles)，且沒有Commerce管理員的存取權。

   ![索引標籤選取](./assets/tab-select.png){width=600 zoomable="yes"}

1. 輸入您要新增為管理員的使用者使用者名稱或電子郵件地址，然後按一下[儲存]。[!UICONTROL **&#x200B;**]

## 角色資源

下列清單說明預設角色有權在Adobe Commerce管理員內部存取的資源。 若要編輯每個角色的預設許可權，請瀏覽至Commerce管理員中的&#x200B;**系統** > **許可權** > **使用者角色**。

**位使用者**

* 目錄
   * 詳細目錄
      * 產品
         * 讀取產品價格

**開發人員**

* 目錄
   * 詳細目錄
      * 產品
         * 讀取產品價格
* 系統
   * 資料傳輸
      * 匯入歷史記錄
* Adobe IO事件設定
   * 組態檢查
   * 建立事件提供者
   * 設定更新
   * 同步事件
   * 取得事件提供者清單
* 事件架構
   * 事件清單
   * 測試事件連線
   * 訂閱事件
   * 取消訂閱事件
   * 事件狀態
   * 取得事件訂閱的API
   * 檢視事件訂閱管理UI
   * 建立事件訂閱管理員UI
   * 請求新的事件管理員UI
* Webhooks
   * Webhooks數位簽名
      * Webhooks數位簽名設定
      * Webhooks數位簽名產生金鑰
   * Webhooks管理
      * Webhooks格線
      * Webhooks編輯
      * 測試Webhook
      * API訂閱webhook
      * API從webhook取消訂閱
      * Webhooks清單
      * 請求新Webhook
      * Webhooks記錄
      * 取得Webhook清單

**管理員**

管理員擁有所有許可權的存取權。
