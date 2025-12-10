---
title: 使用Commerce CLI同步摘要
description: 瞭解如何使用命令列介面命令來管理Adobe Commerce SaaS服務 [!DNL data export extension] 的摘要和程式。
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
source-git-commit: c6725fc524e9d239ccc0f16701e92ad5d2fc7729
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# 使用Commerce CLI同步摘要

`saas:resync`封裝中的`magento/saas-export`命令可讓您管理Adobe Commerce SaaS服務的資料同步處理。

Adobe不建議定期使用`saas:resync`命令。 使用指令的典型情況如下：

- 初始同步
- 變更[SaaS資料空間ID](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/config/services/saas)後，將資料同步處理至新的資料空間
- 疑難排解

監視`var/log/saas-export.log`檔案中的同步作業。

## 初始同步

>[!NOTE]
>
>啟用「即時搜尋」或「產品推薦」時，初始同步會自動執行。 不需要手動指令。

當您從命令列觸發`saas:resync`時，視您的目錄大小而定，可能需要幾分鐘到幾小時的時間才會更新資料。

對於初始同步，Adobe建議依照以下順序執行命令：

```shell
bin/magento saas:resync --feed productattributes
bin/magento saas:resync --feed products
bin/magento saas:resync --feed scopesCustomerGroup
bin/magento saas:resync --feed scopesWebsite
bin/magento saas:resync --feed prices
bin/magento saas:resync --feed productoverrides
bin/magento saas:resync --feed variants
bin/magento saas:resync --feed categories
bin/magento saas:resync --feed categoryPermissions
```

## 使用CLI命令同步

`saas:resync`命令支援各種同步作業：

- 透過SKU進行部分同步
- 繼續已中斷的同步
- 驗證資料而不同步

檢視所有可用選項：

```shell
bin/magento saas:resync --help
```

如需選項說明及範例，請參閱下列章節。


>[!NOTE]
>
>如需管理匯出處理的進階選項，請參閱[自訂匯出處理](customize-export-processing.md)。

## `--by-ids`

依其ID部分重新同步特定實體。 支援`products`、`productAttributes`、`productOverrides`、`inventoryStockStatus`、`prices`、`variants`和`categoryPermissions`摘要。

依預設，當您使用`--by-ids`選項時，您會使用產品SKU值來指定值。 若要改用產品ID，請新增`--id-type=ProductID`選項。

**範例：**

```shell
bin/magento saas:resync --feed products --by-ids='ADB102,ADB111,ADB112'

bin/magento saas:resync --feed= products --by-ids='1,2,3' --id-type='productId'
```


## `--cleanup-feed`

在重新索引並將資料傳送到SaaS之前，請清理摘要索引器表格。 僅支援`products`、`productAttributes`、`productOverrides`、`inventoryStockStatus`、`prices`、`variants`和`categoryPermissions`。

如果與`--dry-run`選項搭配使用，該作業會針對所有專案執行試執行重新同步作業。

>[!IMPORTANT]
>
>僅在環境清理後使用，或搭配`--dry-run`選項使用。 如果用於其他情況，清理操作可能會導致資料遺失和資料同步問題。

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

**範例**

```shell
bin/magento saas:resync --feed products --dry-run --cleanup-feed
```

## `--feed`

必填。 指定要重新同步的摘要實體。

可用的摘要：

- `categories`
- `categoryPermissions`
- `orders`
- `prices`
- `products`
- `productAttributes`
- `productOverrides`
- `scopesWebsite`
- `scopesCustomerGroup`
- `variants`

>[!NOTE]
>
>根據您的Adobe Commerce環境中安裝的模組，環境中可用的摘要可能會不同。

**範例：**

```shell
bin/magento saas:resync --feed products
```

## `--no-reindex`

重新提交現有的目錄資料至[!DNL Commerce Services]，而不重新索引。 不支援產品相關摘要。

行為因[匯出模式](data-synchronization.md#synchronization-modes)而異：

- 舊版模式：重新提交所有資料而不截斷。
- 立即模式：忽略選項，僅同步更新/失敗。

**範例：**

```shell
bin/magento saas:resync --feed productAttributes --no-reindex
```

## `--id-type=ProductId`

依照預設，當您使用包含`saas:resync feed`選項的`--by-ids`命令時所指定的實體是由產品SKU所指定。 使用`--id-type=ProductId`選項，依產品ID指定實體。

```shell
bin/magento saas:resync --feed products --by-ids='1,2,3' --id-type='productId'
```

**範例：**

## 疑難排解

如果您在連線的Commerce服務中未看到預期的資料，請檢查資料匯出錯誤記錄檔，並使用`saas:resync`命令搭配環境變數來檢閱裝載和效能分析工具資料，以疑難排解問題。 檢視[檢閱記錄檔及疑難排解](troubleshooting-logging.md)。
