---
title: 管理 [!DNL Adobe Commerce Optimizer Connector] 同步處理
description: 瞭解如何驗證 [!DNL Adobe Commerce] 和 [!DNL Adobe Commerce Optimizer]之間的目錄資料同步和手動重新同步聯結器摘要。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案（Adobe管理的PaaS基礎結構）和內部部署專案的Adobe Commerce 。"
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 0bfd368c50707692c7a0adda6e70e3776bd9692a
workflow-type: tm+mt
source-wordcount: 349
ht-degree: 0%

---

# 管理與[!DNL Commerce Optimizer]的同步處理

在您設定[!DNL Adobe Commerce Optimizer Connector]後，大部分的目錄更新都會透過已排程的cron工作自動同步。 如需自動同步化如何運作的詳細資訊，請參閱[聯結器同步管道](connector-sync-pipeline.md)。 使用此主題中的工具來驗證資料是否達到[!DNL Adobe Commerce Optimizer]，並視需要手動重新同步摘要。

## 確認資料同步處理運作正常 {#verify-that-the-data-sync-is-working}

{{$include /help/_includes/aco-connector/verify-optimizer-data-sync.md}}

## 手動重新同步資料 {#manually-resync-data}

當部分同步和自動重試無法解決同步問題時，您可以手動重新同步目錄資料。 您選擇的選項取決於問題的起源位置以及您需要的控制程度。

| 任務 | 選項 | 附註 |
| --- | --- | --- |
| 驗證同步狀態，並在缺少產品時從上游系統重新同步 | **上游系統重新同步** | 在[!DNL Commerce Optimizer]中，選取&#x200B;**[!UICONTROL Data Sync]**，然後驗證是否顯示預期的目錄來源、產品、價格和屬性。 當產品遺失時，請使用&#x200B;**[!UICONTROL Data Feed Sync Status]**&#x200B;頁面或Commerce CLI從上游[!DNL Adobe Commerce]執行個體重新同步（請參閱下列列）。 |
| 重新同步選取的失敗或有問題的聯結器饋送專案 | Commerce管理員中的&#x200B;**[!UICONTROL Data Feed Sync Status]頁面** | 從Commerce管理員監視匯出狀態，並重新同步選取的聯結器資訊源專案。 請參閱[確認資料同步正在運作](#verify-that-the-data-sync-is-working)。 |
| 具有操作控制的目標聯結器資訊源重新同步 | **Commerce CLI** | 從Adobe Commerce執行個體執行`saas:resync`以取得聯結器摘要。 請參閱[使用Commerce CLI同步摘要](../data-export/data-export-cli-commands.md)和[支援的摘要](reference/connector-reference.md#supported-feeds)。 |

>[!MORELIKETHIS]
>
> - [聯結器同步管道](connector-sync-pipeline.md) — 瞭解自動同步、cron排程和錯誤處理的運作方式
> - [估算資料量並同步處理時間](reference/estimate-data-volume-sync-time.md) — 計算預期的同步處理持續時間
> - [疑難排解](troubleshooting.md) — 診斷認證、同步和範圍匯出問題
> - [聯結器模組和摘要端點](reference/connector-reference.md) — 檢閱模組、API端點和支援的摘要
> - [Commerce Admin中的資料摘要同步狀態頁面](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status){target="_blank"} — 深入瞭解可用於監視摘要狀態的欄位和功能
> - [資料同步儀表板位於 [!DNL Commerce Optimizer]](https://experienceleague.adobe.com/en/docs/commerce-optimizer/data-sync/data-sync){target="_blank"} — 可用於監視目錄資料同步的欄位和動作參考檔案
