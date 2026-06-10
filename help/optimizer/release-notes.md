---
title: Adobe Commerce Optimizer發行說明
description: ' [!DNL Adobe Commerce Optimizer]的每月發行資訊，包括店面目錄資料擷取的資料擷取REST API和GraphQL API更新。'
feature: Release Notes
role: Admin, Developer, User, Leader
recommendations: noCatalog
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 專案（Adobe管理的SaaS基礎結構）。"
exl-id: e420d461-9ea2-4e32-aa37-230b14a297d7
TQID: https://experienceleague.adobe.com/apcpxN0AOniRcHDCa5MMAVWysxRO5mTcudXXXjET-Lo
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: bd4c59c451d7b08de7dc6ef00da2556fb9a6696f
workflow-type: tm+mt
source-wordcount: 1319
ht-degree: 0%

---

# 發行說明

下列發行說明包含[!DNL Adobe Commerce Optimizer]的更新，包括：

* [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour)的新功能及改進專案。
* 更新[資料擷取REST API](https://developer.adobe.com/commerce/services/reference/rest/)和店面目錄資料擷取[&#128279;](https://developer.adobe.com/commerce/services/reference/graphql/)的GraphQL API。

  {{aco-api-updates-and-dropins}}

## 2026年6月

>[!BEGINSHADEBOX]

### 語意搜尋

[!DNL Adobe Commerce Optimizer]現在支援&#x200B;**[!UICONTROL Settings]**&#x200B;中&#x200B;[**進階搜尋**](./settings.md#advanced-search)&#x200B;索引標籤上的&#x200B;**[語意搜尋]**。 語意搜尋使用AI透過含意和內容以及關鍵字搜尋來比對產品，減少自然語言查詢的空白搜尋頁面。 符合資格的英文目錄預設會啟用此功能。 您可以選擇在相同索引標籤上調整&#x200B;**[!UICONTROL Semantic boost]**、**[!UICONTROL Similarity threshold]**&#x200B;和&#x200B;**[!UICONTROL Fuzzy search]**。 不需要屬性設定或店面變更。 [了解更多](./setup/semantic-search.md)。

### 建議價格篩選器(Beta)

產品推薦單位現在在&#x200B;**[!UICONTROL Filter products]**&#x200B;步驟上支援&#x200B;[**價格篩選器**](./merchandising/recommendations/filters.md#price)。 在產品詳細資料頁面上包含或排除使用&#x200B;**靜態**&#x200B;最小和最大範圍或&#x200B;**動態**&#x200B;規則的適用者，這些規則會將建議的產品與店面使用中價格簿上目前檢視之產品的&#x200B;**最終計算價格**&#x200B;進行比較。 價格規則會篩選候選集。 它們不會重新排名產品。 [了解更多](./merchandising/recommendations/filters.md#price)。

{{aco-release}}

>[!ENDSHADEBOX]

## 2026年5月

>[!BEGINSHADEBOX]

### 智慧型排名提升

搜尋的[銷售規則](./merchandising/rules/add.md#intelligent-ranking-boost)、預設產品清單和[類別頁面](./merchandising/rules/add.md#rule-types) （測試版）現在包含&#x200B;**[!UICONTROL Intelligent Ranking Boost]**。 您可以調整如&#x200B;**檢視次數最多**&#x200B;或&#x200B;**趨勢**&#x200B;等策略對產品訂單的影響，以決定搜尋的相關性，以及類別清單上的行為訊號。 規則預覽會反映您的設定。 提升功能會在查詢時套用，因此當您變更目錄時，就不需要重新同步目錄。

### API更新

_2026年5月28日_

<!-- v1.2 -->

![修正](../assets/fix.svg) **完整的導覽樹狀結構** — 當路徑中存在未標籤的中繼節點時，已標籤的下階類別現在會正確包含在系列篩選的`navigation`樹狀結構中。這項修正可確保購物者在導覽中看見所有相關類別，讓您更輕鬆地瀏覽及探索專案。
<!--DATA-7183-->

![修正](../assets/fix.svg) **在`categoryTree`要求中處理空白的Slug** — 修正當`slugs`引數包含空白字串時，[`categoryTree`](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree)查詢傳回內部伺服器錯誤的問題。空的概要(Slug)值現在會被忽略，因此儲存體和整合功能可繼續解析類別資料，而不會發生請求失敗的情況。
<!--DATA-7184-->

![修正](../assets/fix.svg) **`searchCategory`要求傳回不區分大小寫、以字母順序排列的結果** — 現在`searchCategory`查詢會依字母順序排序搜尋結果，而不會區分大小寫，以確保順序一致且可預測。如果名稱完全相同，首碼較短的類別會先出現。
<!--COMOPT-2142-->

_2026年5月4日_

<!--v1.53-->

**正確的貨幣顯示** — 店面產品價格現在會顯示所有產品型別的正確貨幣代碼（例如USD）。 之前，部分產品顯示`NONE`而非預期的貨幣，導致價格遺失。

<!--DATA-7115-->

{{aco-release}}

>[!ENDSHADEBOX]

## 2026年4月

**發行日期**： 2026年4月7日

>[!BEGINSHADEBOX]

### 目錄規則（測試版）

[類別規則](./merchandising/rules/add.md)可擴充銷售規則，讓您可以在類別頁面上以搜尋相同的排名和動作（釘選、提升、隱藏）鎖定類別並控制產品順序。

### 價格篩選(beta)

建議篩選器現在包含[價格範圍篩選器](./merchandising/recommendations/filters.md#price) （最小值和最大值）。

### API更新

_2026年4月29日_

<!--v1.52 release-->

**需要批次處理請求** — 現在，當您擷取目錄資料時，GraphQL API會針對每個請求強制最多100個SKU。 請參閱[已記錄的限制和邊界](https://experienceleague.adobe.com/zh-hant/docs/commerce/optimizer/boundaries-limits#product-discovery)。

<!--DATA-7156-->

_2026年4月17日_

<!--v1.51 release-->

**使用GraphQL依名稱尋找類別** — 新的[`searchCategory`](https://developer.adobe.com/commerce/services/reference/graphql/)查詢會傳回符合的類別，並包含店面與整合的分頁。 請參閱API參考以取得引數和回應欄位。<!--COMOPT-1819-->

_2026年4月7日_

<!--v1.50 release-->

**較簡單的類別查詢** — [categoryTree](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree)查詢會將`family`視為選用專案，因此您可以透過Slug解析類別，而不需要提供系列。

{{aco-release}}

>[!ENDSHADEBOX]

## 2026年3月

本月沒有[[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour)版本。 請參閱下方的API更新。

>[!BEGINSHADEBOX]

### API更新

_2026年3月24日_

動態套件組合現在會傳回計算的價格範圍。<!--DATA-7014-->

{{aco-release}}

>[!ENDSHADEBOX]

## 2026年2月

**發行日期**：2026年2月19日

>[!BEGINSHADEBOX]

### 銷售規則與建議的目錄檢視(Beta)

現在當您[建立建議單位](./merchandising/recommendations/create.md)或[銷售規則](./merchandising/rules/add.md)時，可以指定目錄檢視。

### API更新

_2026年2月19日_

<!--v1.48-->

**店面更豐富的類別內容** — [categoryTree](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree)查詢現在會傳回說明、影像和SEO中繼標籤，讓店面可以呈現更豐富的類別頁面。<!--DATA-6933-->

_2026年2月12日_

<!--v1.49-->

**依類別增強產品資料** — GraphQL API新增[`CategoryProductView`](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#definition-CategoryProductView){target="blank"}型別，因此您可以依類別查詢及篩選往返較少的產品。

{{aco-release}}

>[!ENDSHADEBOX]

## 2026年1月

本月沒有[[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour)版本。 請參閱下方的API更新。

>[!BEGINSHADEBOX]

### API更新

_2026年1月19日_

* **REST API支援更豐富的類別** — [類別API](https://developer.adobe.com/commerce/services/reference/rest/#operation/createCategories)作業現在除了接受`families`之外，還接受選用的`metaTags`、`images`和`description`值，因此您可以為類別提供更豐富的銷售和SEO詳細資料。

{{aco-release}}

>[!ENDSHADEBOX]

## 2025年12

**發行日期**：2025年12月10日

>[!BEGINSHADEBOX]

### 機會

銷售人員現在可以透過[Adobe Sites Optimizer](./manage-results/opportunities.md)取得AI支援的建議，以偵測網站問題並提出效能修正建議。

### 目錄圖層

銷售人員現在可以使用[目錄圖層](./setup/catalog-layer.md)來覆蓋產品資料，而不需要編輯來源目錄、管理圖層優先順序，以及使用Adobe Sites Optimizer自動修正。

{{aco-release}}

>[!ENDSHADEBOX]

## 2025年11月

本月沒有[[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour)版本。 請參閱下方的API更新。

>[!BEGINSHADEBOX]

### API更新

_2025年11月21日_

**已更新資料擷取REST API的驗證指示** — 指示現在會參考OAuth存取權杖和資料擷取服務的正確Developer Console認證範圍。 如果您的認證範圍已過時，請重新產生以保留存取權。

_2025年11月3日_

<!-- v1.43 -->

**在GraphQL中分層、當地語系化的產品內容** — 您現在可以從[!DNL Adobe Commerce Optimizer]提供通道特定、地區設定感知的產品內容。

* 依客戶區段量身打造產品內容
* 套用地區特定覆寫，而不複製基本目錄資料
* 使用圖層遮色片控制欄位層級覆寫
* 使用優質、季節和行動最佳化內容層

沒有GraphQL API結構描述變更：圖層會透過現有的`products`查詢和請求標頭套用。 請參閱[目錄層](./setup/catalog-layer.md)。

{{aco-release}}

>[!ENDSHADEBOX]

## 2025年10

**發行日期**：2025年10月14日

>[!BEGINSHADEBOX]

### Commerce Optimizer Salesforce Commerce聯結器

[!DNL Commerce Optimizer Salesforce Commerce Connector]是新的App Builder入門套件，可將Salesforce B2C Commerce目錄資料同步至[!DNL Commerce Optimizer]。<!--COMOPT-536-->

管理員的&#x200B;**：**

* Salesforce目錄變更（產品、價格、中繼資料、價格手冊）會自動同步至[!DNL Commerce Optimizer]。
* 在[!DNL Adobe Commerce]之外執行，以取得較少的整合接觸點。
* 排定的更新會讓[!DNL Commerce Optimizer]個資料保持銷售與建議的最新狀態。

開發人員的&#x200B;**：**

* 將Salesforce目錄擷取至SaaS銷售服務的可擴充架構。
* 參考實作、設計檔案和程式碼範例，以加速組建和疑難排解。

### 分層搜尋

* **分層搜尋(GA)** — 產品搜尋現在支援`startsWith`和`contains`比對。 請參閱[分層搜尋和展開的搜尋型別](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#layered-search-and-expansion-of-search-types)。

### API更新

* _2025年10月17日_

  **新增REST API支援以擷取產品層** — 使用[目錄層API](https://developer.adobe.com/commerce/services/reference/rest/#tag/Product-Layers)自訂及覆寫特定內容、地區設定或業務需求的基本產品資料。 建立圖層後，您可以從[Adobe Commerce Optimizer Studio](./setup/catalog-layer.md).<!--DATA-6632-->套用及管理圖層

* _2025年10月14日_

  **程式化類別樹狀結構** — 建立、更新和管理透過REST （全域或通道特定）導覽及分組的類別樹狀結構，規模可達每個樹狀結構10,000個樹狀結構和500個類別。 檢視&#x200B;_目錄資料擷取REST API參考_&#x200B;中的[類別](https://developer.adobe.com/commerce/services/reference/rest/#tag/Categories){target="blank"}。<!--DCAT-2649-->

* _2025年10月8日_

  **更清楚的資料擷取類別對應** — 新指引說明類別概要(Category Slug)格式和階層規則，並釐清產品`routes.path`值必須符合現有的類別概要（例如，`men/clothing`）。

{{aco-release}}

>[!ENDSHADEBOX]

## 2025年9月

本月沒有[[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour)版本。 請參閱下方的API更新。

>[!BEGINSHADEBOX]

### API更新

_2025年9月23日_

* **使用REST API管理類別** — 使用[類別API](https://developer.adobe.com/commerce/services/reference/rest/#operation/createCategories)建立和管理類別。 類別會將產品組織成邏輯群組，並透過概要(Slug-based)路徑支援巢狀階層。 將類別指派給產品後，請使用GraphQL `[navigation](https://developer.adobe.com/commerce/services/reference/graphql/#navigation)`和`[categoryTree](https://developer.adobe.com/commerce/services/reference/graphql/#categorytree)`查詢來擷取這些類別，以轉譯店面功能表和類別樹狀結構。<!--DCAT-2626-->

{{aco-release}}

>[!ENDSHADEBOX]

## 2025年8月

**發行日期**： 2025年8月28日

>[!BEGINSHADEBOX]

### 歐盟區域現已推出

IMS組織可使用EU生產區域(**eu1**)。 當您在Cloud Manager中[新增 [!DNL Commerce Optimizer] 執行個體](./get-started.md#step-1-create-an-instance)時，請選擇&#x200B;**[!UICONTROL European Union]**&#x200B;做為&#x200B;**[!UICONTROL Region]** （僅限生產）。

歐盟區域的基本生產URL為：

* 管理員： `https://eu1.admin.commerce.adobe.com`
* REST和GraphQL： `https://eu1.api.commerce.adobe.com`

![Cloud Manager建立執行個體對話方塊，包含區域欄位](./assets/create-instance.png){width="600" align="center" zoomable="yes"}

{{aco-release}}

>[!ENDSHADEBOX]
