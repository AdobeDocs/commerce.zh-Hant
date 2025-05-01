---
title: 目錄概觀
description: 瞭解如何定義您的管道和原則。
hide: true
recommendations: noCatalog
source-git-commit: d716dd9d75beb642bfad30271b6ecd3490ee7328
workflow-type: tm+mt
source-wordcount: '1604'
ht-degree: 0%

---

# 目錄概觀

>[!NOTE]
>
>本檔案說明提早存取開發中的產品，並未反映所有可供一般使用的功能。

產品目錄對於線上購物體驗至關重要，可讓客戶瀏覽、搜尋和進行購買。 為提升營運效率，產品目錄應密切反映公司的業務結構。 企業經常需要根據地理市場、分銷管道、客戶區段和其他變數，以不同價格銷售產品。 為了因應這種情況，電子商務平台必須提供彈性的目錄資料模型，讓公司能夠根據這些情況量身打造不同的目錄。 Adobe提供由管道和原則支援的促銷服務，以因應這些需求。 銷售服務提供建構元素，商家可使用此建構元素來大規模建立和管理目錄。 如此一來，企業就能根據自身業務結構和上市策略來設定目錄。

基本上，透過銷售服務，您可以：

- 針對您的所有業務需求使用單一基礎目錄。 快速擴展新品牌、市場、業務單位、上市管道和客戶區段的目錄，而不需要完全的重新架構。 如此一來，您便能消除資料重複現象，並設定電子商務平台，以提升營運效率。
- 透過設計產品目錄來反映您的業務（包括產品、客戶、定價和分銷），解除鎖定目錄整合併提供適當的內容。
- 快速擷取和更新目錄資料，並快速將更新傳送至店面，滿足您的促銷活動和行銷活動需求。
- 透過Edge Delivery Services支援的立即可用、超快的UI元件，完成完美的Lighthouse分數，提供順暢的產品瀏覽與建議。
- 採用Adobe擴充性架構([App Builder](https://experienceleague.adobe.com/en/playlists/commerce-get-started-app-builder-development))的現代可撰寫架構，以使用Adobe的[API Mesh](https://experienceleague.adobe.com/en/playlists/commerce-get-started-app-builder-and-api-mesh)匯入產品資料並強化Headless商務店面。

>[!INFO]
>
>若要瞭解由管道和原則支援的銷售服務中可用的API，請參閱[開發人員檔案](https://developer-stage.adobe.com/commerce/services/composable-catalog)。

## 架構

由管道和原則支援的銷售服務是一種高度可擴充、彈性的目錄資料模型，可輕鬆開啟多品牌、多業務單位、多語言使用案例。 此模型以新的Merchandising Services產品範圍（管道、原則和地區設定）取代傳統Adobe Commerce產品範圍（網站、商店、商店檢視）的使用。

下圖提供銷售架構的高階檢視。

![[!DNL Merchandising Services]架構](../assets/merchandising-svcs-architecture.png)

在此圖表頂端，目錄資料（PIM、ERP等）會內嵌至「銷售服務」架構。 此目錄資料包含SKU。 每個SKU都包含範圍詳細資料（地區設定）和產品屬性，這些對應到新的Merchandising Services產品範圍（管道、原則和地區設定）。

當所有這些資料都內嵌到銷售架構中時，結果會在目錄服務資料管道中提供新的統一基礎目錄。 在圖表的下一部分，您會看到多個管道。 每個管道代表一個業務單位。 例如，*Texas零售業*、*Texas零售業季節*&#x200B;等。 從圖表中可看出，所有地區、原則及價格簿皆可在各個管道之間共用&#x200B;。

最後，圖表顯示這種獨特的目錄資料如何出現在各種位置，例如Edge Delivery Services店面、市場、廣告頻道、自訂微型店面等。

若要瞭解如何使用目錄資料擷取API將目錄資料擷取到Merchandising，以及如何使用目錄管理和規則API來設定您的地區、原則和價格手冊，請參閱[開發人員檔案](https://developer-stage.adobe.com/commerce/services/composable-catalog/)。

若要進一步瞭解構成Merchandising Services的概念，請參閱下列章節。

## 產品目錄管理

產品目錄管理包含兩個不同的方面：產品資料和產品內容。 銷售服務尊重這些職責的分離，為每一項提供獨立管理。

- **產品資料** — 售出什麼產品，以什麼價格？
- **產品內容** — 誰在銷售給誰，在哪裡銷售？

![[!DNL Merchandising Services]個方面](../assets/merchandising-svcs-parts.png)

### 產品資料

產品資料包括下列型別：

- **產品** — 代表實體商品或無形服務的個別SKU或SKU集合，其屬性代表產品，包括說明、重量、大小、尺寸等等。 屬性也會指定SKU的通道和原則範圍。 產品可以分組為各種產品型別，例如，簡單、可設定、套件、套件組合、訂閱等。
- **中繼資料** — 產品屬性中繼資料會定義及管理產品屬性在產品清單、詳細資料頁面、搜尋結果等店面中的顯示方式。 中繼資料也會定義產品屬性在搜尋中的使用方式，例如排序、篩選、搜尋權重等。
- **訂價書籍與價格** — 決定產品的售價。 在銷售服務中，產品SKU和價格是分離的，因此您能夠針對單一SKU定義多個價格簿。 藉由將價格與SKU脫鉤，您可以解鎖不同客戶階層、業務單位和地理位置的範圍特定價格。 您可以定義一般和折扣價格，並大規模管理所有這些。
- **Assets** — 與產品相關的成品，例如影像、影片、PDF或其他檔案型別（未來藍圖）。

### 產品內容管理

產品前後關聯管理涵蓋下列方面：

- **管道** — 分銷管道定義企業想要透過哪個路徑銷售產品。 管道是封裝語言環境與原則的最高層級抽象概念。
   - 範例：汽車業的經銷商。 適用於多品牌企業集團的附屬公司。 供應商的製造地點。
- **原則** — 資料存取篩選器，可讓您將正確的內容傳送到正確的目的地。 此概念可啟用目錄整合功能。
   - 範例：銷售點實體商店、市集、廣告管道(Google、Facebook、Instagram)
- **領域** — 代表目錄的語言（地區設定），例如`en-US`。 在目錄資料擷取期間在SKU層級設定範圍。

在產品資料擷取和更新期間，SKU包含範圍和屬性的詳細資訊（屬性對應至管道和原則）。 這些會定義SKU所屬的產品內容識別碼：

![[!DNL Merchandising Services]產品內容識別碼](../assets/merchandising-svcs-product-id.png)

在上圖中，每個SKU提供：

- 範圍識別碼&#x200B;
   - 地區設定：必&#x200B;要
- 產品屬性
   - 產品屬性可用來對應至相關的管道和原則&#x200B;。
   - 範例：作為汽車製造商，您可以選擇建立產品屬性的管道和原則組合： (1)經銷商(2)汽車品牌&#x200B;。
- 價格與指定的價格簿
   - 每個SKU都可以使用多重價格簿來定義多重價格。
   - 範例：您提供員工較低的汽車零件正常價格，額外折扣25%。 您以10%的折扣，為VIP客戶提供更高的正常價格。 產品SKU價格資訊可確保針對每個客戶區段顯示正確的價格。

管道和原則定義是使用專用的API來建立：

![[!DNL Merchandising Services]管道、原則及範圍對應](../assets/merchandising-svcs-scope-map.png)

- **範圍** （地區設定） — 在產品資料擷取期間設定在SKU層級。&#x200B;
- **Channel** — 使用專用API建立的定義。&#x200B;URL
- **原則** — 使用專用API建立的定義。

## 主要功能

| 主要功能 | 優點 |
|---|---|
| **將目錄資料直接擷取至Storefront Services管道**：將目錄資料直接擷取至儲存庫瀏覽與搜尋生命週期（產品顯示頁面、產品清單頁面、搜尋結果頁面等）的目錄服務管道。 | <ul><li>將目錄資料直接擷取到店面服務管道，以下專案可提供支援：目錄服務、產品探索（即時搜尋）和產品推薦。 透過此功能，您可以大規模提供數百萬SKU的目錄更新。 如此一來，時效性很強的大型促銷管理便能順利運作。 </li></ul> |
| **新目錄產品範圍**：頻道、原則及範圍是銷售服務引入的新產品範圍。 這些產品範圍會取代店面服務層中的網站、商店和商店檢閱範圍。 [了解更多](#product-context-management)。 | <ul><li>透過新的範圍，Merchandising Services可讓您輕鬆使用單一基本目錄，擴展至多地理位置、多業務單位、多品牌和多語言的使用案例。</li><li>消除目錄管理中的資料備援。</li></ul> |
| **擴充至數千萬個SKU** | 大規模解除鎖定目錄管理。 您可以在此輕鬆擷取及管理超過200MM的SKU。 |
| **產品型別支援** | <ul><li>簡單，可設定</li><li>套件組合和套件組合（未來藍圖）</li><li>訂閱與計畫（未來藍圖）</li></ul> |
| **Headless商務** | <ul><li>透過目錄服務、產品探索（即時搜尋）和產品推薦API，完整支援Headless商務實作。</li></ul> |
| **新式超快UI元件** | <ul><li>產品搜尋和產品建議的現成UI元件支援。</li><li>UI元件具備可擴充性和彈性，因此可供Adobe的Edge Delivery服務以及任何其他店面實作使用。</li></ul> |

## 哪種型別的商家從銷售服務中受益最大？

下表重點說明商家經常會遇到的挑戰，以及管道和政策支援的促銷服務如何解決這些挑戰。

| 商家型別 | 使用案例 | 已解決的問題 |
|---|---|---|
| 多品牌企業集團 | <ul><li>他們銷售數個品牌</li><li>他們在多個國家/地區銷售</li><li>他們以不同的語言銷售</li></ul> | 使用單一基礎統一目錄並達到營運效率，同時擴展至數個品牌、地理位置和語言。 |
| 汽車/製造零件conglomerate | <ul><li>銷售汽車或機器零件。 所有客戶適用的產品都相同。</li><li>不同的經銷商向客戶銷售零件</li><li>每個經銷商都有各自的價格、庫存和運送方式</li></ul> | 若要進行不同的運送整合，每個經銷商都應該有個別的網站。 但個別網站會強制使用典型的目錄資料模型複製資料。 因此，如果在美國有3000個經銷商，即使所有經銷商都使用相同的目錄，商家也會建立3000個目錄副本。 這種資料重複會影響效能限制。 銷售服務可消除資料重複現象。 |
| 包裝/物流公司 | <ul><li>他們有數個運送地點</li><li>每個客戶的價格各異</li><li>2個地點提供的相同產品有4種可能的價格</li></ul> | 雖然使用客戶群組來涵蓋每個客戶的價格，但典型的目錄資料模型無法管理每個地點的價格。 此外，商家想要依地點/網站設定獨特的可見度規則。 透過銷售服務，您可以大規模解除管理此類複雜價格和可見性規則的鎖定。 |

<!--### Where to go from here

- Ingest data into Merchandising Services using the [data ingestion API](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/).
- Manage your catalog and define the channels, policies, and scopes using the [catalog management API](https://developer-stage.adobe.com/commerce/services/composable-catalog/admin/using-the-api/)
- [Complete a tutorial](https://developer-stage.adobe.com/commerce/services/composable-catalog/merchandising-services-use-case/) that shows how a company with a single base catalog can use the Merchandising Services APIs to add product data, define catalogs using projections, and retrieve the catalog data for display in a headless storefront.-->
