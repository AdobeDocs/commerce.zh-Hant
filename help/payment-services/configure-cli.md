---
title: 命令列組態
description: 安裝之後，您可以使用命令列介面(CLI)設定 [!DNL Payment Services] 。
role: Admin, Developer
level: Intermediate
exl-id: 265ab1be-fe52-41f3-85cb-addbc2ddfb17
feature: Payments, Checkout, Configuration, Integration, Paas
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案(Adobe管理的PaaS基礎結構)和內部部署專案的Adobe Commerce 。"
source-git-commit: 870c2497a2d6dcfc4066c07f20169fc9040ae81a
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 0%

---

# 命令列組態

安裝[!DNL Payment Services]之後，您就可以從[在首頁](payments-home.md)中或透過命令列介面(CLI)輕鬆設定它。

## 設定資料匯出

[!DNL Payment Services]結合從[!DNL Magento Open Source]和[!DNL Adobe Commerce]匯出的訂單資料與來自付款提供者的彙總付款資料，以建立有用的報表。 [!DNL Payment Services]擴充功能使用索引器來有效收集報告的所有必要資料。

若要瞭解[!DNL Payment Services]報表中使用的資料，請參閱[訂單付款狀態報表](order-payment-status.md#data-used-in-the-report)。

### 在[!DNL Magento Open Source]上設定cron

若要在`BY SCHEDULE`上使用[!DNL Magento Open Source]索引模式，您必須設定cron。 請參閱[設定並執行cron](https://experienceleague.adobe.com/zh-hant/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs)。

### 設定索引子

使用兩種索引模式之一 — `ON SAVE` （預設）或`BY SCHEDULE` （建議），匯出訂單資料並保留在付款服務中。

下列索引適用於[!DNL Payment Services]：

| 程式碼 | 名稱 | 說明 |
|    ---    |  ---  |  ---  |
| `sales_order_data_exporter` | 銷售訂單摘要 | 建立訂單資料的索引 |
| `sales_order_status_data_exporter` | 銷售訂單狀態摘要 | 建立銷售訂單狀態資料的索引 |
| `store_data_exporter` | 商店資訊源 | 建立存放區資料的索引 |

若要變更所有三個索引器的索引模式，請執行：

```bash
bin/magento indexer:set-mode schedule sales_order_data_exporter sales_order_status_data_exporter store_data_exporter
```

>[!TIP]
>
>如果您未在指令中指定任何索引子，則所有索引子都會更新為相同的值。 如果要變更特定的索引子，必須在指令中列出它。

若要深入瞭解如何手動變更索引器的模式，請參閱開發人員檔案中的[設定索引器](https://experienceleague.adobe.com/zh-hant/docs/commerce-operations/configuration-guide/cli/manage-indexers#configure-indexers){target="_blank"}。 若要瞭解如何在Admin中進行變更，請參閱核心使用手冊中的[索引管理](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/systems/tools/index-management#change-the-index-mode){target="_blank"}。

### 手動重新索引資料

您可以手動重新索引資料，而不是等待資料自動發生。 如需詳細資訊，請參閱[管理索引子](https://experienceleague.adobe.com/zh-hant/docs/commerce-operations/configuration-guide/cli/manage-indexers#reindex){target="_blank"}中的[重新索引](https://experienceleague.adobe.com/zh-hant/docs/commerce-operations/configuration-guide/cli/manage-indexers){target="_blank"}。

設定`BY SCHEDULE`模式時，系統會追蹤變更的實體，而cron作業會根據設定的排程更新這些實體的索引。 請參閱[設定並執行cron](https://experienceleague.adobe.com/zh-hant/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs#config-cli-cron-group-run)中的命令列[從命令列執行cron](https://experienceleague.adobe.com/zh-hant/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs)，瞭解如何使用cron工作手動觸發索引。

### 將重新索引的資料傳送至付款服務

資料編制索引後，會自動傳送給[!DNL Payment Services]。 您也可以使用此命令手動觸發傳送索引資料的程式：

```bash
bin/magento saas:resync --feed [feedName]
```

使用下列命令選項：

| 命令 | 說明 |
|  ---  |  ---  |
| `bin/magento saas:resync --feed [feedName]` | 執行指定摘要的重新索引，並將其傳送至對應的服務 |
| `bin/magento saas:resync --no-reindex` | 略過索引化並從索引傳送未同步的資料 |

`--feed`引數可讓您指定要傳送的摘要：

| 摘要 | 說明 |
|  ---  |  ---  |
| `paymentServicesOrdersProduction` | 生產模式中的訂單摘要 |
| `paymentServicesOrdersSandbox` | 沙箱模式下的訂單摘要 |
| `paymentServicesOrderStatusesProduction` | 生產模式中的訂單狀態 |
| `paymentServicesOrderStatusesSandbox` | 在沙箱模式中的訂單狀態 |
| `paymentServicesStoresProduction` | 以生產模式儲存 |
| `paymentServicesStoresSandbox` | 以沙箱模式儲存 |

如果已設定並安裝cron，則報告所需的所有資料會自動傳送到[!DNL Payment Services]。 您也可以手動觸發傳送cron資料至[!DNL Payment Services]的程式。

```bash
bin/magento cron:run --group payment_services_data_export
```

若要進一步瞭解重新索引和索引子，請參閱開發人員檔案中的[管理索引子](https://experienceleague.adobe.com/zh-hant/docs/commerce-operations/configuration-guide/cli/manage-indexers)主題。

## 透過CLI設定範圍

[!DNL Payment Services]允許商家使用[多個PayPal帳戶](configure-admin.md#use-multiple-paypal-accounts)。 現在，您可以透過CLI變更這些帳戶的範圍。

若要將範圍設定為`website`層級，請執行：

```bash
bin/magento config:set payment/payment_services/mba_scoping_level website
```

若要將範圍設定為`store`層級，請使用：

```bash
bin/magento config:set payment/payment_services/mba_scoping_level store
```

>[!TIP]
>
> 如果您想要將範圍變更為商店層級，請聯絡您的[!DNL Payment Services]銷售代表。

變更範圍後，排清快取以顯示變更：

```bash
bin/magento cache:clean:payment_services_merchant_scopes
```

## 設定L2/L3處理

[!DNL Payment Services]可以處理信用卡付款交易的層級2與層級3資料，為商家提供其他資訊。

>[!WARNING]
>
> 透過PayPal與第2層及第3層處理功能整合，僅適用於美國商家。 如需詳細資訊，請參閱PayPal開發人員檔案中的[付款處理](https://developer.paypal.com/docs/checkout/advanced/processing/){target=_blank}。

如果您想要使用L2/L3處理[!DNL Payment Services]的資料，或您有任何問題，請洽詢您的[!DNL Payment Services]帳戶管理員。

若要瞭解[!DNL Payment Services]中使用的L2與L3處理，請參閱[Level 2與Level 3處理](levels-card-payment-transactions.md)。
