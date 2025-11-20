---
title: '[!DNL Payment Services]設定'
description: 安裝之後，您可以在商店設定的Admin中設定 [!DNL Payment Services] 。
role: Admin, User
level: Intermediate
exl-id: e1a3269d-bdf9-4b0f-972f-e8a0ef469503
feature: Payments, Checkout, Configuration
source-git-commit: a64aa0425c43a2818735614adde70bdcd1e072d6
workflow-type: tm+mt
source-wordcount: '2716'
ht-degree: 0%

---

# [!DNL Payment Services]設定

您可以使用Admin中實用的組態選項自訂[!DNL Payment Services]以符合您的需求。

當您在Admin中為[!DNL Payment Services]和[!DNL Adobe Commerce]設定[!DNL Magento Open Source]時，這些設定僅適用於&#x200B;_[!UICONTROL Method]_的_[!UICONTROL General Configuration]_&#x200B;欄位中設定的環境。 您在設定欄位中所做的任何變更與切換&#x200B;_[!UICONTROL Method]_選取專案無關 — 如果您切換方法，您的選取專案不會重設。

## 一般設定

您可以為商店和[!DNL Payment Services]啟用&#x200B;_[!UICONTROL Merchant Location]_，並在_[!UICONTROL General Configuration]_&#x200B;區段中啟用沙箱測試或即時付款。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在左側面板中，展開&#x200B;**[!UICONTROL Sales]**&#x200B;並選擇&#x200B;**[!UICONTROL Payment Methods]**。
1. 設定&#x200B;_[!UICONTROL Merchant Country]_中的_[!UICONTROL Merchant Location]_&#x200B;欄位。 如果未指定&#x200B;_[!UICONTROL Merchant Country]_，則會使用一般設定的_[!UICONTROL Default Country]_。
1. 展開&#x200B;_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_區段以存取_[!UICONTROL [!DNL Payment Services]]_&#x200B;區段。
1. 在&#x200B;_[!UICONTROL [!DNL Payment Services]]_區段中，展開_[!UICONTROL General Configuration]_&#x200B;區段。
1. 針對&#x200B;**啟用**，將其設定為`Yes`以啟用您商店的[!DNL Payment Services]。
1. 若為&#x200B;**方法**，若您仍在測試存放區的`Sandbox`，請將其設為[!DNL Payment Services]，或若您已準備啟用即時付款，請設為`Production`。
1. 一旦您設定&#x200B;**[!UICONTROL Payment Services Sandbox ID]** Commerce服務聯結器&#x200B;**[!UICONTROL Payment Services Production ID]**&#x200B;並首次造訪[儀表板，系統就會自動填入您的](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/user-guides/integration-services/saas){target=_blank}和[!DNL Payment Services]值。 執行此動作以完成您的沙箱和/或生產環境的上線。 這些值會將您的SaaS ID與[!DNL Payment Services]建立關聯。

   >[!WARNING]
   >
   > 如果您需要在Commerce Services Connector中變更資料空間ID，需要重設您的[!DNL Payment Services] ID。 按一下&#x200B;**重設付款服務ID**&#x200B;以重設您的沙箱ID。 如果您重設[!DNL Payment Services]沙箱ID，則必須重新上線。

1. 第一次造訪&#x200B;**[!UICONTROL PayPal Merchant ID]**&#x200B;儀表板時，PayPal會自動提供您的&#x200B;**[!UICONTROL PayPal Merchant Status]**&#x200B;和[!DNL Payment Services]值。
1. 對於&#x200B;**軟性描述項** （自訂值，顯示在客戶交易銀行對帳單上，以描述商店/品牌/目錄之間），請在文字欄位中新增自訂文字（最多22個字元），取代`Soft descriptor`或現有值。
1. 按一下&#x200B;**[!UICONTROL Save Config]**&#x200B;以儲存變更。
1. 導覽至&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**，然後按一下&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以重新整理所有無效的快取。

![精選Adobe解決方案檢視](assets/config-view-all.png){width="700" zoomable="yes"}

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

## [!UICONTROL Credit Card Fields]

[!UICONTROL Credit Card Fields]付款選項提供簡易且安全的信用卡或扣帳卡付款方式結帳。

如需詳細資訊，請參閱[付款選項](payments-options.md#paypal-smart-buttons)。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在左側面板中，展開&#x200B;**[!UICONTROL Sales]**&#x200B;並選擇&#x200B;**[!UICONTROL Payment Methods]**。
1. 展開&#x200B;_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_區段。
1. 在&#x200B;_[!UICONTROL Payment Services]_區段中，展開_[!UICONTROL Credit Card Fields]_&#x200B;區段。
1. 針對&#x200B;**[!UICONTROL Title]**，輸入文字（如有需要）以變更結帳時顯示的付款方式名稱。
1. 若要[設定付款動作](production.md#set-payment-services-as-payment-method)，請選取&#x200B;**[!UICONTROL Authorize]**&#x200B;或&#x200B;**授權並擷取**。
1. 若要優先處理結帳頁面上的付款方法，請在`Numeric Only`欄位中提供&#x200B;**[!UICONTROL Sort order]**&#x200B;值。
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
1. 展開&#x200B;_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_區段。
1. 在&#x200B;_[!UICONTROL Payment Services]_區段中，展開_[!UICONTROL Fastlane]_&#x200B;區段。
1. 若要啟用它，請為`Yes`選取&#x200B;**[!UICONTROL Enable Fastlane]** （`No`停用它）。

   >[!NOTE]
   >
   > 如果已啟用[!UICONTROL Fastlane]，則會停用[!UICONTROL Credit Card Fields]付款選項。

1. 針對&#x200B;**[!UICONTROL Title]**，輸入文字（如有需要）以變更結帳時顯示的付款方式名稱。 預設標題為`Credit Card (via Fastlane)`
1. 若要[設定付款動作](production.md#set-payment-services-as-payment-method)，請選取&#x200B;**[!UICONTROL Authorize]**&#x200B;或&#x200B;**授權並擷取**。
1. 若要啟用&#x200B;**[!UICONTROL 3D Secure Authentication for Fastlane]** （預設為`Off`），請選擇`When required`以遵守歐盟法規，或選擇`Always`以新增額外的詐騙保護層。

   >[!NOTE]
   >
   > 如果卡片發行者需要3D安全驗證，則無論[!UICONTROL Payment Services]設定為何，都無法略過此步驟。

1. 若要優先處理結帳頁面上的付款方法，請在`Numeric Only`欄位中提供&#x200B;**[!UICONTROL Sort order]**&#x200B;值。
1. 透過將[!UICONTROL Fastlane]欄位設定為&#x200B;**[!UICONTROL Enable messaging]**，指定是否在Adobe Commerce中籤出期間啟用`Yes`品牌。
1. 按一下&#x200B;**[!UICONTROL Save Config]**&#x200B;以儲存變更。
1. 導覽至&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**，然後按一下&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以重新整理所有無效的快取。

| 欄位 | 範圍 | 說明 |
|---|---|---|
| [!UICONTROL Enable Fastlane] | 存放區檢視 | 啟用或停用結帳頁面上的[!DNL Fastlane]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Title] | 存放區檢視 | 在結帳期間，新增文字以在「付款方式」檢視中顯示為此付款選項的標題。 預設值為`Credit Card (via Fastlane)`。 選項： [!UICONTROL text field] |
| [!UICONTROL Payment Action] | 網站 | 指定的付款方式的[付款動作](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html)。 選項： [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL 3D Secure authentication] | 存放區檢視 | 啟用或停用Fastlane[的](security.md#3ds)3D安全驗證。 選項： [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Sort order] | 存放區檢視 | 結帳頁面上指定付款方式的排序順序。 `Numeric Only`值 |
| [!UICONTROL Enable messaging] | 存放區檢視 | 指定在Adobe Commerce中籤出時是否啟用[!UICONTROL Fastlane]品牌。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |

### 選填。 進階樣式設定

這些選擇性設定可自訂[!UICONTROL Fastlane]在您網站上的顯示方式。

>[!TIP]
>
>不符合協助工具指引的樣式會回覆為預設設定。

1. 在&#x200B;_[!UICONTROL Payment Services]_區段中，導覽至_[!UICONTROL Fastlane]_&#x200B;區段。
1. 展開&#x200B;_[!UICONTROL Advanced Style Settings (optional)]_區段。
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

透過[!DNL Apple Pay]，商家可以在Safari中提供安全、快速且順暢的結帳體驗，每個商家帳戶最多可支援99個網域。 「[!DNL Apple Pay]」按鈕會自動填入來自客戶iOS或macOS裝置的付款、聯絡和運送資訊，讓您能夠進行快速單點購買，有助於提高轉換率。

如需詳細資訊，請參閱[付款選項](payments-options.md#apple-pay-button)。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在左側面板中，展開&#x200B;**[!UICONTROL Sales]**&#x200B;並選擇&#x200B;**[!UICONTROL Payment Methods]**。
1. 展開&#x200B;_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_區段。
1. 在&#x200B;_[!UICONTROL Payment Services]_區段中，展開_[!UICONTROL Apple Pay]_&#x200B;區段。
1. 針對&#x200B;**[!UICONTROL Title]**，輸入文字（如有需要）以變更結帳時顯示的付款方式名稱。
1. 若要[設定付款動作](production.md#set-payment-services-as-payment-method)，請選取&#x200B;**[!UICONTROL Authorize]**&#x200B;或&#x200B;**[!UICONTROL Authorize and Capture]**。
1. 視需要選取下列選項中的[!DNL Apple Pay]，指定在Adobe Commerce中啟用`Yes`選項的位置：
   * **[!UICONTROL Show Apple Pay on checkout page]**
   * **[!UICONTROL Show Apple Pay on product detail page]**
   * **[!UICONTROL Show Apple Pay in mini cart preview]**
   * **[!UICONTROL Show Apple Pay on cart page]**
1. 若要啟用偵錯模式，請為`Yes`選取&#x200B;**[!UICONTROL Debug Mode]** （`No`停用它）。
1. 若要儲存變更，請按一下「**[!UICONTROL Save Config]**」。
1. 導覽至&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**，然後按一下&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以重新整理所有無效的快取。

### 設定選項

| 欄位 | 範圍 | 說明 |
|---|---|---|
| [!UICONTROL Title] | 存放區檢視 | 在結帳期間，新增文字以在「付款方式」檢視中顯示為此付款選項的標題。 選項： [!UICONTROL text field] |
| [!UICONTROL Payment Action] | 網站 | 指定的付款方式的[付款動作](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html)。 選項： [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Show on checkout page] | 網站 | 啟用或停用結帳頁面上的[!DNL Apple Pay]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | 存放區檢視 | 結帳頁面上指定付款方式的排序順序。 `Numeric Only`值 |
| [!UICONTROL Show buttons on product detail page] | 存放區檢視 | 啟用或停用產品詳細資料頁面上的[!DNL Apple Pay]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini-cart preview] | 存放區檢視 | 啟用或停用迷你購物車預覽中的[!DNL Apple Pay]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | 存放區檢視 | 啟用或停用購物車頁面上的[!DNL Apple Pay]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Debug Mode] | 網站 | 啟用或停用偵錯模式。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## [!UICONTROL Google Pay]

[!UICONTROL Google Pay]付款選項可讓商家為購物者提供使用Google Wallet在裝置上進行購買的Google Pay。

如需詳細資訊，請參閱[付款選項](payments-options.md#google-pay-button)。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在左側面板中，展開&#x200B;**[!UICONTROL Sales]**&#x200B;並選擇&#x200B;**[!UICONTROL Payment Methods]**。
1. 展開&#x200B;_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_區段。
1. 在&#x200B;_[!UICONTROL Payment Services]_區段中，展開_[!UICONTROL Google Pay]_&#x200B;區段。
1. （選擇性）在&#x200B;**[!UICONTROL Title]**&#x200B;欄位中輸入新名稱，變更結帳時顯示的付款方式名稱。
1. [選取](production.md#set-payment-services-as-payment-method)或&#x200B;**[!UICONTROL Authorize]**&#x200B;以設定付款動作&#x200B;**[!UICONTROL Authorize and Capture]**。
1. 視需要選取下列選項中的[!DNL Google Pay]，指定在Adobe Commerce中啟用`Yes`選項的位置：
   * **[!UICONTROL Show Google Pay on checkout page]**
   * **[!UICONTROL Show Google Pay on product detail page]**
   * **[!UICONTROL Show Google Pay in mini cart preview]**
   * **[!UICONTROL Show Google Pay on cart page]**
1. 若要啟用&#x200B;**[!UICONTROL 3D Secure authentication]** （預設為`Off`），請選擇`Always`或`When required`。
1. 若要啟用偵錯模式，請為`Yes`選取&#x200B;**[!UICONTROL Debug Mode]** （`No`停用它）。
1. 視需要選取&#x200B;_[!UICONTROL Google Pay]_、**[!UICONTROL Button Color]**和&#x200B;**[!UICONTROL Button Type]**，以設定&#x200B;**[!UICONTROL Button Style]**按鈕的外觀。
1. 若要設定高度，請使用&#x200B;**[!UICONTROL Button Style]**&#x200B;中定義之高度的預設值。
1. 若要儲存變更，請按一下「**[!UICONTROL Save Config]**」。
1. 導覽至&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**，然後按一下&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以重新整理所有無效的快取。

### 設定選項

| 欄位 | 範圍 | 說明 |
|---|---|---|
| [!UICONTROL Title] | 存放區檢視 | 指定結帳時，在「付款方式」檢視中，為此付款選項顯示的文字標籤。 選項： `[!UICONTROL text field]` |
| [!UICONTROL Payment Action] | 網站 | 指定的付款方式的[付款動作](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html)。 選項： `[!UICONTROL Authorize]` / `[!UICONTROL Authorize and Capture]` |
| [!UICONTROL Show on checkout page] | 網站 | 啟用或停用結帳頁面上的[!DNL Google Pay]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | 存放區檢視 | 結帳頁面上指定付款方式的排序順序。 `Numeric Only`值 |
| [!UICONTROL Show buttons on product detail page] | 存放區檢視 | 啟用或停用產品詳細資料頁面上的[!DNL Google Pay]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini-cart preview] | 存放區檢視 | 啟用或停用迷你購物車預覽中的[!DNL Google Pay]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | 存放區檢視 | 啟用或停用購物車頁面上的[!DNL Google Pay]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL 3D Secure authentication] | 存放區檢視 | 啟用或停用[3D安全驗證](security.md#3ds)。 選項： [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Debug Mode] | 網站 | 啟用或停用偵錯模式。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Button Color] | 存放區檢視 | 定義[!DNL Google Pay]按鈕的顏色。 選項： `[!UICONTROL Default]` / `[!UICONTROL Black]` / `[!UICONTROL White]` |
| [!UICONTROL Button Type] | 存放區檢視 | 定義[!DNL Google Pay]按鈕的型別。 選項： `[!UICONTROL buy]` / `[!UICONTROL checkout]` / `[!UICONTROL order]` / `[!UICONTROL pay]` / `[!UICONTROL plain]` |

如需詳細資訊，請參閱[Google Pay API要求物件選項](https://developers.google.com/pay/api/web/reference/request-objects)檔案。

## [!DNL PayPal Payment Buttons]

[!DNL PayPal payment buttons]付款選項可為您的客戶提供簡單、快速且安全的結帳程式。

如需詳細資訊，請參閱[付款選項](payments-options.md#paypal-smart-buttons)。

設定[!DNL PayPal payment buttons]

您可以在「管理員」中啟用並設定PayPal付款按鈕付款選項：

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在左側面板中，展開&#x200B;**[!UICONTROL Sales]**&#x200B;並選擇&#x200B;**[!UICONTROL Payment Methods]**。
1. 展開&#x200B;_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_區段。
1. 在&#x200B;_[!UICONTROL Payment Services]_區段中，展開_[!UICONTROL PayPal payment buttons]_&#x200B;區段。
1. 若要變更結帳時顯示的付款方式名稱，請編輯&#x200B;_[!UICONTROL Title]_欄位。
1. 若要[設定付款動作](production.md#set-payment-services-as-payment-method)，請選取&#x200B;**[!UICONTROL Authorize]**&#x200B;或&#x200B;**[!UICONTROL Authorize and Capture]**。
1. 若要優先處理結帳頁面上的付款方法，請在`Numeric Only`欄位中提供&#x200B;**[!UICONTROL Sort order]**&#x200B;值。
1. 若要啟用/停用[稍後付款訊息](payments-options.md#pay-later-button)，請為`Yes`選取`No`/**[!UICONTROL Display Pay Later Message]**。

   * 如果您啟用[稍後付款訊息](payments-options.md#pay-later-button)，則會顯示&#x200B;**[!UICONTROL Configure Messaging]**&#x200B;強制回應按鈕，讓您能夠設定&#x200B;**[!UICONTROL PayPal Pay Later messaging]**&#x200B;的樣式。

1. 視需要選取下列選項中的`Yes`，指定在Adobe Commerce中啟用PayPal付款按鈕的位置：
   * **[!UICONTROL Show buttons on checkout page]**
   * **[!UICONTROL Show buttons on product detail page]**
   * **[!UICONTROL Show buttons in mini cart preview]**
   * **[!UICONTROL Show buttons on cart page]**
1. 若要啟用Venmo作為付款選項，請為`Yes`選取&#x200B;**[!UICONTROL Venmo Enabled]**。
1. 若要啟用信用卡和借記卡作為付款選項（PayPal智慧按鈕），請為`Yes`選取&#x200B;**[!UICONTROL Credit and Debit Card Enabled]**。
1. 若要啟用/停用[PayPal稍後付款](payments-options.md#pay-later-button)付款選項，請為`Yes`選取`No`/**[!UICONTROL PayPal Pay Later Enabled]**。
1. 若要啟用偵錯模式，請為`Yes`選取&#x200B;**[!UICONTROL Debug Mode]** （`No`停用它）。
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
| [!UICONTROL Show buttons on product detail page] | 存放區檢視 | 啟用或停用產品詳細資料頁面上的[!DNL PayPal payment buttons]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini-cart preview] | 存放區檢視 | 啟用或停用迷你購物車預覽中的[!DNL PayPal payment buttons]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | 存放區檢視 | 啟用或停用購物車頁面上的[!DNL PayPal payment buttons]。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Venmo Enabled] | 存放區檢視 | 啟用或停用顯示付款按鈕的Venmo付款選項。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Credit and Debit Card Enabled] | 存放區檢視 | 啟用或停用顯示付款按鈕的「信用卡」與「借記卡」選項。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL PayPal Pay Later Enabled] | 存放區檢視 | 啟用或停用顯示付款按鈕的PayPal Pay Later付款選項外觀。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Debug Mode] | 網站 | 啟用或停用偵錯模式。 選項： `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## 按鈕樣式

您也可以設定付款按鈕的&#x200B;_[!UICONTROL Button style]_選項：

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在左側面板中，展開&#x200B;**[!UICONTROL Sales]**&#x200B;並選擇&#x200B;**[!UICONTROL Payment Methods]**。
1. 展開&#x200B;_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_區段。
1. 在&#x200B;_[!UICONTROL [!DNL Payment Services]]_區段中，展開_[!UICONTROL PayPal Smart Button Styling]_&#x200B;區段。
1. 若要設定配置，請為`Vertical`選取`Horizontal`或&#x200B;**[!UICONTROL Layout]**
1. 若要設定顏色，請在&#x200B;**[!UICONTROL Color]**&#x200B;中選取可用的顏色。
1. 若要設定圖案，請為`Rectangular`選取`Pill`或&#x200B;**[!UICONTROL Shape]**。
1. 若要使用預設高度，請為`Yes`選取`No`或&#x200B;**[!UICONTROL Use Default Height]**。
1. 若要設定自訂高度，請為&#x200B;**[!UICONTROL Height]**&#x200B;新增所需的畫素高度。
1. 若要設定標語，請為`Yes`選取`No`或&#x200B;**[!UICONTROL Tagline]**。
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

如需詳細資訊，請參閱安全性[中的](security.md#3ds)3DS。

## 使用多個PayPal帳戶

在[!UICONTROL Payment Services]中，您可以在網站層級的&#x200B;**one**&#x200B;商家帳戶中使用多個PayPal帳戶。 例如，如果您在多個國家/地區經營您的商店（使用不同的[貨幣](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/currency/currency)），或想將Adobe Commerce用於您企業的某些部分而非&#x200B;_所有_，您可以將您的商家帳戶設定為使用多個PayPal帳戶。

如需有關網站、商店和商店檢視階層的詳細資訊，請參閱[網站、商店和檢視範圍](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html)。

如需透過CLI為多個PayPal帳戶設定範圍的詳細資訊，請參閱[命令列設定](configure-cli.md#configure-scope-via-cli)。

您的銷售代表可以為您的商家帳戶建立新的[範圍](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings)，並使用PayPal加入其他網站，以便您設定要顯示的任何PayPal按鈕都會顯示在您的網站上。 聯絡您的銷售人員
代表您協助為網站使用多個PayPal帳戶。
