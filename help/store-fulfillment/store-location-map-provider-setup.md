---
title: 存放區位置和對應系統設定
description: 設定距離提供者，以在店面UI中支援商店位置對應。 「商店履行」解決方案需要距離提供者，以啟用零售商店搜尋及其他端對端履行工作流程的對應和排程功能。
role: Admin
level: Intermediate
feature: Shipping/Delivery, Integration, Tools and External Services, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# 存放區位置和對應設定

設定[距離提供者](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/inventory/configuration/distance-priority-algorithm)來搜尋零售商店位置，以啟用「商店履行」的商店位置和對應功能。

**需求**

在設定程式期間，您會提供Google Maps平台的Google API金鑰。 如果您沒有這類地圖，請[從Google地圖平台](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/inventory/configuration/distance-priority-algorithm#configure-google-maps)產生一個。

設定距離提供者：

1. 從管理員的&#x200B;**[!UICONTROL Stores > General]**&#x200B;設定，為地圖內容型別新增Google地圖整合。

   - 移至&#x200B;**[!UICONTROL Stores > Configuration  > General > Content Management]**。

   - 將您的Google API金鑰新增至&#x200B;**[!UICONTROL Google Maps API Key]**&#x200B;欄位。

1. 從「管理員」的&#x200B;**[!UICONTROL Stores > Inventory]**&#x200B;設定中，選取「商店履行」的距離提供者。

   - 移至&#x200B;**[!UICONTROL Stores > Configuration > Catalog > Inventory]**。

   - 展開&#x200B;**[!UICONTROL Distance Provider for Distance Based SSA]**&#x200B;區段。

   - 將&#x200B;**提供者**&#x200B;設定為&#x200B;**Google對應**。

1. 設定&#x200B;**[!UICONTROL Google Distance Provider]**&#x200B;的設定。

   - 新增您的&#x200B;**Google API金鑰**。

   - 將&#x200B;**[!UICONTROL Computation Mode]**&#x200B;設為`Driving`並將&#x200B;**[!UICONTROL Value]**&#x200B;設為`Distance`
