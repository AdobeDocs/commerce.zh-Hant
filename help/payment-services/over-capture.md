---
title: 過度擷取
description: 瞭解過度擷取支付服務擴充功能的需求和設定。
role: Admin, User
level: Intermediate
feature: Payments, Paas
source-git-commit: d2bcc58f34af50f26d4a4f082e5b3fc30089ab58
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%
---
# 過度擷取

超額擷取可讓具有PayPal超額擷取合約的合格商戶，在開立訂單發票時，擷取超過原始授權金額的金額。 例如，最終金額可能會因重量調整或授權與履行之間原物料成本的變更而增加。

PayPal會決定每個商家帳戶的過度擷取限制。 在[!DNL Payment Services]中啟用過度擷取不會建立合約或增加PayPal核准的限制。

>[!NOTE]
>
>本主題說明[!DNL Payment Services]擴充功能中的過度擷取。 若為[!DNL Adobe Commerce as a Cloud Service]，請參閱[自訂擷取金額](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#custom-capture-amounts)，以取得個別的可用性與啟用需求。

## 先決條件

啟用過度擷取之前：

* 過度擷取僅適用於[!DNL Payment Services] 2.17.0或更新版本。
* 過度擷取僅適用於美國企業。 PayPal的[過度擷取需求(PSD2)](https://www.paypal.com/us/cshelp/article/overcapture-requirements-psd2-help954)也適用於在歐洲經濟區(EEA)向PayPal買家銷售的美國商家。
* 過度擷取不適用於替代付款方法(APM)。
* 請向PayPal取得過度擷取合約，並向PayPal客戶經理確認已為您的商家帳戶核准的限制。
* 將付款方法的&#x200B;**[!UICONTROL Payment Action]**&#x200B;設定為`Authorize`。 超量擷取會套用至稍後在開立商業發票時擷取的授權訂單，而非套用至`Authorize and Capture`自動擷取的訂單。 檢視[設定 [!DNL Payment Services] 為付款方式](production.md#set-payment-services-as-payment-method)。

## 啟用過度擷取

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在左側面板中，展開&#x200B;**[!UICONTROL Sales]**&#x200B;並選擇&#x200B;**[!UICONTROL Payment Methods]**。
1. 使用商店範圍選擇器選取要設定的網站。
1. 展開&#x200B;_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_區段。
1. 在&#x200B;_[!UICONTROL Payment Services]_區段中，展開_[!UICONTROL General Configuration]_&#x200B;區段。
1. 將&#x200B;**[!UICONTROL Over Capture Enabled]**&#x200B;設為`Yes`。
1. 按一下&#x200B;**[!UICONTROL Save Config]**&#x200B;以儲存變更。
1. 導覽至&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**，然後按一下&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以重新整理所有無效的快取。

## 擷取授權付款

在管理員開立發票期間會發生過度擷取。 要求的擷取金額必須在PayPal針對您的商家帳戶核准的限制內。 請參閱[針對標準開立發票工作流程建立發票](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice)。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Orders]**。
1. 開啟尚未擷取的授權付款訂單。
1. 按一下&#x200B;**[!UICONTROL Invoice]**。
1. 在自訂擷取數量欄位中，輸入要擷取的總量。 例如，如果授權金額是USD 100，而同意的最終費用是USD 110，請輸入`110`，而不是`10`。 要求的金額必須在您的PayPal核准限制內。
1. 選取透過付款提供者要求付款的商業發票線上擷取。
1. 檢閱發票並按一下&#x200B;**[!UICONTROL Submit Invoice]**。

### 使用發票API擷取

使用標準[建立發票](https://developer.adobe.com/commerce/webapi/rest/tutorials/orders/order-create-invoice)端點：

```http
POST /rest/<store_code>/V1/order/<orderId>/invoice
```

使用訂單的商店代碼和訂單的內部ID。 使用授權的管理員或整合權杖進行驗證，並設定`Content-Type: application/json`。

下列範例裝載要求完整發票，並透過線上擷取USD 110，以取得授權USD 100的訂單，前提是商家的PayPal合約允許該金額：

```json
{
  "capture": true,
  "notify": false,
  "arguments": {
    "extension_attributes": {
      "custom_capture_amount": 110
    }
  }
}
```

在此範例中：

1. `capture`個要求線上擷取。
1. `notify`控制Commerce是否傳送發票通知電子郵件。
1. `custom_capture_amount`是要擷取的最終數量，而不是超過授權數量的增加。

## 疑難排解拒絕的擷取

如果PayPal拒絕過度擷取要求：

* 確認用於付款的PayPal商家帳戶有有效的超額擷取協定。
* 檢查要求的金額是否在核准的限制內。 如果超過限制，請要求降低金額，或聯絡您的PayPal客戶經理以討論提高金額。
