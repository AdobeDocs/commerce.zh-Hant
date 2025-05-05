---
title: 更新Commerce資料擷取的時間序列事件結構
description: 瞭解如何建立結構、資料集和資料串流，以收集和傳送Commerce資料擷取的時間序列事件資料。
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 0%

---

# 更新Commerce資料擷取的時間序列事件結構

使用[!DNL Data Connection]擴充功能的[上線步驟](overview.md#onboarding-steps)之一，是存取資料流工作區並[建立Adobe Commerce專屬的資料流](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=zh-Hant)。 當您建立該資料流時，也必須選取描述您計畫擷取之資料的結構描述。 該結構描述必須包含商務特定欄位群組。

本文提供結構描述必須包含的欄位群組，才能成功收集Adobe Commerce事件提供的下列時間序列資料：

- [行為](events.md) — 包含店面、個人資料、搜尋和B2B事件。
- [後台](events-backoffice.md) — 包含訂單狀態和設定檔事件。

深入瞭解[時間序列資料](data-ingestion.md)。

深入瞭解結構描述組合[的基本概念](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=zh-Hant)。

## 使用時間序列行為和後台事件資料更新結構描述

在本節中，您將瞭解如何更新現有的結構描述或建立結構描述，以包含行為和後台事件資料。

>[!NOTE]
>
>請參閱[時間序列設定檔事件資料](#time-series-profile-event-data)，瞭解如何新增設定檔特定欄位。

1. 如果您還沒有結構描述，請[建立](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=zh-Hant#create)類別設定為&#x200B;**體驗事件**&#x200B;的結構描述。

1. [新增](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=zh-Hant#add-field-groups)下列Commerce專屬欄位群組（或編輯您現有的結構描述並新增這些欄位群組）：

   - 網站搜尋
   - 造訪網頁
   - 使用者登入程式
   - 參考索引鍵
   - 個人聯絡詳細資訊
   - 管道詳細資料
   - Commerce詳細資料
   - Adobe Analytics ExperienceEvent Commerce (如果您想要傳送資料給Adobe Analytics)

   >[!NOTE]
   >
   > 請勿將任何Commerce特定的欄位群組設為`Primary identity`。 這麼做會識別必填欄位，而Experience Platform會預期每個事件中都會有該欄位。 如果此欄位不存在，資料擷取會失敗。

   您的結構描述現在包含Commerce特定的欄位群組，因此從Commerce [行為](events.md)和[後台](events-backoffice.md)事件收集的時間序列資料會顯示在結構描述中。

1. [為設定檔啟用](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=zh-Hant#profile)結構描述。

   為設定檔啟用結構描述時，從此結構描述建立的任何資料集都會參與Real-Time CDP，其會合併來自不同來源的資料，以建構每個客戶的完整檢視。

1. [根據您建立或更新的結構描述建立資料集](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html?lang=zh-Hant#create-a-dataset)。

   資料集是資料集合的儲存和管理結構，通常是包含結構（欄）和欄位（列）的表格。 資料集也包含中繼資料，可說明其儲存資料的各個層面。

1. [建立資料流](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=zh-Hant)，並選取包含Commerce特定欄位群組和對應資料集的結構描述。

   資料流會將收集的資料轉送至資料集。 資料會根據所選的結構描述顯示在資料集中。

使用為行為和後台資料設定的結構描述、資料集和資料串流，您可以[設定](connect-data.md#data-collection)您的Commerce執行個體，以收集該資料並將其傳送到Experience Platform。

若要包含購物者的設定檔資訊，請參閱[時間序列設定檔事件資料](#time-series-profile-event-data)。

## 時間序列設定檔事件資料

時間序列設定檔事件資料產生自下列事件：

- [&#39;accountCreated&#39;](events-backoffice.md#accountcreated)
- [&#39;帳戶已更新&#39;](events-backoffice.md#accountupdated)
- [&#39;帳戶已刪除&#39;](events-backoffice.md#accountdeleted)

如果您想要將客戶的設定檔事件資料擷取至Experience Platform，您可以更新現有的Commerce結構描述，並使用已設定的相同資料流，或者您可以建立設定檔專屬的資料流和結構描述。 該決定取決於您公司的資料控管。 接下來的兩個區段將引導您瞭解這兩種情況。

### 使用您現有的資料流將時間序列設定檔事件資料傳送到Experience Platform

如果您想要將時間序列[伺服器端設定檔事件資料](events-backoffice.md#customer-profile-events-server-side)新增至您現有的Commerce資料流，請將`Demographic Details`欄位群組新增至您的結構描述。 您的結構描述現在包含下列Commerce專用欄位群組：

- 網站搜尋
- 造訪網頁
- 使用者登入程式
- 參考索引鍵
- 個人聯絡詳細資訊
- 管道詳細資料
- Commerce詳細資料
- Adobe Analytics ExperienceEvent Commerce (如果您想要傳送資料給Adobe Analytics)
- 新增： **人口統計詳細資料**

當您現有的Commerce結構描述中新增`Demographic Details`欄位群組後，已與Commerce結構描述關聯的資料集和資料流將用於此時間序列設定檔資料。

### 以單獨的資料流將時間序列設定檔事件資料傳送至Experience Platform

如果您要將[伺服器端設定檔事件資料](events-backoffice.md#customer-profile-events-server-side)新增至新的設定檔特定資料流和結構描述，請完成下列步驟。

1. [建立](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=zh-Hant#create)結構描述並將類別設定為&#x200B;**體驗事件**。

1. [新增](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=zh-Hant#add-field-groups)下列設定檔特定欄位群組：

   - 人口統計細節
   - 個人聯絡詳細資訊
   - 管道詳細資料
   - Commerce詳細資料

1. [為設定檔啟用](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=zh-Hant#profile)結構描述。

   為設定檔啟用結構描述時，從此結構描述建立的任何資料集都會參與Real-Time CDP，其會合併來自不同來源的資料，以建構每個客戶的完整檢視。

1. [根據您建立的結構描述建立資料集](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html?lang=zh-Hant#create-a-dataset)。

   資料集是資料集合的儲存和管理結構，通常是包含結構（欄）和欄位（列）的表格。 資料集也包含中繼資料，可說明其儲存資料的各個層面。

1. [建立資料串流](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=zh-Hant)，並選取包含Commerce特定欄位群組和對應資料集的XDM結構描述。

   資料流會將收集的資料轉送至資料集。 資料會根據所選的結構描述顯示在資料集中。

針對客戶設定檔資料設定的結構描述、資料集和資料串流後，您可以[設定](connect-data.md#data-collection)您的Commerce執行個體，以收集該資料並傳送至Experience Platform。

若要為設定檔記錄資料建立結構描述、資料集和資料流，請參閱[將設定檔記錄資料傳送至Experience Platform](profile-data.md)。
