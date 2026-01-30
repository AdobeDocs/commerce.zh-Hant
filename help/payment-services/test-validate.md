---
title: 測試及驗證
description: 測試和驗證可確保 [!DNL Payment Services] 功能如預期般運作，並為您的客戶提供最佳付款選項
exl-id: 95b4615e-73b0-41e8-83e2-e65a0b22f10f
feature: Payments, Checkout, Paas, Saas
source-git-commit: 91a4b8fa7228fb91c8ee0bf0a1623d104f061894
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 0%

---

# 測試及驗證

在您將[!DNL Payment Services]和[!DNL Adobe Commerce]的[!DNL Magento Open Source]公開給購物者之前，最好在沙箱環境&#x200B;_和_&#x200B;中在生產環境中進行測試。 測試和驗證可確保[!DNL Payment Services]功能如預期般運作，並為您的商店和客戶提供最佳付款選項。

## 在沙箱環境中測試

在沙箱環境中測試[!DNL Payment Services]是重要的驗證步驟，即使它是僅連線到PayPal沙箱的模擬環境，而不是連線到真正的銀行和商家。

1. 使用[信用卡欄位](payments-options.md#credit-card-fields)或任何[PayPal付款按鈕](payments-options.md#paypal-smart-buttons)，完成從商店成功結帳。 請參閱[測試認證](#testing-credentials)，以取得使用假信用卡進行測試的詳細資訊。
1. 擷取（當您的付款動作是[設定為`Authorize and Capture`](onboard.md#set-payment-services-as-payment-method)時）、[退款](refunds.md)或[void](voids.md)剛完成的訂單。 如果您的付款動作設為[而非](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice){target="_blank"}，您也可以`Authorize`為訂單建立發票`Authorize and Capture`。
1. 在24到48小時內，檢視[付款報表](payouts.md)中的交易與其他資訊。
1. 在[訂單付款狀態報表](order-payment-status.md)中檢視訂單詳細資料。

### 在本機開發環境中測試

在本機開發環境中測試PayPal、PayLater和Venmo支付方法時，您的環境必須可從網際網路存取。 這些付款方式使用[伺服器端送貨回撥](https://developer.paypal.com/docs/multiparty/checkout/standard/customize/shipping-module/)，需要PayPal與您的Commerce執行個體通訊，以擷取送貨選項並計算總計。

>[!INFO]
>
>如果沒有可存取網際網路的URL，送貨回呼將無法運作，導致結帳流程與生產環境不同。 務必使用可存取的URL進行測試，以確保準確的結果。

若要公開您的本機環境：

1. 使用通道服務（例如[ngrok](https://ngrok.com/)）為您的本機環境建立可公開存取的URL。

1. 更新您的Commerce基本URL設定以符合登入URL：

   ```bash
   bin/magento config:set web/unsecure/base_url https://your-ngrok-url.ngrok.io/
   bin/magento config:set web/secure/base_url https://your-ngrok-url.ngrok.io/
   bin/magento cache:flush
   ```

1. 使用PayPal、PayLater或Venmo付款方式完成您的測試。

1. 測試完成時，還原您的原始基底URL設定。

如果端點的回應時間少於5秒，PayPal會在快顯視窗中顯示錯誤訊息。

#### Apple Pay本機開發

Apple Pay需要額外的設定才能進行本機開發。 Apple Pay使用網域註冊來驗證您的網站是否有權接受Apple Pay付款。 這表示Apple必須能夠連線到您的網域，以驗證位於`/.well-known/apple-developer-merchantid-domain-association`的網域驗證檔案。

對於本機開發，您的環境必須符合以下要求：

* **可公開存取**，Apple必須能夠透過網際網路存取您的網域。
* **HTTPS通訊協定**，Apple Pay僅適用於安全連線。

使用[ngrok](https://ngrok.com/)之類的通道服務符合兩個要求。 依照上述方式設定ngrok之後，使用[ngrok](https://developer.paypal.com/docs/checkout/apm/apple-pay/#link-registeryoursandboxdomains) URL在PayPal中&#x200B;**註冊您的沙箱網域**。

### 測試認證

在測試及驗證您的沙箱時，您必須使用假的信用卡號碼，這樣您就不會對現有信用卡帳戶建立真正的費用。

使用PayPal的信用卡產生器來[產生隨機信用卡資訊](https://www.paypal.com/us/smarthelp/article/where-can-i-find-test-credit-card-numbers-ts2157)以進行測試。

若要以沙箱模式測試Apple Pay：

* 建立[Apple沙箱測試器帳戶](https://developer.apple.com/apple-pay/sandbox-testing/#create-a-sandbox-tester-account)，包含假信用卡和帳單資訊。
* [註冊您的沙箱網域](https://developer.paypal.com/docs/checkout/apm/apple-pay/#link-registeryoursandboxdomains)。

>[!NOTE]
>
>PayPal的沙箱支付處理有時很慢，服務偶爾可能會停止運作。 此情況無法表示即時產品付款處理的速度和效率。

## 在生產環境中測試

強烈建議您先在生產環境中測試[!DNL Payment Services]，使用真實的信用卡和銀行，然後再將此功能公開給購物者。 雖然在沙箱中測試[!DNL Payment Services]很重要，但在生產環境中測試是確保[!DNL Payment Services]如預期般運作的最萬無一失的方法。

您可以使用下列兩種方式之一在生產環境中測試[!DNL Payment Services]：

* 選擇您知道購物者不會下訂單的時間。
* 使用購物者暫時無法存取但可供您存取以進行測試的網站商店。

使用真正的信用卡和PayPal帳戶完成您的生產測試，測試付款的整個生命週期，包括擷取和退款。 在測試期間完成整個結帳和付款流程，可讓您清楚瞭解當即時購物者使用您的[!DNL Payment Services]功能時將會如何運作。

您也應確認出現在銀行對帳單上，用於生產測試之付款方式的資訊正確且符合預期（包括業務說明）。

### 在生產環境中測試Apple Pay

若要在生產模式下測試Apple Pay，您必須[註冊您的生產網域](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain)。
