---
title: 退款
description: 在管理系統中建立 [!DNL Payment Services] 訂單的退款，作為銷退折讓單處理的一部分。
feature: Payments, Checkout
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# 退款

[!DNL Payment Services]訂單的退款是在管理程式中建立的，作為銷退折讓單處理的一部分。 銷退折讓單是一份檔案，顯示全部或部分退款應付給客戶的金額，可用於採購或直接退款給客戶。 只能針對[已開立商業發票](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice){target="_blank"}的訂單發出銷退折讓單。

請參閱我們的核心使用手冊中的[銷退折讓單](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memos){target="_blank"}，以取得詳細資訊，並瞭解如何簽發及列印銷退折讓單。

對於使用PayPal或信用卡處理的訂單，您可以：

* 退回訂單的全部金額
* 退款訂單的部分金額（或多個部分金額）
* 退回小於特定訂單料號值的金額

如需詳細資訊，請參閱我們的核心使用手冊中的[簽發銷退折讓單](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memo-create){target="_blank"}。

>[!NOTE]
>
>如果您嘗試對超過剩餘訂單金額（原始金額減去現有退款總額）的訂單進行部份退款，或您核發的退款金額大於全部訂單金額，PayPal或信用卡處理的訂單就會發生錯誤。

您[!UICONTROL Payment Settings]組態中的[!UICONTROL Payment Action]設定（可能是`Authorize`或`Authorize and Capture`）決定訂單的[基本退款工作流程](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memos#refund-workflow){target="_blank"}。

如需詳細資訊，請參閱&#x200B;_發出銷退折讓單_&#x200B;的[付款動作設定區段](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memo-create#payment-action-setting){target="_blank"}。
