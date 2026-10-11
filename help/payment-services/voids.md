---
title: 空隙
description: 「作廢」可讓您從信用卡或借記卡帳戶中釋放資金，這些帳戶因授權而被封鎖或保留，以支付購買金額。
exl-id: 029a7038-2812-46ce-b188-929a7a758d89
feature: Payments, Checkout, Paas, Saas
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%
---
# 空隙

[!DNL Payment Services]支援Commerce現有的作廢交易功能。 作廢會解除由採購金額授權所持有之信用卡或借記卡帳戶中的資金。 只有在尚未抓取付款時，才能使交易失效。

* 如果您的商店[已設定](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"}在銷售點僅授權（非擷取）資金，則在商店購買會導致訂單在Commerce管理中具有`Processing`狀態。

* 您也可以[取消未開立商業發票的訂單](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/assist/customer-account-create-order){target="_blank"}。 在該取消程式中，任何未擷取的授權也會失效。

>[!NOTE]
>
>取消訂單也會產生作廢，但作廢訂單不會觸發取消。

若要進一步瞭解訂單所執行的基本步驟，請參閱核心使用手冊中的[訂單工作流程](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing){target="_blank"}主題。

若要瞭解作廢功能以及如何作廢訂單交易，請參閱核心使用手冊中的[處理訂單](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#process-an-order){target="_blank"}。
