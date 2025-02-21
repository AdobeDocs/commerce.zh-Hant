---
title: 管理Facet
description: 瞭解如何管理現有的 [!DNL Live Search] 多面向。
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# 管理Facet

請依照這些指示更新現有Facet的屬性，或在店面中變更其簡報。

## 設定價格面向群組

請參閱[設定](settings.md)以設定價格多面向間隔與群組。

## 編輯Facet

1. 尋找您要編輯的Facet。
1. 如果清單中有許多Facet，請將&#x200B;*篩選依據*&#x200B;設定為下列其中一項：

   * 已固定
   * 動態

   若要深入瞭解，請前往[Facet型別](facets-type.md)。

   ![篩選Facet](assets/facets-filter-by-cropped.png)

1. 若要編輯Facet屬性，請按一下&#x200B;**更多** (...)選項。
1. 按一下&#x200B;**編輯**

   ![編輯選項](assets/facet-edit-menu.png)

1. 若要編輯多面標籤，請執行下列任一項作業：

   * 針對[!DNL Commerce]店面，編輯[屬性標籤](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html)。
   * 對於Headless實作，請按一下第一欄中的值，然後視需要編輯文字。

   ![編輯標籤](assets/facet-edit-label.png)

1. （僅限Headless）若要變更用於排序Facet值的方法，請按一下&#x200B;*排序型別*&#x200B;欄中的值，然後選擇下列其中一項：

   * 字母順序
   * 計數

   ![編輯計數](assets/facets-edit-count.png)

1. 在&#x200B;**最大值**&#x200B;欄中，設定要顯示在店面中的Facet篩選值數目上限（從0到10）。
1. 完成時，按一下&#x200B;**儲存**。

   您的變更要等到發佈後才顯示在店面上。

## 釘選/取消釘選面向

圖釘在按一下時會變更顏色，可用來將多面向移動至&#x200B;*釘選多面向*&#x200B;或&#x200B;*動態多面向*&#x200B;區段。

1. 若要將Facet釘選到&#x200B;*篩選器*&#x200B;清單的頂端，請在&#x200B;*動態Facet*&#x200B;清單中尋找Facet，然後按一下灰色圖釘（![釘選器](assets/btn-pin-gray.png)）。

   圖釘會變成藍色，而Facet會移至&#x200B;*釘住Facet*&#x200B;區段。

1. 若要取消釘選Facet，請在&#x200B;*釘選Facet*&#x200B;清單中尋找Facet，然後按一下藍色圖釘（![釘選器](assets/btn-pin-blue.png)）。

   圖釘會變成灰色，而多面會移至&#x200B;*動態Facet*&#x200B;區段。

   ![釘選與動態Facet](assets/facets-pinned-unpinned.png)

>[!NOTE]
>
>如果有兩個標籤具有相同名稱，則釘選Facet排序可能會不一致。

## 移動釘選Facet

>[!NOTE]
>
>釘選Facet的排序僅在Headless實施中受支援。 如果需要排序的Facet，請使用[!DNL Live Search] PLP Widget。

將列移至不同位置可變更釘選多面的順序。 釘選的多面資料列開頭有&#x200B;*移動*&#x200B;圖示（![移動選取器](assets/btn-move.png)）。 與釘選多面不同，動態Facet無法移動。

1. 在清單的&#x200B;*釘選Facet*&#x200B;區段中尋找Facet。
1. 使用&#x200B;**移動** （![移動選取器](assets/btn-move.png)）圖示，將資料列拖曳至&#x200B;*釘選Facet*&#x200B;區段中的新位置。

   發佈變更後，重新排序的多面會出現在店面&#x200B;*篩選器*&#x200B;清單中。

## 刪除Facet

1. 在清單中尋找Facet，然後按一下&#x200B;**更多** (...)選項。
1. 按一下&#x200B;**刪除**。
1. 提示確認時，按一下&#x200B;**刪除Facet**。
多面在變更發佈後會從店面中移除。

## 發佈變更

1. 若要以您的變更更新店面，請按一下&#x200B;**發佈變更**。
1. 請等候約15分鐘，讓更新出現在您的商店中。
