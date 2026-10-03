---
title: B2B共用目錄的監視器目錄檢視同步處理
last-update: 2026-09-03
description: 您可以使用「目錄檢視同步狀態」頁面，監督與調解同步至Adobe Commerce Optimizer的目錄檢視、原則、價格簿參考及金鑰組態資料。
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案（Adobe管理的PaaS基礎結構）和內部部署專案的Adobe Commerce 。"
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
    internal-label: Data Transfer
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: 1fd5e3d84d5249ce96014cae46e045528d2790d0
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 0%
---

# 監視B2B共用目錄的目錄檢視同步處理

使用Commerce管理員中的[!UICONTROL Catalog View Sync Status]儀表板追蹤[!DNL Adobe Commerce]到[!DNL Adobe Commerce Optimizer]的B2B目錄檢視同步處理。

[!UICONTROL Catalog View Sync Status]驗證[!DNL Adobe Commerce Optimizer]中每個B2B共用目錄的目錄檢視、原則、價格簿參考和受限制的存取金鑰設定是否存在，並且符合您的[!DNL Adobe Commerce]設定。 若要改為追蹤產品、價格和類別摘要同步處理，請參閱[管理資料同步處理](data-sync-status.md#verify-that-the-data-sync-is-working)。

## 存取同步狀態頁面 {#access-the-sync-status-page}

從Commerce Admin移至&#x200B;**[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Catalog View Sync Status]**。

![目錄檢視[同步狀態]頁面，用來監視Adobe Commerce Optimizer中目錄檢視、原則、價格手冊及存取金鑰組態的同步狀態](assets/catalog-view-sync-status.png){width="600" zoomable="yes"}

此頁面有三個索引標籤： [!UICONTROL Catalog Views]、[!UICONTROL Orphaned in ACO]和[!UICONTROL Deleted]。

## 解譯共用目錄的同步狀態 {#interpret-sync-status}

在[!UICONTROL Catalog View]標籤上，每一列代表一個自訂共用目錄檢視，投影自共用目錄和存放區檢視組合。 此投影是目錄檢視、原則、價格簿參考和限制存取金鑰組態資料，[!DNL Commerce Optimizer Connector]會針對共用目錄將其匯出至[!DNL Adobe Commerce Optimizer]。 使用狀態資訊可判斷傳送至公司店面體驗的資料是否完整且正確。 下表摘要列出最常見的狀態值，以及這些值對共用目錄的意義：

| 狀態 | 這對您共用目錄的意義 |
| --- | --- |
| **已降級** | 在[!DNL Adobe Commerce Optimizer]中直接變更了某些專案，例如原則或連結的價格簿。 公司可能會看到錯誤的分類或定價，直到您解決問題為止。 如果在Commerce Optimizer中變更存取金鑰、檢視名稱或來源，也會發生此狀況。 |
| **失敗** | 目錄檢視不存在於[!DNL Adobe Commerce Optimizer]中，或寬限期在第一個投影完成之前過期。 （請參閱[設定ACO目錄檢視同步處理設定](#configure-aco-catalog-view-sync-settings)）。 如果目錄同步狀態為`Failed`，則公司無法存取此共用目錄的店面體驗。 |
| **正在退休** | 您已刪除[!DNL Adobe Commerce]中的共用目錄。 在刪除寬限期過期之前，目錄檢視仍可存取。 預設寬限期為七天。 您可以更新[目錄檢視同步處理設定](#configure-aco-catalog-view-sync-settings)來修改預設值。 |
| **孤立** | 目錄檢視或金鑰是直接在[!DNL Adobe Commerce Optimizer] Studio中建立，而非由聯結器建立。 請參閱[檢閱孤立和已刪除的專案](#review-orphaned-and-deleted-entries)。 |

[!UICONTROL Healthy]、[!UICONTROL Pending]和[!UICONTROL Deleted]是不需要動作的資訊狀態。 如需完整清單，請參閱&#x200B;*Commerce管理指南*&#x200B;中的[同步狀態值](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/catalog-view-sync-status#sync-status-values){target="_blank"}。

### 設定ACO目錄檢視同步處理設定 {#configure-aco-catalog-view-sync-settings}

從[!DNL Adobe Commerce] Admin （非[!DNL Adobe Commerce Optimizer] Studio），移至&#x200B;**[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Services]** > **[!UICONTROL ACO Catalog View Sync]**&#x200B;以控制聯結器刪除和建立的時間方式，以及它是否自動修復漂移。

![ACO目錄檢視同步設定頁面，顯示刪除、建立及漂移調解器區段](assets/aco-catalog-view-sync-configuration.png){width="600" zoomable="yes"}

- **[!UICONTROL Deletion Grace Period (days)]** — 刪除的共用目錄目錄檢視、原則及中繼資料在移除前保留在[!DNL Adobe Commerce Optimizer]中的天數。 預設為七天。 設定為`0`以立即移除投影，沒有寬限期。

- **[!UICONTROL Creation Grace Period (days)]** — 新註冊的目錄檢視在回報為[!UICONTROL Pending]時，可等待其第一個投影到[!DNL Adobe Commerce Optimizer]的天數。 如果寬限期在沒有投影的情況下過期，則狀態會變成[!UICONTROL Failed]。 預設為1。

- **[!UICONTROL Enabled]** （漂移調解器） — 執行排程的漂移調解器，將[!DNL Adobe Commerce Optimizer]與[!DNL Adobe Commerce]投影狀態進行比較，並修復或報告差異。

- **[!UICONTROL Automatically Repair Drift]** — 當設為&#x200B;**[!UICONTROL Yes]**&#x200B;時，排定的執行會將[!DNL Adobe Commerce Optimizer]收斂回[!DNL Adobe Commerce]以進行可修復的漂移。 設定為&#x200B;**[!UICONTROL No]**&#x200B;時，排定的執行只會偵測並記錄漂移；孤立的專案一律會回報，永遠不會自動移除。 此設定只會影響排定的調解器。 此頁面上的&#x200B;**[!UICONTROL Reconcile & Repair]**&#x200B;動作一律會修復漂移。 請參閱[選擇監視或修復](#choose-monitoring-or-repair)。

如需每個設定的詳細資訊，請參閱&#x200B;*[!DNL Commerce Admin]指南*&#x200B;中的[ACO目錄檢視同步設定](https://experienceleague.adobe.com/en/docs/commerce-admin/configuration-reference/services/aco-catalog-view-sync.md)。

## 選擇監視或修復 {#choose-monitoring-or-repair}

[!DNL Adobe Commerce]一律是B2B共用型錄的型錄檢視、原則、價格簿和主要設定的真實來源。 如果您或其他管理員直接在[!DNL Adobe Commerce Optimizer] Studio中變更原則、價格簿或金鑰組態設定，調解會將組態差異報告為漂移。

- 選取「**[!UICONTROL Reconcile]**」以檢查漂移，而不變更任何專案，這樣您就可以在採取行動之前檢視差異。
- 選取&#x200B;**[!UICONTROL Reconcile & Repair]**&#x200B;以還原任何可修復的漂移的預期組態。

若要檢閱變更的內容及原因，請開啟目錄檢視的詳細資訊頁面，並檢查其漂移歷史記錄。

## 檢閱孤立和刪除的專案 {#review-orphaned-and-deleted-entries}

**[!UICONTROL Orphaned in ACO]**&#x200B;和&#x200B;**[!UICONTROL Deleted]**&#x200B;標籤涵蓋聯結器無法自動修復的兩個情況，因為沒有要調解的[!DNL Adobe Commerce]共用目錄：

- **[!UICONTROL Orphaned in ACO]** — 聯結器會報告處於同步狀態及在漂移調解期間孤立的實體。 即使調解在啟用修復的情況下執行，它也不會採用或自動刪除它們。

  當實體存在於[!DNL Adobe Commerce Optimizer]中時為孤立實體，但聯結器並未追蹤該實體或將其與追蹤的目錄檢視建立關聯。 當實體由其他整合手動建立，或在聯結器作業中斷後留下時，就會發生這種情況。

  - **目錄檢視** — 聯結器未追蹤檢視。 選取目錄檢視連結以在[!DNL Adobe Commerce Optimizer] Studio中開啟[目錄檢視]詳細資訊頁面。 如果不再需要該目錄檢視，請將其移除。

  - **受限制的存取金鑰** — 沒有即時目錄檢視參考該金鑰。 選取目錄檢視連結以在[!DNL Adobe Commerce Optimizer] Studio中開啟[目錄檢視]詳細資訊頁面。 檢閱設定的存取金鑰，並在不再需要時將其移除。

  - **原則** — 聯結器不會追蹤原則，而且沒有即時目錄檢視參考它。 選取原則連結以在[!DNL Adobe Commerce Optimizer] Studio中開啟它。  檢閱它，並在不再需要它時將其移除。

- **[!UICONTROL Deleted]** — 您已刪除[!DNL Adobe Commerce]中的共用目錄，其目錄檢視投影隨後已移除。 這些列會保留90天，以記錄所移除的內容。

>[!MORELIKETHIS]
>
> - [目錄檢視同步狀態監視](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/catalog-view-sync-status.md){target="_blank"} — *Commerce管理指南*&#x200B;中目錄檢視同步狀態頁面的完整檔案參考 — >
> - [管理資料同步處理](data-sync-status.md) — 驗證產品、價格和類別摘要同步處理
> - [私人目錄檢視](/help/optimizer/setup/private-catalog-view.md) — 瞭解什麼是聯結器管理的私人目錄檢視
> - [受限制的存取金鑰](/help/optimizer/setup/restricted-access-keys.md) — 瞭解聯結器管理的金鑰如何運作
> - [監視B2B共用目錄變更](get-started-b2b-shared-catalogs.md#monitor-b2b-shared-catalog-changes) — 瞭解聯結器會自動為B2B共用目錄執行哪些動作
