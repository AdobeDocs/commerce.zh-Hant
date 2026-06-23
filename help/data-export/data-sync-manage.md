---
title: 檢視及管理同步化程式
description: 瞭解如何使用「資料管理」控制面板和「資料摘要同步狀態」頁面檢視及管理 [!DNL SaaS Data Export] 同步化程式。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 98d604a71c2062a44070b207fc43b9d9b1c434fd
workflow-type: tm+mt
source-wordcount: 557
ht-degree: 0%

---

# 檢視及管理同步化程式

大部分同步活動都會使用完整同步、部分同步或重試失敗的專案同步自動處理。 如需每個型別執行時間的詳細資訊，請參閱[同步化型別](sync-overview.md#synchronization-types)。 [!DNL SaaS Data Export]也提供工具來監視、管理及疑難排解程式。 您可以檢視同步化狀態，並使用您部署的儀表板來管理資料同步化程式。

>[!BEGINTABS]

>[!TAB Adobe Commerce]

對於雲端上的Adobe Commerce、內部部署或Adobe Commerce as a Cloud Service部署，請從以下Commerce管理員資源檢視及管理同步程式：

- **[資料摘要同步狀態頁面](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)** — 檢查與[!DNL Live Search]、[!DNL Product Recommendations]或[!DNL Catalog Service]連線的部署的摘要匯出狀態。 此儀表板會顯示每個摘要的摘要匯出狀態，包括遇到的任何錯誤。 詳細資料檢視會顯示個別摘要專案的摘要匯出狀態。

- **[資料管理儀表板](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)** — 管理員使用者可以檢視及追蹤已成功匯出並同步處理至連線之Commerce服務的資料。 此儀表板會顯示同步至Commerce服務的產品資料。

>[!NOTE]
>
>資料管理儀表板和資料摘要同步狀態頁面僅在您已安裝[!DNL Live Search]、[!DNL Product Recommendations]或[!DNL Catalog Service]時才可用。

>[!TAB Adobe Commerce與Commerce Optimizer]

對於雲端上的Commerce或與[!DNL Commerce Optimizer]整合的內部部署，請使用下列資源檢視及管理同步化程式：

- **[資料摘要同步狀態頁面](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)** — 從Commerce管理員監視聯結器摘要匯出狀態。 此頁面顯示是否成功從[!DNL Adobe Commerce]匯出目錄資料，包括每個摘要和每個專案的錯誤詳細資料。

- **[資料同步頁面](../optimizer/setup/data-sync.md)** — 資料同步頁面提供從上游目錄來源到[!DNL Commerce Optimizer]的產品資料同步狀態概觀。

如需有關如何使用這些儀表板來確認資料同步處理是否正常運作，以及手動重新同步資料的詳細資訊，請參閱&#x200B;_Adobe Commerce Optimizer Connector指南_&#x200B;中的[管理同步處理](../aco-connector/data-sync-manage.md)。

>[!ENDTABS]

## 確認資料同步處理運作正常 {#verify-that-the-data-sync-is-working}


{{$include /help/_includes/data-export/verify-commerce-service-data-sync.md}}

## 手動重新同步資料

當部分同步和自動重試無法解決同步問題時，您可以從Commerce管理員手動重新同步資料，或使用Commerce CLI命令手動重新同步資料。 可用選項取決於您的部署。

### 可用的手動重新同步選項 {#manual-resync-options-commerce}

使用下列選項手動重新同步摘要資料。

| 任務 | 選項 | 附註 |
| --- | --- | --- |
| 重新同步選取的失敗或有問題的摘要專案 | **[!UICONTROL Data Feed Sync Status]頁** | 從Commerce管理員監視和重新同步所選的摘要專案。 請參閱[確認資料同步正在運作](#verify-that-the-data-sync-is-working)。 |
| 完整重新同步所有摘要 | **[!UICONTROL Data Management Dashboard]** | 從Commerce管理員對所有摘要執行完整重新同步；Adobe建議這主要是當您首次連線到Commerce服務時。 會略過自上次匯出以來內容雜湊未變更的專案。 請參閱[確認資料同步正在運作](#verify-that-the-data-sync-is-working)。 |
| 目標摘要與作業控制重新同步 | **Commerce CLI** | 使用`saas:resync`命令進行目標摘要重新同步。 請參閱[使用Commerce CLI同步摘要](data-export-cli-commands.md)。 |

>[!MORELIKETHIS]
>
> - [同步如何運作](sync-overview.md) — 瞭解同步模式、完整同步、部分同步以及重試失敗的專案。
> - [使用Commerce CLI同步摘要](data-export-cli-commands.md) — 針對目標摘要重新同步使用`saas:resync`命令。
> - [檢閱記錄檔並疑難排解](troubleshooting/logging.md) — 診斷資料匯出和SaaS匯出錯誤。
> - [管理與 [!DNL Commerce Optimizer]](../aco-connector/data-sync-manage.md)的同步處理 — 驗證目錄資料同步處理並手動重新同步聯結器摘要。
