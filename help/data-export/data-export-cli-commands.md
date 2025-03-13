---
title: 使用Commerce CLI同步摘要
description: 瞭解如何使用命令列介面命令來管理Adobe Commerce SaaS服務 [!DNL data export extension] 的摘要和程式。
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
source-git-commit: 086a571b69e8ad76a912c339895409b0037642b9
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---

# 使用Commerce CLI同步摘要

`magento/saas-export`封裝中的`saas:resync`命令可讓您管理Adobe Commerce SaaS服務的資料同步處理。

Adobe不建議定期使用`saas:resync`命令。 使用指令的典型情況如下：

- 初始同步
- 變更[SaaS資料空間ID](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas)後，將資料同步處理至新資料空間
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

依其ID部分重新同步特定實體。 支援`products`、`productAttributes`和`productOverrides`摘要。

依預設，實體是由產品SKU指定的。 使用`--id-type=ProductID`以改用產品ID。

**範例：**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --by-ids='<SKU-1>,<SKU-2>,<SKU-3>'

bin/magento saas:resync --feed='<FEED_NAME>' --by-ids='<ID-1>,<ID-2>,<ID-3>' --id-type='productId'
```

## `--cleanup-feed`

在重新索引並將資料傳送到SaaS之前，先清理摘要索引器表格。 僅支援`products`、`productOverrides`和`prices`摘要。

>[!IMPORTANT]
>
>僅在環境清理後使用。 可能會導致Commerce Services出現資料同步問題。

**範例：**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --cleanup-feed
```

## `--continue-resync`

繼續執行中斷的重新同步作業。 僅支援`products`、`productAttributes`和`productOverrides`摘要。

**範例：**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --continue-resync
```

## `--dry-run`

執行摘要重新索引程式，而不提交至SaaS或儲存至摘要表格。 使用驗證資料。

新增`EXPORTER_EXTENDED_LOG=1`環境變數以將裝載儲存至`var/log/saas-export.log`。

**範例：**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed='<FEED_NAME>' --dry-run
```

## `--feed`

必填。 指定要重新同步的摘要實體。

可用的摘要：

- `categories`
- `categoryPermissions`
- `inventoryStockStatus`
- `orders`
- `prices`
- `products`
- `productAttributes`
- `productOverrides`
- `scopesWebsite`
- `scopesCustomerGroup`
- `variants`

**範例：**

```shell
bin/magento saas:resync --feed='<FEED_NAME>'
```

## `--no-reindex`

重新提交現有的目錄資料至[!DNL Commerce Services]，而不重新索引。 不支援產品相關摘要。

行為因[匯出模式](data-synchronization.md#synchronization-modes)而異：

- 舊版模式：重新提交所有資料而不截斷。
- 立即模式：忽略選項，僅同步更新/失敗。

**範例：**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --no-reindex
```

## 疑難排解

如果您在連線的Commerce服務中未看到預期的資料，請檢查資料匯出錯誤記錄檔，並使用`saas:resync`命令搭配環境變數來檢閱裝載和效能分析工具資料，以疑難排解問題。 檢視[檢閱記錄檔及疑難排解](troubleshooting-logging.md)。
