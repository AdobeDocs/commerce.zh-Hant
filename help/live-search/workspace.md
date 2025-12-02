---
title: 設定即時搜尋
description: ' [!DNL Live Search] 工作區是用來設定、管理和監視搜尋效能。'
exl-id: 07c32b26-3fa4-4fae-afba-8a10866857c3
source-git-commit: 1e127a217130648923bcbaf97d5b1504b90d73fa
workflow-type: tm+mt
source-wordcount: '2117'
ht-degree: 0%

---

# 設定即時搜尋

工作區是您設定、管理和監視[!DNL Live Search]效能的地方。 頂端的功能表可讓您存取每個功能區域中的工具。 可用的功能會反映目前的選單選取範圍。

![Workspace](assets/workspace.png)

## 資料收集

為確保工作區上的每個功能區域都包含正確的資料，您需要根據所選的店面實作來設定資料收集：

1. Luma — 現成提供資料收集功能。
1. Headless — 視店面實作而定，必須手動設定資料收集。

如果您使用的是Headless店面，請參閱以下檔案以取得有關您需要新增的所需事件的詳細資訊：

- [即時搜尋儀表板的必要事件](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#live-search)。
- [需要新增為先決條件的Storefront事件收集器](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/)。
- 事件結構的[範例](https://github.com/adobe/commerce-events/tree/main/examples)。

### 醫療保健客戶

如果您是醫療保健客戶，且已安裝[Data Services HIPAA擴充功能](../data-connection/hipaa-readiness.md#installation) （屬於[Data Connection](../data-connection/overview.md)擴充功能的一部分），則不會再擷取[!DNL Live Search]使用的店面事件資料。 這是因為店面事件資料是在使用者端產生。 若要繼續擷取和傳送店面事件資料，請重新啟用[!DNL Live Search]的事件收集。 請參閱[一般組態](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general#data-services)以瞭解更多資訊。

## 設定範圍

所有[設定的](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings)領域[!DNL Live Search]最初設定為`Default Store View`。 如果您的[!DNL Commerce]安裝包含多個存放區檢視，請將&#x200B;**範圍**&#x200B;設定為您的Facet設定套用的[存放區檢視](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html)。

## 功能表選項

| 選項 | 說明 |
|--- |--- |
| [效能](performance.md) | 控制面板提供insight產品搜尋效能資訊。 |
| [多面向](facets.md) | 使用屬性值的多個維度來調整搜尋條件的高效能篩選。 |
| [同義字](synonyms.md) | 擴大搜尋範圍，納入購物者可能會用來尋找與目錄中不同產品的字詞。 |
| [搜尋銷售](rules.md) | 使用可觸發已排程動作的邏輯規則來塑造搜尋體驗。 提升、隱藏、釘選或隱藏產品，以校正搜尋結果，支援您的業務目標。 |
| [類別銷售](category-merch.md) | 在類別層級套用規則和智慧型銷售。 |
| [GraphQL](graphql.md) | 開發人員若已登入您商店的管理員，可使用實際目錄資料撰寫和測試查詢。 若要深入瞭解，請前往[開發人員檔案中的](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/)GraphQL概觀[!DNL Live Search]。 |
| [設定](settings.md) | 決定如何在店面中依價格範圍分組價格方面值，並設定索引語言。 |

## 將屬性設定為可搜尋

若要產生高針對性的結果，請檢閱[可搜尋](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html) (`searchable=true`)產品屬性集。 為確保關聯性，請讓屬性只有在包含具有清晰精簡含義的內容時才可供搜尋。 避免使用包含較不精確、長度較長的文字的屬性，例如`description`，雖然預設會啟用搜尋，但可能會降低搜尋結果的精確度。 例如，如果有人搜尋「短褲」，而且有描述包含「短袖」字樣的襯衫，則這些襯衫會包含在搜尋結果中。

若要允許搜尋屬性，請完成下列步驟：

1. 在管理員中，移至&#x200B;**商店** > *屬性* > **產品**。
1. 選取您要搜尋的屬性，例如`color`。
1. 選取&#x200B;**店面內容**&#x200B;並將&#x200B;**在搜尋中使用**&#x200B;設定為`yes`。

[!DNL Live Search]也會遵從產品屬性的[權重](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-results.html#weighted-search)，如在Adobe Commerce中所設定。 權重較高的屬性會顯示在搜尋結果中較高的位置。

下列屬性一律可供搜尋：

- `sku`
- `name`
- `categories`

### 複雜產品中的屬性行為

對於複雜的產品型別（可配置、套件組合和群組產品），[!DNL Live Search]會索引來自父項和子項產品的屬性值，允許父項產品與相同屬性的多個值相關聯。 這會啟用變體式篩選；例如，如果任何變體為藍色，即使父產品沒有顏色設定，當依「藍色」篩選時會顯示可設定的襯衫。

這非常適合色彩和大小等屬性，但可能會導致`new_arrival`、`product_ranking`、`promotion_label`或自訂價格屬性產生非預期的結果。 例如，如果可設定的產品(SKU-001)有`new_arrival = true`，但其子變體(SKU-001-01)有`new_arrival = false`，則父產品SKU-001會以兩個值（`true`和`false`）建立索引，使其顯示在任一條件的搜尋結果中。

### 分層搜尋和展開搜尋型別

階層式搜尋（或搜尋內的搜尋）是一種功能強大、以屬性為基礎的篩選系統，可擴充傳統的搜尋功能，以包含其他搜尋引數。 這些額外的搜尋引數可讓您更精確、更靈活地探索產品。

>[!NOTE]
>
>分層搜尋適用於Live Search 4.6.0。

使用分層搜尋，您可以：

- 讓購物者能夠在搜尋結果中搜尋。
- 在分層搜尋的第二層中使用`startsWith`和`contains`搜尋索引，以進一步調整結果。

進階搜尋功能是使用特定運運算元，透過`filter`查詢[`productSearch`中的](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/)引數實作：

- **分層搜尋** — 在另一個搜尋內容中搜尋 — 使用此功能，您最多可以執行兩個層級的搜尋來搜尋您的搜尋查詢。 例如：

   - **第1層搜尋** — 在`product_attribute_1`上搜尋「馬達」。
   - **第2層搜尋** — 搜尋`product_attribute_2`上的「零件編號123」。 此範例會在結果中搜尋「馬達」的「零件編號123」。

  分層搜尋可用於分層搜尋的第二層中的`startsWith`搜尋索引和`contains`搜尋索引，如下所述：

- **startsWith搜尋索引** — 使用`startsWith`索引搜尋。 這項新功能可讓：

   - 搜尋屬性值以指定字串開頭的產品。
   - 設定「結尾為」搜尋，讓購物者可以搜尋屬性值結尾為特定字串的產品。 若要啟用「結尾為」搜尋，產品屬性需要反向擷取，且API呼叫也應該為反向字串。 例如，如果您想要搜尋結尾為「pants」的產品名稱，您必須將此專案傳送為「stap」。

- **包含搜尋索引** — 使用搜尋包含索引的屬性。 這項新功能可讓：

   - 在較大的字串中搜尋查詢。 例如，如果購物者搜尋字串「HAPE-123」中的產品編號「PE-123」。

      - 注意：此搜尋型別與執行自動完成搜尋的現有[片語搜尋](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#phrase)不同。 例如，如果您的產品屬性值是&quot;outdoor pants&quot;，則短語搜尋會傳回&quot;out pan&quot;的回應，但不會傳回&quot;oor ants&quot;的回應。 但是，「包含搜尋」會傳回「或螞蟻」的回應。

這些新條件會增強搜尋查詢篩選機制，以縮小搜尋結果。 這些新條件不會影響主要搜尋查詢。

#### 實施

1. 在Admin中，[將產品屬性](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes-add#step-5-describe-the-storefront-properties)設定為可搜尋。

   檢視可搜尋的[屬性](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types)清單。

1. 指定該屬性的搜尋功能，例如&#x200B;**包含** （預設）或&#x200B;**開頭為**。 您最多可以為&#x200B;**Contains**&#x200B;指定6個要啟用的屬性，並為&#x200B;**Starts with**&#x200B;指定6個要啟用的屬性。 此外，對於&#x200B;**Contains**&#x200B;索引，字串長度限製為50個字元或更少。

   ![指定搜尋功能](./assets/search-filters-admin.png)

1. 請參閱[開發人員檔案](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability)，以取得如何使用新的[!DNL Live Search]和`contains`搜尋功能更新`startsWith` API呼叫的範例。

   您可以在搜尋結果頁面上實作這些新條件。 例如，您可以在頁面上新增區段，讓購物者可以進一步縮小搜尋結果。 您可以允許購物者選取特定產品屬性，例如「製造商」、「零件編號」和「說明」。 從該位置，他們使用`contains`或`startsWith`條件在這些屬性中搜尋。

### 何時使用分層搜尋而非Facet

階層式搜尋和Facet在產品探索中有不同的用途，而且兩者之間的選擇取決於您的特定使用案例：

**在下列情況下使用分層搜尋：**

- 您需要使用多個條件在搜尋結果中搜尋。
- 使用使用者知道部分資訊的零件編號、SKU或技術規格。
- 購物者需要透過巢狀條件逐步縮小結果。
- 您想要透過在單一查詢中合併多個搜尋條件來減少API呼叫的數量。
- 您需要實作企業專屬的搜尋模式，這些模式不僅限於標準多面嚮導覽。

**使用Facet，時間：**

- 提供一般類別、價格、品牌和屬性篩選
- 提供使用者可輕鬆瞭解及選取的直覺式篩選器選項
- 根據目前的搜尋結果顯示可用選項
- 顯示有助於使用者瞭解可用選項的篩選器計數和範圍
- 使用常見的產品特性，例如顏色、尺寸、材質等。

**最佳實務：**&#x200B;使用階層式搜尋來搜尋使用者具有特定條件的複雜技術搜尋，並使用Facet來篩選標準電子商務篩選，讓使用者以視覺化方式探索及縮小選項。

## 多面向和同義字

多面向和同義字是另一種提升購物者搜尋體驗的方式。

[Facet](facets.md)是在[!DNL Live Search]中定義的可篩選產品屬性。 您可以在[!DNL Live Search]中將任何可篩選的屬性設定為Facet，但您一次可搜尋的Facet數目有[限制](boundaries-limits.md)。

>[!NOTE]
>
>產品屬性只有在產品屬性組態具有必要的屬性時才可篩選： *在搜尋中使用=是*、*在搜尋結果中使用Layered Navigation=是*&#x200B;以及&#x200B;*在分層導覽中使用Layered Navigation=可篩選（含結果）*。 如果這些屬性遺失或未正確設定，則在Facet設定中不會顯示此屬性。 如需設定指示，請參閱[新增Facet](facets-add.md#add-a-facet)。

[同義字](synonyms.md)是可定義的術語，可協助引導使用者使用正確的產品。 尋找褲子的使用者可能會輸入「trousers」或「slacks」。 您可以設定同義字，讓這些搜尋詞將使用者帶到「褲子」結果。

## Commerce組態設定

下節說明[!DNL Live Search]支援和不支援的Commerce組態設定。

### 支援的設定值

>[!IMPORTANT]
>
>強烈建議您使用在Live Search 4.0.0中預設為啟用的產品清單Widget。Widget的目標是完全取代未來版本中的介面卡實作。 請參閱[啟用產品清單Widget](install.md#enable-product-listing-widgets)以深入瞭解。

| Commerce組態設定 | 說明 | 由Popover支援 | 由介面卡支援 |
|---|---|---|---|
| 商店>設定>目錄>目錄>目錄搜尋>允許每頁所有產品 | 如果設為`Yes`，則在「每頁顯示」控制項中包含`ALL`選項。 | 是。 最多500種產品 | 是。 最多500種產品 |
| 儲存>設定>目錄>目錄>目錄搜尋>最小查詢長度 | 目錄搜尋中允許的最小字元數。 | 是 | 是 |
| 儲存>設定>目錄>目錄>目錄搜尋>每頁產品網格允許值 | 決定格線檢視中顯示的產品數目。 | 是 | 是 |
| 商店>設定>目錄>目錄>目錄搜尋>產品每頁格點預設值 | 決定網格檢視中預設每頁顯示的產品數目。 | 是。 最多500種產品 | 是。 最多500種產品 |
| 儲存>設定>目錄>庫存>顯示無庫存產品 | 顯示無庫存的產品。 | 是 | 是 |
| 儲存>組態>幣別>預設顯示幣別 | 用來顯示價格的主要貨幣。 | 是 | 是 |
| 儲存>組態>一般>貨幣設定>貨幣選項>基本貨幣 | 用於所有線上付款交易的主要幣別。 | 是 | 是 |

「Widget產品清單」頁面與「彈出視窗」中的價格會使用設定的幣別匯率，轉換為預設顯示幣別。

### 不支援的設定值

| Commerce組態設定 | 說明 | 附註 |
|---|---|---|
| 商店>設定>目錄>店面>清單模式 | 決定搜尋結果清單的格式。 | 正確轉譯，但部分頁面互動不會傳送事件 |
| 儲存>組態>目錄>目錄>目錄搜尋>查詢長度上限 | 目錄搜尋中允許的最大字元數。 | 未實作；搜尋服務接受最多255個字元 |
| 組態>銷售>稅捐>價格顯示設定>在目錄中顯示產品價格 | 決定目錄中所發佈的產品價格是否包含或排除稅捐，或顯示兩個版本的價格；一個含稅，另一個不含稅 |  |
| 商店>設定>目錄>店面>產品清單排序依據 | 決定搜尋結果清單的排序順序。 | 不適用於[!DNL Live Search] [產品清單頁面Widget](plp-styling.md) |

## 預設屬性值

下列產品屬性具有[店面屬性](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html)，已由[!DNL Live Search]使用並預設啟用。

| 屬性 | 店面屬性 | 屬性 |
|---|---|---|
| 可排序 | 用於產品清單中的排序 | `price` |
| 可搜尋 | 用於搜尋 | `price` <br />`sku`<br />`name` |
| FilterableInSearch | 用於分層導覽 — 可篩選（含結果） | `price`<br />`visibility`<br />`category_name` |

## 預設非系統屬性屬性

下表顯示非系統屬性的預設搜尋和可篩選屬性，包括特定於Luma範例資料的屬性。 將&#x200B;*Use in Search*&#x200B;屬性屬性設定為`Yes`，可讓屬性在[!DNL Live Search]與原生Adobe Commerce中均可搜尋。

| 屬性代碼 | 可搜尋 | 用於分層導覽 |
|--- |--- |--- |
| 活動 | 是 | 可篩選（包含結果） |
| attributes_brand | 是 | 否 |
| 品牌 | 是 | 否 |
| 氣候 | 是 | 可篩選（包含結果） |
| 項圈 | 是 | 可篩選（包含結果） |
| 顏色 | 是 | 可篩選（包含結果） |
| 成本 | 是 | 否 |
| eco_collection | 是 | 可篩選（包含結果） |
| 性別 | 是 | 可篩選（包含結果） |
| 製造商 | 是 | 可篩選（包含結果） |
| 材質 | 是 | 可篩選（包含結果） |
| 用途 | 是 | 可篩選（包含結果） |
| strap_bag | 是 | 可篩選（包含結果） |
| style_general | 是 | 可篩選（包含結果） |

## 預設系統屬性屬性

下表顯示系統屬性的預設搜尋和可篩選特性。

| 屬性代碼 | 可搜尋 | 用於分層導覽 |
|--- |--- |--- |
| allow_open_amou | 是 | 可篩選（包含結果） |
| 說明 | 是 | 否 |
| 名稱 | 是 | 否 |
| 價格 | 是 | 可篩選（包含結果） |
| short_description | 是 | 否 |
| sku | 是 | 否 |
| 狀態 | 是 | 否 |
| tax_class_id | 是 | 否 |
| url_key | 是 | 否 |
| 權重 | 是 | 否 |
