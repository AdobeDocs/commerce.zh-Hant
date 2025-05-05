---
title: 付款選項
description: 設定付款選項，以自訂商店客戶可用的方式。
feature: Payments, Checkout, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 0%

---

# 付款選項

透過[!DNL Adobe Commerce]和[!DNL Magento Open Source] [!DNL Payment Services]，您有多個可用的付款選項。

您可以在[住家設定](payments-home.md)或[商店設定](configure-admin.md) （建議用於舊版付款選項或多商店設定）中設定這些付款選項。

根據您在結帳過程中的位置，每種付款方式都有不同的行為：

* 產品頁面 — 專案的產品頁面
* 迷你購物車 — 當產品已新增至購物車時，按一下購物車圖示即可使用
* 購物車 — 按一下&#x200B;_從迷你購物車檢視及編輯購物車_&#x200B;即可使用
* 結帳檢視 — 按一下&#x200B;_從迷你購物車或購物車前往結帳_&#x200B;即可使用

>[!IMPORTANT]
>
>必須完成[!DNL Payment Services]上線才能處理付款。

## 標準與進階付款體驗

[!DNL Payment Services]會根據您營運的國家/地區，提供&#x200B;**進階** （完全支援）和&#x200B;**標準** （快速結帳）付款選項和上線流程。

* **進階** — 所有可用的[付款選項](../payment-services/payments-options.md)都適用於目前的[完整支援的國家](../payment-services/overview.md#availability)。 在上線以啟用即時付款時，請選取[進階上線選項](../payment-services/production.md#advanced-onboarding)。
* **Standard** — 付款選項（快速結帳） （PayPal信用卡和借記卡）的子集適用於其他支援的國家/地區。 [信用卡欄位](#credit-card-fields)和[Apple Pay](#apple-pay-button)不適用於此上線選項。 在上線以啟用即時付款時，請選取[標準上線選項](../payment-services/production.md#standard-onboarding)。

如需完成「進階」和「標準」上線的相關資訊，請參閱[為生產啟用 [!DNL Payment Services] ](../payment-services/production.md#complete-merchant-onboarding)。

## [!UICONTROL Credit Card Fields]

[!UICONTROL Credit Card Fields]提供簡易且安全的信用卡或扣帳卡付款方式結帳。 當購物者使用信用卡欄位結帳時，他們會輸入自己的姓名、帳單地址以及信用卡或扣帳卡資訊來下訂單。 客戶資訊在購買作業期間會安全地使用，以順暢地引導他們完成結帳流程。

![結帳中的信用卡欄位](assets/credit-card-fields.png){width="500" zoomable="yes"}

啟用商店的[信用卡存放區](#vaulting)，讓購物者可以儲存信用卡資訊，以便稍後快速結帳。

您可以在存放區組態或[!DNL Payment Services]首頁中設定[!UICONTROL Credit Card Fields]。 如需詳細資訊，請參閱[設定](settings.md#credit-card-fields)。

您也可以變更信用卡欄位的版面、寬度、高度及外部樣式。 如需詳細資訊，請參閱[PayPal檔案](https://developer.paypal.com/docs/checkout/advanced/customize/card-field-style/)。

## [!DNL Apple Pay]按鈕

客戶可使用儲存在iOS或macOS裝置上的使用信用卡與扣帳卡付款認證的[[!DNL Apple Pay]](https://www.apple.com/apple-pay/)進行購買。

[!DNL Apple Pay]僅適用於Safari瀏覽器。 商家每個商家帳戶最多可新增99個網域。

迷你藝術中的![Apple付款按鈕](assets/applepay-button.png){width="500" zoomable="yes"}

產品頁面、迷你購物車、購物車和結帳檢視中會顯示[!DNL Apple Pay]按鈕。

若要將[!DNL Apple Pay]用於您的商店，請完成[使用 [!DNL Apple Pay]](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain)的自我註冊（_僅註冊您的即時網域_&#x200B;區段），並[在 [!DNL Payment Services]](settings.md#payment-buttons)中為您的商店設定它。

>[!NOTE]
>
> 請參閱PayPal開發人員檔案中的[進階結帳](https://www.paypal.com/us/cshelp/article/what-is-paypal-advanced-checkout-and-how-do-i-get-started-help953){target=_blank}，瞭解如何讓買家能夠在您的網站上使用Apple Pay付款。

您可以在商店設定或付款服務首頁設定[!UICONTROL Apple Pay]。 如需詳細資訊，請參閱[設定](settings.md#apple-pay)。

## [!DNL Google Pay]按鈕

客戶可以將付款詳細資料新增至其Google帳戶，以使用[[!DNL Google Pay]](https://pay.google.com/about/)，並安全地儲存該帳戶，提供順暢的結帳體驗。

[!DNL Google Pay]僅適用於特定國家或地區以及特定裝置。 如需詳細資訊，請參閱[[!DNL Google Pay] 檔案](https://developer.paypal.com/docs/checkout/apm/google-pay/#link-googlepayintegration)。

結帳中的![Google付款按鈕](assets/google-pay-button.png){width="500" zoomable="yes"}

產品頁面、迷你購物車、購物車和結帳檢視中會顯示[!DNL Google Pay]按鈕。

您可以在商店設定或付款服務首頁設定[!UICONTROL Google Pay]。 如需詳細資訊，請參閱[設定](configure-admin.md)。

>[!NOTE]
>
> [!DNL Google Pay] API只能在安全內容中的網站上使用。 如需詳細資訊，請參閱[疑難排解](https://developers.google.com/pay/api/web/support/troubleshooting)檔案。

## [!DNL PayPal Payment Buttons]

使用PayPal完成購買的[!DNL PayPal payment buttons]會儲存購物者的運送地址、帳單地址和付款詳細資料，以供日後使用。 購物者可以使用PayPal先前儲存或提供的任何付款方式。

![PayPal按鈕](assets/paypal-button.png){width="350" zoomable="yes"}

您可以在存放區組態或[!DNL Payment Services]首頁中設定[!UICONTROL PayPal payment buttons]。 如需詳細資訊，請參閱[設定](settings.md#payment-buttons)。

在PayPal的[付款方式檔案](https://developer.paypal.com/docs/checkout/payment-methods/)中，瞭解依國家/地區的付款方式可用性。

### [!DNL PayPal]按鈕

客戶可以使用PayPal按鈕輕鬆自信地結帳。

產品頁面、迷你購物車、購物車和結帳檢視中會顯示[!DNL PayPal]按鈕。

### [!DNL Venmo]按鈕

客戶可以使用[Venmo](https://venmo.com/)按鈕結帳。

產品頁面、迷你購物車、購物車和結帳檢視中會顯示[!DNL Venmo]按鈕。

### PayPal借方或信用卡按鈕

客戶可以使用「PayPal扣款」或「信用卡」按鈕結帳。

「PayPal扣款」或「信用卡」按鈕可從結帳頁面顯示。

此選項可用來透過PayPal代管按鈕，向購物者顯示扣款或信用卡付款選項，作為信用卡整合的替代方案。

### [!DNL Pay Later]按鈕

為客戶提供短期、免息的付款和其他融資選項，讓客戶可以立即購買產品，稍後再使用[!DNL Pay Later]按鈕付款。

產品頁面、迷你購物車、購物車和結帳檢視中會顯示[!DNL Pay Later]按鈕。

請參閱[PayPal的「稍後付款」優惠檔案](https://developer.paypal.com/docs/checkout/pay-later/us/)中有關「稍後付款」優惠的資訊。 使用&#x200B;**國家或地區**&#x200B;下拉式清單來選取感興趣的地區。

瞭解如何更新[設定](settings.md#payment-buttons)設定，以停用或啟用[!DNL Pay Later]訊息。

## 僅使用PayPal付款按鈕

若要將您的商店快速進入生產模式，您只能設定&#x200B;_個_ PayPal付款按鈕（Venmo、PayPal等）。 — 不要再使用PayPal信用卡付款選項。

這可讓您：

* 為您的客戶提供各種付款選項，包括Venmo和PayPal付款按鈕，可選擇關閉PayPal代管卡欄位，並使用現有的信用卡提供者。
* 使用您現有的信用卡提供者進行信用卡付款，同時使用PayPal的其他付款選項。
* 在PayPal不支援信用卡付款選項的地區，使用PayPal的付款按鈕。

若要&#x200B;**僅以&#x200B;_擷取付款_ PayPal付款按鈕（_不是_ PayPal信用卡付款選項）**：

1. 確定您的存放區在生產模式[&#128279;](settings.md#enable-payment-services)中為。
1. [在[設定]中設定所需的PayPal付款按鈕](settings.md#payment-buttons)。
1. 開啟&#x200B;_[!UICONTROL Payment buttons]_&#x200B;區段中的_&#x200B;關閉&#x200B;_&#x200B;**[[!UICONTROL Show PayPal Credit and Debit card button]](settings.md#payment-buttons)**&#x200B;選項。

要&#x200B;**擷取您現有信用卡提供者的付款&#x200B;_和_ PayPal付款按鈕**：

1. 確定您的存放區在生產模式[&#128279;](settings.md#enable-payment-services)中為。
1. [設定所需的PayPal付款按鈕](settings.md#payment-buttons)。
1. 開啟&#x200B;_[!UICONTROL Payment buttons]_&#x200B;區段中的_&#x200B;關閉&#x200B;_&#x200B;**[[!UICONTROL PayPal Show Credit and Debit card button]](settings.md#payment-buttons)**&#x200B;選項。
1. 開啟&#x200B;_[!UICONTROL Credit card fields]_&#x200B;區段中的_&#x200B;關閉&#x200B;_&#x200B;**[[!UICONTROL Show on checkout page]](settings.md#credit-card-fields)**&#x200B;選項，並使用您的[現有信用卡提供者帳戶](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/payments/payments.html?lang=zh-Hant#payments)。

## 訂單重新計算

當客戶從迷你購物車、購物車或產品頁面進入結帳流程時，會被導向至訂單稽核頁面，他們可在PayPal快顯視窗中看到選取的運送地址。 客戶選取出貨方式後，會適當重新計算訂單金額，而客戶可以看到出貨成本與稅捐。

當客戶從結帳頁面進入結帳流程時，系統已知道送貨地址和最終計算的金額，且總計已適當呈現。

免稅期、運費和銷售稅可能因地點而異。 在[!DNL Payment Services]收到送貨地址及費率後，它會快速重新計算所有適用的成本，並在結帳的最後階段適當地顯示這些成本。

## 信用卡保險存放

購物者可以儲存或「儲存」他們的信用卡資訊，以供日後在網站層級（相同商家帳戶內的任何商店）購買。

如需詳細資訊，請參閱[信用卡存放](vaulting.md)。

## 安全性

如需詳細資訊，請參閱[PCI相容性](security.md#pci-compliance)。
