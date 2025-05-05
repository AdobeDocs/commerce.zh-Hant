---
title: 連線您的執行個體
description: 使用API金鑰和私密金鑰連線您的Commerce執行個體，並在設定中指定資料空間。
feature: Payments, Checkout, Configuration, Saas
exl-id: f2b3be02-e9dd-4bca-b9e4-c80a56bf8691
source-git-commit: 16bd0e7ed1e8982e1571e2593115824a2004b7dc
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---

# 連線您的執行個體

[!DNL Payment Services]由Commerce Services提供技術支援，並部署為SaaS （軟體即服務）。 您使用API金鑰和私密金鑰來連線Commerce執行個體，並使用[Commerce Services Connector](https://experienceleague.adobe.com/docs/commerce/user-guides/saas.html)指定設定中的資料空間。 **您只設定此連線一次。**

>[!VIDEO](https://video.tv.adobe.com/v/3447835)

>[!INFO]
>
> 如需其他資訊，請參閱我們的[[!DNL Adobe Commerce] 服務聯結器](https://experienceleague.adobe.com/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector.html?lang=zh-Hant)影片。

* 如果您&#x200B;*已連線您的執行個體*，透過取得和使用您的API認證並設定Commerce服務，您可以繼續[設定您的測試沙箱](https://experienceleague.adobe.com/docs/commerce/payment-services/get-started/sandbox.html?lang=zh-Hant)。
* 如果您仍&#x200B;*需要連線執行個體*，請參閱本主題中有關[取得API認證](#obtain-api-credentials)和[設定Commerce服務](#configure-commerce-services)的資訊。
* 如果您&#x200B;*不確定您的執行個體是否已連線*，請瀏覽至&#x200B;**系統** >服務> **Commerce服務聯結器**，並檢視[!UICONTROL Sandbox Keys]和[!UICONTROL Production Keys]區段中的公開和私人API金鑰值，以及[!UICONTROL SaaS Identifier]區段中的&#x200B;*專案*&#x200B;和&#x200B;*資料空間*&#x200B;欄位。 如果這些值存在，表示您的執行個體已連線。

>[!NOTE]
>
>所有有權使用支付服務的商戶都可以使用一個生產資料空間和兩個測試資料空間。

## 取得API認證

若要使用Commerce SaaS服務，您必須針對沙箱和生產使用執行個體的API金鑰(Commerce公開API金鑰和私密金鑰)，這些API金鑰是在[我的帳戶控制面板](https://account.magento.com/customer/account/login)中建立和管理的。 [可以為Commerce帳戶建立金鑰組](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/config/services/saas)，一個用於沙箱，一個用於生產，但一次只能使用一對金鑰組。

>[!NOTE]
>
>需要協助存取您的[!UICONTROL My Account]儀表板嗎？ 請參閱[建立Commerce帳戶](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/start/commerce-account/commerce-account-create)。

公開API金鑰一經建立，即可在您的「我的帳戶控制面板」中使用。 您可以視需要複製或刪除它。 當您為沙箱或生產環境建立公用API金鑰時，私用API金鑰會變成可見；它只能從後續的對話方塊中複製或儲存，並且之後無法存取。

指定的API金鑰組對環境中所有Commerce服務都有效，因此如果您已針對執行個體設定Commerce服務，則API金鑰組已存在於Commerce服務聯結器中。

如果您的API金鑰遺失，新的API金鑰組必須[產生](https://experienceleague.adobe.com/docs/commerce/payment-services/get-started/connect.html?lang=zh-Hant#generate-an-api-key-and-private-key)且[已套用](https://experienceleague.adobe.com/docs/commerce/payment-services/get-started/connect.html?lang=zh-Hant#configure-saas-project)至Admin中的Commerce Services Connector設定。 如果設定了錯誤的金鑰或設定中沒有金鑰，則付款服務中會顯示帳戶驗證錯誤對話方塊，通知您帳戶未驗證。

檢視使用API[&#128279;](https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/integration-services/saas#availableservices)的可用Commerce服務清單。

若要瞭解如何為沙箱或生產環境產生API金鑰，請參閱[認證](https://experienceleague.adobe.com/docs/commerce/user-guides/saas.html#apikey)。

>[!IMPORTANT]
>
>建議您不要重新產生API金鑰組&#x200B;*和*，並變更使用中生產執行個體上的SaaS識別碼和/或資料空間。 如果修改執行個體的資料，您將會遺失這些資料。

## 設定Commerce服務

相同的API金鑰可用於多個執行個體，但每個執行個體都必須有自己的[SaaS資料空間](https://experienceleague.adobe.com/docs/commerce/user-guides/saas.html#saasenv)。

>[!NOTE]
>
>商家必須使用針對MageID產生的相同金鑰來取得其付款權益。

現在您已取得認證，您可以設定SaaS專案和Saas資料空間。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]**。
1. 按一下&#x200B;**[!UICONTROL Configure Commerce Services]**。

   如果您尚未為帳戶設定Commerce Services，便會顯示此選項。

   您將被導向到「管理員」**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**>**[!UICONTROL Commerce Services Connector]**&#x200B;中的設定區域，以設定您的Commerce服務聯結器。

1. 若要設定您的Commerce服務，請依照[SaaS設定](https://experienceleague.adobe.com/docs/commerce/user-guides/integration-services/saas.html?lang=zh-Hant#saasenv)中所述的步驟進行。

   >[!INFO]
   >
   > 如需其他資訊，請參閱我們的[[!DNL Adobe Commerce] 服務聯結器](https://experienceleague.adobe.com/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector.html?lang=zh-Hant#configuration-faqs)影片。

## 端點

[!DNL Payment Services]使用[Commerce Services Connector](https://experienceleague.adobe.com/docs/commerce/user-guides/saas.html)連線至Commerce Services並部署為SaaS。 此[!DNL Commerce Services Connector]透過下列位置的端點通訊：

* 沙箱環境的`commerce-beta.adobe.io`。
* 適用於即時環境的`commerce.adobe.io for`。
