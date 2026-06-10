---
title: '[!DNL Adobe Commerce Optimizer Connector]'
description: 瞭解目錄同步、搜尋和店面傳遞的 [!DNL Adobe Commerce] 與 [!DNL Adobe Commerce Optimizer] 之間的 [!DNL Adobe Commerce Optimizer Connector] 整合。
feature: Integration, Storefront, Configuration
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案（Adobe管理的PaaS基礎結構）和內部部署專案的Adobe Commerce 。"
autotag-review: '2026-06-09T19:00:00.000Z'
TQID: 'https://experienceleague.adobe.com/-C-XP5YYxwyGrkvVR6CDd-FpDybqnlaKMmFPKOKUbFA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
  - id: dad884f1-e840-49a1-970e-2f965bdbc410
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 6d4493db5e0714577a8800007cc6d2c552578fa4
workflow-type: tm+mt
source-wordcount: 1037
ht-degree: 0%

---

# Adobe Commerce Optimizer聯結器

[!DNL Adobe Commerce Optimizer Connector]是[!DNL Adobe Commerce] （雲端或內部部署）與[!DNL Adobe Commerce Optimizer]之間的原生第一方整合。 它將您的[!DNL Adobe Commerce]存放區的目錄和定價資料同步至[!DNL Adobe Commerce Optimizer]，因此您可以：

- 支援&#x200B;**AI驅動的產品探索與建議**
- 執行&#x200B;**高效能Headless店面** （包括由[!DNL Edge Delivery Services]提供支援的Commerce店面）
- 在單一位置分析&#x200B;**個之前和之後的**&#x200B;個KPI和資料同步健康狀態

[!DNL Adobe Commerce]保留您產品、價格和目錄結構的記錄系統。 [!DNL Adobe Commerce Optimizer]成為您的體驗和銷售層，為任何連線的店面或頻道提供快速且相關的結果。

## 主要優點 {#key-benefits}

| 優點 | 這對您有何意義 |
| --- | --- |
| **沒有要建置的自訂聯結器** | 使用支援的第一方整合，而非撰寫及維護客製化摘要和指令碼。 |
| **使用[!DNL Adobe Commerce Optimizer]**&#x200B;更快產生值 | 在您現有的[!DNL Adobe Commerce]部署上開啟AI 搜尋、建議和Headless店面。 |
| **與Commerce領域對齊** | 自動將網站、商店檢視和客戶群組對應到[!DNL Adobe Commerce Optimizer]個目錄建構（目錄來源和價格簿）。 |
| **作業可見度** | 從專用的[!UICONTROL Data Feed Sync Status]檢視監視摘要健康狀態、上次同步時間和每個SKU的狀態。 |
| **通往SaaS的未來可用路徑** | 提供從PaaS到[!DNL Adobe Commerce as a Cloud Service] + [!DNL Adobe Commerce Optimizer]的低風險現代化路徑，無需重新平台。 |

## 聯結器架構 {#connector-architecture}

下圖說明聯結器的端對端架構，從[!DNL Adobe Commerce]到[!DNL Adobe Commerce Optimizer]，再到店面及結帳系統。

![Adobe Commerce Optimizer Connector端對端架構圖](./assets/aco-connector-end2end-architecture.png){width="700" zoomable="yes"}

在此架構中：

- [!DNL Adobe Commerce] （在雲端或內部部署）是記錄和摘要製作者的系統
- 聯結器會匯出目錄、價格和類別摘要
- [!DNL Adobe Commerce Optimizer]內嵌摘要資料並將摘要資料標準化至目錄來源、價格簿和目錄檢視
- 店面（[!DNL Edge Delivery Services]上的Commerce店面或自訂Headless組建）呼叫[!DNL Commerce Optimizer]個GraphQL API以進行探索和推薦，並呼叫[!DNL Adobe Commerce]或其他連線的協力廠商平台以進行購物車和結帳作業

## 聯結器如何與[!DNL Adobe Commerce]搭配運作

[!DNL Adobe Commerce Optimizer Connector]的運作方式是使用您現有的Commerce範圍（網站和商店檢視）和客戶細分來填入[!DNL Adobe Commerce Optimizer]目錄模型：

![將Commerce資料對應至Adobe Commerce Optimizer](./assets/storeview-to-catalogview-mapping.png){width="750" zoomable="yes"}

- **存放區檢視→目錄來源** — 每個存放區檢視在[!DNL Adobe Commerce Optimizer]中會變成個別的目錄Source。 該來源包含當地語系化的產品屬性以及任何商店檢視特有的資料
- **網站→價格手冊** — 每個[!DNL Adobe Commerce]網站對應到[!DNL Commerce Optimizer]中的一或多個價格手冊。 網站訂價與客戶群組訂價匯出為價格簿與價格輸入項
- **客戶群組→價格變體** — [!DNL Adobe Commerce]客戶群組定價會在相關的價格手冊中顯示為其他專案

[!DNL Commerce Optimizer]內嵌資料後，您可以設定：

- [!DNL Adobe Commerce Optimizer] Studio中的&#x200B;**目錄檢視與原則** （用於建立地區、品牌或客戶特定子集）
- **產品探索** （搜尋、Facet、銷售規則）
- **[!DNL Product Recommendations]**

當您啟用聯結器時，[!DNL Adobe Commerce]執行個體會保留目錄和價格資料的記錄系統。 當您在[!DNL Adobe Commerce]中更新資料時，聯結器會將這些更新同步到[!DNL Adobe Commerce Optimizer]執行個體。

>[!NOTE]
>
>如需設定[!DNL Adobe Commerce Optimizer]的詳細資訊，請參閱[[!DNL Adobe Commerce Optimizer] 銷售工具](../optimizer/overview.md#quick-tour)。

## 典型工作流程 {#typical-workflows}

這些工作流程說明團隊如何設定和使用[!DNL Adobe Commerce Optimizer Connector]。 如需有關如何設定整合及啟用這些工作流程的詳細資訊，請參閱[開始使用](get-started.md)。

### 初始設定 {#initial-setup}

請參閱&#x200B;_開始使用_&#x200B;指南中的[設定步驟](./get-started.md#configuration-steps)。

### 進行中的資料同步 {#ongoing-sync}

在初始設定後，聯結器支援：

- **完整目錄同步**&#x200B;以進行初始移轉或大型結構變更
- 當產品或價格變更時，針對持續更新進行&#x200B;**差異同步**
- 針對目標摘要重新同步命令&#x200B;**&#x200B;**

下列摘要可用於[!DNL Adobe Commerce Optimizer Connector]：

- `products` — 產品資料
- `productAttributes` — 產品屬性的中繼資料
- `priceBooks` — 價格簿
- `prices` — 產品價格
- `categories` — 類別資料

如需其他詳細資訊，請參閱下列主題：

- 如需[!DNL Adobe Commerce] CLI重新同步作業，請參閱[CLI重新同步命令](../data-export/data-export-cli-commands.md#sync-using-cli-commands){target="_blank"}
- [[!DNL Commerce Optimizer Connector]模組和摘要端點](reference/connector-reference.md)
- [聯結器摘要的欄位對應](reference/field-mapping.md)

### 設定銷售與店面 {#merchandising-storefronts}

在[!DNL Adobe Commerce Optimizer]中有[!DNL Adobe Commerce]資料可用後，請使用[[!DNL Commerce Optimizer] Studio](https://experienceleague.adobe.com/en/docs/commerce/optimizer/overview#quick-tour)將銷售和店面體驗連結到您的同步目錄。

**若要在[!DNL Commerce Optimizer] Studio中設定銷售與店面：**

1. 從[!UICONTROL Store setup]功能表&#x200B;**建立目錄檢視與原則**。

   - 依品牌、地區、客戶區段或管道篩選目錄
   - 根據店面或合作夥伴強制執行資料存取規則

1. **從[!UICONTROL Merchandising]功能表設定產品探索與建議**。

   - 建立銷售規則、Facet、同義字和建議單位
   - 聯結器會將所有搜尋和建議設定解除安裝至[!DNL Commerce Optimizer] （「Commerce管理員」中的[!DNL Live Search]個規則和[!DNL Product Recommendations]不再套用至這些流程）

1. **連線店面**&#x200B;至[!DNL Commerce Optimizer]：

   - 針對由[!DNL Edge Delivery Services]提供支援的Commerce店面，請設定店面使用正確的Optimizer租使用者和目錄檢視，並透過Merchandising API呼叫搜尋和建議端點
   - 若是協力廠商店面，請使用Optimizer公用API或SDK進行搜尋和建議呼叫

   >[!NOTE]
   >
   >如需協力廠商整合的範例，請參閱 [!DNL Adobe Commerce Optimizer][&#128279;](../optimizer/developer/salesforce-connector.md)的Salesforce Commerce Connector 。

1. **在您的現有平台上維護簽出**：

   - 將購物車、結帳、訂單管理和客戶帳戶保留在[!DNL Adobe Commerce]或協力廠商平台中
   - 當您與外部結帳系統整合時，使用[!DNL App Builder]和[!DNL API Mesh]進行購物車移交

## 支援的情況 {#supported-scenarios}

聯結器是專為雲端和內部部署上具有[!DNL Adobe Commerce]的B2C商家所設計，這些商家想要採用[!DNL Adobe Commerce Optimizer]而不重建其後端。

**常見使用案例：**

- **僅更新店面**
保留您現有的[!DNL Adobe Commerce]後端，將PLP/Search/PDP移至[!DNL Edge Delivery Services]個由[!DNL Adobe Commerce Optimizer]提供支援的店面

- **正在縮放目錄和搜尋效能**
將大量目錄索引和搜尋解除安裝到[!DNL Adobe Commerce Optimizer]的SaaS服務，同時在[!DNL Adobe Commerce]中維持產品和價格所有權

- **遞增SaaS採用**
使用聯結器作為[!DNL Adobe Commerce as a Cloud Service] + [!DNL Adobe Commerce Optimizer]的跳板，並搭配相容的可撰寫目錄[!DNL Adobe Commerce]

## 責任與實作必要條件 {#responsibilities-prerequisites}

[!DNL Adobe Commerce]是產品、定價和客戶群組的真實來源。 在[!DNL Adobe Commerce]中進行變更；聯結器會將變更同步至[!DNL Adobe Commerce Optimizer]。

**[!DNL Adobe Commerce Optimizer]負責：**

- 目錄模型（目錄來源、價格簿、目錄檢視、原則）
- 產品探索和建議
- 店面量度、資料同步控制面板和成功量度報表

**聯結器不是：**

- 修改[!DNL Adobe Commerce]購物車、結帳或訂購流程
- 自動布建店面專案（Commerce Storefront / [!DNL Edge Delivery Services]個工具控點）

**開始之前：**

- 驗證[!DNL Adobe Commerce]是否符合最低版本和[!DNL Commerce Optimizer Connector]需求。 如需詳細資訊，請參閱[開始使用](get-started.md#requirements-to-use-the-integration)。
- 確定您擁有IMS組織存取權、[!DNL Adobe Commerce Optimizer]執行個體，以及必要的認證和區域詳細資料。

## 相關檔案 {#related-documentation}

- 設定整合併啟用關鍵工作流程： [開始使用 [!DNL Commerce Optimizer Connector]](get-started.md)
- 瞭解[!DNL Adobe Commerce Optimizer]概念和架構： [什麼是 [!DNL Adobe Commerce Optimizer]？](../optimizer/overview.md)
- 瞭解同步機制、初始化和錯誤處理： [聯結器同步管道](connector-sync-pipeline.md)
- 所有摘要的欄位層級資料對應： [聯結器摘要的欄位對應](reference/field-mapping.md)
- 使用GraphQL和套裝編碼整合Headless店面： [Headless店面整合](headless-storefront.md)
- 診斷同步和設定問題： [疑難排解](troubleshooting.md)
