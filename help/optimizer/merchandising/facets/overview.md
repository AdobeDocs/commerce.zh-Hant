---
title: Facet概述
description: 瞭解 [!DNL Adobe Commerce Optimizer] 中的Facet及其如何改善搜尋結果。
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"
exl-id: cf16626e-8f85-47ca-b973-891b16c31fe3
source-git-commit: b786a8675625dc969b9542b4b4f716de5342c1af
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 0%

---

# Facet

Facet是一種高效能篩選方法，使用多個屬性值的維度做為搜尋條件。

![篩選的搜尋結果](../../assets/storefront-search-results-run.png)

在一個Facet中，購物者可以選取多個選項，例如「樣式」下的「基本」和「緊貼」，而搜尋結果會更新以僅顯示這些樣式。 同樣地，如果購物者選取Facet間的選項，例如「樣式」下的「基本」和「氣候」下的「室內」，搜尋結果會更新以顯示所選樣式和所選氣候。

任何已定義的Facet都可以用作URL引數，而且會根據引數值篩選結果： `http://yourstore.com?brand=acme&color=red`。

## Facet彙總

多面向彙總的執行方式如下：如果店面有三個Facet （類別、顏色和價格），且購物者篩選全部三個（顏色=藍色，價格為$10.00-50.00，類別= `promotions`）。

- `categories`彙總 — 彙總`categories`，然後套用`color`和`price`篩選器，但不套用`categories`篩選器。
- `color`彙總 — 彙總`color`，然後套用`price`和`categories`篩選器，但不套用`color`篩選器。
- `price`彙總 — 彙總`price`，然後套用`color`和`categories`篩選器，但不套用`price`篩選器。

## 預設屬性值

下列產品屬性由[!DNL Adobe Commerce Optimizer]使用且預設為啟用。

| 屬性 | 說明 | 屬性 |
|---|---|---|
| 可排序 | 用於產品清單中的排序 | `price` |
| 可搜尋 | 用於搜尋 | `price` <br />`sku`<br />`name` |

請參閱[資料擷取中繼資料API](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/#metadata)，進一步瞭解產品屬性及其屬性。

## 分層搜尋和展開搜尋型別

分層搜尋（或搜尋內的搜尋）是一種以屬性為基礎的篩選系統，可擴充傳統的搜尋功能，以包含其他搜尋引數。 這些額外的搜尋引數可讓您更精確、更靈活地探索產品。

使用分層搜尋，您可以：

- 讓購物者能夠在搜尋結果中搜尋。
- 在分層搜尋的第二層中使用`startsWith`和`contains`搜尋索引，以進一步調整結果。

進階搜尋功能是使用特定運運算元，透過`filter`查詢[`productSearch`中的](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/)引數實作：

- **分層搜尋** — 在另一個搜尋內容中搜尋 — 使用此功能，您最多可以執行兩個層級的搜尋來搜尋您的搜尋查詢。 例如：

   - **第1層搜尋** — 在`product_attribute_1`上搜尋「馬達」。
   - **第2層搜尋** — 搜尋`product_attribute_2`上的「零件編號123」。 此範例會在結果中搜尋「馬達」的「零件編號123」。

  分層搜尋可用於分層搜尋的第二層中的`startsWith`搜尋索引和`contains`搜尋索引，如下所述：

- **startsWith搜尋索引** — 使用`startsWith`索引搜尋。 此功能可讓：

   - 搜尋屬性值以指定字串開頭的產品。
   - 設定「結尾為」搜尋，讓購物者可以搜尋屬性值結尾為特定字串的產品。
      - 若要啟用「結尾為」搜尋，產品屬性需要反向擷取，且API呼叫也應該為反向字串。 例如，如果您想要搜尋結尾為「pants」的產品名稱，您必須將此專案傳送為「stap」。

- **包含搜尋索引** — 使用搜尋包含索引的屬性。 這項新功能可讓：

   - 在較大的字串中搜尋查詢。 例如，如果購物者搜尋字串「HAPE-123」中的產品編號「PE-123」。

      - 注意：此搜尋型別與執行自動完成搜尋的現有[片語搜尋](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#phrase)不同。 例如，如果您的產品屬性值是&quot;outdoor pants&quot;，則短語搜尋會傳回&quot;out pan&quot;的回應，但不會傳回&quot;oor ants&quot;的回應。 但是，「包含搜尋」會傳回「或螞蟻」的回應。

這些新條件會增強搜尋查詢篩選機制，以縮小搜尋結果。 這些新條件不會影響主要搜尋查詢。

### 實施

1. [將屬性設定為可搜尋](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata)。

1. 指定該屬性的搜尋功能，例如&#x200B;**包含** （預設）或&#x200B;**開頭為**。 您最多可以為&#x200B;**Contains**&#x200B;指定六個要啟用的屬性，以及為&#x200B;**Starts with**&#x200B;指定六個要啟用的屬性。 此外，對於&#x200B;**Contains**&#x200B;索引，字串長度限製為50個字元或更少。

1. 請參閱[開發人員檔案](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability)，以取得如何使用新的[!DNL Commerce Optimizer]和`contains`搜尋功能更新`startsWith` API呼叫的範例。

   您可以在搜尋結果頁面上實作這些新條件。 例如，您可以在頁面上新增區段，讓購物者可以進一步縮小搜尋結果。 您可以允許購物者選取特定產品屬性，例如「製造商」、「零件編號」和「說明」。 從該位置，他們使用`contains`或`startsWith`條件在這些屬性中搜尋。

### 何時使用分層搜尋而非Facet

階層式搜尋和Facet在產品探索中有不同的用途，而且兩者之間的選擇取決於您的特定使用案例：

**使用分層搜尋：**

- 使用多個條件在搜尋結果中搜尋
- 使用使用者知道部分資訊的零件編號、SKU或技術規格
- 允許購物者使用巢狀條件逐步縮小結果
- 結合單一查詢中的多個搜尋條件，減少API呼叫的數量
- 實作比標準多面嚮導覽更深入的業務特定搜尋模式

**使用Facet：**

- 提供一般類別、價格、品牌和屬性篩選
- 提供使用者可輕鬆瞭解及選取的直覺式篩選器選項
- 根據目前的搜尋結果顯示可用選項
- 顯示有助於使用者瞭解可用選項的篩選器計數和範圍
- 使用常見的產品特性，例如顏色、尺寸、材質等

**最佳實務：**&#x200B;針對使用者具有特定條件的複雜技術搜尋，使用階層式搜尋，並針對使用者想要以視覺化方式探索和調整選項的標準電子商務篩選，使用Facet。
