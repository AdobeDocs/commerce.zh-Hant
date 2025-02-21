---
title: 應用程式設定
description: 設定 [!DNL Store Assist] 應用程式，以管理線上購買、商店訂單取貨的端對端商店履行工作流程和程式。
level: Intermediate
role: Admin
feature: Shipping/Delivery, Configuration, Tools and External Services
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 0%

---

# 應用程式設定

Store Assist是由Walmart Commerce Technologies提供支援的以服務方式履行(FaaS)平台應用程式。 應用程式提供店內履行功能，以處理[!DNL buy online, pick up in store] (BOPIS)訂單。 透過「商店協助」，店舖夥伴可以檢視客戶訂購的料號、更快地挑選正確的料號，以及設定已履行訂單，以便店內或路邊取貨交貨給客戶。

Store Assist應用程式會接收所有訂單和客戶資訊 — 從訂單詳細資料到取貨時間，並透過行動裝置將資料提供給線上商店夥伴。 應用程式包含[!UICONTROL Pick]、[!UICONTROL Stage]、[!UICONTROL Handoff]和[!UICONTROL Orders]模組，可協助商店關聯處理如下列的履行活動：

- 指定訂單交貨日期和時間。
- 當客戶抵達取貨地點時，接收他們的通知。
- 中繼客戶移交訂單。
- 追蹤其指定商店位置中所有訂單的訂單狀態。

>[!NOTE]
>
>檢閱[Store Assist履行工作流程](store-assist-modules.md)主題，以進一步瞭解Store Assist應用程式。

## 設定商店協助應用程式

Store Assist應用程式需要兩種設定型別：

- Adobe Commerce系統管理系統設定可[管理使用者帳戶、使用者角色、資源許可權](user-setup.md)，以及[客戶在簽到程式期間可用的汽車製造和模型選擇](check-in-experience-setup.md)。

- 前端組態設定可自訂Store Assist應用程式介面和其他設定，包括：

   - **品牌化Store Assist應用程式** — 使用您公司的標誌和顏色自訂應用程式使用者介面。

   - **更新預設指示** — 自訂「商店協助挑選」、「預備」、「移交」及「訂購」模組中的指示，以引導「商店夥伴」完成公司履行工作流程的每個步驟。

   - **本地化** — 選取應用程式可用的語言。 選擇您的日期和時間格式，並選取您的預設度量單位和預設貨幣。

   - **非使用中時間** — 指定應用程式在登出前必須處於非使用中狀態的時間長度。

   - **從商店取消** — 指定是否可以從商店取消訂單，以及哪些角色具有取消許可權

   - **訂單清理視窗** — 指定撿料訂單在重新上架前要經過多長時間超過預估[撿料前置時間](enable-general.md#delivery-method-title-configuration)，例如三天。 預設值為七天。 如果開啟此設定，則當此時間到期時，會自動取消訂單。 商品已補充庫存，商家會收到取消電子郵件。

   - 自訂所有應用程式內指示（挑選、分段、交出）。

   - **撿料通知** — 指定是否傳送推播通知，以在客戶下訂單後開始撿料程式。

   - **簽到通知** — 指定是否要在簽到過程中傳送推播通知，以收取訂單 — 簽到後、客戶等待時間超過指定時段後。 或者，停用通知。

   - **交出程式** — 當「商店關聯」將訂單交付給客戶時（例如，需要客戶簽名或提示關聯檢查客戶ID），啟用選擇性程式。

   - **在移交時啟用專案拒絕** — 允許客戶在訂單移交期間退回或取消訂單專案。

  請與Walmart Commerce Technologies Client Services團隊合作，完成「商店協助」應用程式的前端設定。

## 應用程式下載和安裝

設定Store Assist應用程式後，Store Associates可以從行動裝置下載、安裝並登入Store Assist應用程式。

- 確認行動裝置符合Store Fulfillment解決方案的[軟硬體需求](solution-requirements.md#store-assist-app-requirements)。

- 從[Apple App Store](https://apps.apple.com/us/app/store-assist-by-walmart/id1609281539){target="_blank"}或[Google Play市集](https://play.google.com/store/apps/details?id=com.walmart.faas.storeassist){target="_blank"}下載「市集協助」應用程式。

- 存放區關聯需要下列資訊才能登入：

   - 與Store Assist帳戶關聯的&#x200B;**[!UICONTROL Company name]**

   - **儲存協助帳戶認證** — 其帳戶的使用者名稱和密碼認證。

  Adobe Commerce管理員可以針對在「管理商店」設定中啟用[店內取貨](merchant-store-configuration.md#pickup-location-configuration)的所有商店位置，建立和管理[!DNL Store Assist app]使用者帳戶。
