---
title: 檢視AEM Assets同步狀態
description: 在Commerce管理員中以資產為中心的清單中，檢閱已同步資產。
feature: CMS, Media, Integration
source-git-commit: 446739ffad0da97e2e923e6e02be3f8f6b3eb2b3
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---


# 檢視AEM Assets同步狀態

**[!UICONTROL Sync Status]**&#x200B;檢視提供透過AEM Assets整合約步化的以資產為中心的資產清單。 使用它可依資產本身的屬性來尋找、檢閱和疑難排解，而非在目錄中依產品導覽。

![AEM Assets同步處理狀態檢視](../assets/aem-assets-sync-status-view.png){width="700" zoomable="yes"}

>[!NOTE]
>
> [!UICONTROL Sync Status]不適用於[!DNL Adobe Commerce Optimizer]。

## 開啟同步處理狀態

在&#x200B;_管理員_&#x200B;側邊欄中，瀏覽至&#x200B;**[!UICONTROL System]** > **[!UICONTROL AEM Assets]** > **[!UICONTROL Sync Status]**。

![系統功能表中的AEM Assets同步處理狀態](../assets/aem-assets-configuration-admin-menu.png){width="600" zoomable="yes"}

## 整合約步健康狀態

在頁面頂端，**AEM同步狀態**&#x200B;橫幅會摘要說明管道健康情況，以及有多少事件正在等待處理。 選取&#x200B;**[!UICONTROL Refresh]**&#x200B;以更新同步處理狀況橫幅。

## 資產清單

此格線會列出AEM Assets同步管道處理的資產及其目前的同步狀態。 每一列代表一個資產及其Commerce中的同步狀態。 它不代表產品記錄。

| 欄 | 說明 |
|--------|-------------|
| **資產ID** | AEM資產識別碼（例如，`urn:aaid:aem:…`）。 |
| **狀態** | 資產最新同步嘗試的結果。 可能的值為&#x200B;**成功**、**失敗**&#x200B;或&#x200B;**等待**。 |
| **正在處理** | 開始處理資產的日期和時間。 |
| **已分派** | 傳送同步事件的日期和時間。 |
| **錯誤** | 當&#x200B;**狀態**&#x200B;指出失敗時的錯誤訊息；同步成功時為空白。 |

### 篩選資產

1. 選取&#x200B;**[!UICONTROL Filters]**&#x200B;以展開篩選面板。

1. 輸入&#x200B;**資產識別碼**&#x200B;或選擇&#x200B;**狀態**&#x200B;值。

1. 選取&#x200B;**[!UICONTROL Apply Filters]**&#x200B;以更新網格，或選取&#x200B;**[!UICONTROL Cancel]**&#x200B;以關閉面板而不套用變更。

篩選器會套用至資產層級的資料，讓您隔離失敗的同步，或追蹤特定資產而不開啟個別產品。

## 失敗的同步

當&#x200B;**狀態**&#x200B;顯示失敗時，請檢閱網格中的&#x200B;**錯誤**&#x200B;欄，以取得同步處理管道傳回的訊息。

檢閱完整的錯誤訊息和上次同步嘗試的詳細資料，以診斷失敗。

僅[!BADGE PaaS]{type=Informative tooltip="僅適用於雲端專案上的Adobe Commerce （Adobe管理的PaaS基礎結構）。"}如需其他疑難排解，請參閱[預設自動比對](../synchronize/default-match.md)。 整合記錄檔可在您的Commerce執行個體上的`/var/log/aem-assets-integration.log`和`/var/log/aem-assets-integration-errors.log`取得。
