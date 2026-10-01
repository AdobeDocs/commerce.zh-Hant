---
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 27%
---

# 移除衝突的擴充功能

如果您已安裝下列任何擴充功能，請在安裝[!DNL Adobe Commerce Optimizer Connector for B2B]之前解除安裝它們：

* [!DNL Adobe Commerce Live Search] (`magento/live-search`)
* [!DNL Adobe Commerce Product Recommendations] (`magento/product-recommendations`)
* [!DNL Adobe Commerce Catalog Service] (`magento/catalog-service`, `magento/catalog-service-installer`)
* **[!UICONTROL Data Management Dashboard]** (`magento-catalog-sync-admin`)

與這些擴充功能相關聯的資料仍可在Commerce資料庫中使用。 但是，當聯結器啟用時，它不會匯出到[!DNL Commerce Optimizer]。 若要在啟用聯結器後實作這些擴充功能提供的Adobe Commerce搜尋和銷售功能，請從[[!DNL Commerce Optimizer] 管理UI](https://experienceleague.adobe.com/en/docs/commerce/optimizer/overview#quick-tour)進行設定。

>[!IMPORTANT]
>
>若在啟用聯結器之前未移除這些擴充功能，會導致設定畫面損毀、[!DNL Commerce Optimizer]中的資料重複，以及401或403驗證錯誤。