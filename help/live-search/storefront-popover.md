---
title: '[!DNL Storefront Popover]'
description: ' [!DNL Live Search storefront popover] 會動態傳回建議的產品與縮圖。'
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---

# [!DNL Storefront Popover]

當[!DNL Live Search]已[安裝](install.md)時，當購物者在[搜尋](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search.html#quick-search)方塊中鍵入時，店面中會出現[!DNL popover]。 輸入每個字元後，[!DNL popover]會以建議的產品和排名最前的搜尋結果的縮圖影像更新。

[!DNL Live Search]傳回兩個或更多字元之查詢的結果。 若為部分相符，則每個字的字元數上限為20。 「鍵入時搜尋」查詢中的字元數無法設定。

依預設，[!DNL Live Search]支援[搜尋字詞重新導向](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-terms.html)。

![[!DNL Live Search popover]](assets/storefront-search-as-you-type.png)

>[!TIP]
>
>瞭解如何在[設定即時搜尋](workspace.md)文章中將產品屬性設定為可搜尋。

## [!DNL Popover]頁大小

[!DNL popover]的頁面大小決定可以傳回多少行的自動完成產品。 在Live Search安裝期間，`page_size`值變更為[目錄搜尋](https://experienceleague.adobe.com/docs/commerce-admin/config/catalog/catalog.html) - `Autocomplete Limit`設定的目前值。

依預設，「目錄搜尋 — 自動完成限制」值會設定為八行（或數列）。 若要變更[!DNL popover]的頁面大小，請執行下列動作：

1. 在&#x200B;*管理員*&#x200B;側邊欄上，移至&#x200B;**商店** >設定> **設定**。
1. 在左側面板中，展開&#x200B;**目錄**，然後從設定清單中選擇&#x200B;**目錄**。
1. 展開&#x200B;*目錄搜尋*&#x200B;區段。
1. 將&#x200B;**自動完成限制**&#x200B;設定為您要在[!DNL popover]中允許的行數。
1. 完成時，按一下&#x200B;**儲存設定**。

## 樣式化[!DNL Popover]範例

您可以自訂[!DNL Popover] Widget的外觀與風格，以符合貴公司的風格與品牌指南。

[!DNL storefront popover]一律顯示產品`name`和`price`，且無法設定欄位選項。 不過，可以使用[CSS](https://developer.adobe.com/commerce/frontend-core/guide/css/)類別來設定[!DNL popover]元素的樣式。 例如，下列宣告會變更[!DNL popover]容器和頁尾的背景顏色。

```css
.livesearch.popover-container {
    background-color: lavender;
}

.livesearch.view-all-footer {
    background-color: magenta;
}
```

## 容器可見性

`.livesearch.popover-container`的父元件為`.search-autocomplete`。  `.active`類別表示容器的可見性。 當[!DNL popover]開啟時，`.active`類別會有條件地新增。

```css
.search-autocomplete.active   /* visible */
.search-autocomplete          /* not visible */
```

如需有關樣式化店面元素的詳細資訊，請參閱[Frontend開發人員指南](https://developer.adobe.com/commerce/frontend-core/guide/)中的[階層式樣式表(CSS)](https://developer.adobe.com/commerce/frontend-core/guide/css/)。

## 類別選取器

您可以使用下列類別選取器來設定[!DNL popover]中容器和產品元素的樣式。

- `.livesearch.popover-container`
- `.livesearch.view-all-footer`
- `.livesearch.products-container`
- `.livesearch.product-result`
- `.livesearch.product-name`
- `.livesearch.product-price`

### 容器類別選取器

#### .livesearch.pover-container

![[!DNL Popover]容器](assets/livesearch-popover-container.png)

#### .livesearch.view-all-footer

![檢視所有頁尾](assets/livesearch-view-all-footer.png)

### 產品類別選擇器

#### .livesearch.products-container

![產品容器](assets/livesearch-product-container.png)

#### .livesearch.product-result

![產品結果](assets/livesearch-product-result.png)

#### .livesearch.product-name

![產品名稱](assets/livesearch-product-name.png)

#### .livesearch.product-price

![產品價格](assets/livesearch-product-price.png)

#### .livesearch product-link

![產品結果](assets/livesearch-product-link.png)

## 使用修改的主題 {#working-with-modified-theme}

您可以使用自訂[佈景主題](https://developer.adobe.com/commerce/frontend-core/guide/themes/)的[!DNL storefront popover]，該佈景主題會繼承&#x200B;*Luma*&#x200B;的所需檔案。 不得修改`Magento_Search`模組之`header-wrapper`中的`top.search`區塊。

```html
<referenceContainer name="header-wrapper">
   <block class="Magento\Framework\View\Element\Template" name="top.search" as="topSearch" template="Magento_Search::form.mini.phtml">
      <arguments>
         <argument name="configProvider" xsi:type="object">Magento\Search\ViewModel\ConfigProvider</argument>
      </arguments>
   </block>
</referenceContainer>
```

## 正在停用[!DNL popover]

若要停用[!DNL popover]並還原標準[快速搜尋](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search.html#quick-search)功能，請輸入下列命令：

```bash
bin/magento module:disable Magento_LiveSearchStorefrontPopover
```

## Headless實施

對於具有Headless實作的使用者，您可以使用[npm套件](https://www.npmjs.com/package/@magento/ds-livesearch-storefront-utils)來安裝[!DNL Live Search popover]。
