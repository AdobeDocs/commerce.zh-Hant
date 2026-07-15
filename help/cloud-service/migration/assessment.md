---
title: 移轉評估
description: 瞭解如何閱讀Adobe Commerce PaaS移轉評估報告、解讀店面和後端複雜性訊號，以及使用Adobe AI開發人員工具開始建立Adobe Commerce as a Cloud Service的擴充功能。
feature: Cloud, Migration
role: Developer, Admin
level: Intermediate
nudge: true1
autotag-review: '2026-06-18T16:09:41.112Z'
TQID: 'https://experienceleague.adobe.com/-OrsBVtHRcEV5EzgHzzP0JVf0aQWfSO2Fu1R5F5jtAw'
product_v2:
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
subfeature_v2:
  - id: a743e5dc-8f37-4b5d-a848-03c32ca30598
role_v2:
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 4cd054b64c3b95fd50ab9bb682469ace7cc871a3
workflow-type: tm+mt
source-wordcount: 2497
ht-degree: 0%

---


# 移轉評估

>[!IMPORTANT]
>
> 移轉評估只有在將[!DNL Adobe Commerce on Cloud Infrastructure]或[!DNL Adobe Commerce on-premises]個專案移轉到[!DNL Adobe Commerce as a Cloud Service]時才可用。

Commerce移轉評估是對您現有Adobe Commerce實作的自動分析。 Adobe的工具會掃描您的Commerce程式碼基底，並產生結構化報表，以清查所有建置、自訂或修改的內容。 報表接著會指出對程式碼基底所做的自訂如何影響移轉至[!DNL Adobe Commerce as a Cloud Service]。

可以在`https://experience.adobe.com/@<ims-org-name>/commerce-migration-assessment/shared-assessments`存取已處理的移轉評估報告。 除了最初共用您的專案程式碼基底外，不需要存取您的生產環境。

**評定提供：**

- 依型別和影響層級組織您商店中每個自訂模組的完整詳細目錄
- 從風險預測性量度計算的移轉複雜性評等（高、Medium或低）
- 需要規劃移轉計畫的最高影響力後端和店面區域的優先順序檢視
- 每個自訂模組的說明，可作為AdobeAI開發人員工具的直接輸入

## 瞭解移轉評估報告

報告分為三個索引標籤： **[!UICONTROL Summary]**、**[!UICONTROL Module Reports]**&#x200B;和&#x200B;**[!UICONTROL Report Reliability]**。

>[!NOTE]
>
>並非報表的所有區段都適用於每個商店。 此評估旨在涵蓋所有可能的自訂型別和複雜性驅動因素，但您的商店只有此處所列區段的子集。

## 摘要標籤

「**[!UICONTROL Summary]**」索引標籤提供整理到下列區域的主要訊號概觀：

- 移轉複雜性
- 檔案型別劃分
- 影響最大的模組
- 移轉驅動程式
- 自訂劃分

### 移轉複雜性

移轉複雜性區段包含您商店整體的評估評等。 它說明分數的計算方式，並突顯您的主要風險驅動因素。

**移轉複雜性和複雜性分數**

![顯示加權分數、主要風險驅動程式和關鍵量度的移轉複雜性區段](../assets/assessment-migration-complexity.png){width="600" zoomable="yes"}

複雜性分數會根據移轉的難度來加權每個輸入。 此分數會使用固定臨界值對應至移轉複雜性評等：

| 評等 | 評分範圍 | 典型的移轉方法 |
| --- | --- | --- |
| 低 | 150或以下 | 標準移轉 — 透過付款提供者協調直接移轉，以及將資料移轉作為平行工作流程。 |
| Medium | 151-375 | 模組化移轉 — 在區段中移轉，分類高影響力的自訂模組。 |
| 高 | 375以上 | 分階段移轉，可能持續12至24個月。 |

**自訂模組比率**

![自訂模組比率量度資料列顯示自訂模組百分比、協力廠商模組、自訂主題計數、重要掛接、檔案總數和PHP程式碼基底大小](../assets/assessment-custom-module-ratio.png){width="600" zoomable="yes"}

專為您實作建置的模組百分比。 比例較高表示必須對更多自訂程式碼進行稽核和移轉。 客戶的平均自訂模組比率約為62%。

>[!TIP]
>
>自訂模組比例是範圍訊號，而非複雜性訊號。 如果商店中有80%的自訂模組是隔離式的，而且風險較低，比起風險較高40%的自訂模組更容易移轉。 使用「複雜性分數」和鏈衝突數來評估難度。 使用自訂模組比率來預估數量。

**檔案型別劃分**

![檔案型別劃分資料表，列出具有檔案計數和程式碼行的副檔名](../assets/assessment-file-type-breakdown.png){width="600" zoomable="yes"}

程式碼基底中檔案數的清單，依型別組織。

**影響最高的模組**

![最高影響模組清單，顯示模組名稱、說明、影響評等和連結計數](../assets/assessment-highest-impact-modules.png){width="600" zoomable="yes"}

存放區中需要最多移轉注意的特定模組精選清單。 這些模組通常是與結帳、付款或訂單管理互動的模組。 每個高影響力模組都需要各自的移轉計畫。 此清單是與您的技術團隊交談的最佳起點。

### 店面複雜性

![店面複雜性區段顯示自訂主題名稱空間、總區塊計數、配置XML檔案、核心控制代碼覆寫和可操作的訊號](../assets/assessment-storefront-complexity.png){width="600" zoomable="yes"}

「店面複雜性」區段顯示移轉店面前端展示層所需的工作。 此工作流程與後端程式碼移轉不同的工作流程，由前端開發人員處理，通常需要單獨的規劃對話。

>[!NOTE]
>
>商店的後端複雜度可能較低，店面複雜度可能較高。 在設定移轉作業範圍之前，請務必檢閱這兩個區段。

- 自訂主題 — 商店自訂主題的名稱空間（例如，BrandName_Theme）。 自訂佈景主題存在表示[!DNL Adobe Commerce as a Cloud Service]需要完整佈景主題重新建置。 每個具有自訂主題名稱空間的評估存放區都必須規劃專用的前端移轉工作流程。

- 區塊總數 — 您存放區中的區塊和範本(.phtml)檔案數目。 區塊是主要伺服器端轉譯成品，每個區塊代表個別移轉任務。

| 區塊計數 | 付出 |
| --- | --- |
| 100以下 | 基線 — 標準工時 |
| 100-300 | Medium — 規劃結構化的前端波動 |
| 超過300個 | 高 — 作為專用工作流程排定優先順序 |

### 移轉驅動程式

![移轉驅動程式區段顯示自訂足跡、外掛程式和觀察者，以及工作評等的「類別偏好設定」卡](../assets/assessment-migration-drivers.png){width="600" zoomable="yes"}

「移轉驅動程式」區段會顯示驅動複雜度評等的前幾個因素。

| 驅動程式 | 定義 |
| --- | --- |
| 自訂空間 | 相對於總體實作的自訂程式碼整體數量 |
| 外掛程式和觀察者 | 在執行階段攔截核心平台行為的程式碼 |
| 類別偏好設定 | 脆弱的自訂模式，會完全取代核心類別，並在升級時無訊息中斷 |
| 資料模型 | 自訂和修改的資料庫結構 |
| 整合 | 外部系統已連線至您的商店 |

每個驅動程式出現時會有「高」、「Medium」或「低」工作量。 設定範圍及規劃時，請先處理最高評等的驅動程式。

### 資料模型

![資料模型區段顯示自訂表格、核心表格修改和關鍵EAV屬性的計數](../assets/assessment-data-model.png){width="600" zoomable="yes"}

「資料模型」段落會顯示自訂表格的計數、[!DNL Adobe Commerce]核心資料庫表格的修改，以及關鍵實體屬性值(EAV)屬性。

核心表格修改是最難移轉的類別，因為它們會在特定平台結構描述版本上建立相依性，且對「複雜性分數」公式有較高影響。

>[!TIP]
>
>如果您的報表列出超過15項核心表格修改，請在範圍後端模組移轉之前規劃專用的資料移轉工作流程。

## 自訂劃分

![自訂劃分割槽段列出所有具有計數和影響指標的自訂類別](../assets/assessment-customization-breakdown.png){width="600" zoomable="yes"}

「自訂劃分」區段提供您商店中每個自訂類別的詳細量度。

>[!NOTE]
>
>並非所有子區段都會顯示在每個報表中，只有程式碼基底中偵測到的類別才會顯示。
>
>影響前端展示層的子區段是與後端程式碼移轉不同的工作流程，通常需要個別的計畫交談。
>
>商店的後端複雜度可能較低，而前端複雜度可能較高。 在設定移轉作業範圍之前，請務必檢閱後端和店面相關的子區段。

### 配置XML

配置XML檔案的數目及其作業總數。 版面XML定義每個頁面的結構，包括出現哪些區塊、這些區塊出現的容器，以及這些區塊下的頁面型別。

含有許多作業的高檔案計數代表重要的頁面結構自訂必須重新架構。

### 核心控制代碼覆寫

您的配置XML覆寫核心[!DNL Adobe Commerce]頁面控制代碼的地點數目（例如，`checkout_cart_index`或`catalog_product_view`）。 核心控制代碼覆寫是風險最高的配置訊號，因為它們會在平台層級修改頁面結構，而且需要明確重建。

| 覆寫計數 | 付出 |
| --- | --- |
| 0 | 無核心配置覆寫 |
| 1-3 | 執行階段風險 — 每個覆寫都需要明確重新建置配置 |
| 4個或更多 | 關鍵 — 規劃專用配置移轉衝刺 |

### 個區塊

存放區中的區塊和範本(`.phtml`)檔案數目。 區塊是主要伺服器端轉譯成品。 每個區塊代表一個分散式移轉工作。

| 區塊計數 | 付出 |
| --- | --- |
| 100以下 | 基線 — 標準工時 |
| 100-300 | Medium — 規劃結構化的前端波動 |
| 超過300個 | 高 — 作為專用工作流程排定優先順序 |

### 高風險區塊

接觸核心轉譯路徑的區塊，例如結帳轉譯、購物車顯示和類似的前端表面。 任何高風險區塊都需要在排程前進行個別移轉評估。

### 主題和電子郵件範本

您商店的自訂主題的名稱空間（例如，`BrandName_Theme`）。 自訂佈景主題存在表示需要完整佈景主題重新建置。 每個具有自訂主題名稱空間的評估存放區都必須規劃專用的前端移轉工作流程。

### 範本覆寫（核心已修改）

已覆寫的核心[!DNL Adobe Commerce] `.phtml`範本數目。 每個核心範本覆寫都會建立該範本特定版本的相依性。 平台更新會變更範本，以無訊息方式中斷覆寫。

### 需要外掛程式移轉

[!DNL Adobe Commerce as a Cloud Service]對店面使用模組化放置元件架構，包括結帳、購物車和產品詳細資訊。 這些曲面的自訂必須重建為下拉元件。 這些自訂功能涵蓋廣泛的功能，例如新增自訂結帳步驟、修改購物車顯示邏輯或擴充產品詳細資料頁面。

[!UICONTROL Drop-in migration required]欄位指出哪些店面區域需要插入式重建。

>[!IMPORTANT]
>
>如果&#x200B;**簽出**&#x200B;列為外掛程式移轉需求，請規劃專用的簽出外掛程式工作流程。 這項工作是最複雜且關鍵業務的店面移轉工作。

## 「模組報表」標籤

![顯示可搜尋模組清單的[模組報告]索引標籤，內含影響篩選器和詳細的模組分析面板](../assets/assessment-module-reports-tab.png){width="600" zoomable="yes"}

**[!UICONTROL Module Reports]**&#x200B;索引標籤包含您商店中每個自訂模組的專用專案。 請與您的技術團隊分享此資訊。

對於每個模組，報表都會顯示：

| 欄位名稱 | 定義 |
| --- | --- |
| 作用 | 自訂模組的用途和業務功能的說明 |
| 影響層級 | 根據模組觸及的商務行為，**高**、**Medium**&#x200B;或&#x200B;**低**&#x200B;影響 |
| 勾點計數 | webhook的數量，表示此模組會攔截核心平台行為的位置數 |
| 移轉建議 | **重新建置**，**重新調整**，**以原生功能取代**，或&#x200B;**移除** |
| 相依性 | 此模組與哪些其他模組互動，可告知移轉順序 |

**工作流程**

1. 請先篩選為&#x200B;**高影響**&#x200B;模組。 這些正是移轉的最大努力和成本。
1. 針對每個自訂模組，決定下列問題的答案：
   - 此模組是否仍在使用中？
   - 是否可由原生[!DNL Adobe Commerce as a Cloud Service]功能取代模組？
   - 如果必須重建模組，取代模組需要提供哪些功能？
1. 識別可淘汰或取代的自訂模組。 每一個都會在寫入任何程式碼之前縮小移轉範圍。
1. 複製每個自訂模組的說明，並附上&#x200B;**重新建置**&#x200B;移轉建議。 這些說明可以直接提供給Adobe的AI開發人員工具，如需詳細資訊，請參閱[適用於Commerce擴充性的AI開發人員工具](#ai-developer-tools-for-commerce-extensibility)。

## 參考資料：主要條款

| 詞語 | 定義 |
| --- | --- |
| **模組** | 自訂、獨立功能的套件。 您的商店可能有20個模組到數百個模組。 |
| **外掛程式（攔截器）** | 此程式碼會擷取Commerce函式並變更其執行之前、期間或之後的行為。 |
| **觀察者** | 監聽特定平台事件（例如「已下訂單」）並在該事件觸發時執行自訂邏輯的程式碼。 |
| **喜好設定（類別覆寫）** | 一種脆弱的自訂型別，可完全取代核心Commerce類別，當平台升級該類別時，這種型別會無訊息中斷。 |
| **鏈結衝突** | 當兩個或多個外掛程式攔截相同函式，且其中一個無法將控制項傳遞至下一個外掛程式時。 這可能會導致功能以無訊息方式停止運作，而不會出現錯誤訊息。 |
| **核心資料表修改** | 對Commerce的內建資料庫表格進行結構性變更，這會對特定平台架構版本建立無法復原的相依性。 這些選項具有「複雜性分數」公式中的最高權重。 |
| **Entity-Attribute-Value (EAV)** | 新增至產品或客戶的彈性自訂欄位，例如，自訂「保固期間」欄位。 高的EAV數量會增加資料遷移的複雜性。 |
| **勾點密度** | 每個模組的外掛程式和觀察者平均數量。 密度較高表示客製化更緊密地編織在核心平台中。 |
| **下拉式清單** | [!DNL Adobe Commerce's]個用於店面元件的模組化方法（包括結帳、購物車和產品詳細資料頁面）。 在[!DNL Adobe Commerce on Cloud Infrastructure]或[!DNL Adobe Commerce on Premises]的自訂簽出行為通常需要在[!DNL Adobe Commerce as a Cloud Service]上重新建置下拉式清單。 |
| **App Builder** | Adobe的程式外擴充性平台，以及取代程式內PHP擴充功能，建置自訂功能的建議方式。 |
| **配置XML** | 定義哪些區塊會顯示在哪些頁面上的組態檔。 必須為[!DNL Adobe Commerce as a Cloud Service's]頁面結構重新架構自訂配置XML。 |
| **核心控制代碼覆寫** | 版面XML自訂，可全域修改核心Commerce頁面結構。 這些具有最高風險的移轉配置模式。 |

## 適用於Commerce擴充性的AI開發人員工具

您可以在&#x200B;**[!UICONTROL Module Reports]**&#x200B;標籤中使用模組說明，作為Adobe AI開發人員工具的提示。 工具可協助您建置和部署與[!DNL Adobe Commerce as a Cloud Service]相容的取代擴充功能。

### 工具提供的內容

Adobe的[AI開發人員工具適用於Commerce擴充性](https://developer.adobe.com/commerce/extensibility/developer-agent/)，包含兩項主要功能。

- [!DNL Adobe Commerce] [!DNL App Builder] MCP伺服器 — 模型內容通訊協定(MCP)整合，可將AI編碼助理直接連線至[!DNL Adobe Commerce]檔案、API和App Builder開發模式。 開發人員可以描述他們想要建置的內容，而MCP伺服器可提供Commerce感知的程式碼產生、架構指引，以及IDE內的部署自動化。
- 代理程式技能 — 涵蓋常見Commerce擴充性模式（例如REST API、結帳擴充功能、店面元件和事件導向整合）的預建AI技能。 技能可指導AI完成[!DNL Adobe Commerce as a Cloud Service]和[!DNL App Builder]專屬的架構、實作、測試和部署步驟。

#### 安裝AI工具

請參考[安裝AI開發人員工具](https://developer.adobe.com/commerce/extensibility/developer-agent/coding-tools)，以取得完整指示和特定的IDE設定。

**必要條件：** Node.js 22.x、npm 9.0.0或更新版本、Adobe I/O CLI。

安裝命令：

```bash
aio commerce extensibility tools-setup
```

### 從評估報告中建立提示

雖然評估為您提供開發藍圖，但AI工具可讓您的團隊在完整移轉計畫完成之前立即開始建立。

1. 開啟&#x200B;**[!UICONTROL Module Reports]**&#x200B;索引標籤並尋找具有&#x200B;**重新建置**&#x200B;建議的高影響模組。
1. 閱讀模組的說明，例如：

```shell-session
Manages custom shipping rate calculations based on customer account tier and order    weight thresholds.
```

1. 開啟IDE，例如GitHub Copilot、Cursor或Claude，並啟用Commerce擴充性MCP伺服器。
1. 使用模組說明來提示AI代理程式。
1. 檢閱支架式[!DNL App Builder]應用程式，並與代理程式反複運算以調整實作。

## 後續步驟

1. 開啟&#x200B;**[!UICONTROL Summary]**&#x200B;標籤。 請檢閱移轉複雜性和影響最高的模組，然後檢視自訂劃分子區段。 如果您的商店有自訂主題、高風險區塊或簽出下拉式清單清單，請規劃平行的前端工作流程和後端移轉。
1. 與您的技術團隊或開發合作夥伴共用&#x200B;**[!UICONTROL Module Reports]**&#x200B;標籤。 要求他們標幟不再使用中或可由[!DNL Adobe Commerce as a Cloud Service]功能取代的任何自訂模組。
1. 開始建立您的自訂。 使用模組說明作為AI工具輸入，開始建立與支架相容的擴充功能。
1. 與您的Adobe客戶團隊排程逐步解說通話。 Adobe可與您一同檢閱發現、回答有關特定模組和店面訊號的任何問題，並協助您針對複雜性設定檔規劃移轉方法。

## 資源

- [!DNL Adobe Commerce as a Cloud Service]
   - [概觀](../overview.md)
   - [移轉概述](./overview.md)
   - [評等擴充功能教學課程](../tutorials/ratings-extension.md)
   - [送貨方法教學課程](../tutorials/shipping-method-extension.md)
- 擴充性
   - [概觀](https://developer.adobe.com/commerce/extensibility/)
   - [AI開發人員工具](https://developer.adobe.com/commerce/extensibility/developer-agent/)
      - [最佳實務](https://developer.adobe.com/commerce/extensibility/developer-agent/best-practices)
      - [設定](https://developer.adobe.com/commerce/extensibility/developer-agent/coding-tools)
      - [技能與提示](https://developer.adobe.com/commerce/extensibility/developer-agent/skills-and-prompts)
      - [使用案例](https://developer.adobe.com/commerce/extensibility/developer-agent/use-cases)
   - [App Builder概觀](https://developer.adobe.com/app-builder/docs/intro_and_overview/)
   - [適用於Adobe Commerce的App Builder](https://experienceleague.adobe.com/zh-hant/docs/commerce-learn/tutorials/extensibility/adobe-developer-app-builder/introduction-to-app-builder)
   - 入門套件
      - [後端整合入門套件](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/)
      - [結帳入門套件](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/)
- 店面開發
   - [概觀](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=zh-Hant)
   - [Storefront AI技能](https://experienceleague.adobe.com/developer/commerce/storefront/boilerplate/ai-agent-skills/?lang=zh-Hant)

>[!TIP]
>
>請連絡您的解決方案客戶經理，以要求您現有執行個體的移轉評估。
