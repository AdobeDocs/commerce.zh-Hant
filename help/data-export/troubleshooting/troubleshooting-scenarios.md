---
title: 疑難排解 [!DNL SaaS Data Export]的情況
description: 瞭解如何診斷並解決因設定錯誤、索引器設定或同步結果誤解所導致的意外 [!DNL SaaS Data Export] 同步行為。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案（Adobe管理的PaaS基礎結構）和內部部署專案的Adobe Commerce 。"
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: c32adafa-ed01-4b31-997e-2413013911b0id: e7dae43f-215c-4cdf-90d3-c5a461a6e669id: c18ed297-2187-4aec-affb-9d9654eca6fc
subfeature_v2: id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 991
ht-degree: 0%

---


# [!DNL SaaS Data Export]的疑難排解案例

此頁面說明在使用[!DNL SaaS Data Export]時可能會觀察到的行為，這些行為通常是由設定錯誤或錯誤解讀同步結果所造成。 請依照下列說明找出根本原因並套用適當的解決方法。

## Commerce服務中缺少可設定或套件組合產品 {#configurable-bundle-missing}

**問題：**&#x200B;可設定或套件組合產品在[!DNL Adobe Commerce]中具有&#x200B;*已啟用*&#x200B;狀態，但未在店面傳回或在Commerce SaaS服務中顯示&#x200B;*已停用*&#x200B;狀態。

**原因：**&#x200B;複合產品的有效狀態取決於其子產品的狀態，而不只是父產品的狀態。 Commerce SaaS服務會反映此運算狀態：

- **可設定的產品** — 至少必須啟用一個產品變體。
- **套裝產品** — 每個必要的套裝選項至少必須啟用一個產品。

如果不符合這些條件，即使父產品的狀態設定為&#x200B;*已啟用*，父產品也會被視為已停用。

**解決方案：**

- 針對可設定產品，請確認至少有一個相關聯的簡單產品變體已啟用，並指派給正確的網站和商店檢視。
- 若是套件組合產品，請檢查每個必要的套件組合選項是否至少具有一個已啟用的子產品。 包含所有已停用子項的必要選項會導致整個套件組合被視為已停用。
- 啟用適當的子產品後，觸發重新同步或等待下一個排程同步，然後在Commerce SaaS服務中確認更新狀態。

## 目錄價格規則啟用後未更新價格 {#prices-not-updated}

**問題：**&#x200B;使用「排程更新」功能啟用型錄價格規則後，價格不會更新。 套用排定的更新後，`commerce-data-export.log`會顯示`prices`摘要的`synced: 0`。

**原因：**&#x200B;當已排程的更新用於目錄價格規則時，cron群組之間可能會發生競爭狀況。 `catalog_data_exporter_product_prices`索引器可能在其相依性`catalogrule_product`索引完成重建之前執行。 因此，價格匯出程式會讀取過時資料，且不會匯出任何變更。

**解決方案：**

此問題的即時修正是一種解決方法：將兩個cron群組都設定為依序執行以消除競爭條件：

1. 前往「**[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Advanced]** > **[!UICONTROL System]** > **[!UICONTROL Cron (Scheduled Tasks)]**」。
1. 將&#x200B;**[!UICONTROL Use Separate Process]**&#x200B;設定為&#x200B;**[!UICONTROL No]**，兩者皆為：
   - 群組&#x200B;**[!UICONTROL index]**&#x200B;的Cron組態選項
   - 群組&#x200B;**[!UICONTROL staging]**&#x200B;的Cron組態選項
1. 儲存後排清設定快取。

>[!NOTE]
>
>當兩個群組都在處理中執行並循序執行時，緩慢的完整重新索引區塊會停止執行，直到它完成為止。 在大型目錄中，這可能會延遲中繼更新。

## [!DNL Adobe Commerce]與連線服務之間的目錄資料不一致 {#catalog-data-discrepancy}

**問題：**&#x200B;連線的Commerce服務中顯示的產品資料（例如[!DNL Live Search]或[!DNL Product Recommendations]）與[!DNL Adobe Commerce]中的目錄資料不符。 例如，產品名稱、價格或說明在店面看來過時或不正確。

**原因：**&#x200B;觸發重新同步後，最多可能需要一小時的時間才會更新資料並反映在UI元件中。 如果差異持續超過該視窗，表示上次同步處理可能未擷取該專案，或同步處理未偵測到變更，因為摘要資料已標示為最新。

**解決方案：**

1. 從Commerce店面，開啟搜尋結果。 然後，選取相關產品以開啟其詳細檢視。
1. 複製JSON輸出，並確認其符合您在[!DNL Commerce]目錄中所擁有的內容。
1. 如果內容不符，請對目錄中的產品進行微幅編輯，例如新增空格或句點，以強制偵測變更。
1. 等候重新同步或從CLI或Admin中的[[!UICONTROL Data Feed Sync Status]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)頁面觸發手動重新同步。

如需[!DNL Product Recommendations]中目錄資料的其他疑難排解，請參閱Commerce知識庫中的[產品建議模組疑難排解](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-product-recommendations-module-in-magento-commerce)。

## 資料同步未依排程執行 {#sync-not-on-schedule}

**問題：**&#x200B;資料同步處理未依排程執行，或無任何專案正在同步處理，儘管[!DNL Adobe Commerce]中有產品變更。

**原因：**&#x200B;最常見的原因是cron工作未執行，或未在&#x200B;**[!UICONTROL Update by Schedule]**&#x200B;模式中設定索引子。

**解決方案：**

- [確認cron工作正在執行](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues)。
- 確認下列摘要的索引子已設定為&#x200B;**[!UICONTROL Update by Schedule]**：目錄屬性、產品、產品覆寫和產品變體。 在Commerce管理員中或使用CLI從[[!UICONTROL Index Management]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management)檢查： `bin/magento indexer:show-mode | grep -i feed`。

## 目錄同步處理具有「失敗」狀態 {#catalog-sync-failed}

**問題：**&#x200B;目錄同步處理在&#x200B;**[!UICONTROL Data Feed Sync Status]**&#x200B;頁面上顯示&#x200B;**失敗**&#x200B;狀態。

**原因：**&#x200B;在資料收集或提交階段期間發生無法復原的錯誤。 常見原因包括API驗證問題、網路錯誤或資料驗證失敗。

**解決方案：**

1. 請檢閱資料匯出錯誤記錄檔，以取得失敗的詳細資訊。 請參閱[檢閱記錄檔及疑難排解](logging.md)，以取得記錄檔格式及擴充的記錄檔選項：
   - `var/log/commerce-data-export-errors.log`在資料收集期間發生錯誤。
   - `var/log/saas-export-errors.log`資料提交期間發生錯誤。
1. 如果錯誤與組態或協力廠商延伸無關，請[提交支援票證](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket)以及相關記錄專案。

## 記錄顯示「作業已略過 — 處理程式已鎖定」訊息 {#process-locked}

**問題：** `commerce-data-export.log`檔案包含類似下列的專案：

```json
{"feed":"products","operation":"partial sync","status":"operation skipped - process locked by \"full sync(1234)\"", ...}
```

**原因：**&#x200B;這是預期行為，而非錯誤。 當已在進行完整重新索引或`saas:resync`時，cron觸發的部分同步嘗試執行時，會顯示此訊息。 [!DNL SaaS Data Export]擴充功能使用摘要鎖定機制，以防止發生衝突的並行同步處理作業。

**解決方案：**

不需要採取任何動作。 當執行中的程式完成並解除鎖定後，下一個cron執行就會擷取並同步任何暫止的變更。 如需鎖定機制運作方式的詳細資訊，請參閱[ SaaS資料匯出的摘要鎖定機制](../feed-lock-mechanism.md)。

>[!MORELIKETHIS]
>
> - [檢閱記錄檔並進行疑難排解](logging.md)
> - [記錄檔代碼參考](log-codes-reference.md)
> - SaaS資料匯出的摘要鎖定機制[](../feed-lock-mechanism.md)
