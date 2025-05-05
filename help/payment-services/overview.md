---
title: ' [!DNL Payment Services]簡介'
description: 瞭解如何為您的 [!DNL Adobe Commerce] 和 [!DNL Magento Open Source] 網站安裝及使用 [!DNL Payment Services] 作為全包式、健全且安全的付款處理解決方案。
role: User
level: Intermediate
feature: Payments, Checkout
exl-id: 1d41f86a-f874-48df-9173-9cf9f07e6d79
source-git-commit: 62b708f79ac011ef33b37f67384df7c94571ced2
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# [!DNL Payment Services]簡介

[!DNL Adobe Commerce]和[!DNL Magento Open Source]的[!DNL Payment Services]是您的turnkey自助式解決方案，包括沙箱測試和簡單的設定，可為您的Commerce網站提供穩定且安全的付款處理。

無論您是小型企業、中端市場競爭者或大型企業，此支付解決方案都能協助您減少營運開銷並增加收入，同時為您提供有用的工具以改善整體購物體驗。

[!DNL Payment Services]是：

* 易於設定與維護
* 專為最大化您的利潤而設計
* 安全無虞
* 專為滿足您的所有支付需求而設計
* 在管理員內獨立

## 功能

[!DNL Payment Services]是您線上結帳的一站式商店（從結算與退款到收取款項）。 它提供強大的工具，讓您獲得所需的洞察力和控制力，為您的買家創造最佳體驗。

* [**上線**](onboard.md) — 程式會引導您完成商業註冊、技術設定、權益、沙箱環境設定和即時付款啟用。
* [**付款選項**](payments-options.md) — 設定付款選項，以自訂商店（或多商店）客戶可用的方式。
* **現金流量管理Financial Reporting** — 將[付款詳細資料](order-payment-status.md)與訂單同步處理，以取得已處理量、付款餘額、[付款](payouts.md)及詳細[交易層級報表](transactions.md)的完整透明度，以進行財務對帳，並充分掌握交易可見度。
* **透明的定價** — 價格是明確且預先的；您所看到的就是您得到的東西。
* **有效的結帳體驗** — 使用[卡存放](vaulting.md)和[立即購買](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/point-of-purchase/checkout-instant-purchase.html?lang=zh-Hant) (預設啟用Adobe Commerce)功能，移除任何快速簡易結帳的障礙，並建立忠實客戶。

## 可用性

[!DNL Payment Services]可用於[!DNL Adobe Commerce]和[!DNL Magento Open Source]。 [!DNL Payment Services]延伸與[!DNL Adobe Commerce]版本2.4.4 - 2.4.7-p3相容。

目前，[!DNL Payment Services]針對下列國家/地區的所有付款選項提供完整支援（透過[進階上線](../payment-services/production.md#advanced-onboarding)）：

* 美國（美國）
* 加拿大（加州）
* 澳洲(AUS)
* 法國(FR)
* 英國（英國）

付款服務在上線期間為其他[&#128279;](../payment-services/production.md#complete-merchant-onboarding)可用國家/地區提供[快速結帳功能](../payment-services/payments-options.md) （付款選項的子集）。

如需發行版本和特定版本的詳細資訊，請參閱[生命週期原則](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/lifecycle-policy.html?lang=zh-Hant)和[[!DNL Payment Services] 發行說明](release-notes.md)頁面。

### 哪個[!DNL Payment Services]選項適合您？

>[!VIDEO](https://video.tv.adobe.com/v/3447929?captions=chi_hant)

如需設定[!DNL Payment Services]擴充功能的詳細資訊，請參閱[連線](connect.md)。

### 接受的信用卡與貨幣

[!DNL Payment Services]接受其可用國家[的貨幣](#availability)。 如需詳細資訊，請參閱[貨幣組態](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration.html?lang=zh-Hant)。

若要檢視PayPal支援哪些貨幣，請參閱[支援的貨幣檔案](https://developer.paypal.com/docs/reports/reference/paypal-supported-currencies/)。

若要檢視PayPal支援的付款方式，請參閱其[付款方式檔案](https://developer.paypal.com/docs/checkout/payment-methods/)。

## 開始使用

上線和設定[!DNL Payment Services]只需幾個步驟即可完成：

1. 取得[[!DNL Payment Services] 擴充功能](install.md)。
1. 將您的Commerce執行個體連線至Commerce Services。
1. 上線並設定沙箱服務。
1. 啟用[!DNL Payment Services]作為您的付款方式，並開始處理測試付款。
1. 完成商家上線以啟用您網站的即時付款。
1. 以即時模式啟動[!DNL Payment Services]以開始處理即時付款。

若要取得完整指示並開始上線程式，請參閱[上線 [!DNL Payment Services]](onboard.md)。
