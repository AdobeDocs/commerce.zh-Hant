---
title: SaaS資料匯出命令列介面
description: 瞭解如何使用命令列介面命令來管理Adobe Commerce SaaS服務 [!DNL data export extension] 的摘要和程式。
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---

# SaaS資料匯出命令列介面參考

開發人員和系統管理員可以使用[Adobe Commerce命令列工具](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/config-cli) (CLI)，管理SaaS資料匯出的同步作業。 `saas:resync`命令包含在`magento/saas-export`封裝中。

Adobe不建議定期使用`saas:resync`命令。 使用指令的典型情況如下：

- 初始同步
- [SaaS資料空間識別碼](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas)已變更，您必須將資料同步處理至新的資料空間。
- 疑難排解

## 初始同步

>[!NOTE]
>如果您使用「即時搜尋」或「產品建議」，就不需要執行初始同步。 此程式會在您將服務連線至您的Commerce執行個體後自動啟動。

當您從命令列觸發`saas:resync`時，視您的目錄大小而定，可能需要幾分鐘到幾小時的時間才會更新資料。

對於初始同步，Adobe建議依照以下順序執行命令：

```bash
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

## 命令範例

在使用`saas:resync`命令之前，請先檢閱[選項說明](#command-options)。

- 執行實體摘要的完整重新同步。

  ```
  bin/magento saas:resync --feed='<FEED_NAME>' 1
  ```

  已成功匯出的摘要不會重新同步。

- 完全重新同步指定的摘要和清理資料

  ```
  bin/magento saas:resync --feed='FEED_NAME' --cleanup-feed
  ```

  僅在執行[!DNL Data Space ID Cleanup]作業之後使用。

- 如需立即匯出摘要，請重新傳送所有資料至連線的Commerce服務，而不會截斷摘要表格中的索引資料

  ```
   bin/magento saas:resync --feed='FEED_NAME' --no-reindex
  ```

- 列出可用的命令和選項以及說明。

  ```
  bin/magento saas:resync --help
  ```

## 命令選項

下列選項可用於管理`saas:resync`作業。

>[!NOTE]
>
>`saas:resync`命令也支援進階選項，藉由增加批次大小和新增多執行緒處理來改善資料匯出命令。 請參閱[自訂匯出處理](customize-export-processing.md)。

### `feed`

這個必要選項指定要重新同步處理的摘要實體，例如`products`。

`feed`選項值可包含任何可用的實體摘要：

- `products`：產品資料摘要
- `productAttributes`：產品屬性資料摘要
- `categories`：類別資料摘要
- `variants`：可設定的產品變數資料摘要
- `prices`：產品價格資料摘要
- `categoryPermissions`：類別許可權資料摘要
- `productOverrides`：產品許可權資料摘要
- `inventoryStockStatus`：庫存狀態資料摘要
- `scopesWebsite`：有商店和商店檢視資料摘要的網站
- `scopesCustomerGroup`：客戶群組資料摘要
- `orders`：銷售訂單資料摘要

視已安裝的[Commerce Services](../landing/saas.md)而定，`saas:resync`命令可能有不同的摘要集。

### `no-reindex`

此選項會將現有的目錄資料重新提交至[!DNL Commerce Services]，而不重新索引。 如果未指定此選項，則命令會在同步資料之前執行完整重新索引。

此選項的行為取決於摘要是以[舊版或立即匯出模式](data-synchronization.md#synchronization-modes)匯出

- 對於舊版匯出摘要，同步程式不會截斷摘要表格中的索引資料。 而是將所有資料重新傳送至Adobe Commerce服務。
- 對於立即匯出摘要，如果指定，則會忽略此選項。 對於這些摘要，重新同步程式不會截斷索引，而只會重新同步更新或先前失敗的專案。

### `cleanup`

此選項會在同步之前清除摘要索引器表格。 指定後，SaaS資料匯出會針對指定的摘要執行完全重新同步，並清除摘要表格中的所有現有資料。

Adobe建議僅在執行[!DNL Data Space ID Cleanup]作業之後使用此命令。

>[!WARNING]
>
>**請勿定期使用此選項**。 這可能會導致Adobe Commerce Services出現資料同步問題。 例如，如果使用`cleanup`選項，`delete product event`可能不會傳播至Adobe Commerce服務。

## 疑難排解

如果您在連線的Commerce服務中未看到預期的資料，請檢查資料匯出錯誤記錄檔，並使用`saas:resync`命令搭配環境變數來檢閱裝載和效能分析工具資料，以疑難排解問題。 檢視[檢閱記錄檔及疑難排解](troubleshooting-logging.md)。
