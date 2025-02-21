---
title: 設定測試沙箱
description: 使用PayPal沙箱帳戶在測試模式中使用 [!DNL Payment Services] 。
feature: Payments, Checkout, Configuration, Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# 設定測試沙箱

在開始使用沙箱之前，您必須註冊一個免費的PayPal開發人員帳戶，並建立商人（用於上線）和購物者帳戶（用於測試您的結帳）。 如有需要，您可以建立多個開發人員帳戶。

PayPal沙箱帳戶可讓您在測試模式中使用[!DNL Payment Services]。 PayPal要求您使用PayPal開發人員入口網站產生的企業沙箱測試帳戶、電子郵件和密碼來上線沙箱。 *在沙箱上線流程中不要建立其他帳戶。*

## 沙箱上線

若要完成沙箱上線：

1. 瀏覽至[PayPal開發人員帳戶頁面](https://developer.paypal.com/developer/accounts/)。
1. 按一下&#x200B;**[!UICONTROL Log in to Dashboard]**&#x200B;並以您現有的PayPal Developer Portal產生的Business沙箱測試帳戶登入，或按一下&#x200B;**註冊**&#x200B;以建立帳戶。
1. 建立PayPal沙箱帳戶：
   1. 前往&#x200B;_[!UICONTROL Testing Tools]_>**[!UICONTROL Sandbox Accounts]**。
   1. 按一下&#x200B;**[!UICONTROL Create account]**。

      如果您在沙箱PayPal上線流程中建立PayPal沙箱帳戶，您必須[重設您的上線沙箱](#reset-your-sandbox-account)，否則您無法驗證電子郵件。

   1. 選取&#x200B;**[!UICONTROL Business]**&#x200B;作為帳戶型別並按一下&#x200B;**[!UICONTROL Create]**。
   1. 在&#x200B;_[!UICONTROL Sandbox Accounts]_區段中，針對您建立的沙箱帳戶，按一下_[!UICONTROL Manage accounts]_&#x200B;欄中的三個點。
   1. 按一下&#x200B;**[!UICONTROL View/edit account]**。

      ![PayPal — 檢視/編輯沙箱帳戶](assets/onboarding-viewedit-sandbox.png){width="300" zoomable="yes"}

   1. 複製並儲存電子郵件ID和系統產生的密碼以供將來使用。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**。
1. 按一下&#x200B;**[!UICONTROL Sandbox onboarding]**。

   如果您尚未完成[!DNL Payment Services]的沙箱上線，則會顯示此選項。

   沙箱商家識別碼會自動產生，並填入[設定](settings.md)。 請勿變更或變更此ID。

   您會看到PayPal視窗，讓您連線PayPal帳戶以開始接受付款。

1. 輸入您在步驟3產生的PayPal沙箱帳戶的電子郵件和密碼（不是您的PayPal企業帳戶資訊）以及您所在的國家/地區。
1. 按一下&#x200B;**[!UICONTROL Next]**。

   ![PayPal — 連線PayPal帳戶以進行付款](assets/paypal-connectacct.png){width="300" zoomable="yes"}

1. 使用您先前儲存的沙箱帳戶認證，繼續遵循PayPal流程。
1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**。

   **[!UICONTROL Sandbox onboarding]**&#x200B;按鈕不再可見，並且您看到「沙箱付款待處理」文字。

當您的PayPal沙箱上線獲得核準時，您應該會看到一則通知，指出您的付款系統目前處於沙箱模式，且未處理即時付款。

>[!IMPORTANT]
>
>如果您撤銷[!DNL Adobe Commerce]與[!DNL Magento Open Source]對[!DNL Payment Services]的同意，以處理您的付款（在您的PayPal帳戶設定中），則[!DNL Payment Services]無法處理您商店中的訂單。 在您的「付款服務」首頁上，會出現有關撤銷同意的警報。 若要關閉警示，請按一下&#x200B;**[!UICONTROL Do not show again]**。

### 重設您的沙箱帳戶

如果您在沙箱PayPal上線流程中建立PayPal沙箱帳戶，您必須重設上線沙箱，因為或您無法驗證電子郵件。

若要重設您的沙箱帳戶：

1. 按一下&#x200B;**[!UICONTROL Reset sandbox]**。 [建立PayPal商務沙箱帳戶](https://developer.paypal.com/docs/api-basics/sandbox/accounts/#create-a-business-sandbox-account)。
1. 按一下&#x200B;**[!UICONTROL Sandbox onboarding]**&#x200B;並完成下一組步驟。

## 啟用聯絡電話號碼

聯絡電話號碼可讓您取得PayPal向客戶收集的聯絡電話號碼。 PayPal一律會向PayPal帳戶持有人收集連絡電話號碼，以協助確認其身分並連絡他們以解決其帳戶上的問題，或完成其履行流程。 不過，PayPal不鼓勵直接使用商家的連絡電話號碼，因為這可能對銷售造成負面影響。 如需詳細資訊，請參閱[PayPal取得聯絡電話號碼](https://www.sandbox.paypal.com/businessmanage/preferences/website)檔案。

此功能預設為`off`。 啟用後，當客戶在結帳頁面外部完成品牌結帳流程時，商店管理員可以看到電話號碼。

>[!IMPORTANT]
>
>此設定不適用於其他結帳流程。

## 在沙箱環境中測試

強烈建議您先將測試資料空間用於整合和中繼環境，並使用真實的信用卡和銀行在生產環境中測試付款，然後再向購物者公開此功能。

如需詳細資訊，請參閱[測試及驗證](test-validate.md)。
