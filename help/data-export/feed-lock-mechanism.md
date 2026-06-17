---
title: SaaS資料匯出的饋送鎖定機制
description: 瞭解 [!DNL SaaS Data Export] 如何使用摘要鎖定，以防止衝突的同步作業，並在同時更新摘要期間保護資料完整性。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Services
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
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 355
ht-degree: 0%

---


# SaaS資料匯出的饋送鎖定機制

[!DNL SaaS Data Export]擴充功能使用摘要鎖定機制，以防止多個處理序同時同步處理相同摘要時發生競爭情形。 例如，當cron觸發的重新同步與手動`saas:resync` CLI呼叫重疊時，就可能發生這種情況。

## 摘要鎖定的運作方式

每個摘要同步作業（不論是由cron作業或手動`saas:resync` CLI呼叫所觸發）都遵循相同的順序：

1. 該程式會嘗試取得摘要鎖定。 鎖定嘗試不會受阻，如果鎖定已被其他處理序保留，則會立即傳回。
1. 如果鎖定為&#x200B;**無法使用**，則會略過作業並加以記錄。

   不會遺失任何資料。 下次cron執行會在目前程式完成後挑選擱置的變更。
1. 如果鎖定為&#x200B;**已取得**，處理序會記錄其名稱和PID以供診斷之用，然後執行同步。
1. 當同步完成或失敗時，鎖定會無條件釋放，以便下一個排程的cron工作可正常繼續。

一次只能有一個同步作業可以保持摘要鎖定，無論它是由cron啟動還是由CLI啟動。 摘要鎖定是透過[!DNL Adobe Commerce]的`LockManagerInterface`實作。 預設後端是MySQL，它使用`GET_LOCK`和`RELEASE_LOCK`函式。 若要設定不同的鎖定提供者，請參閱[設定鎖定提供者](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/lock-provider){target="_blank"}。

## 預期的記錄訊息

`commerce-data-export.log`中的下列訊息是正常的，並不表示有問題：

```json
{"feed":"products","operation":"partial sync","status":"operation skipped - process locked by \"full sync(1234)\"", ...}
```

當已在進行完整重新索引或`saas:resync`時，cron觸發的部分同步嘗試執行時，會出現此訊息。 略過的作業不會遺失。 當執行中的程式完成並解除鎖定後，下一個cron執行就會擷取並同步任何暫止的變更。

>[!NOTE]
>
>如需`commerce-data-export.log`中記錄之記錄檔格式與作業型別的一般資訊，請參閱[檢閱記錄檔與疑難排解](troubleshooting/logging.md)。

>[!MORELIKETHIS]
>
> - [使用SaaS資料匯出同步處理資料](sync-overview.md)
> - [使用Commerce CLI同步摘要](data-export-cli-commands.md)
> - [聯結器同步管道](../aco-connector/connector-sync-pipeline.md)
> - [設定鎖定提供者](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/lock-provider){target="_blank"}
