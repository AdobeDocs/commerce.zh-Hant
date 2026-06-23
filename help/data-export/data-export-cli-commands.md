---
title: 使用Commerce CLI同步摘要
description: 瞭解如何使用Commerce CLI命令來管理Adobe Commerce SaaS服務中 [!DNL data export extension] 的摘要和同步程式。
autotag-review: '2026-06-17T15:08:59.000Z'
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
TQID: 'https://experienceleague.adobe.com/Vi8hMKOBjTPkSQp0t8DCkjZsJ8s3Q5GSbSXyX2gmWRo'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: ef1a9efc579d8d21c145e6981235489a2e4ea203
workflow-type: tm+mt
source-wordcount: 728
ht-degree: 0%

---

# 使用Commerce CLI同步摘要

`magento/saas-export`封裝中的`saas:resync`命令可讓您管理[!DNL Adobe Commerce] SaaS服務的資料同步處理。

>[!NOTE]
>
>`saas:resync`命令也適用於[!DNL Adobe Commerce Optimizer Connector]摘要，例如`products`、`categories`和`priceBooks`。 如需聯結器摘要和索引器名稱的完整清單，請參閱[支援的摘要](../aco-connector/reference/connector-reference.md#supported-feeds)。

Adobe不建議定期使用`saas:resync`命令。 使用指令的典型情況如下：

- 初始同步
- 變更[SaaS資料空間ID](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas)後，將資料同步處理至新的資料空間
- 疑難排解

監視`var/log/saas-export.log`檔案中的同步作業。

## 初始同步

>[!NOTE]
>
>啟用「即時搜尋」或「產品推薦」時，初始同步會自動執行。 不需要手動指令。
>
>對於[!DNL Adobe Commerce Optimizer Connector]部署，`aco:config:init`命令會透過讓所有聯結器摘要索引器失效來排程初始完整同步。 請參閱[啟用 [!DNL Commerce Optimizer] 整合](../aco-connector/get-started.md#enable-the-adobe-commerce-optimizer-integration)和[管理與 [!DNL Commerce Optimizer]](../aco-connector/data-sync-manage.md)的同步處理。

當您從命令列觸發`saas:resync`時，視您的目錄大小而定，可能需要幾分鐘到幾小時的時間才會更新資料。

摘要同步可以任何順序執行 — 它們之間沒有硬性相依性。 下列順序會先從範圍資料開始，這是邏輯起點，因為範圍會定義其他摘要參考的存放區檢視。

```shell
bin/magento saas:resync --feed scopesWebsite
bin/magento saas:resync --feed scopesCustomerGroup
bin/magento saas:resync --feed productAttributes
bin/magento saas:resync --feed categories
bin/magento saas:resync --feed products
bin/magento saas:resync --feed prices
bin/magento saas:resync --feed variants
bin/magento saas:resync --feed productoverrides
```

>[!NOTE]
>
>您的環境可能不包括此序列中的每個摘要。 如需完整摘要清單、CLI摘要名稱以及模組需求，請參閱[支援的摘要](reference/feed-table-reference.md#supported-feeds)。

## 命令選項

`saas:resync`命令支援各種同步作業：

- 透過SKU進行部分同步
- 繼續已中斷的同步
- 驗證資料而不同步

檢視所有命令選項和旗標：

```shell
bin/magento saas:resync --help
```

如需選項說明及範例，請參閱下列章節。

>[!NOTE]
>
>如需管理匯出處理的進階選項，請參閱[自訂匯出處理](customize-export-processing.md)。

## `--feed`

必填。 指定要重新同步的摘要實體。

`bin/magento saas:resync --help`檔案命令選項和旗標。 它不會列出您環境中可用的每個摘要。 如需包含CLI摘要名稱、索引器ID和摘要表格的完整摘要清單，請參閱[支援的摘要](reference/feed-table-reference.md#supported-feeds)。

>[!NOTE]
>
>已安裝的模組會決定您可以重新同步哪些摘要。 例如，`productOverrides`需要雲端、內部部署或Commerce as a Cloud Service上的[!DNL Adobe Commerce]，而`orders`需要銷售訂單模組。

>[!NOTE]
>
>`saas:resync`命令只會傳輸新專案、更新的專案，以及先前無法匯出的專案。 會略過自上次匯出以來內容雜湊未變更的專案。

**範例：**

```shell
bin/magento saas:resync --feed products
```

## `--by-ids`

依其ID部分重新同步特定實體。 支援`products`、`productAttributes`、`productOverrides`、`inventoryStockStatus`、`prices`、`variants`和`categoryPermissions`摘要。

依預設，當您使用`--by-ids`選項時，您會使用產品SKU值來指定值。 若要改用產品ID，請新增`--id-type=productId`選項。

>[!NOTE]
>
>與標準重新同步不同，`--by-ids`會略過雜湊驗證，並強制將指定的實體提交至連線的Commerce服務，無論其內容在上次匯出後是否有所變更。

**範例：**

```shell
bin/magento saas:resync --feed products --by-ids='ADB102,ADB111,ADB112'

bin/magento saas:resync --feed products --by-ids='1,2,3' --id-type='productId'
```

## `--cleanup-feed`

在重新索引並將資料傳送到SaaS之前，請清理摘要索引器表格。 僅支援`products`、`productAttributes`、`productOverrides`、`inventoryStockStatus`、`prices`、`variants`和`categoryPermissions`。

如果與`--dry-run`選項搭配使用，該作業會針對所有專案執行試執行重新同步作業。

>[!WARNING]
>
>使用包含`cleanup-feed`選項的resync命令會清除本機摘要匯出狀態，並可能導致不完整的同步。 例如，[!DNL Adobe Commerce]中的實體刪除可能不會反映在連線的Commerce Services中，或即使在[!DNL Adobe Commerce]中刪除或更新，過時的實體仍可能保留在遠端Commerce Services索引中。 此選項僅適用於完整環境重建，例如SaaS資料空間清理後。

**範例：**

```shell
bin/magento saas:resync --feed products --cleanup-feed
```

## `--continue-resync`

繼續執行中斷的重新同步作業。 僅支援`products`、`productAttributes`和`productOverrides`摘要。

**範例：**

```shell
bin/magento saas:resync --feed productAttributes --continue-resync
```

## `--dry-run`

執行摘要重新索引程式，而不將摘要提交至SaaS且不儲存至摘要表格。 此選項對於識別資料集的任何問題很有用。

新增`EXPORTER_EXTENDED_LOG=1`環境變數以將裝載儲存至`var/log/saas-export.log`。

**範例：**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed products --dry-run
```

### 測試特定摘要專案

將`--by-ids`選項與擴充的記錄集合一起新增，以測試特定的摘要專案，在`var/log/saas-export.log`檔案中檢視產生的裝載。

**範例：**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed products --dry-run --by-ids='ADB102,ADB111,ADB112'
```

### 測試所有摘要專案

依預設，在`resync --dry-run`作業期間提交的摘要僅包含新專案，或先前無法匯出的專案。 若要在要處理的摘要中包含所有專案，請使用`--cleanup-feed`選項。

**範例：**

```shell
bin/magento saas:resync --feed products --dry-run --cleanup-feed
```

## `--no-reindex`

重新提交現有的目錄資料至[!DNL Commerce Services]，而不重新索引。 不支援產品相關摘要。

行為因[匯出模式](sync-overview.md#synchronization-modes)而異：

- 舊版模式：重新提交所有資料而不截斷。
- 立即模式：忽略選項，僅同步更新/失敗。

**範例：**

```shell
bin/magento saas:resync --feed productAttributes --no-reindex
```

>[!MORELIKETHIS]
>
> - [檢閱記錄檔並疑難排解](troubleshooting/logging.md) — 診斷資料匯出和SaaS匯出錯誤。
> - [疑難排解案例](troubleshooting/troubleshooting-scenarios.md) — 解決設定錯誤和意外的同步處理結果。
> - [同步如何運作](sync-overview.md) — 瞭解同步模式及重試行為。
