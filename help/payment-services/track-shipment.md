---
title: 正在追蹤您在 [!DNL Payment Services]中的出貨
description: 自訂Paypal商家儀表板中顯示的 [!DNL Payment Services] 出貨與追蹤資訊。
feature: Payments, Paas, Saas
exl-id: 17aede1f-56ae-441a-b723-3193e865e469
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# 在[!DNL Payment Services]中追蹤您的出貨

[!DNL Payment Services]可讓商家在其PayPal商家儀表板中檢視運送的追蹤資訊。

請參閱[出貨](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/stores-sales/order-management/shipments){target=_blank}主題，以取得有關Adobe Commerce出貨格線的詳細資訊。

## 追蹤您運送的運作方式

此功能取決於是否已對訂單開立商業發票，因為PayPal必須接收`capture_id`以處理追蹤資訊。 如果商家在擷取前寄出其產品，則不會將追蹤資訊傳送給PayPal。

>[!NOTE]
>
> 建議為每個追蹤編號建立一個出貨，將正確的料號與出貨相關聯。

## 新增追蹤編號

下列指示將引導您逐步完成在Adobe Commerce中建立具有[!DNL Payment Services]之出貨的程式：

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Orders]**。

1. 在選取順序的&#x200B;**[!UICONTROL Action]**&#x200B;欄中，按一下&#x200B;**[!UICONTROL View]**。

1. 按一下&#x200B;**[!UICONTROL Ship]**。

1. 向下捲動至&#x200B;**[!UICONTROL Payment & Shipping Method]**&#x200B;區塊，然後按一下&#x200B;**[!UICONTROL Shipping Information]**&#x200B;中的&#x200B;**[!UICONTROL Add Tracking Number]**。

1. 設定&#x200B;**[!UICONTROL Carrier]**。

1. 若要追蹤出貨，請輸入&#x200B;**[!UICONTROL Title]**&#x200B;和&#x200B;**[!UICONTROL Number]** 。

1. 按一下&#x200B;**[!UICONTROL Submit Shipment]**。

>[!NOTE]
>
> 或者，您可以使用送貨模組來輸入追蹤號碼資訊。 確定送貨模組在`tracking_number`欄位中儲存追蹤號碼資訊。

### 與協力廠商的相容性

任何協力廠商擴充功能與透過[Commerce API](https://developer.adobe.com/commerce/webapi/rest/attributes/#ShipmentRepositoryInterface){target=_blank}建立出貨實體時的功能相容。
