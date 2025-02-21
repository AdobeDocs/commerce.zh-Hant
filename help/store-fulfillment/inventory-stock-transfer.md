---
title: Inventory management Source傳輸
description: 使用Adobe Commerce Inventory management設定 [!DNL Store Fulfillment solution] 的庫存。 設定新存貨並將存貨移出預設存貨，以便您可以將其指定給設定為啟用「商店履行」解決方案所需的「商店提貨」功能的來源。
role: Admin
level: Intermediate
feature: Shipping/Delivery, Inventory, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# Inventory management Source傳輸

[!DNL Store Fulfillment]解決方案使用原生Adobe Commerce Inventory management。 根據預設，[!DNL Commerce]設定會將所有網頁詳細目錄指派給預設存貨，此預設存貨不能有其他指派的來源。 由於網站只能指定單一存貨，因此商家必須設定新存貨，並選擇性地將其預設來源存貨轉移至指定至適當範圍的來源。 然後，可將來源指派給新庫存。

>[!IMPORTANT]
>
>商家必須維護群組及套件產品型別中包含之所有產品的預設來源。 這些產品需要存貨數量符合庫存料號的最低數量臨界值，並包含[!UICONTROL In Stock]的庫存狀態。

這些設定變更可協助您完成下列三件事：

1. [將存貨移轉到來源](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/quantities/inventory-transfer)，以將存貨從預設存貨/來源移轉到新存貨/來源。

1. [大量指派來源](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/quantities/bulk-assignment)以新增您所有產品的新來源。

1. [完成產品屬性的大量更新](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/bulk-product-attribute-update)以將`Allow Store Pickup`和`Allow Home Delivery`屬性新增到現有產品。 安裝方案時，屬性具有最佳的&#x200B;*預設*&#x200B;值。 不過，在您完成大量更新內容程式之前，這些屬性不會套用至現有產品。

存貨是從選取的來源（零售商店地點或電子商務倉儲）中扣除。 用作電子商務倉儲的來源必須指派給與商店取貨地點相同的存貨，並在零售地點之前排定優先順序。 如需詳細資訊，請參閱[排定股票來源的優先順序](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/stocks/stocks-prioritize-sources)。

如需管理存貨、庫存和來源的詳細資訊，請參閱Adobe Commerce使用者檔案：

- [管理詳細目錄](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction)

- [管理存貨數量](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/quantities/quantities-manage)

- [管理庫存](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/stocks/stocks-manage)

- [管理來源](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/sources/sources-manage)

- [優先順序化Stock的來源](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/stocks/stocks-prioritize-sources)

- 產品屬性的[大量更新](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/bulk-product-attribute-update)


>[!IMPORTANT]
>
>變更存貨與存貨來源的設定，也會對整合的系統造成下游影響。 確保您瞭解庫存組態的變更如何影響這些系統。
