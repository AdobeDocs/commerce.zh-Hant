---
source-git-commit: 3d05a7307e58ea2758ac4b6f2b70d24b8ea7a5ac
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---
# 驗證Optimizer資料同步

確認資料已成功從Commerce管理員匯出，且資料已成功傳遞至[!DNL Commerce Optimizer]。 從Commerce管理員中的匯出開始，然後在[!DNL Commerce Optimizer]中確認傳遞。

1. **在Commerce管理員中檢查同步狀態：**

   前往&#x200B;**[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**。

   ![具有摘要專案狀態報告的[資料摘要同步處理狀態]頁面](/help/aco-connector/assets/data-feed-sync-status.png){width="700" zoomable="yes"}

   同步執行時，摘要資料會顯示已成功傳送的記錄。 選取摘要以檢視詳細資料或疑難排解同步問題。

1. **確認資料已傳遞至[!DNL Commerce Optimizer]：**

   從[!DNL Commerce Optimizer]功能表選取&#x200B;**[!UICONTROL Data Sync]**。

   Adobe Commerce Optimizer中的![資料同步頁面顯示同步的目錄資料](/help/aco-connector/assets/data-sync.png){width="700" zoomable="yes"}

   確認已出現預期的產品、價格和屬性。

當同步如預期運作時：

- **[!UICONTROL Data Feed Sync Status]**&#x200B;顯示聯結器摘要的成功傳送記錄，沒有未解決的專案層級錯誤。
- [!DNL Commerce Optimizer]中的&#x200B;**[!UICONTROL Data Sync]**&#x200B;列出預期的目錄來源、產品、價格和屬性。

>[!TIP]
>
>如果您有任何資料同步的問題，請參閱[疑難排解](/help/aco-connector/troubleshooting.md)指南。
