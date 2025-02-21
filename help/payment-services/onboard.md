---
title: 內建 [!DNL Payment Services]
description: 完成幾個上線步驟，以使用 [!DNL Payment Services] 功能連線您的執行個體。
role: User
level: Intermediate
feature: Payments, Checkout, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# 上線[!DNL Payment Services]

若要開始使用[!DNL Adobe Commerce]和[!DNL Magento Open Source]的[!DNL Payment Services]，您必須完成一些上線步驟，將執行個體與付款功能連線。

## 上線流程

此流程圖顯示上線[!DNL Payment Services]的一般程式。

![上線流程](assets/onboarding-diagram.svg){width="600" zoomable="yes"}

>[!NOTE]
>
> 若為Adobe Commerce 2.4.7或更新版本，您可以略過Marketplace擴充步驟，因為[!DNL Payment Services]已可立即使用。

在您完成沙箱或即時付款上線後，即可從Admin的[!DNL Payment Services]存取Financial Reporting。

如果沙箱和即時付款都已上線並啟用，您可以從[!DNL Payment Services]首頁輕鬆地在這些模式之間切換。

## 先決條件

若要使用[!DNL Payment Services]，您必須啟用所有相依模組，且您的執行個體可使用下列專案：

* 服務聯結器模組
* 服務識別碼模組
* API金鑰

服務聯結器與服務ID模組會在[安裝 [!DNL Payment Services]](install.md)期間自動安裝。

安裝完成時，如果您展開&#x200B;**[!UICONTROL Services]**—**[!UICONTROL Commerce Services Connector]**，您可以在組態設定(**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**)中看到新區段。

若要瞭解如何建立或存取您的API金鑰，請參閱[API認證](#obtain-api-credentials)。

## 入門步驟

1. [安裝 [!DNL Payment Services] 擴充功能](install.md#get-payment-services)。
1. [取得API認證](connect.md#obtain-api-credentials)。
1. [將您的執行個體](connect.md#configure-commerce-services)連線至Commerce服務。 每個Commerce執行個體只能完成此連線一次。
1. [使用測試PayPal付款處理帳戶，設定沙箱服務](sandbox.md#enable-sandbox-testing) （或者，如果您已在其他環境中測試功能，請繼續[啟用即時付款](sandbox.md#enable-live-payments)）。
1. [將 [!DNL Payment Services] 設定為您的付款方式](production.md#set-payment-services-as-payment-method) （在沙箱模式下），以開始處理測試付款。
1. [要求付款權益](production.md#request-payments-entitlement-from-adobe)以啟用即時上線。
1. [完成商家入門](production.md#complete-merchant-onboarding)以啟用您Commerce網站的即時付款。
1. [取得您的 [!DNL Payment Services] 商家識別碼](production.md#configure-pricing-tier)並交給銷售人員以設定正確的定價層級。
1. [啟用即時模式](production.md#enable-live-payments)中的 [!DNL Payment Services] 以開始處理即時付款。
1. 在[沙箱](sandbox.md#test-in-sandbox-environment)和[生產](production.md#test-in-production)環境中測試付款。

>[!NOTE]
>
>如果您未在管理員（步驟3）中設定Commerce服務，則無法設定沙箱或即時付款。

## 疑難排解

* [疑難排解 [!DNL Payment Services] 安裝](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-install.html?lang=en)
* [未驗證PayPal沙箱帳戶](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-paypal-acct.html)
* [延遲 [!DNL Payment Services] 報告資料](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-report-info-delayed.html)
* 在沙箱環境中處理付款時，[測試信用卡無法透過PayPal](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-cc-sandbox-failure.html?lang=en)
