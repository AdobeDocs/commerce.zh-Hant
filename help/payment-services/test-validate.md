---
title: 測試及驗證
description: 測試和驗證可確保 [!DNL Payment Services] 功能如預期般運作，並為您的客戶提供最佳付款選項
feature: Payments, Checkout
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# 測試及驗證

在您將[!DNL Adobe Commerce]和[!DNL Magento Open Source]的[!DNL Payment Services]公開給購物者之前，最好在沙箱環境&#x200B;_和_&#x200B;中在生產環境中進行測試。 測試和驗證可確保[!DNL Payment Services]功能如預期般運作，並為您的商店和客戶提供最佳付款選項。

## 在沙箱環境中測試

在沙箱環境中測試[!DNL Payment Services]是重要的驗證步驟，即使它是僅連線到PayPal沙箱的模擬環境，而不是連線到真正的銀行和商家。

1. 使用[信用卡欄位](payments-options.md#credit-card-fields)或任何[PayPal付款按鈕](payments-options.md#paypal-smart-buttons)，完成從商店成功結帳。 請參閱[測試認證](#testing-credentials)，以取得使用假信用卡進行測試的詳細資訊。
1. 擷取（當您的付款動作是[設定為`Authorize and Capture`](onboard.md#set-payment-services-as-payment-method)時）、[退款](refunds.md)或[void](voids.md)剛完成的訂單。 如果您的付款動作設為`Authorize`而非`Authorize and Capture`，您也可以[為訂單](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice){target="_blank"}建立發票。
1. 在24到48小時內，檢視[付款報表](payouts.md)中的交易與其他資訊。
1. 在[訂單付款狀態報表](order-payment-status.md)中檢視訂單詳細資料。

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

若要在生產模式下測試Apple Pay，您必須[註冊您的生產網域](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain)。
