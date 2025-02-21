---
title: 邊界和限制
description: 瞭解 [!DNL Live Search] 的界限和限制，以確保其符合您的業務需求。
role: Admin, Developer
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 0%

---

# 邊界和限制

在網站搜尋方面，Adobe Commerce會提供您選項。 請檢閱下列界限和限制，以確保[!DNL Live Search]和[!DNL Catalog Service]符合您的業務需求。 如果您需要進階搜尋功能，例如內容搜尋、自備演演算法(BYOA)或屬性型銷售，請考慮使用協力廠商搜尋解決方案。

## 一般

- 安裝[!DNL Live Search]時，[進階搜尋](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search)模組已停用，且店面頁尾中的進階搜尋連結已移除。
- [層級定價](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-tier)在[!DNL Live Search]欄位和產品清單頁面Widget中不受支援。
- 產品價格不含增值稅(VAT)。
- 不支援內容搜尋(CMS頁面和區塊)。
- 可分頁的產品上限為10,000件。 雖然此限制可以增加，但會影響效能。 若類別或搜尋結果中有大量產品，請務必提供有意義的產品篩選方式，讓購物者不必使用深層分頁。
- 每個屬性有1MB的硬性限制，包括說明和自訂屬性。
- 搜尋配接卡不支援使用自訂來源模型建立並當作Facet使用的產品屬性。 若要支援此功能，您必須使用[產品清單頁面Widget](plp-styling.md)。
- 不支援自訂產品型別。
- 不支援以`"is_user_defined": false`程式化建立的自訂屬性。
- 您可以使用「開頭為」或「包含」條件篩選結果，但有一些限制，如[此處](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#limitations)所述。
- 您只能追蹤去年內的績效量度。

## 索引

- [!DNL Live Search] [索引](indexing.md)每個商店檢視最多總共450個產品屬性。 其分佈如下：
   - 50個可排序屬性
   - 200個可篩選屬性
   - 200個可搜尋屬性
- [!DNL Live Search]只會索引Adobe Commerce資料庫中的產品。
- CMS頁面不會編制索引。
- SKU、名稱和類別屬性預設可搜尋，且無法從搜尋中排除。 如果您不打算將產品歸入這些類別，請務必從這些類別中取消指派產品。

## Facet

- 最多可以將100個屬性設定為Facet，這些屬性來自可以編制索引的200個可篩選屬性。
- 在一個Facet中，最多可傳回100個值區。 如果您需要傳回100個以上的貯體，請[建立支援票證](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide)，讓Adobe能夠分析效能影響，並判斷為您的環境提高此限制是否可行。
- 動態Facet可能會在大型索引和高序數的索引中造成效能問題。 如果您已建立動態Facet，且發現任何效能降低或頁面未載入時發生逾時錯誤，請嘗試將您的Facet變更為Pined ，以判斷這是否會解決您的效能問題。
- Stock狀態(`quantity_and_stock_status`)不支援為Facet。 您可以使用`inStock: 'true'`來篩選無庫存的產品。 當[!DNL Commerce]管理員中的「顯示無庫存產品」設為「True」時，`LiveSearchAdapter`模組可立即支援此功能。
- 日期型別屬性不支援為Facet。
- 將屬性新增為Facet後，對該屬性中繼資料所做的任何變更都不會反映在Facet中。

## 查詢

- [!DNL Live Search]使用唯一的[GraphQL端點](https://developer.adobe.com/commerce/services/graphql/live-search/)進行查詢，以支援dynamic faceting和search-as-you-type等功能。 雖然與[GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/)類似，但有一些差異且部分欄位可能並不完全相容。
- 搜尋查詢中可傳回的結果數量上限為10,000。
- 每頁的結果數量上限為500。
- 無法使用日期型別屬性來篩選結果。

## 規則

- 每個存放區檢視的搜尋銷售[規則](rules.md)最大數量為50。
- 類別銷售在每個類別中可以有一個規則。
- 每個規則的條件數上限為10。
- 每個規則的事件數上限為25。
- 為了避免分頁回應產生無法預測的結果，釘選產品的數量不應超過要求的頁面大小。

## 同義字

- 每個存放區檢視最多可管理200個[同義字](synonyms.md)。[!DNL Live Search]
- 多字同義字可能無法總是如預期般運作。 請務必先在中繼環境中測試這些同義字，之後再用於生產環境，因為它們可能會對關聯性造成負面影響。

## 類別銷售

- 可以為每個商店檢視為每個類別建立一個規則。 每個規則可以具有：
   - 最多10個條件
   - 最多25個事件

## B2B和類別許可權

- 產品若未新增至預設共用目錄，則不會顯示。
- 若要使用[類別許可權](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/category-permissions)限制客戶群組：
   - 必須將產品指派給根類別。
   - 必須向「未登入」客戶群組提供「允許」瀏覽許可權。
   - 若要將產品限制在「未登入」客戶群組，請移至每個類別，並為每個[客戶群組](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared-manage)設定許可權。
- 目前不支援在PWA Studio上透過PLP Widget提供B2B的現成支援。 不過，您可以[使用API](install.md#pwa-support)來實作此功能。
- [!DNL Live Search]中的類別Facet可能會顯示無法顯示給特定[客戶群組](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared-manage)的類別。
- [!DNL Live Search]最多可支援1,000個客戶群組。

## [!DNL Storefront popover]

- [[!DNL popover]](storefront-popover.md)僅適用於使用&#x200B;*Luma*&#x200B;佈景主題或以&#x200B;*Luma*&#x200B;為基礎的自訂佈景主題之存放區。 搜尋結果頁面上的階層連結不會有&#x200B;*Luma*&#x200B;樣式。
- [!DNL popover]不支援&#x200B;*空白*&#x200B;主題。
- 快速訂購表單不支援[!DNL popover]。
- 不支援願望清單和產品比較。
- 不支援秘魯索爾(PEN)的貨幣符號。

## 疑難排解

如需疑難排解[!DNL Live Search]中某些常見問題的協助，請參閱下列知識庫文章：

- [[!DNL Live Search] 目錄未同步](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-catalog-data-sync)
- [[!DNL Live Search] 儀表板和搜尋結果排名不正確](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-dashboard-ranking-incorrect)
- 無論Admin](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-displays-out-of-stock-products)中的庫存狀態設定為何，[[!DNL Live Search] 都會顯示無庫存的產品
- [[!DNL Live Search] Facet未依字母順序排序](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-facets-not-sorted)

如果您需要其他協助，請連絡[支援](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide)。
