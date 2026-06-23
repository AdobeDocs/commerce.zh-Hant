---
source-git-commit: e7d9c056ef8d565b4a143b05ff4e06d607fbfa8e
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---
# 驗證Commerce服務資料同步

若要確認資料同步處理是否正常運作，請確認已成功從[!DNL Adobe Commerce]匯出資料，且資料已成功傳遞至連線的Commerce服務。 使用您部署的控制面板來檢查兩個步驟。

從匯出開始，然後確認傳送。

1. 在「Commerce管理員」中檢查同步狀態。

   前往&#x200B;**[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**。

   ![具有摘要專案狀態報告的[資料摘要同步處理狀態]頁面](/help/data-export/assets/data-feed-sync-status.png){width="800" zoomable="yes"}

   同步執行時，摘要資料會顯示已成功傳送的記錄。 選取摘要以檢視詳細資料或疑難排解同步問題。

1. 確認資料已傳送至連線的Commerce服務。

   從Commerce Admin移至&#x200B;**[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Management Dashboard]**。

   ![資料管理儀表板顯示已連線之Commerce服務中的同步目錄資料](/help/data-export/assets/data-management-dashboard.png){width="700" zoomable="yes"}

   確認已出現預期的產品、價格和屬性。

>[!TIP]
>
>如果您有任何其他資料同步問題，請參閱[檢閱記錄檔及疑難排解](/help/data-export/troubleshooting/logging.md)。

