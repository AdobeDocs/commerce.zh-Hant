---
title: 支援SaaS目錄資料匯出中的自訂產品型別
description: 瞭解Commerce Storefront MCP目錄啟用模組如何讓SaaS資料匯出將無法辨識的自訂第三方產品型別顯示為傳送至即時搜尋和目錄服務的目錄資料中的簡單產品。
role: Admin, Developer
hide: true
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
source-git-commit: fd87417a494987f33009d386019d870b306dcf73
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%
---
# 支援SaaS目錄資料匯出中的自訂產品型別

>[!IMPORTANT]
>
>自訂產品型別的支援目前是在&#x200B;**早期存取**&#x200B;中，屬於[!DNL Commerce Storefront MCP]的一部分。 Adobe Commerce版本2.4.4及更新版本支援此模組。 可用性、封裝和安裝需求在正式發行之前可能會有所變更。 若要要求此&#x200B;**搶先存取**&#x200B;的邀請，請傳送電子郵件至[commerceeap@adobe.com](mailto:commerceeap@adobe.com)。 Adobe團隊會採取後續步驟和資格要求來回應。

## 概觀

[!DNL SaaS Data Export]在為連線的Adobe Commerce服務（例如[即時搜尋](../live-search/overview.md)和[目錄服務](../catalog-service/overview.md)）準備目錄資料時，可辨識標準Commerce產品型別（簡單、可設定、套件組合等）。 協力廠商擴充功能可引入[!DNL SaaS Data Export]無法原生辨識的&#x200B;**自訂產品型別**。

Commerce Storefront MCP目錄啟用模組可讓[!DNL SaaS Data Export]在輸出目錄裝載中，將這些無法辨識的自訂產品型別表示為&#x200B;**簡單產品**，因此使用[!DNL Commerce Storefront MCP]的購物者可以透過目錄支援的服務來探索這些產品。

## 行為的範圍

- Commerce Storefront MCP目錄啟用模組不會變更Adobe Commerce中儲存的產品型別。 將自訂產品型別表示為簡單產品僅適用於傳送至[!DNL Live Search]和[!DNL Catalog Service]的目錄資料。
- 不需要管理員設定或執行階段設定。 標準產品型別會繼續正常匯出。
- 此模組會鎖定協力廠商擴充功能匯入的自訂產品型別，而非標準Commerce產品型別。

## 安裝模組

若要啟用Commerce Storefront MCP目錄啟用模組，請從命令列執行以下命令：

```bash
composer require magento/module-storefront-mcp-enablement --no-update
composer update magento/module-storefront-mcp-enablement --with-dependencies
bin/magento setup:upgrade
```

## 重新同步目錄資料

安裝模組不會變更Adobe Commerce中的基礎產品資料，因此不會自動重新匯出現有的自訂產品型別專案。 若要將新的簡單產品表示套用至安裝模組之前已同步的目錄資料，請手動重新同步目錄資料。 請參閱[手動重新同步資料](data-sync-manage.md#manually-resync-data)。
