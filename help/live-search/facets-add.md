---
title: 新增Facet
description: 瞭解如何將可篩選的產品屬性新增為 [!DNL Live Search] Facet。
exl-id: 80559107-2b2d-411f-8c32-99ff024e7a09
source-git-commit: 053533bc5f3f990ce8219f1e0c7c4930b28f0cd5
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# 新增Facet

任何可篩選的產品屬性都可以當作Facet使用。 *新增Facet*&#x200B;面板會列出目前的Facet，並可讓您輕鬆指派其他產品屬性作為Facet。 在這三個步驟的流程中，選擇屬性作為多面，視需要編輯屬性，並將變更發佈到店面。

![新增Facet](assets/facets-add.png)

## 步驟1：新增多面向

1. 在Admin中，前往&#x200B;**行銷** > SEO與搜尋> **[!DNL Live Search]**。
1. 在&#x200B;*多面向*&#x200B;索引標籤上，按一下&#x200B;**新增Facet**。
1. 在&#x200B;*新增Facet*&#x200B;清單中，每個可用屬性都有個別的![新增按鈕](assets/btn-add.png)。 完成下列任一項作業：

   * 在&#x200B;*Faceting屬性*&#x200B;清單中，選擇您要用作Facet的產品屬性，然後按一下&#x200B;**新增**。
   * 若要尋找特定的產品屬性，請在&#x200B;*搜尋*&#x200B;方塊中輸入屬性名稱的前幾個字元。 然後，按一下&#x200B;**新增**。

     若要設定價格多面向間隔與群組，請參閱[設定](settings.md)。 若要深入瞭解，請前往[Facet型別](facets-type.md)。
Facet已新增至*動態Facet*&#x200B;清單底部，且&#x200B;*發佈變更*&#x200B;按鈕可供使用。

1. 如果找不到您要新增的Facet，請移至&#x200B;**商店** >屬性> **產品**，並確認屬性具有[要當作Facet使用的必要屬性](facets.md)。 如有必要，請更新屬性的下列店面屬性：

   * 用於搜尋 — `No`
   * 用於搜尋結果階層式導覽 — `Yes`
   * 用於分層導覽 — `Filterable (with results)`

1. 出現提示時，請重新整理快取。

   下次目錄與[!DNL Live Search]同步時，Facet便可在店面中使用。 如果兩小時後無法使用Facet，請參閱[同步目錄資料](install.md#synchronize-catalog-data)。

## 步驟2：編輯Facet屬性（選用）

1. 若要編輯Facet屬性，請按一下最右邊欄中的&#x200B;**更多** （![更多選取器](assets/btn-more.png)）選項。
1. 在功能表上，按一下&#x200B;**編輯**。 接著，視需要調整下列屬性。

   * 標籤 — （僅限[Headless](facets-type.md)）輸入您要使用的Facet標籤。
   * 排序型別 — Facet會依字母順序排序所有[!DNL Commerce]個店面。 針對Headless實作，Facet可依字母順序或計數排序。 選項：字母順序、計數（僅限Headless）
   * 最大值 — 輸入店面中顯示的多面值數目上限。 有效專案： 0 - 100；預設： 8

1. 完成時，按一下&#x200B;**儲存**。

   ![編輯Facet](assets/facet-edit.png)

1. 若要將Facet釘選到&#x200B;*篩選器*&#x200B;清單的頂端，請按一下灰色圖釘（![釘選器](assets/btn-pin-gray.png)）。
1. 若要變更釘選Facet的順序，請按一下&#x200B;**移動** （![移動選取器](assets/btn-move.png)）圖示，並將列拖曳至&#x200B;*釘選Facet*&#x200B;區段中的新位置。

## 步驟3：發佈變更

1. 當Facet完成時，按一下&#x200B;**發佈變更**。
1. 等候多面向出現在存放區中。
如果兩小時後無法使用Facet，請參閱安裝指示中的[驗證匯出](install.md#synchronize-catalog-data)。

## 欄位說明

| 欄位 | 說明 |
|--- |--- |
| 標籤 | （僅限[Headless](facets-type.md)）可編輯店面中顯示的[Facet標籤](facets-type.md)，使其與您的品牌保持一致。 |
| 排序型別 | 用於[排序](facets-type.md)多面向的方法。 所有[!DNL Commerce]店面僅依字母順序排序Facet。 Headless實作也可以依`Count`排序。 選項：<br />依字母順序 — 依字母順序排序多面向。<br />計數 — （僅限Headless）根據找到的相符數來排序Facet。 |
| 最大值 | 可在店面中針對每個多面顯示的最大值數量。 代表值範圍的多面會平均分佈。 有效專案： 0 - 100；預設： 8 |

### 控制項

| 控制 | 說明 |
|--- |--- |
| ![釘選器](assets/btn-pin-blue.png) | 將Facet釘選或取消釘選到&#x200B;*篩選器*&#x200B;清單的頂端。 |
| ![更多選擇器](assets/btn-more.png) | 顯示可套用至所選Facet的其他動作功能表。 選項：編輯、刪除 |
| ![移動選擇器](assets/btn-move.png) | 使用「*移動*」圖示將釘選Facet拖曳至&#x200B;*釘選Facet*&#x200B;區段中的其他位置。 |
