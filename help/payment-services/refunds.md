---
title: 退款
description: 在管理系統中建立[!DNL Payment Services]訂單的退款，作為銷退折讓單處理的一部分。
exl-id: 2b3721a1-9c9d-4e3f-ab7d-5bd61573dcb4
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
source-wordcount: '305'
ht-degree: 0%
---
# 退款

[!DNL Payment Services]訂單的退款是在管理程式中建立的，作為銷退折讓單處理的一部分。 銷退折讓單是一份檔案，顯示全部或部分退款應付給客戶的金額，可用於採購或直接退款給客戶。 只能針對[已開立商業發票](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice){target="_blank"}的訂單發出銷退折讓單。

請參閱我們的核心使用手冊中的[銷退折讓單](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memos){target="_blank"}，以取得詳細資訊，並瞭解如何簽發及列印銷退折讓單。

對於使用PayPal或信用卡處理的訂單，您可以：

* 退回訂單的全部金額
* 退款訂單的部分金額（或多個部分金額）
* 退回小於特定訂單料號值的金額

如需詳細資訊，請參閱我們的核心使用手冊中的[簽發銷退折讓單](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memo-create){target="_blank"}。

>[!NOTE]
>
>如果您嘗試對超過剩餘訂單金額（原始金額減去現有退款總額）的訂單進行部份退款，或您核發的退款金額大於全部訂單金額，PayPal或信用卡處理的訂單就會發生錯誤。

您[!UICONTROL Payment Settings]組態中的[!UICONTROL Payment Action]設定（是`Authorize`或`Authorize and Capture`）決定訂單的[基本退款工作流程](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memos#refund-workflow){target="_blank"}。

如需詳細資訊，請參閱&#x200B;_簽發銷退折讓單_&#x200B;的[付款動作設定區段](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memo-create#payment-action-setting){target="_blank"}。
