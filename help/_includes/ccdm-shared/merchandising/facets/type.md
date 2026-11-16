---
source-git-commit: 4032a0871d0a9b129ad870c93f62a2a7596ea8b7
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%
---
<!--
SOURCE OF TRUTH: Edit this file in the commerce.en repo:
https://github.com/Adobe-Enterprise-Docs/commerce.en/blob/main/help/_includes/ccdm-shared/merchandising/facets/type.md

This content is shared by the Adobe Commerce Optimizer Guide (commerce.en) and the
Merchandising Services with CCDM Guide (commerce-admin.en). Changes made in commerce.en
are synced automatically to commerce-admin.en, so do not edit the copy in that repo.
This includes related images in help/assets/ccdm-shared/.
-->

# 多面向型別

Facet有多種型別，只有在相關時才會出現在&#x200B;*篩選器*&#x200B;清單中。 可用Facet清單會根據傳回的產品而變更。 下列特性會影響其顯示和行為：

- 釘選多面 — 最常用的多面可釘選到清單頂端。 其餘的Facet會在釘選Facet之後以&#x200B;*排序型別*&#x200B;順序列出。
- 動態Facet - [Adobe AI](https://business.adobe.com/ai.html)找到與產品集和查詢最相關的產品屬性。 計算會考量整個目錄的屬性中繼資料，並在查詢時決定與查詢最相關的Facet。
- 價格Facet — 依價格範圍傳回產品。 您可以在&#x200B;[*設定*](https://experienceleague.adobe.com/en/docs/commerce/optimizer/settings)工作區上指定選取專案的數目和價格範圍間隔。

## Facet標籤

您可以從[多面向工作區](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/facets/workspace)編輯多面向標籤。

## 排序型別

為店面演算的所有多面都會依字母順序或計數排序。

| 排序型別 | 說明 |
|--- |--- |
| 字母 | 在店面&#x200B;*篩選器*&#x200B;清單中，Facet是以字母順序排序。 |
| 計數 | Facet也可以依照目前傳回產品集合中每個Facet的值數量排序。 |
