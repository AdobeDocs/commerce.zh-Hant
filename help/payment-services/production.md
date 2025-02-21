---
title: '為生產啟用 [!DNL Payment Services] '
description: 啟用 [!DNL Payment Services] 以進行生產，以完成入門流程。
feature: Payments, Checkout, Configuration, Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 0%

---

# 為生產啟用[!DNL Payment Services]

您可以在下列步驟之後，依照此主題中的步驟，將服務投入生產並完成[上線程式](onboard.md)：

* [安裝](install.md)付款服務延伸
* [設定並連線](connect.md)您的執行個體
* [設定](sandbox.md)並[測試](test-validate.md)您的沙箱

## 將[!DNL Payment Services]設為付款方式

在您[設定您的Commerce服務](connect.md#configure-commerce-services)並啟用[沙箱測試](sandbox.md#enable-sandbox-testing)或[即時付款](#enable-live-payments)之後，您必須將[!DNL Payment Services]設定為您的付款方式。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**。
1. 按一下&#x200B;**[!UICONTROL Enable Payment Services]**。

   如果您尚未將[!DNL Payment Services]設定為您一或多個網站的付款方式，便會顯示此選項。

   您被導向到[首頁]檢視中的設定區域，並展開相關選項(**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Settings]_)，您可以在此啟用[!DNL Payment Services]選項做為您的[付款方式](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods){target="_blank"}。

1. 在&#x200B;_[!UICONTROL General Configuration]_中，將&#x200B;**[!UICONTROL Enable]**設為`Yes`。
1. 將&#x200B;_[!UICONTROL Credit Card Fields]_和_[!UICONTROL PayPal payment buttons]_&#x200B;的&#x200B;**[!UICONTROL Payment Action]**&#x200B;設定為下列其中一項：

   | 設定 | 說明 |
   |---|---|
   | `Authorize` | 核准購買並保留資金。 此金額必須等到商家「擷取」後才會提取。 |
   | `Authorize and Capture` | 核准購買且商家「擷取」資金。 |

   >[!IMPORTANT]
   >
   >[!DNL Payment Services]支援部分擷取。 商家可以部份擷取訂單的（商業發票）部分。 例如，您可以分別擷取每個專案，或現在擷取一個專案，稍後擷取其餘的專案。

1. 按一下&#x200B;**[!UICONTROL Save]**。
1. 按一下&#x200B;**[!UICONTROL Go to Payment Services]**&#x200B;以導向回[!DNL Payment Services]首頁。
1. [清除您的快取](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cache-management.html)。

   應在每次設定變更後進行清除。

請參閱[設定付款服務](settings.md)，以取得有關設定信用卡欄位和PayPal付款按鈕的詳細資訊。

## 完成商家入門

若要讓您的商店上線付款服務，下一步就是完成上線。

根據您營運的國家和您偏好的付款體驗，「付款服務」會提供&#x200B;[**進階** （完全支援）和&#x200B;**標準** （快速結帳）付款選項](../payment-services/payments-options.md#standard-vs-advanced-payments-experience)和上線流程。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**。
1. 按一下&#x200B;**[!UICONTROL Live onboarding]**。

   如果您尚未完成[!DNL Payment Services]的即時上線，便會顯示此選項。

1. 在&#x200B;_選取您所在的國家_&#x200B;強制回應視窗中，選取您正在作業的國家/地區。

   付款服務目前針對[五個國家/地區](../payment-services/overview.md#availability)的所有付款選項提供完整支援。 Payment Services為國家/地區清單中代表的所有其他國家/地區提供快速結帳功能（付款選項的子集）。

   您從清單中選擇的國家將決定您可用的付款選項，以及上線流程 — [進階](#advanced-onboarding) （完全支援）或[標準](#standard-onboarding) （快速結帳）。

>[!TIP]
>
> 選擇並繼續上線選項（標準或進階）後，您必須重新完成上線，才能從初始選擇升級或降級。

### 進階上線

此入門流程適用於[完全支援國家/地區](../payment-services/overview.md#availability)的商家。

選取國家/地區後：

1. 在出現的強制回應視窗中，選取&#x200B;**進階**。

   針對&#x200B;**標準**&#x200B;選項，請繼續進行[標準上線流程](#standard-onboarding)。

1. 按一下&#x200B;**繼續**。
1. 繼續使用PayPal流程，以取得完全支援的進階上線，使用您的PayPal帳戶認證（不是您的沙箱帳戶認證） _或_&#x200B;註冊新的PayPal帳戶。

>[!IMPORTANT]
>
>**進階上線**&#x200B;要求商家[要求付款權益](#request-payments-entitlement-from-adobe)以啟用即時上線。

### 標准入門

此Standard上線流程適用於[僅支援Express Checkout](../payment-services/overview.md#availability)的可用國家/地區的商家。

選取國家/地區後：

1. 在出現的&#x200B;_付款服務合約_&#x200B;強制回應視窗中，按一下&#x200B;**付款服務合約**&#x200B;連結以檢視Adobe Commerce付款服務合約。
1. 在&#x200B;_付款服務合約_&#x200B;強制回應視窗中，按一下&#x200B;**我接受**。
1. 繼續使用您的PayPal帳戶認證（不是沙箱帳戶認證）或註冊新的PayPal帳戶，進行PayPal快速登入流程。

>[!IMPORTANT]
>
>[Apple付款和信用卡欄位](../payment-services/payments-options.md)不適用於&#x200B;**標准入門**。

## 確認電子郵件地址

1. 在管理員側邊欄上，前往&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**

   _[!UICONTROL Live onboarding]_按鈕不再可見，您會看到「[!UICONTROL Live payments pending]」文字方塊。

   在該文字方塊中，系統可能會要求您確認使用PayPal的電子郵件地址，以便完成上線。

1. 如果系統提示您確認您的電子郵件地址，請檢查您的電子郵件是否有從PayPal傳送的確認訊息，然後按一下以確認您的電子郵件地址。
1. 在管理員側邊欄上，前往&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**。
1. 重新整理您的瀏覽器視窗。

   當您的PayPal商家上線獲得核準時，您應該會看到一則通知，指出您的付款系統處於沙箱模式，且未處理即時付款。

   >[!IMPORTANT]
   >
   >如果您撤銷[!DNL Adobe Commerce]與[!DNL Magento Open Source]對[!DNL Payment Services]的同意，以處理您的付款（在您的PayPal帳戶設定中），則[!DNL Payment Services]無法處理您商店中的訂單。 在您的「付款服務首頁」上，會出現有關撤銷同意的警報。

## 向Adobe要求付款權益

若要讓您的商店上線，請向Adobe要求付款權益（僅限[進階上線](#advanced-onboarding)）：

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**。
1. 在您的[!DNL Payment Services]首頁按一下&#x200B;**[!UICONTROL Get Live Payments]**。

   ![要求權益](assets/request-entitlements.png){width="500" zoomable="yes"}

1. 完成表單。
1. 銷售團隊的成員將會與您連絡。

或者，您可以透過[business.adobe.com](https://business.adobe.com/resources/payment-services.html)，向Adobe索取付款權益。

>[!IMPORTANT]
>
>在核准付款權益之前，無法存取&#x200B;**即時上線**。

## 設定定價層

取得您的[!DNL Payment Services] _商家識別碼_：

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**。
1. 在[首頁]檢視中，按一下&#x200B;**[!UICONTROL Settings]**。 如需詳細資訊，請參閱[首頁](payments-home.md)。
1. 選取必要的&#x200B;_商家識別碼_，然後將其提交給您的銷售代表，銷售代表將會設定正確的定價層級。

如需付款交易的詳細資訊，請參閱[層級2與層級3處理](levels-card-payment-transactions.md)。

## 啟用即時付款

_生產商家識別碼_&#x200B;已自動產生，並填入[組態](configure-admin.md)。 請勿變更或變更此ID。

啟用即時付款：

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**。
1. 在首頁上，按一下頁面右上角的&#x200B;**[!UICONTROL Settings]**。 如需詳細資訊，請參閱[首頁](payments-home.md)。
1. 在&#x200B;_[!UICONTROL General Configuration]_區段中，將&#x200B;**[!UICONTROL Payment mode]**設為`Production`。
1. 按一下&#x200B;**[!UICONTROL Save]**。
1. [清除您的快取](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/cache-management){target="_blank"}。

   >[!IMPORTANT]
   >
   >如果您未清除快取，客戶在結帳時就無法看到PayPal付款選項。

如果您導覽回[!DNL Payment Services]首頁，沙箱付款模式訊息將不再出現，因為您正在處理即時付款。

如需舊版組態選項，請參閱[在Admin](configure-admin.md)中設定。

>[!IMPORTANT]
>
>如果您撤銷[!DNL Payment Services]處理付款（在您的PayPal帳戶設定中）的同意，[!DNL Payment Services]將無法處理您商店中的訂單。 如果您想要重新啟用付款處理功能，必須重新完成上線。 在您的「付款服務首頁」上，會出現有關撤銷同意的警報。

## 在生產環境中測試

強烈建議您先在生產環境中測試付款，並使用真正的信用卡和銀行，然後再向購物者公開此功能。

如需詳細資訊，請參閱[測試及驗證](test-validate.md)。
