---
title: 背景處理程式設定
description: 設定與履行服務同步資料時所使用的 [!DNL Store Fulfillment] 背景處理作業的排程。
role: Admin, Developer
level: Intermediate
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---


# 背景處理程式設定

「商店履行」整合使用背景流程和訊息佇列，以獲得最佳效能和規模。 使用會自動啟動[訊息佇列執行者](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/message-queues/message-queue-framework)的[部署變數](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy#cron_consumers_runner)，為您的Adobe Commerce存放區建置環境。

背景處理程式是使用標準Adobe Commerce [排程工作](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/cron)功能來管理。 這些程式負責將訂單和商家商店設定資料與商店履行Web服務同步。

## 管理「商店履行」的排程工作

從Admin移至&#x200B;**[!UICONTROL Stores > Configuration > Advanced > System > Cron (Scheduled Tasks) > Cron configuration options for group:store_fulfillment]**。

檢閱Store Fulfillment服務的預設設定。 您可以根據訂單處理量及可用資源來自訂這些設定。
