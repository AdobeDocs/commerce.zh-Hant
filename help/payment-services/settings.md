---
title: 付款服務設定
description: 安裝之後，您可在首頁設定 [!DNL Payment Services] 。
role: Admin, User
level: Intermediate
exl-id: 108f2b24-39c1-4c87-8deb-d82ee1c24d55
feature: Payments, Checkout, Configuration, Paas, Saas
source-git-commit: 870c2497a2d6dcfc4066c07f20169fc9040ae81a
workflow-type: tm+mt
source-wordcount: '2420'
ht-degree: 0%

---

# 設定

您可以使用[!DNL Payment Services]首頁中有用的設定，根據您的需求自訂[!DNL Payment Services]。

若要為[!DNL Payment Services]和[!DNL Adobe Commerce]設定[!DNL Magento Open Source]，請按一下&#x200B;**[!UICONTROL Settings]**。 這些組態選項僅適用於在&#x200B;_[!UICONTROL Payment mode]_&#x200B;一般[_&#x200B;組態選項&#x200B;_的](#configure-general-settings)欄位中設定的環境。

如需多存放區或舊版組態，請參閱[在管理員中設定](configure-admin.md)。

## 設定一般設定

[!UICONTROL General]設定可讓您啟用或停用「付款服務」作為付款方式，並新增資訊至客戶交易，以標籤或加上自訂資訊做為網站或商店檢視的字首。

### 啟用付款服務

您可以為網站啟用[!DNL Payment Services]，並啟用沙箱測試或即時付款。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**。

1. 按一下&#x200B;**[!UICONTROL Settings]**。 如需詳細資訊，請參閱[ [!DNL Payment Services] 首頁](payments-home.md)簡介。

   ![React設定檢視](assets/react-settings-view.png){width="500" zoomable="yes"}

   _[!UICONTROL General]_&#x200B;區段包含用來啟用[!DNL Payment Services]作為付款方式的設定。

1. 若要啟用[!DNL Payment Services]作為商店的付款方式，請在&#x200B;_[!UICONTROL General]_&#x200B;區段中，將&#x200B;**[!UICONTROL Enable Payment Services as payment method]**&#x200B;切換為`Yes`。

1. 如果您仍在測試商店的[!DNL Payment Services]，請將&#x200B;**付款模式**&#x200B;設定為`Sandbox`。 如果您已準備好啟用即時付款，請將其設為`Production`。

1. 一旦您設定&#x200B;**[!UICONTROL Payment Services Sandbox ID]** Commerce服務聯結器&#x200B;**[!UICONTROL Payment Services Production ID]**&#x200B;並首次造訪[儀表板，系統就會自動填入您的](https://experienceleague.adobe.com/zh-hant/docs/commerce-merchant-services/user-guides/integration-services/saas){target=_blank}和[!DNL Payment Services]值。 執行此動作以完成您的沙箱和/或生產環境的上線。 這些值會將您的SaaS ID與[!DNL Payment Services]建立關聯。

   >[!WARNING]
   >
   > 如果您重設[!DNL Payment Services] ID，則必須重新上線。

1. 按一下&#x200B;**[!UICONTROL Save]**。

   如果您嘗試離開此檢視而不儲存變更，會出現一個強制回應視窗，提示您捨棄變更、繼續編輯或儲存變更。

1. 導覽至&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**，然後按一下&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以重新整理所有無效的快取。

您現在可以繼續變更[付款選項](#configure-payment-options)功能和店面顯示的預設設定。

### 新增軟性描述項

您可以新增[!UICONTROL Soft Descriptor]至您的網站或個別商店檢視設定。 軟性描述元會顯示在客戶交易銀行對帳單上。 例如，如果您有多個商店/品牌/目錄，您可以將自訂文字新增至「[!UICONTROL Soft Descriptor]」欄位，以輕鬆地在這些商店/品牌/目錄之間劃線。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**。
1. 按一下&#x200B;**[!UICONTROL Settings]**。 如需詳細資訊，請參閱[ [!DNL Payment Services] 首頁](payments-home.md)簡介。
1. 在&#x200B;**[!UICONTROL Scope]**&#x200B;下拉式功能表中選取您要為其建立軟性描述項的網站或商店檢視。 對於初始設定，請將此項保留為&#x200B;**[!UICONTROL Default]**&#x200B;以設定預設值。
1. 在文字欄位中新增自訂文字（最多22個字元），取代`Soft descriptor`。
1. 按一下&#x200B;**[!UICONTROL Save]**。
1. 若要為網站或商店檢視建立非預設的可變描述項：
   1. 在&#x200B;**[!UICONTROL Scope]**&#x200B;下拉式功能表中選取您要為其建立軟性描述項的網站或商店檢視。
   1. 切換&#x200B;_關閉_ **[!UICONTROL Use website]** （或&#x200B;**[!UICONTROL Use default]**，視您選取的範圍而定）。
   1. 在文字欄位中新增自訂文字。
   1. 按一下&#x200B;**[!UICONTROL Save]**。
1. 若要為網站或商店啟用檢視預設軟性描述項&#x200B;_或_&#x200B;父網站所使用的軟性描述項：
   1. 在&#x200B;**[!UICONTROL Scope]**&#x200B;下拉式功能表中選取您要啟用現有軟性描述項的網站或商店檢視。
   1. 將&#x200B;_切換為_ **[!UICONTROL Use website]** （或&#x200B;**[!UICONTROL Use default]**，視您選取的範圍而定）。
   1. 按一下&#x200B;**[!UICONTROL Save]**。

   如果您嘗試離開此檢視而不儲存變更，會出現一個強制回應視窗，提示您捨棄變更、繼續編輯或儲存變更。

### 設定選項

| 欄位 | 範圍 | 說明 |
|---|---|---|
| [!UICONTROL Enable] | 網站 | 啟用或停用您網站的[!DNL Payment Services]。 選項： [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Payment mode] | 存放區檢視 | 設定商店的方法或環境。 選項： [!UICONTROL Sandbox] / [!UICONTROL Production] |
| [!UICONTROL Payment Services Sandbox ID] | 存放區檢視 | 您的沙箱商家ID，會在沙箱上線期間自動產生。 |
| [!UICONTROL Payment Services Production ID] | 存放區檢視 | 您的生產廠商ID，會在生產（即時）上線期間自動產生。 |
| [!UICONTROL Soft Descriptor] | 網站或商店檢視 | 在您的網站和商店檢視中新增軟性描述項，以將資訊新增到客戶交易，其中會描述品牌、商店或產品線。 [!UICONTROL Use website]切換會套用網站層級新增的任何軟性描述項。 [!UICONTROL Use default]切換會套用新增為預設的任何軟性描述項。 |

## 設定付款選項

現在您已啟用網站的[!UICONTROL Payment Services]，您可以變更付款功能和店面顯示的預設設定。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**。
1. 按一下&#x200B;**[!UICONTROL Settings]**。 如需詳細資訊，請參閱[ [!DNL Payment Services] 首頁](payments-home.md)簡介。
1. 依下列區段設定[信用卡](#credit-card-fields)、[付款按鈕](#payment-buttons)和[按鈕樣式](#button-style)的付款選項。

### 信用卡欄位

_[!UICONTROL Credit Card Fields]_&#x200B;設定為信用卡或扣帳卡付款方式提供簡單且安全的結帳選項。

如需詳細資訊，請參閱[付款選項](payments-options.md#credit-card-fields)。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**。
1. 在&#x200B;**[!UICONTROL Scope]**&#x200B;下拉式功能表中選取您要啟用付款方式的商店檢視。
1. 在&#x200B;**[!UICONTROL Credit card fields]**&#x200B;區段中，編輯&#x200B;**[!UICONTROL Checkout title]**&#x200B;欄位中的值，以變更結帳時顯示的付款方式名稱。
1. 若要[設定付款動作](production.md#set-payment-services-as-payment-method)，請將&#x200B;**[!UICONTROL Payment action]**&#x200B;切換為`Authorize`或`Authorize and Capture`。
1. 若要優先處理結帳頁面上的付款方法，請在`Numeric Only`欄位中提供&#x200B;**[!UICONTROL Sort order]**&#x200B;值。
1. 若要啟用[3DS Secure驗證](security.md#3ds) （預設為`Off`）將&#x200B;**[!UICONTROL 3DS Secure authentication]**&#x200B;選取器切換為`Always`或`When required`。
1. 若要啟用或停用結帳頁面上的信用卡欄位，請切換&#x200B;**[!UICONTROL Show on checkout page]**&#x200B;選取器。
1. 若要啟用或停用[卡片存放](#card-vaulting)，請切換&#x200B;**[!UICONTROL Vault enabled]**&#x200B;選取器。
1. 若要啟用或停用Admin[中的](#card-vaulting)保管式付款方法（供商戶使用保管式付款方法來完成Admin中客戶的訂單），請切換&#x200B;**[!UICONTROL Show vaulted methods in Admin]**&#x200B;選取器。
1. 若要啟用或停用偵錯模式，請切換&#x200B;**[!UICONTROL Debug Mode]**&#x200B;選取器。
1. 按一下&#x200B;**[!UICONTROL Save]**。

   如果您嘗試離開此檢視而不儲存變更，會出現一個強制回應視窗，提示您捨棄變更、繼續編輯或儲存變更。

1. [排清快取](#flush-the-cache)。

#### 設定選項

| 欄位 | 範圍 | 說明 |
|---|---|---|
| [!UICONTROL Title] | 存放區檢視 | 在結帳期間，在「付款方式」檢視中，新增文字以顯示為此付款選項的標題。 選項： [!UICONTROL text field] |
| [!UICONTROL Payment Action] | 網站 | 指定的付款方式的[付款動作](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"}。 選項： [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | 存放區檢視 | 結帳頁面上指定付款方式的排序順序。 `Numeric Only`值 |
| [!UICONTROL 3DS Secure authentication] | 網站 | 啟用或停用[3DS安全驗證](security.md#3ds)。 選項： [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Show on checkout page] | 網站 | 啟用或停用要在結帳頁面上顯示的信用卡欄位。 選項： [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Vault enabled] | 存放區檢視 | 啟用或停用[信用卡存放區](vaulting.md)。 選項： [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show vaulted payment methods in Admin] | 存放區檢視 | 啟用或停用商家使用存放的付款方式[，為管理員](vaulting.md)中的客戶完成訂單的功能。 選項： [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Debug Mode] | 網站 | 啟用或停用偵錯模式。 選項： [!UICONTROL Off] / [!UICONTROL On] |

### Apple Pay

[!UICONTROL Apple Pay]按鈕付款選項可讓您從Safari瀏覽器在您的商店結帳中提供[!UICONTROL Apple Pay]付款按鈕（每個商家帳戶最多99個網域）。

只有當您透過Paypal完成[Apple Pay自助註冊](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain)，然後[為商店設定Apple Pay](configure-admin.md/#payment-buttons)時，才能使用Apple Pay。

如需詳細資訊，請參閱[付款選項](payments-options.md#apple-pay-button)。

您可以啟用並設定[!UICONTROL Apple Pay]按鈕付款選項：

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**。
1. 在&#x200B;**[!UICONTROL Scope]**&#x200B;下拉式功能表中選取您要啟用付款方式的商店檢視。
1. 在&#x200B;**[!UICONTROL Apple Pay]**&#x200B;區段中，編輯&#x200B;_[!UICONTROL Checkout title]_&#x200B;欄位中的值，以變更結帳時顯示的付款方式名稱。
1. 若要[設定付款動作](production.md#set-payment-services-as-payment-method)，請將&#x200B;**[!UICONTROL Payment action]**&#x200B;切換為`Authorize`或`Authorize and Capture`。
1. 若要在結帳頁面上啟用或停用Apple Pay，請切換&#x200B;**[!UICONTROL Show Apple Pay on checkout page]**&#x200B;選取器。
1. 若要在產品詳細資料頁面上啟用或停用Apple Pay，請切換&#x200B;**[!UICONTROL Show Apple Pay on product detail page]**&#x200B;選取器。
1. 若要在迷你購物車預覽上啟用或停用Apple Pay，請切換&#x200B;**[!UICONTROL Show Apple Pay on the mini cart preview]**&#x200B;選取器。
1. 若要在購物車頁面上啟用或停用Apple Pay，請切換&#x200B;**[!UICONTROL Show Apple Pay on cart page]**&#x200B;選取器。
1. 若要啟用或停用偵錯模式，請切換&#x200B;**[!UICONTROL Debug Mode]**&#x200B;選取器。
1. 按一下&#x200B;**[!UICONTROL Save]**。

   如果您嘗試離開此檢視而不儲存變更，會出現一個強制回應視窗，提示您捨棄變更、繼續編輯或儲存變更。

1. [排清快取](#flush-the-cache)。

#### 設定選項

| 欄位 | 範圍 | 說明 |
|---|---|---|
| [!UICONTROL Checkout title] | 存放區檢視 | 在結帳期間，在「付款方式」檢視中，新增文字以顯示為此付款選項的標題。 選項： [!UICONTROL text field] |
| [!UICONTROL Payment Action] | 網站 | 指定的付款方式的[付款動作](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions)。 選項： [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Show on checkout page] | 網站 | 啟用或停用「Apple付款」按鈕以顯示於結帳頁面。 選項： [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show on checkout page] | 網站 | 啟用或停用Apple Pay按鈕以顯示於產品詳細資料頁面上。 選項： [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show on mini cart preview] | 網站 | 啟用或停用Apple Pay按鈕以在迷你購物車預覽上顯示。 選項： [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show on cart page] | 網站 | 啟用或停用「Apple付款」按鈕以顯示於購物車頁面。 選項： [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Debug Mode] | 網站 | 啟用或停用偵錯模式。 選項： [!UICONTROL Off] / [!UICONTROL On] |

### 付款按鈕

[!DNL PayPal payment buttons]付款選項可為您的客戶提供簡單、快速且安全的結帳程式。 如需詳細資訊，請參閱[付款選項](payments-options.md#paypal-smart-buttons)。

您可以啟用並設定PayPal付款按鈕付款選項：

1. 在&#x200B;**[!UICONTROL Scope]**&#x200B;下拉式功能表中選取您要啟用付款方式的商店檢視。
1. 若要變更結帳時顯示的付款方式名稱，請編輯&#x200B;**[!UICONTROL Checkout Title]**&#x200B;欄位中的值。
1. 若要[設定付款動作](production.md#set-payment-services-as-payment-method)，請將&#x200B;**[!UICONTROL Payment action]**&#x200B;切換為`Authorize`或`Authorize and Capture`。
1. 若要優先處理結帳頁面上的付款方法，請在`Numeric Only`欄位中提供&#x200B;**[!UICONTROL Sort order]**&#x200B;值。
1. 使用切換選擇器來啟用或停用[!DNL PayPal smart button]顯示功能：

   - **[!UICONTROL Show PayPal buttons on product checkout page]**
   - **[!UICONTROL Show PayPal buttons on product detail page]**
   - **[!UICONTROL Show PayPal buttons in mini-cart preview]**
   - **[!UICONTROL Show PayPal buttons on cart page]**
   - **[!UICONTROL Show PayPal Pay Later button]**
   - **[!UICONTROL Show PayPal Pay Later message]**
   - **[!UICONTROL Show Venmo button]**
   - **[!UICONTROL Show Apple Pay button]**
   - **[!UICONTROL Show PayPal Credit and Debit Card button]**

     >[!NOTE]
     >
     > 若要使用Apple Pay，您[必須擁有Apple沙箱測試程式帳戶](https://developer.apple.com/apple-pay/sandbox-testing/#create-a-sandbox-tester-account) （包含假信用卡和帳單資訊）才能進行測試。 當您準備好在沙箱&#x200B;_或_&#x200B;生產模式下使用Apple Pay時，在完成任何[測試和驗證](test-validate.md#test-in-sandbox-environment)後，完成[向 [!DNL Apple Pay]](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain)自我註冊（_僅註冊您的即時網域_&#x200B;區段），並在[!DNL Payment Services]中為您的商店設定它。

     當您開啟/關閉付款按鈕或PayPal Pay Later訊息的可見度時，「設定」頁面底部會顯示該設定的視覺化預覽。

1. 若要啟用偵錯模式，請切換&#x200B;**[!UICONTROL Debug Mode]**&#x200B;選取器。
1. 按一下&#x200B;**[!UICONTROL Save]**。

   如果您嘗試離開此檢視而不儲存變更，會出現一個強制回應視窗，提示您捨棄變更、繼續編輯或儲存變更。

1. [排清快取](#flush-the-cache)。

#### 設定選項

| 欄位 | 範圍 | 說明 |
|---|---|---|
| [!UICONTROL Title] | 存放區檢視 | 在結帳期間，在「付款方式」檢視中，新增要顯示為此付款選項標題的文字。 選項：文字欄位 |
| [!UICONTROL Payment Action] | 網站 | 指定的付款方式的[付款動作](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"}。 選項： [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | 存放區檢視 | 結帳頁面上指定付款方式的排序順序。 `Numeric Only`值 |
| [!UICONTROL Show PayPal buttons on checkout page] | 存放區檢視 | 啟用或停用結帳頁面上的[!DNL PayPal payment buttons]。 選項： [!UICONTROL &#x200B; Yes] / [!UICONTROL No] |
| [!UICONTROL Show PayPal buttons on product detail page] | 存放區檢視 | 啟用或停用產品詳細資料頁面上的[!DNL PayPal payment buttons]。 選項： [!UICONTROL &#x200B; Yes] / [!UICONTROL No] |
| [!UICONTROL Show PayPal buttons in mini-cart preview] | 存放區檢視 | 啟用或停用迷你購物車預覽中的[!DNL PayPal payment buttons]。 選項： [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show PayPal buttons on cart page] | 存放區檢視 | 啟用或停用購物車頁面上的[!DNL PayPal payment buttons]。 選項： [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show PayPal Pay Later button] | 存放區檢視 | 啟用或停用付款按鈕顯示的稍後付款選項外觀。 選項： [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show PayPal Pay Later Message] | 網站 | 在購物車、產品頁面、迷你購物車和結帳流程中啟用或停用「稍後付款」訊息。 選項： [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show Venmo button] | 存放區檢視 | 啟用或停用顯示付款按鈕的Venmo付款選項。 選項： [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show Apple Pay button] | 存放區檢視 | 啟用或停用顯示付款按鈕的Apple付款選項。 選項： [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show PayPal Credit and Debit card button] | 存放區檢視 | 啟用或停用顯示付款按鈕的「信用卡與借記卡」付款選項。 選項： [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Debug Mode] | 網站 | 啟用或停用偵錯模式。 選項： [!UICONTROL Off] / [!UICONTROL On] |

### 按鈕樣式

您也可以設定付款按鈕的&#x200B;_[!UICONTROL Button style]_&#x200B;選項：

1. 若要變更&#x200B;**[!UICONTROL Layout]**，請選取`Vertical`或`Horizontal`。

   >[!NOTE]
   >
   > 如果按鈕樣式設定為`Horizontal`，而您的商店設定為顯示多個付款按鈕，則您只能看到產品頁面、結帳頁面和迷你購物車上顯示的兩個按鈕，以及購物車中顯示的一個按鈕。

1. 若要啟用水準版面配置中的標語，請切換&#x200B;**[!UICONTROL Show tagline]**&#x200B;選取器。
1. 若要修改&#x200B;**[!UICONTROL Color]**，請選取所需的顏色選項。
1. 若要修改&#x200B;**[!UICONTROL Shape]**，請選取`Pill`或`Rectangle`。
1. 若要啟用按鈕高度選擇器，請切換&#x200B;**[!UICONTROL Responsive button height]**&#x200B;選擇器。
1. 若要修改&#x200B;**[!UICONTROL Label]**，請選取所需的標籤選項。

   當您變更版面、顏色、形狀、高度和標籤的組態選項時，該組態的視覺預覽會顯示在「設定」頁面底部。 在下圖中，**[!UICONTROL Shape]**&#x200B;設定為&#x200B;_矩形_，**[!UICONTROL Label]**&#x200B;設定為&#x200B;_PayPal （建議）_。

   ![[!DNL PayPal payment buttons]選項](assets/payment-buttons.png){width="400" zoomable="yes"}

1. 按一下&#x200B;**[!UICONTROL Save]**。

   如果您嘗試離開此檢視而不儲存變更，會出現一個強制回應視窗，提示您捨棄變更、繼續編輯或儲存變更。

1. [排清快取](#flush-the-cache)。

您可以在Admin[的舊版設定中或在](configure-admin.md#configure-paypal-smart-buttons)這裡設定付款按鈕樣式[!DNL Payment Services Home]。 請參閱[PayPal的按鈕樣式指南](https://developer.paypal.com/docs/checkout/standard/customize/buttons-style-guide/)，以取得有關設定PayPal付款按鈕樣式的詳細資訊。

#### 設定選項

| 欄位 | 範圍 | 說明 |
|--- |--- |--- |
| [!UICONTROL Layout] | 存放區檢視 | 定義付款按鈕的配置樣式。 選項： [!UICONTROL Vertical] / [!UICONTROL Horizontal] |
| [!UICONTROL Tagline] | 存放區檢視 | 啟用/停用標語。 選項： [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Color] | 存放區檢視 | 定義付款按鈕的顏色。 選項： [!UICONTROL Blue] / [!UICONTROL Gold] / [!UICONTROL Silver] / [!UICONTROL White] / [!UICONTROL Black] |
| [!UICONTROL Shape] | 存放區檢視 | 定義付款按鈕的形狀。 選項： [!UICONTROL Rectangular] / [!UICONTROL Pill] |
| [!UICONTROL Responsive Button Height] | 存放區檢視 | 定義付款按鈕是否使用預設高度。 選項： [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Height] | 存放區檢視 | 定義付款按鈕的高度。 預設值：無 |
| [!UICONTROL Label] | 存放區檢視 | 定義出現在付款按鈕中的標籤。 選項： [!UICONTROL PayPal] / [!UICONTROL Checkout] / [!UICONTROL Buynow] / [!UICONTROL Pay] / [!UICONTROL Installment] |

## 設定角色

為確保管理員使用者可以在Commerce管理員中建立和管理訂單，請針對使用者角色啟用[!DNL Payment Services]特定資源。

請參閱[使用者角色](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions-user-roles.html?lang=zh-Hant)以瞭解如何管理角色。

將資源指派給角色時，您必須選取：

- **以[!DNL Payment Services]**&#x200B;付款 — 此資源可確保當您在Admin中建立訂單時，[!DNL Payment Services]信用卡可作為付款方式使用。 如果您選取&#x200B;**動作**&#x200B;父資源，也會選取此資源。
- **[!DNL Payment Services]** — 此資源包含&#x200B;**儀表板**&#x200B;和&#x200B;**SaaS服務Proxy**&#x200B;資源，也必須選取這些資源。 他們確定[!DNL Payment Services]出現在&#x200B;_銷售_&#x200B;功能表中。

  ![付款服務資源](assets/roles-payments.png){width="400" zoomable="yes"}

## 排清快取

如果您在&#x200B;_設定_&#x200B;中變更設定，例如切換Apple Pay、Venmo或PayPal PayLater按鈕，請手動清除快取，讓您的商店顯示最新設定。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**。
1. 按一下&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以重新整理所有無效的快取。

如果快取管理表格中的任何快取型別具有`INVALIDATED`狀態，您的存放區可能不會顯示該專案的最新設定。 排清快取以更新您的存放區以顯示最新設定。

為確保您的存放區顯示正確的設定，請定期[排清快取](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/systems/tools/cache-management)。

## 卡片存放

您可以啟用功能，讓您的客戶可以將「我的帳戶」中的信用卡資訊儲存起來（或「儲存」），以便日後購買。

您也可以在「管理員」中使用卡存放，為現有客戶完成後續訂單。

在[信用卡欄位設定](#credit-card-fields)中啟用或停用卡片存放。

如需詳細資訊，請參閱[信用卡存放](vaulting.md)。

## 3DS

3DS可保護客戶與商家，避免其商店內的詐騙活動，並可確保符合歐盟(EU)標準。

啟用或停用[信用卡欄位設定](#credit-card-fields)中的3DS。

如需詳細資訊，請參閱安全性[中的](security.md#3ds)3DS。

## 使用多個PayPal帳戶

在[!UICONTROL Payment Services]中，您可以在網站層級的&#x200B;**one**&#x200B;商家帳戶中使用多個PayPal帳戶。 例如，如果您在多個國家/地區經營您的商店（使用不同的[貨幣](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/stores-sales/site-store/currency/currency)），或想將Adobe Commerce用於您企業的某些部分而非&#x200B;_所有_，您可以將您的商家帳戶設定為使用多個PayPal帳戶。

如需有關網站、商店和商店檢視階層的詳細資訊，請參閱[網站、商店和檢視範圍](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=zh-Hant)。

如需透過CLI為多個PayPal帳戶設定範圍的詳細資訊，請參閱[命令列設定](configure-cli.md#configure-scope-via-cli)。

您的銷售代表可以為您的商家帳戶建立新的[範圍](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=zh-Hant#scope-settings)，並使用PayPal加入其他網站，以便您設定要顯示的任何PayPal按鈕都會顯示在您的網站上。 請聯絡您的銷售代表，以取得使用您網站的多個PayPal帳戶的相關協助。
