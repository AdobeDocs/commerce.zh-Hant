---
title: 改善SaaS資料匯出效能
description: 瞭解如何使用多執行緒資料匯出模式，改善Commerce服務的SaaS資料匯出效能。
role: Admin, Developer
exl-id: 7151118c-5e30-44d0-b515-5801a73e44ec
source-git-commit: b8b7af1119163589b7d83654b13edae656fea339
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# 改善SaaS資料匯出效能

**多執行緒資料匯出模式**&#x200B;將摘要資料分割成批次，然後並行處理，加速匯出程式。

開發人員或系統整合經銷商可以使用多執行緒資料匯出模式，而不是預設的單執行緒模式，來改善效能。 在單執行緒模式中，摘要提交程式不會平行化。 此外，由於設定了預設限制，所有使用者端都限製為僅使用一個執行緒。 在大多數情況下，不需要自訂設定。

## 使用多執行緒模式的考量事項

使用資料匯出服務時，您想要在確保精確同步的同時最佳化效能。
Adobe建議使用資料擷取的預設設定，這通常符合Commerce商家的同步需求。 但是，在某些情況下，自訂可能會加快處理時間。

在決定是否自訂資料匯出設定時，請考慮下列關鍵因素：

- **初始同步處理** — 評估產品數量，並根據預設組態估算資料量及傳輸時間[。 ](estimate-data-volume-sync-time.md)請自問：您上線Commerce服務後，可以等待此初始資料同步嗎？

- **新增商店檢視或網站** — 如果您計畫在上線後新增具有相同產品數的商店檢視或網站，請估計資料量和傳輸時間。 判斷使用預設設定是否可接受同步化時間，或是是否需要多執行緒處理。

- **一般匯入** — 預期一般匯入，例如價格更新或庫存狀態變更。 評估這些更新是否可以在可接受的時間範圍內套用，或是否需要更快速的處理。

- **產品重量** — 考慮您的產品是輕量還是重量。 如果產品說明或屬性誇大產品大小，請相應地調整批次大小。

請記住，周詳的規劃（包括估計資料量和同步時間）通常可免除自訂需求。 根據這些預估值，排程摘要擷取作業，以獲得最佳結果。

>[!NOTE]
>
>Adobe建議在使用多執行緒處理時務必謹慎。 如果您設定多執行緒以提升效能，可以觸發內含的Adobe Commerce Services護欄，以防止在資料擷取期間誤用系統。 這些護欄也會限制使用者觸發可能使系統過載的同步化變更。 觸發護欄時，請求會遭到封鎖，系統傳回429錯誤。 如果您遇到這些錯誤，請調整您的設定，並提交支援票證以尋求協助。

## 設定多執行緒

所有[同步處理方法](data-synchronization.md#synchronization-process)都支援多重執行緒模式 — 完整同步處理、部分同步處理及失敗專案同步處理。 若要設定多執行緒，請指定同步處理期間要使用的執行緒數目和批次大小。

- `thread-count`是啟動以處理實體的執行緒數目。 預設`thread-count`為`1`。
- `batch-size`是在一個反複專案中處理的實體數目。 除價格摘要外，所有摘要的預設`batch-size`都是`100`記錄。 對於價格摘要，預設值為`500`筆記錄。

您可以在執行resync命令時將多執行緒設定為暫存選項，或將多執行緒組態新增到Adobe Commerce應用程式組態中。

>[!NOTE]
>
>請確定SaaS資料匯出的效能符合為消費者端使用者端定義的速率限制。

### 在執行階段設定多執行緒

當您從命令列執行完整同步處理命令時，請將`thread-count`和`batch-size`選項新增至CLI命令以指定多執行緒處理。

```
bin/magento saas:resync --feed=products --thread-count=2 --batch-size=200
```

命令列上指定的選項會覆寫Adobe Commerce應用程式`config.php`檔案中指定的資料匯出組態。

### 將多執行緒新增至Commerce設定

若要使用多執行緒處理所有資料匯出作業，系統整合經銷商或開發人員可以在Commerce應用程式設定中修改每個摘要的執行緒數目和批次大小。

可將自訂值加入組態檔[的](https://experienceleague.adobe.com/zh-hant/docs/commerce-operations/configuration-guide/files/config-reference-configphp#system)系統區段`app/etc/config.php`，以套用這些變更。

**範例：設定產品與價格的多執行緒**

```php
<?php
return [
    'system' => [
        'default' => [
            'commerce_data_export' => [
                'feeds' => [
                    'products' => [
                        'batch_size' => 100,
                        'thread_count' => 2,
                    ],
                    'prices' => [
                        'batch_size' => 400,
                        'thread_count' => 4,
                    ]
                ]
            ],
//   ...
```
