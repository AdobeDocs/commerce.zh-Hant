---
title: 空隙
description: 「作廢」可讓您從信用卡或借記卡帳戶中釋放資金，這些帳戶因授權而被封鎖或保留，以支付購買金額。
feature: Payments, Checkout
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# 空隙

透過[!DNL Payment Services]，您可以使用現有的Commerce功能來作廢交易。 「作廢」可讓您從信用卡或借記卡帳戶中釋放資金，這些帳戶因授權而被封鎖或保留，以支付購買金額。

>[!NOTE]
>
>只有在尚未抓取付款時，您才能作廢交易。

如果您的商店設定為[設定](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"}，以便在銷售點僅授權（非擷取）資金，則從您的商店購買會導致訂單在Commerce管理中具有`Processing`狀態。

您也可以[取消未開立商業發票的訂單](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/stores-sales/point-of-purchase/assist/customer-account-create-order){target="_blank"}。 在該取消程式中，任何未擷取的授權也會失效。

>[!NOTE]
>
>取消訂單也會產生作廢，但作廢訂單不會觸發取消。

若要進一步瞭解訂單所執行的基本步驟，請參閱核心使用手冊中的[訂單工作流程](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/stores-sales/order-management/orders/order-processing){target="_blank"}主題。

若要瞭解void功能以及如何使訂單交易失效，請參閱核心使用手冊中的[處理訂單](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/stores-sales/order-management/orders/order-processing#process-an-order){target="_blank"}。
