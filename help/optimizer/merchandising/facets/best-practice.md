---
title: Facet最佳作法
description: 瞭解在商店中實作Facet的最佳實務。
role: Admin, Developer
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"
source-git-commit: 3131cc27a25d1bf958071b973f1d4bf1a68be152
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---


# Facet最佳作法

篩選和Facet功能是您[!DNL Adobe Commerce Optimizer]網站的關鍵元件，其設計可讓購物者縮小搜尋結果範圍並更有效率地尋找產品，藉此提升購物者體驗。 此功能可協助購物者套用特定條件，排序種類繁多的商品，讓購物程式更快、更容易、更令人滿意。 透過實作有效率、方便購物者的篩選器和Facet，您可以協助客戶快速並有效率地找到他們需要的內容，最終提高滿意度和轉換率。

## 多面向最佳化秘訣

- 決定產品最相關且最實用的屬性，例如標題、類別、品牌、價格範圍、顏色和大小，並將它們設定為[動態Facet](type.md)。 
- 設定和排序產品屬性，這些屬性在您的目錄中均保持一致，且與您的產品高度相關，以提高相關性和篩選功能，方便購物者。
- 請確保網站上的Facet標籤容易理解且命名一致。 例如，使用「價格範圍」而非「成本」。
- 將多面數量限製為最重要的多面，以免讓購物者不知所措。 太多選項可能會導致決策疲勞。 根據預設，[!DNL Adobe Commerce Optimizer]限製為最多100個設定為Facet的屬性，以及在每個Facet中傳回30個貯體。 深入瞭解[Facet限制](../../boundaries-limits.md#catalog-views-and-policies)。 
- 允許購物者同時選取多個篩選條件來縮小結果。 例如，讓購物者同時選取「紅色」和「藍色」顏色。
- 在每個Facet選項旁顯示可用產品的數量，讓購物者瞭解可預期的搜尋結果。
- 實作可摺疊的Facet區段，保持介面整潔且易於管理，尤其是在行動裝置上。
- 允許購物者輕鬆重設個別面向或所有選取的篩選器，以開始新搜尋。
- 如果要與許多屬性競爭，請考慮將屬性合併為單一「meta-attribute」。 例如，鞋子通常有數字大小，而襯衫通常是「S/M/L/XL」大小。 這兩種大小型別可合併為單一可搜尋屬性。
