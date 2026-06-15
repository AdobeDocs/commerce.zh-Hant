---
title: '[!DNL Payment Services]設定'
description: 安裝之後，您可以在商店設定的Admin中設定 [!DNL Payment Services] 。
role: Admin, User
level: Intermediate
exl-id: e1a3269d-bdf9-4b0f-972f-e8a0ef469503
feature: Payments, Checkout, Configuration, Paas, Saas
source-git-commit: 379345261bebe5bee9cdbcb6fd3b0ce6275df6ea
workflow-type: tm+mt
source-wordcount: '3710'
ht-degree: 0%

---

# [!DNL Payment Services]設定

您可以使用Admin中實用的組態選項自訂[!DNL Payment Services]以符合您的需求。

當您在Admin中為[!DNL Adobe Commerce]和[!DNL Magento Open Source]設定[!DNL Payment Services]時，這些設定僅適用於&#x200B;_[!UICONTROL General Configuration]_&#x200B;的_[!UICONTROL Method]_&#x200B;欄位中設定的環境。 您在設定欄位中所做的任何變更與切換&#x200B;_[!UICONTROL Method]_&#x200B;選取專案無關 — 如果您切換方法，您的選取專案不會重設。

## 一般設定

您可以為商店和&#x200B;_[!UICONTROL Merchant Location]_&#x200B;啟用[!DNL Payment Services]，並在&#x200B;_[!UICONTROL General Configuration]_&#x200B;區段中啟用沙箱測試或即時付款。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在左側面板中，展開&#x200B;**[!UICONTROL Sales]**&#x200B;並選擇&#x200B;**[!UICONTROL Payment Methods]**。
1. 設定&#x200B;_[!UICONTROL Merchant Location]_&#x200B;中的&#x200B;_[!UICONTROL Merchant Country]_&#x200B;欄位。 如果未指定&#x200B;_[!UICONTROL Merchant Country]_，則會使用一般設定的&#x200B;_[!UICONTROL Default Country]_。
1. 展開&#x200B;_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;區段以存取&#x200B;_[!UICONTROL [!DNL Payment Services]]_&#x200B;區段。
1. 在&#x200B;_[!UICONTROL [!DNL Payment Services]]_&#x200B;區段中，展開&#x200B;_[!UICONTROL General Configuration]_&#x200B;區段。
1. 針對&#x200B;**啟用**，將其設定為`Yes`以啟用您商店的[!DNL Payment Services]。
1. 若為&#x200B;**方法**，若您仍在測試存放區的[!DNL Payment Services]，請將其設為`Sandbox`，或若您已準備啟用即時付款，請設為`Production`。
1. 一旦您設定[Commerce服務聯結器](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/user-guides/integration-services/saas){target=_blank}並首次造訪[!DNL Payment Services]儀表板，系統就會自動填入您的&#x200B;**[!UICONTROL Payment Services Sandbox ID]**&#x200B;和&#x200B;**[!UICONTROL Payment Services Production ID]**&#x200B;值。 執行此動作以完成您的沙箱和/或生產環境的上線。 這些值會將您的SaaS ID與[!DNL Payment Services]建立關聯。

   >[!WARNING]
   >
   > 如果您需要在Commerce Services Connector中變更資料空間ID，需要重設您的[!DNL Payment Services] ID。 按一下&#x200B;**重設付款服務ID**&#x200B;以重設您的沙箱ID。 如果您重設[!DNL Payment Services]沙箱ID，則必須重新上線。

1. 第一次造訪[!DNL Payment Services]儀表板時，PayPal會自動提供您的&#x200B;**[!UICONTROL PayPal Merchant ID]**&#x200B;和&#x200B;**[!UICONTROL PayPal Merchant Status]**&#x200B;值。
1. 對於&#x200B;**軟性描述項** （自訂值，顯示在客戶交易銀行對帳單上，以描述商店/品牌/目錄之間），請在文字欄位中新增自訂文字（最多22個字元），取代`Soft descriptor`或現有值。
1. 按一下&#x200B;**[!UICONTROL Save Config]**&#x200B;以儲存變更。
1. 導覽至&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**，然後按一下&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以重新整理所有無效的快取。

### 設定選項

| 欄位 | 範圍 | 說明 |
|---|---|---|
| [!UICONTROL Enable] | 網站 | 啟用或停用您網站的[!DNL Payment Services]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Method] | 存放區檢視 | 設定商店的方法或環境。 選項： [!UICONTROL Sandbox] / [!UICONTROL Production] |
| [!UICONTROL Payment Services Sandbox ID] | 存放區檢視 | 您的沙箱商家ID，會在沙箱上線期間自動產生。 |
| [!UICONTROL Payment Services Production ID] | 存放區檢視 | 您的生產廠商ID，會在生產（即時）上線期間自動產生。 |
| [!UICONTROL PayPal Merchant ID] | 存放區檢視 | 您在建立PayPal帳戶時產生的唯一PayPal商家帳戶ID。 |
| [!UICONTROL PayPal Merchant Status] | 存放區檢視 | 您的PayPal商家ID的狀態。 |
| [!UICONTROL Soft Descriptor] | 網站或商店檢視 | 在您的網站和商店檢視中新增軟性描述項，以將資訊新增到客戶交易，其中會描述品牌、商店或產品線。 |

## 為網站連線其他PayPal帳戶

如果您執行具有&#x200B;**多個網站** （和商店檢視）的單一Commerce執行個體，某些網站可能需要&#x200B;**不同的PayPal商家帳戶**。 在執行個體設定並上線至&#x200B;**全域** （預設）範圍後，[!DNL Payment Services]可讓您在Admin中完成&#x200B;**網站範圍**&#x200B;的PayPal上線。

在舊版中，網站層級PayPal帳戶對應通常要求您[聯絡支援人員](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#Solution)或您的Adobe代表。 當您符合下列必要條件時，請使用&#x200B;**[!UICONTROL Connect different account for website]**&#x200B;動作。

### 先決條件（全域範圍）

**[!UICONTROL Connect different account for website]**&#x200B;控制項只能在&#x200B;**網站**&#x200B;範圍上使用並啟用，但下列的&#x200B;**全部**&#x200B;專案在&#x200B;**預設/全域**&#x200B;組態的執行個體中已經為True：

1. [Commerce Services Connector](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas)安裝完成。

1. [沙箱和生產](connect.md#configure-commerce-services) API金鑰（公開和私人）儲存在Admin中。

1. 已在[一般組態](#general-configuration)中填入&#x200B;**[!UICONTROL Payment Services Sandbox ID]**&#x200B;和&#x200B;**[!UICONTROL Payment Services Production ID]**。

1. **全域** PayPal商家帳戶已&#x200B;**連線**，而您已為該預設範圍&#x200B;**完成PayPal上線** （已為[一般設定](#general-configuration)中說明的全域範圍填入&#x200B;**[!UICONTROL PayPal Merchant ID]**&#x200B;和相關欄位）。

   如果全域上線未完成，請將設定範圍切換為&#x200B;**[!UICONTROL Website]**，在&#x200B;**[!UICONTROL Payment Methods]**&#x200B;中開啟&#x200B;**[!UICONTROL Payment Services]**，且&#x200B;**[!UICONTROL Connect different account for website]**&#x200B;按鈕為&#x200B;**已停用**；請先完成聯結器設定和&#x200B;**全域** PayPal上線。

## [!UICONTROL Credit Card Fields]

[!UICONTROL Credit Card Fields]付款選項提供簡易且安全的信用卡或扣帳卡付款方式結帳。

如需詳細資訊，請參閱[付款選項](payments-options.md#paypal-payment-buttons)。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在左側面板中，展開&#x200B;**[!UICONTROL Sales]**&#x200B;並選擇&#x200B;**[!UICONTROL Payment Methods]**。
1. 展開&#x200B;_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;區段。
1. 在&#x200B;_[!UICONTROL Payment Services]_&#x200B;區段中，展開&#x200B;_[!UICONTROL Credit Card Fields]_&#x200B;區段。
1. 針對&#x200B;**[!UICONTROL Title]**，輸入文字（如有需要）以變更結帳時顯示的付款方式名稱。
1. 若要[設定付款動作](production.md#set-payment-services-as-payment-method)，請選取&#x200B;**[!UICONTROL Authorize]**&#x200B;或&#x200B;**授權並擷取**。
1. 若要優先處理結帳頁面上的付款方法，請在&#x200B;**[!UICONTROL Sort order]**&#x200B;欄位中提供`Numeric Only`值。
1. 對於&#x200B;**[!UICONTROL Show on checkout page]**，請選擇`Yes`以啟用結帳頁面上的信用卡欄位。
1. 針對&#x200B;**[!UICONTROL Vault Enabled]**，選擇`Yes`以啟用信用卡存放區以進行簽出。
1. 針對&#x200B;**[!UICONTROL Vault Enabled in Admin]**，選擇`Yes`以讓商家使用客戶的保管卡建立訂單。
1. 若要啟用&#x200B;**[!UICONTROL 3D Secure authentication]** （預設為`Off`），請選擇`Always`或`When required`。
1. 針對&#x200B;**[!UICONTROL Debug Mode]**，選擇`Yes`以啟用偵錯模式，或選擇`No`以停用偵錯模式。
1. 按一下&#x200B;**[!UICONTROL Save Config]**&#x200B;以儲存變更。
1. 導覽至&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**，然後按一下&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以重新整理所有無效的快取。

### 設定選項

| 欄位 | 範圍 | 說明 |
|---|---|---|
| [!UICONTROL Title] | 存放區檢視 | 在結帳期間，新增文字以在「付款方式」檢視中顯示為此付款選項的標題。 選項： [!UICONTROL text field] |
| [!UICONTROL Payment Action] | 網站 | 指定的付款方式的[付款動作](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html)。 選項： [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | 存放區檢視 | 結帳頁面上指定付款方式的排序順序。 `Numeric Only`值 |
| [!UICONTROL Show on checkout page] | 網站 | 啟用或停用結帳頁面上的信用卡欄位。 選項： [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL Vault enabled] | 存放區檢視 | 啟用或停用[信用卡存放區](vaulting.md)。 選項： [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL Vault enabled in Admin] | 存放區檢視 | 啟用或停用[商家使用保管庫付款方式完成管理員](vaulting.md)中客戶訂單的功能。 選項： [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL 3D Secure authentication] | 網站 | 啟用或停用[3DS安全驗證](security.md#3ds)。 選項： [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Debug Mode] | 網站 | 啟用或停用偵錯模式。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## [!UICONTROL Fastlane]

[[!DNL Fastlane by PayPal]](https://www.paypal.com/us/cshelp/article/what-is-fastlane-by-paypal-help1096)是快速且簡便的線上付款方式。 在&#x200B;**訪客結帳**&#x200B;期間，您可以安全地儲存您的卡片及運送詳細資料，以便日後更快地進行購買。

如需詳細資訊，請參閱[付款選項](payments-options.md#fastlane-button)。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在左側面板中，展開&#x200B;**[!UICONTROL Sales]**&#x200B;並選擇&#x200B;**[!UICONTROL Payment Methods]**。
1. 展開&#x200B;_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;區段。
1. 在&#x200B;_[!UICONTROL Payment Services]_&#x200B;區段中，展開&#x200B;_[!UICONTROL Fastlane]_&#x200B;區段。
1. 若要啟用它，請為&#x200B;**[!UICONTROL Enable Fastlane]**&#x200B;選取`Yes` （`No`停用它）。

   >[!NOTE]
   >
   > 如果已啟用[!UICONTROL Fastlane]，則會停用[!UICONTROL Credit Card Fields]付款選項。

1. 針對&#x200B;**[!UICONTROL Title]**，輸入文字（如有需要）以變更結帳時顯示的付款方式名稱。 預設標題為`Credit Card (via Fastlane)`
1. 若要[設定付款動作](production.md#set-payment-services-as-payment-method)，請選取&#x200B;**[!UICONTROL Authorize]**&#x200B;或&#x200B;**授權並擷取**。
1. 若要啟用&#x200B;**[!UICONTROL 3D Secure Authentication for Fastlane]** （預設為`Off`），請選擇`When required`以遵守歐盟法規，或選擇`Always`以新增額外的詐騙保護層。

   >[!NOTE]
   >
   > 如果卡片發行者需要3D安全驗證，則無論[!UICONTROL Payment Services]設定為何，都無法略過此步驟。

1. 若要優先處理結帳頁面上的付款方法，請在&#x200B;**[!UICONTROL Sort order]**&#x200B;欄位中提供`Numeric Only`值。
1. 透過將&#x200B;**[!UICONTROL Enable messaging]**&#x200B;欄位設定為`Yes`，指定是否在Adobe Commerce中籤出期間啟用[!UICONTROL Fastlane]品牌。
1. 按一下&#x200B;**[!UICONTROL Save Config]**&#x200B;以儲存變更。
1. 導覽至&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**，然後按一下&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以重新整理所有無效的快取。

| 欄位 | 範圍 | 說明 |
|---|---|---|
| [!UICONTROL Enable Fastlane] | 存放區檢視 | 啟用或停用結帳頁面上的[!DNL Fastlane]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Title] | 存放區檢視 | 在結帳期間，新增文字以在「付款方式」檢視中顯示為此付款選項的標題。 預設值為`Credit Card (via Fastlane)`。 選項： [!UICONTROL text field] |
| [!UICONTROL Payment Action] | 網站 | 指定的付款方式的[付款動作](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html)。 選項： [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL 3D Secure authentication] | 存放區檢視 | 啟用或停用Fastlane[&#128279;](security.md#3ds)的3D安全驗證。 選項： [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Sort order] | 存放區檢視 | 結帳頁面上指定付款方式的排序順序。 `Numeric Only`值 |
| [!UICONTROL Enable messaging] | 存放區檢視 | 指定在Adobe Commerce中籤出時是否啟用[!UICONTROL Fastlane]品牌。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |

### 選填。 進階樣式設定

這些選擇性設定可自訂[!UICONTROL Fastlane]在您網站上的顯示方式。

>[!TIP]
>
>不符合協助工具指引的樣式會回覆為預設設定。

1. 在&#x200B;_[!UICONTROL Payment Services]_&#x200B;區段中，導覽至&#x200B;_[!UICONTROL Fastlane]_&#x200B;區段。
1. 展開&#x200B;_[!UICONTROL Advanced Style Settings (optional)]_&#x200B;區段。
1. 視需要修改設定。
1. 按一下&#x200B;**[!UICONTROL Save Config]**&#x200B;以儲存變更。

如需自訂的詳細資訊，請參閱[PayPal開發人員檔案](https://developer.paypal.com/limited-release/accelerated-checkout-bt/)。

#### 根設定

這些選擇性設定會修改整個[!UICONTROL Fastlane]簽出元件。

| 欄位 | 範圍 | 說明 |
|---|---|---|
| [!UICONTROL Background Color] | 存放區檢視 | 定義元件的背景顏色。 僅`RGB`個值 |
| [!UICONTROL Border Color] | 存放區檢視 | 定義元件的邊框顏色。 僅`RGB`個值 |
| [!UICONTROL Font Family] | 存放區檢視 | 設定元件的字型。 只會顯示您的主題中可用的字型 |
| [!UICONTROL Font Size Base] | 存放區檢視 | 定義字型的大小。 僅`px` （畫素）值 |
| [!UICONTROL Padding] | 存放區檢視 | 設定元件中的內距。 僅`px` （畫素）值 |
| [!UICONTROL Primary Color] | 存放區檢視 | 定義元件的主要顏色。 僅`RGB`個值 |
| [!UICONTROL Text Color] | 存放區檢視 | 定義元件中文字的主要色彩。 僅`RGB`個值 |

#### 輸入設定

這些選擇性設定套用至[!UICONTROL Fastlane]元件的客戶輸入欄位。

| 欄位 | 範圍 | 說明 |
|---|---|---|
| [!UICONTROL Background Color] | 存放區檢視 | 定義元件的背景顏色。 僅`RGB`個值 |
| [!UICONTROL Border Color] | 存放區檢視 | 定義元件的邊框顏色。 僅`RGB`個值 |
| [!UICONTROL Border Radius] | 存放區檢視 | 定義框線的半徑。 僅`px` （畫素）值 |
| [!UICONTROL Border Width] | 存放區檢視 | 定義框線的寬度。 僅`px` （畫素）值 |
| [!UICONTROL Focus Border Color] | 存放區檢視 | 定義元件的焦點框線色彩。 僅`RGB`個值 |
| [!UICONTROL Text Color Base] | 存放區檢視 | 定義元件中文字的主要色彩。 僅`RGB`個值 |

## [!UICONTROL Apple Pay]

透過[!DNL Apple Pay]，商家可以提供安全、快速且順暢的結帳體驗，每個商家帳戶最多可支援99個網域。 在&#x200B;**Safari** （macOS和iOS）中，「[!DNL Apple Pay]」按鈕會在開始結帳（快速）和最終結帳頁面上，自動填入客戶裝置的付款、連絡人和運送資訊。 在&#x200B;**Chrome、Firefox或Microsoft Edge**&#x200B;中，[!DNL Apple Pay]在&#x200B;**快速結帳**&#x200B;期間以及&#x200B;**最終結帳步驟**&#x200B;皆可使用；在桌上型電腦上，QR碼和&#x200B;**iPhone** （iOS 18或更新版本）可讓購物者完成Apple Pay工作表的付款。 確定已在您想要快速簽出的位置啟用&#x200B;**[!UICONTROL Show Apple Pay on product detail page]**&#x200B;或其他位置。

>[!IMPORTANT]
>
> Apple會拒絕來自未驗證網域的付款。 商家必須驗證任何使用Apple Pay按鈕的網域。 國家限制適用。 如需網域驗證要求的詳細資訊，請參閱[Apple Pay檔案](https://developer.apple.com/documentation/apple_pay_on_the_web)。

如需詳細資訊，請參閱[付款選項](payments-options.md#apple-pay-button)。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在左側面板中，展開&#x200B;**[!UICONTROL Sales]**&#x200B;並選擇&#x200B;**[!UICONTROL Payment Methods]**。
1. 展開&#x200B;_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;區段。
1. 在&#x200B;_[!UICONTROL [!DNL Payment Services]]_&#x200B;區段中，展開&#x200B;_[!UICONTROL Apple Pay]_&#x200B;區段。
1. 針對&#x200B;**[!UICONTROL Title]**，輸入文字（如有需要）以變更結帳時顯示的付款方式名稱。
1. 若要[設定付款動作](production.md#set-payment-services-as-payment-method)，請選取&#x200B;**[!UICONTROL Authorize]**&#x200B;或&#x200B;**[!UICONTROL Authorize and Capture]**。
1. 視需要選取下列選項中的`Yes`，指定在Adobe Commerce中啟用[!DNL Apple Pay]選項的位置：
   * **[!UICONTROL Show Apple Pay on checkout page]**
   * **[!UICONTROL Show Apple Pay at start of checkout]**
   * **[!UICONTROL Show Apple Pay on product detail page]**
   * **[!UICONTROL Show Apple Pay in mini cart preview]**
   * **[!UICONTROL Show Apple Pay on cart page]**
1. 若要啟用偵錯模式，請為&#x200B;**[!UICONTROL Debug Mode]**&#x200B;選取`Yes` （`No`停用它）。
1. 若要儲存變更，請按一下「**[!UICONTROL Save Config]**」。
1. 導覽至&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**，然後按一下&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以重新整理所有無效的快取。

### 設定選項

| 欄位 | 範圍 | 說明 |
|---|---|---|
| [!UICONTROL Title] | 存放區檢視 | 在結帳期間，新增文字以在「付款方式」檢視中顯示為此付款選項的標題。 選項： [!UICONTROL text field] |
| [!UICONTROL Payment Action] | 網站 | 指定的付款方式的[付款動作](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html)。 選項： [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Show Apple Pay on checkout page] | 網站 | 啟用或停用結帳頁面上的[!DNL Apple Pay]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show Apple Pay at start of checkout] | 存放區檢視 | 在結帳流程開始時啟用或停用[!DNL Apple Pay]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | 存放區檢視 | 結帳頁面上指定付款方式的排序順序。 `Numeric Only`值 |
| [!UICONTROL Show Apple Pay on product detail page] | 存放區檢視 | 啟用或停用產品詳細資料頁面上的[!DNL Apple Pay]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show Apple Pay in mini cart preview] | 存放區檢視 | 啟用或停用迷你購物車預覽中的[!DNL Apple Pay]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show Apple Pay on cart page] | 存放區檢視 | 啟用或停用購物車頁面上的[!DNL Apple Pay]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Debug Mode] | 網站 | 啟用或停用偵錯模式。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## [!UICONTROL Google Pay]

[!UICONTROL Google Pay]付款選項可讓商家為購物者提供使用Google Wallet在裝置上進行購買的Google Pay。

如需詳細資訊，請參閱[付款選項](payments-options.md#google-pay-button)。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在左側面板中，展開&#x200B;**[!UICONTROL Sales]**&#x200B;並選擇&#x200B;**[!UICONTROL Payment Methods]**。
1. 展開&#x200B;_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;區段。
1. 在&#x200B;_[!UICONTROL [!DNL Payment Services]]_&#x200B;區段中，展開&#x200B;_[!UICONTROL Google Pay]_&#x200B;區段。
1. （選擇性）在&#x200B;**[!UICONTROL Title]**&#x200B;欄位中輸入新名稱，變更結帳時顯示的付款方式名稱。
1. [選取&#x200B;**[!UICONTROL Authorize]**&#x200B;或&#x200B;**[!UICONTROL Authorize and Capture]**&#x200B;以設定付款動作](production.md#set-payment-services-as-payment-method)。
1. 視需要選取下列選項中的`Yes`，指定在Adobe Commerce中啟用[!DNL Google Pay]選項的位置：
   * **[!UICONTROL Show Google Pay on checkout page]**
   * **[!UICONTROL Show Google Pay at start of checkout]**
   * **[!UICONTROL Show Google Pay on product detail page]**
   * **[!UICONTROL Show Google Pay in mini cart preview]**
   * **[!UICONTROL Show Google Pay on cart page]**
1. 若要選擇購物者是否在Google薪資表之後看到單獨的&#x200B;**Google薪資檢閱**&#x200B;頁面，請將&#x200B;**[!UICONTROL Skip Review]**&#x200B;設為`Yes`或`No`。 當設定為`Yes`時，支援的快速流程會在Google工資單&#x200B;**（使用者端送貨回撥）中顯示**&#x200B;送貨方法，且無需額外的稽核步驟即可完成。 設定為`No`時，購物者可以在付款前先在檢閱頁面上確認運費和總計。
1. 若要啟用&#x200B;**[!UICONTROL 3D Secure authentication]** （預設為`Off`），請選擇`Always`或`When required`。
1. 若要啟用偵錯模式，請為&#x200B;**[!UICONTROL Debug Mode]**&#x200B;選取`Yes` （`No`停用它）。
1. 視需要選取&#x200B;**[!UICONTROL Button Color]**、**[!UICONTROL Button Type]**&#x200B;和&#x200B;**[!UICONTROL Button Style]**，以設定&#x200B;_[!UICONTROL Google Pay]_&#x200B;按鈕的外觀。
1. 若要設定高度，請使用&#x200B;**[!UICONTROL Button Style]**&#x200B;中定義之高度的預設值。
1. 若要儲存變更，請按一下「**[!UICONTROL Save Config]**」。
1. 導覽至&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**，然後按一下&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以重新整理所有無效的快取。

### 設定選項

| 欄位 | 範圍 | 說明 |
|---|---|---|
| [!UICONTROL Title] | 存放區檢視 | 指定結帳時，在「付款方式」檢視中，為此付款選項顯示的文字標籤。 選項： `[!UICONTROL text field]` |
| [!UICONTROL Payment Action] | 網站 | 指定的付款方式的[付款動作](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html)。 選項： `[!UICONTROL Authorize]` / `[!UICONTROL Authorize and Capture]` |
| [!UICONTROL Show Google Pay on checkout page] | 網站 | 啟用或停用結帳頁面上的[!DNL Google Pay]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show Google Pay at start of checkout] | 存放區檢視 | 在結帳流程開始時啟用或停用[!DNL Google Pay]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | 存放區檢視 | 結帳頁面上指定付款方式的排序順序。 `Numeric Only`值 |
| [!UICONTROL Show Google Pay on product detail page] | 存放區檢視 | 啟用或停用產品詳細資料頁面上的[!DNL Google Pay]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show Google Pay in mini cart preview] | 存放區檢視 | 啟用或停用迷你購物車預覽中的[!DNL Google Pay]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show Google Pay on cart page] | 存放區檢視 | 啟用或停用購物車頁面上的[!DNL Google Pay]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Skip Review] | 存放區檢視 | 設定為`[!UICONTROL Yes]`時，符合資格的[!DNL Google Pay]快速流程可以在薪資表之後省略個別的稽核頁面；送貨方法會出現在Google薪資表中。 設定為`[!UICONTROL No]`時，購物者會前往檢閱頁面以確認運費和總計。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL 3D Secure authentication] | 存放區檢視 | 啟用或停用[3D安全驗證](security.md#3ds)。 選項： [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Debug Mode] | 網站 | 啟用或停用偵錯模式。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Button Color] | 存放區檢視 | 定義[!DNL Google Pay]按鈕的顏色。 選項： `[!UICONTROL Default]` / `[!UICONTROL Black]` / `[!UICONTROL White]` |
| [!UICONTROL Button Type] | 存放區檢視 | 定義[!DNL Google Pay]按鈕的型別。 選項： `[!UICONTROL buy]` / `[!UICONTROL checkout]` / `[!UICONTROL order]` / `[!UICONTROL pay]` / `[!UICONTROL plain]` |

如需詳細資訊，請參閱[Google Pay API要求物件選項](https://developers.google.com/pay/api/web/reference/request-objects)檔案。

## [!DNL PayPal Payment Buttons]

[!DNL PayPal payment buttons]付款選項可為您的客戶提供簡單、快速且安全的結帳程式。

如需詳細資訊，請參閱[付款選項](payments-options.md#paypal-payment-buttons)。

設定[!DNL PayPal payment buttons]

您可以在「管理員」中啟用並設定PayPal付款按鈕付款選項：

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在左側面板中，展開&#x200B;**[!UICONTROL Sales]**&#x200B;並選擇&#x200B;**[!UICONTROL Payment Methods]**。
1. 展開&#x200B;_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;區段。
1. 在&#x200B;_[!UICONTROL Payment Services]_&#x200B;區段中，展開&#x200B;_[!UICONTROL PayPal payment buttons]_&#x200B;區段。
1. 若要變更結帳時顯示的付款方式名稱，請編輯&#x200B;_[!UICONTROL Title]_&#x200B;欄位。
1. 若要[設定付款動作](production.md#set-payment-services-as-payment-method)，請選取&#x200B;**[!UICONTROL Authorize]**&#x200B;或&#x200B;**[!UICONTROL Authorize and Capture]**。
1. 若要優先處理結帳頁面上的付款方法，請在&#x200B;**[!UICONTROL Sort order]**&#x200B;欄位中提供`Numeric Only`值。
1. 若要啟用/停用[稍後付款訊息](payments-options.md#pay-later-button)，請為&#x200B;**[!UICONTROL Display Pay Later Message]**&#x200B;選取`Yes`/`No`。

   * 如果您啟用[稍後付款訊息](payments-options.md#pay-later-button)，則會顯示&#x200B;**[!UICONTROL Configure Messaging]**&#x200B;強制回應按鈕，讓您能夠設定&#x200B;**[!UICONTROL PayPal Pay Later messaging]**&#x200B;的樣式。

1. 視需要選取下列選項中的`Yes`，指定在Adobe Commerce中啟用PayPal付款按鈕的位置：
   * **[!UICONTROL Show buttons on checkout page]**
   * **[!UICONTROL Show buttons at start of checkout]**
   * **[!UICONTROL Show buttons on product detail page]**
   * **[!UICONTROL Show buttons in mini cart preview]**
   * **[!UICONTROL Show buttons on cart page]**
1. 若要啟用Venmo作為付款選項，請為&#x200B;**[!UICONTROL Venmo Enabled]**&#x200B;選取`Yes`。
1. 若要啟用信用卡和借記卡作為付款選項（PayPal智慧按鈕），請為&#x200B;**[!UICONTROL Credit and Debit Card Enabled]**&#x200B;選取`Yes`。
1. 若要啟用/停用[PayPal稍後付款](payments-options.md#pay-later-button)付款選項，請為&#x200B;**[!UICONTROL PayPal Pay Later Enabled]**&#x200B;選取`Yes`/`No`。
1. 若要啟用偵錯模式，請為&#x200B;**[!UICONTROL Debug Mode]**&#x200B;選取`Yes` （`No`停用它）。
1. 若要儲存變更，請按一下「**[!UICONTROL Save Config]**」。
1. 導覽至&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**，然後按一下&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以重新整理所有無效的快取。

### 設定選項

| 欄位 | 範圍 | 說明 |
|---|---|---|
| [!UICONTROL Title] | 存放區檢視 | 在結帳期間，在「付款方式」檢視中，新增要顯示為此付款選項標題的文字。 選項：文字欄位 |
| [!UICONTROL Payment Action] | 網站 | 指定的付款方式的[付款動作](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"}。 選項： [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Display Pay Later Message] | 網站 | 在購物車、產品頁面、迷你購物車和結帳流程中啟用或停用PayPal Pay Later訊息。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Configure Messaging] | 存放區檢視 | 修改PayPal Pay Later傳訊樣式。 選項： `[!UICONTROL Product page]` / `[!UICONTROL Cart]` |
| [!UICONTROL Show buttons on checkout page] | 存放區檢視 | 啟用或停用結帳頁面上的[!DNL PayPal payment buttons]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons at start of checkout] | 存放區檢視 | 在結帳流程開始時啟用或停用[!DNL PayPal payment buttons]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | 存放區檢視 | 結帳頁面上指定付款方式的排序順序。 `Numeric Only`值 |
| [!UICONTROL Show buttons on product detail page] | 存放區檢視 | 啟用或停用產品詳細資料頁面上的[!DNL PayPal payment buttons]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini cart preview] | 存放區檢視 | 啟用或停用迷你購物車預覽中的[!DNL PayPal payment buttons]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | 存放區檢視 | 啟用或停用購物車頁面上的[!DNL PayPal payment buttons]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL App Switch] | 存放區檢視 | 此選項僅適用於&#x200B;**US**&#x200B;商家和購買者。 啟用後，所有Express PayPal付款將嘗試透過PayPal行動應用程式（可用時）。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Contact Preference] | 存放區檢視 | 此選項僅適用於&#x200B;**US**&#x200B;商家和購買者。 若設為&#x200B;**是**，買家電子郵件和電話號碼將會顯示在PayPal付款強制回應視窗中。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Venmo Enabled] | 存放區檢視 | 啟用或停用顯示付款按鈕的Venmo付款選項。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Credit and Debit Card Enabled] | 存放區檢視 | 啟用或停用顯示付款按鈕的「信用卡」與「借記卡」選項。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL PayPal Pay Later Enabled] | 存放區檢視 | 啟用或停用顯示付款按鈕的PayPal Pay Later付款選項外觀。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Debug Mode] | 網站 | 啟用或停用偵錯模式。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## 本地付款方法

「當地付款方式(LPM)」除了現有的卡片型選項外，也支援特定地區和當地付款方式，例如銀行轉帳與當地化付款解決方案。 商家可以直接在Commerce設定中啟用或停用可用的LPM。 如需可用方法的詳細資訊，請參閱[付款選項](payments-options.md#local-payment-methods)。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在左側面板中，展開&#x200B;**[!UICONTROL Sales]**&#x200B;並選擇&#x200B;**[!UICONTROL Payment Methods]**。
1. 展開&#x200B;_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;區段。
1. 在&#x200B;_[!UICONTROL Payment Services]_&#x200B;區段中，展開&#x200B;_[!UICONTROL Local Payment Methods]_&#x200B;區段。
1. 針對&#x200B;**[!UICONTROL Active]**，選取`Yes`以啟用LPM，或選取`No`以停用LPM。
1. 針對&#x200B;**[!UICONTROL Title]**，輸入在結帳時顯示為付款方式名稱的文字。 此標題也會顯示在銷售訂單網格中。
1. 針對&#x200B;**[!UICONTROL Allowed Payment Methods]**，選取您要提供的付款方式。 可用的方法取決於買家的帳單地址和網站的基本貨幣。
1. 針對&#x200B;**[!UICONTROL Sort Order]**，請輸入數值以決定可用付款方式清單中LPM的顯示位置。
1. 若要儲存變更，請按一下&#x200B;**[!UICONTROL Save Config]**。
1. 導覽至&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**，然後按一下&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以重新整理所有無效的快取。

### 設定選項

| 欄位 | 範圍 | 說明 |
|---|---|---|
| [!UICONTROL Active] | 網站 | 啟用或停用本機付款方法。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Title] | 存放區檢視 | 結帳期間和銷售訂單網格中顯示的付款方式名稱。 選項： [!UICONTROL text field] |
| [!UICONTROL Allowed Payment Methods] | 網站 | 選取要提供的LPM。 只有帳單地址和網站貨幣符合方法需求的客戶，才能看見方法。 選項： `Bancontact` / `BLIK` / `eps` / `iDEAL` / `MyBank` / `Przelewy24` |
| [!UICONTROL Sort Order] | 存放區檢視 | LPM群組在可用付款方式清單中的顯示位置。 此設定會以群組形式套用至所有LPM；個別LPM無法獨立排序。 `Numeric Only`值 |

>[!NOTE]
>
>每個當地付款方式(LPM)都有特定的國家/地區與貨幣需求。 只有當客戶的帳單地址國家/地區與網站的基本貨幣符合這些需求時，才會顯示付款方法。 例如，Bancontact只會在基準貨幣為EUR時，針對帳單地址為比利時之客戶顯示。

## 條列專案

明細專案會將詳細的訂單資訊傳送至PayPal，包括產品詳細資料、數量及價格。 此功能預設為啟用。 如需詳細資訊，請參閱[條列專案](line-items.md)。

### 設定選項

| 欄位 | 範圍 | 說明 |
|---|---|---|
| [!UICONTROL Line Items Enabled] | 網站 | 啟用或停用傳送明細專案和金額劃分至PayPal。 如果您使用協力廠商擴充功能，但新增[!DNL Payment Services]不支援的自訂費用，請停用此設定。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## 按鈕樣式

您也可以設定付款按鈕的&#x200B;_[!UICONTROL Button style]_&#x200B;選項：

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在左側面板中，展開&#x200B;**[!UICONTROL Sales]**&#x200B;並選擇&#x200B;**[!UICONTROL Payment Methods]**。
1. 展開&#x200B;_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;區段。
1. 在&#x200B;_[!UICONTROL [!DNL Payment Services]]_&#x200B;區段中，展開&#x200B;_[!UICONTROL PayPal Smart Button Styling]_&#x200B;區段。
1. 若要設定配置，請為&#x200B;**[!UICONTROL Layout]**&#x200B;選取`Vertical`或`Horizontal`
1. 若要設定顏色，請在&#x200B;**[!UICONTROL Color]**&#x200B;中選取可用的顏色。
1. 若要設定圖案，請為&#x200B;**[!UICONTROL Shape]**&#x200B;選取`Rectangular`或`Pill`。
1. 若要使用預設高度，請為&#x200B;**[!UICONTROL Use Default Height]**&#x200B;選取`Yes`或`No`。
1. 若要設定自訂高度，請為&#x200B;**[!UICONTROL Height]**&#x200B;新增所需的畫素高度。
1. 若要設定標語，請為&#x200B;**[!UICONTROL Tagline]**&#x200B;選取`Yes`或`No`。
1. 若要儲存變更，請按一下「**[!UICONTROL Save Config]**」。
1. 導覽至&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**，然後按一下&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以重新整理所有無效的快取。

### 設定選項

| 欄位 | 範圍 | 說明 |
|--- |--- |--- |
| [!UICONTROL Layout] | 存放區檢視 | 定義Paypal付款按鈕的版面樣式。 選項： `[!UICONTROL Vertical]` / `[!UICONTROL Horizontal]` |
| [!UICONTROL Color] | 存放區檢視 | 定義Paypal付款按鈕的色彩。 選項： [!UICONTROL Blue] / `[!UICONTROL Gold]` / `[!UICONTROL Silver]` / `[!UICONTROL White]` / `[!UICONTROL Black]` |
| [!UICONTROL Shape] | 存放區檢視 | 定義Paypal付款按鈕的形狀。 選項： `[!UICONTROL Rectangular]` / `[!UICONTROL Pill]` |
| [!UICONTROL Use Default Height] | 存放區檢視 | 定義PayPal付款按鈕是否使用預設高度。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Height] | 存放區檢視 | 定義PayPal付款按鈕的高度。 預設值：無 |
| [!UICONTROL Label] | 存放區檢視 | 定義出現在PayPal付款按鈕中的標籤。 選項： `[!UICONTROL PayPal]` / `[!UICONTROL Checkout]` / `[!UICONTROL Buynow]` / `[!UICONTROL Pay]` / `[!UICONTROL Installment]` |
| [!UICONTROL Tagline] | 存放區檢視 | 啟用標語。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## 排清快取

如果您在&#x200B;_設定_&#x200B;中變更設定，例如切換Apple Pay、Venmo或PayPal PayLater按鈕，請手動清除快取，讓您的商店顯示最新設定。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**。
1. 按一下&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以重新整理所有無效的快取。

如果快取管理表格中的任何快取型別具有`INVALIDATED`狀態，您的存放區可能不會顯示該專案的最新設定。 排清快取以更新您的存放區以顯示最新設定。

為確保您的存放區顯示正確的設定，請定期[排清快取](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/cache-management)。

## 設定角色

為確保管理員使用者可以在Commerce管理員中建立和管理訂單，請針對使用者角色啟用[!DNL Payment Services]特定資源。

請參閱[使用者角色](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions-user-roles.html)以瞭解如何管理角色。

將資源指派給角色時，您必須選取：

* **以[!DNL Payment Services]**&#x200B;付款 — 此資源可確保當您在Admin中建立訂單時，[!DNL Payment Services]信用卡可作為付款方式使用。 如果您選取&#x200B;**動作**&#x200B;父資源，也會選取此資源。

* **[!DNL Payment Services]** — 此資源包含&#x200B;**儀表板**&#x200B;和&#x200B;**SaaS服務Proxy**&#x200B;資源，也必須選取這些資源。 他們確定[!DNL Payment Services]出現在&#x200B;_銷售_&#x200B;功能表中。

  ![付款服務資源](assets/roles-payments.png){width="400" zoomable="yes"}


## 卡片存放

您可以啟用功能，讓您的客戶可以將「我的帳戶」中的信用卡資訊儲存起來（或「儲存」），以便日後購買。

您也可以在「管理員」中使用卡存放，為現有客戶完成後續訂單。

在[信用卡欄位設定](#credit-card-fields)中啟用或停用卡片存放。

如需詳細資訊，請參閱[信用卡存放](vaulting.md)。

## 3DS

3DS可保護客戶與商家，避免其商店內的詐騙活動，並可確保符合歐盟(EU)標準。

啟用或停用[信用卡欄位設定](#credit-card-fields)中的3DS。

如需詳細資訊，請參閱安全性[&#128279;](security.md#3ds)中的3DS。

## 使用多個PayPal帳戶

在[!UICONTROL Payment Services]中，您可以在網站層級的&#x200B;**one**&#x200B;商家帳戶中使用多個PayPal帳戶。 例如，如果您在多個國家/地區經營您的商店（使用不同的[貨幣](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/currency/currency)），或想將Adobe Commerce用於您企業的某些部分而非&#x200B;_所有_，您可以將您的商家帳戶設定為使用多個PayPal帳戶。

如需有關網站、商店和商店檢視階層的詳細資訊，請參閱[網站、商店和檢視範圍](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html)。

若要在&#x200B;**全域** Commerce服務和PayPal上線完成之後，從管理員將&#x200B;**不同的PayPal帳戶連線至個別網站**，請在&#x200B;**[!UICONTROL Website]**&#x200B;範圍使用&#x200B;**[!UICONTROL Connect different account for website]**。 請參閱[為網站連線其他PayPal帳戶](#connect-a-different-paypal-account-for-a-website)。

如需透過CLI為多個PayPal帳戶設定範圍的詳細資訊，請參閱[命令列設定](configure-cli.md#configure-scope-via-cli)。
