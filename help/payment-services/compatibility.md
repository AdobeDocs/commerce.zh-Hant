---
title: ' [!DNL Payment Services]的相容性'
description: 瞭解 [!DNL Payment Services] 是否可在您的國家/地區使用，以及是否可與您的Adobe Commerce版本相容。
role: User
level: Intermediate
feature: Payments, Checkout, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---


# [!DNL Payment Services]的相容性

[!DNL Payment Services]可用於Adobe Commerce和Magento Open Source。 [!DNL Payment Services]現在與Adobe Commerce 2.4.x版相容。

## 先決條件

若要使用[!DNL Payment Services]，您必須先連線您的Commerce執行個體。 **您只設定一次此連線**。

1. 如果您不確定您的執行個體是否已連線，請導覽至&#x200B;**系統** >服務> **Commerce服務聯結器**，並在「沙箱金鑰」和「生產金鑰」區段中檢視公開和私人API金鑰值，並在「SaaS識別碼」區段中檢視「專案」和「資料空間」欄位。 如果這些值存在，表示您的執行個體已連線。

1. 如果您還是需要連線執行個體，請檢視[Commerce服務聯結器](../landing/saas.md)頁面上的指示。

   >[!TIP]
   >
   > 如需詳細資訊，請參閱我們的[Adobe Commerce Services Connector](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector)教學課程影片。

1. 如果您已經連線執行個體，請瀏覽至[上線](onboard.md)頁面以瞭解後續步驟。

>[!IMPORTANT]
>
> 所有擁有[!DNL Payment Services]資格的商家都可以使用&#x200B;**一個生產資料空間**&#x200B;和&#x200B;**兩個測試資料空間**。

## 標準與進階[!DNL Payment Services]體驗

[!DNL Payment Services]會根據您營運的國家/地區，提供&#x200B;**標準** （快速結帳）和&#x200B;**進階** （完全支援）付款選項和上線流程。

>[!NOTE]
>
> [!DNL Payment Services]在上線期間為其他[&#128279;](../payment-services/production.md#complete-merchant-onboarding)可用國家/地區提供[快速結帳功能](../payment-services/payments-options.md) （付款選項的子集）。

### 哪個[!DNL Payment Services]選項適合您？

>[!VIDEO](https://video.tv.adobe.com/v/3447811)

如需設定[!DNL Payment Services]擴充功能的詳細資訊，請參閱[連線](connect.md)。

>[!BEGINTABS]

>[!TAB 標準（快速簽出）]

![簽出](assets/icon-check.png) PayPal簽出

![支票](assets/icon-check.png) PayPal扣款或信用卡按鈕

![檢查](assets/icon-check.png)自訂簽出設定

![check](assets/icon-check.png)標準價格

![檢查](assets/icon-check.png) **在XX國家/地區提供**

[![深入瞭解](assets/learn-more-button.svg)](onboard.md)

>[!TAB 進階（完全支援）]

![支票](assets/icon-check.png)扣帳卡

![支票](assets/icon-check.png) PayPal點數

![檢查](assets/icon-check.png)信用卡欄位

![支票](assets/icon-check.png) Apple付款按鈕

![支票](assets/icon-check.png) Google付款按鈕

![支票](assets/icon-check.png) PayPal付款按鈕

![check](assets/icon-check.png) Venmo按鈕

![支票](assets/icon-check.png) PayPal扣款或信用卡按鈕

![支票](assets/icon-check.png)稍後付款按鈕

![檢查](assets/icon-check.png)自訂簽出設定

![check](assets/icon-check.png)自訂價格

![檢查](assets/icon-check.png) （L2/L3定價功能 — 僅限美國）

![檢查](assets/icon-check.png) **僅於美國（美國）、加拿大(CA)、澳洲(AUS)提供。 法國(FR)、英國(UK)**

[![深入瞭解](assets/learn-more-button.svg)](onboard.md)

>[!ENDTABS]

如需發行版本和特定版本的詳細資訊，請參閱[生命週期原則](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/lifecycle-policy.html)和[[!DNL Payment Services] 發行說明](release-notes.md)頁面。

若要取得完整指示並開始入門流程，請參閱[開始使用 [!DNL Payment Services]](onboard.md)。

### 接受的信用卡與貨幣

[!DNL Payment Services]接受其可用國家[的貨幣](#availability)。 如需設定貨幣匯率的詳細資訊，請參閱[貨幣組態](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration.html)。

如需PayPal產品與服務可用貨幣與付款方式的詳細資訊，請參閱下列頁面：

* [支援的貨幣檔案](https://developer.paypal.com/docs/reports/reference/paypal-supported-currencies/)。

* [付款方式檔案](https://developer.paypal.com/docs/checkout/payment-methods/)。
