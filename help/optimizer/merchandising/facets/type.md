---
title: Facet型別
description: 瞭解 [!DNL Adobe Commerce Optimizer]中不同型別的面向。
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"
exl-id: f4ab1f27-b393-45e0-94bf-c77d46e3f994
source-git-commit: 458f34c45406db871ec61ff408aa624f163b6ee0
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# 多面向型別

[!DNL Adobe Commerce Optimizer]使用各種Facet型別，只有在相關時才會出現在&#x200B;*篩選器*&#x200B;清單中。 可用Facet清單會根據傳回的產品而變更。 下列特性會影響其顯示和行為：

- 釘選Facet — 最常用的Facet可以釘選到清單頂端。 其餘的Facet會在釘選Facet之後以&#x200B;*排序型別*&#x200B;順序列出。
- 動態Facet - [Adobe AI](https://business.adobe.com/tw/ai.html)找到與產品集和查詢最相關的產品屬性。 計算會考量整個目錄的屬性中繼資料，並在查詢時決定與查詢最相關的Facet。
- 價格Facet — 依價格範圍傳回產品。 您可以在&#x200B;[*設定*](../../settings.md)&#x200B;工作區中指定選取專案的數目和價格範圍間隔。

## Facet標籤

您可以從[多面向工作區](workspace.md)編輯多面向標籤。

## 排序型別

為店面演算的所有多面都會依字母順序或計數排序。

| 排序型別 | 說明 |
|--- |--- |
| 字母 | 在店面&#x200B;*篩選器*&#x200B;清單中，Facet是以字母順序排序。 |
| 計數 | Facet也可以依照目前傳回產品集合中每個Facet的值數量排序。 |
