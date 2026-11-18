---
title: Adobe Commerce as a Cloud Service限制和邊界
description: 瞭解Adobe Commerce as a Cloud Service授許可權制和系統界限。 規劃容量、追蹤使用量，以及避免延遲和超過限制時的節流現象。
role: Admin, Developer
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和[!DNL Adobe Commerce as a Cloud Service]個專案（Adobe管理的SaaS基礎結構）。"
nudge: true
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: a13aaee57732f27b51a2d2acdd0ca3de364ee6ab
workflow-type: tm+mt
source-wordcount: '1378'
ht-degree: 1%
---
# 限制和邊界

[!DNL Adobe Commerce as a Cloud Service]套用&#x200B;**授許可權制**&#x200B;和&#x200B;**系統界限**，以定義專案可使用的容量：

- **授許可權制**&#x200B;是以您購買的容量為基礎，可透過購買其他套件加以擴充。
- **系統界限**&#x200B;是固定的限制，可保護系統資源並確保所有使用者的可靠效能。

>[!IMPORTANT]
>
> 您的使用量必須維持在這些限制內。 超過上限可能會導致延遲增加並要求節流。

## 請求額外容量

您可以購買[授許可權制與系統界限](#license-limits-and-system-boundaries)中說明的授權套件，或針對不重複的使用案例洽談自訂授權，以增加授許可權制。 請聯絡您的Adobe客戶代表以討論您的需求。

若有關於系統界限的問題，請連絡[Adobe支援](https://experienceleague.adobe.com/home?lang=en#support)。

## 避免效能問題

遵循這些最佳實務，以保持在限制內並避免營運問題：

- **檢閱您的限制** — 在啟動新店面或行銷活動之前，瞭解您的[容量限制](#license-limits-and-system-boundaries)。
- **追蹤您的使用情形** — 使用內建的量度儀表板或CDN記錄。

## 授許可權制和系統界限

下表按功能區域摘要說明許可證限制和系統界限，並包含使用其他許可證來擴充適用容量的相關資訊。

### 環境限制

| **環境** | **描述** | **基底配置** | **可擴充？** |
| --- | --- | --- | --- |
| **沙箱環境** | 包含的沙箱環境數量 | 每個執行個體2個 | 是<p>為每個執行個體新增額外的環境授權</p> |
| **生產環境** | 包含的生產環境數量 | 每個執行個體1個 | 是<p>為每個執行個體新增額外的環境授權</p> |

{style="table-layout:auto"}

### 目錄

| **功能** | **描述** | **基底配置** | **可擴充？** |
| --- | --- | --- | --- |
| 產品擷取率 | 已建立或已更新的產品數 | 每分鐘1K更新<p>每天最多可更新100,000個</p> | 是<p>新增一個授權套件：</p><ul><li>每分鐘5K更新<br>每天最多可更新500K</li><li>每分鐘10K更新<br>每天最多可更新1M</li></ul><p>資料擷取的最大容量為每天100萬次更新。</p> |
| 產品裝載大小 | 使用API建立、更新或擷取產品資訊時允許的最大資料量 | 200 KB | 否 |
| 類別 | 可分組在下的類別產品數量 | 6,000 | 否 |
| 產品數量 | 目錄中支援的SKU數量 | 25萬SKU | 是<p>新增100K SKU授權套件</p> |
| 各產品的變體 | 每個產品允許的產品變數（大小、顏色組合）數量 | 10K | 否 |
| 存放區檢視 | 存放區檢視前後關聯的數量（例如，地區） | 50 | 否 |
| SLA讓產品更新出現在搜尋中 | 產品建立/更新出現在店面搜尋中的時間 | 10 - 15分鐘 | 否 |

{style="table-layout:auto"}

### 簽出

| **功能** | **描述** | **基底配置** | **可擴充？** |
| --- | --- | --- | --- |
| 購物車中的產品 | 每個購物車允許的產品數 | 650 | 否 |
| 每個帳戶的客戶地址 | 每個帳戶允許的客戶地址數 | 2,000 | 否 |
| 購物車價格規則 | 根據一組條件對購物車中的專案套用折扣的購物車價格規則數 | 100,000 | 否 |
| 優惠券 | 與購物車價格規則搭配使用的優惠券代碼數 | 1,000,000 | 否 |

{style="table-layout:auto"}

<!--
# Price books

# | **Capability** | **Description** | **Base allocation** | **Expandable?** |
# | --- | --- | --- | --- |
# | Price books | The number of price books allowed per instance | Based on the number of [Catalog variations](#catalog) | Yes<br>Increase catalog variations |
# | Discounts per price record | The number of discounts that can be applied to a product price within a single price book | 10 | No |

{style="table-layout:auto"}
-->

### [!DNL Product Visuals]限制

| **功能** | **描述** | **基底配置** | **可擴充？** |
| --- | --- | --- | --- |
| 產品視覺效果進階使用者 | 具有完整數位資產管理功能（包括AI工具、[!DNL Adobe Express]/[!DNL Firefly]整合和Content Hub共用）的授權使用者，可處理核心DAM任務和進階雲端原生功能以獲得最佳效率。 | 2 | 是<p>升級至[!DNL AEM Assets]授權</p> |
| 產品視覺效果共同作業人員使用者 | 透過AEM Commerce整合存取及使用資產、使用[!DNL Adobe Express]和[!DNL Firefly]建立及編輯內容，以及（如果已啟用）透過Content Hub入口網站運用已核准的資產。 | 2 | 是<p>升級至[!DNL AEM Assets]授權</p> |
| 產品視覺效果儲存 | 為資產配置的儲存空間 | 1 TB儲存空間 | 否 |
| Dynamic Media使用情況 | 動態媒體處理作業的裕量，包括：<ul><li>影像傳送</li><li>智慧型影像</li><li>視訊傳送</li></ul><p>如需詳細資訊，請參閱下方的&#x200B;*計算Dynamic Media使用量*。 | 根據GMV （商品總值）<p>最小配置：每月500萬項作業</p> | 是<ul><li>購買其他操作的授權</li><li>升級至[!DNL AEM Assets]授權</li></ul> |
| 視訊傳送 | 視訊傳送或下載的備抵 | 300部影片，每部影片1分鐘 | 是<p>升級至[!DNL AEM Assets]授權</p> |
| 資產產生 | 存取用於建立影像的[!DNL Adobe Express]和[!DNL Adobe Firefly]產生AI | 無 | 單獨購買Generative AI積分 |

{style="table-layout:auto"}

>[!NOTE]
>
>**超級使用者**&#x200B;可以直接存取[!DNL Adobe Express]或在[!DNL Adobe Commerce as a Cloud Service]記憶體取。
>
>**Collaborator使用者**&#x200B;可以直接存取[!DNL Adobe Express]應用程式。 使用方式受[Adobe Express與Firefly產品特定授權條款](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/PSLT-AdobeExpressWFirefly-WW-2025v1.pdf)所規範。

>[!BEGINSHADEBOX 「計算Dynamic Media使用量」]

Dynamic Media使用方式會追蹤進入[!DNL Adobe Commerce as a Cloud Service]內「產品視覺效果」元件的API要求，以促進下列其中一個動作：

- **影像傳送每次發生下列情況時，都會耗用一個Dynamic Media作業**：
  - 數位資產的&#x200B;**基本影像轉換**，例如調整大小、縮放、格式轉換、壓縮或裁切作業。
  - **靜態影像傳遞或下載**&#x200B;此數位資產或數位資產轉譯（視訊除外）。
- **智慧型影像傳遞會針對單一數位資產的每個最佳化傳遞，自動產生最適合一般使用者裝置和瀏覽器的影像轉譯，耗用20個Dynamic Media作業**。
- **視訊傳送會花費20個Dynamic Media作業**，用於單一傳送或下載視訊或視訊的轉換變體。

>[!ENDSHADEBOX]

>[!NOTE]
>
>上述限制涵蓋容量與使用量配置。 如需產品視覺效果功能概觀和功能限制，請參閱[AEM Assets產品視覺效果](../optimizer/setup/product-visuals.md)。

<!--
### Catalog views and policies

| **Capability** | **Description** | **Base allocation** | **Expandable?** |
| --- | --- | --- | --- |
| Catalog views | Number of configurable subsets of your master catalog | Based on the number of [Catalog variations](#catalog) | Yes<br>Increase catalog variations |
| Policies per catalog view | Number of data filters allowed | 10 | No |
| Attribute values in a policy | Number of product characteristics that can be configured for filtering | 100 | No |
| [Restricted access key assignment](setup/private-catalog-view.md) | Number of restricted access keys that can be assigned to a single catalog view | 3 | No |
| RSA key size (restricted access keys) | Minimum and maximum key strength accepted for a restricted access key | 2048-bit minimum, 8192-bit maximum | No |
| Restricted access keys | Key revocation propagation delay | Up to 5 minutes, due to caching. Tokens signed by a removed key are denied once the delay elapses. | Not applicable |

{style="table-layout:auto"}
-->

### 目錄店面

目錄店面功能的基本配置是根據GMV （毛商品價值）層級來決定。 此表格指出每項功能的最小配置。

| **功能** | **描述** | **基底配置** | **可擴充？** |
| --- | --- | --- | --- |
| 目錄擷取率 | 系統（店面、交易系統、ERP或其他）每月呼叫目錄API以從目錄中擷取資料的次數 | 根據GMV層級<p>最小配置：1000萬/月</p> | 是<p>每月新增100萬個授權套件要求</p> |
| 內容請求 | 要求店面提供HTML頁面檢視或JSON API呼叫。 計為1次頁面檢視或5次API呼叫。 | 根據GMV層級<p>最小配置：每月200萬</p> | 是<p>每月新增100萬個授權套件</p> |
| 店面GenAI變數 | 允許產生文字式內容 | 根據GMV層級<p>最小配置：1K個變數/月</p> | 是<p>單獨購買Generative AI積分</p> |

{style="table-layout:auto"}

>[!NOTE]
>
>產生影像需要布建至與[!DNL Adobe Commerce as a Cloud Service]相同的IMS組織的[!DNL Adobe Firefly]授權。

### 產品探索

下列限制適用於店面產品搜尋、清單和銷售設定。

| **功能** | **描述** | **基底配置** | **可擴充？** |
| --- | --- | --- |---------------------------------------------------|
| 產品擷取 | 擷取具有`products`、`productSearch`、`refineProduct`和`variants`的產品資料時，每個[!DNL Catalog Service] GraphQL要求的最大SKU數。 將較大的請求分割為多個呼叫。 | 100 | 否 |
| 可篩選的屬性 | 可針對分層導覽和多面向啟用的產品特性（如顏色、大小、品牌或材質）數量 | 200 | 否 |
| 可搜尋的屬性 | 可針對目錄搜尋編制索引的產品特性數 | 200 | 否 |
| 可排序的屬性 | 搜尋和類別頁面上可作為排序選項的產品特性數。 | 50 | 否 |
| 搜尋分頁深度 | 透過搜尋分頁可存取的產品上限（例如，第100頁×100個產品/頁面） | 10K | 否 |
| Facet | 可篩選的產品屬性數量（例如品牌、顏色、大小、價格），可設定為協助購物者調整搜尋結果和瀏覽類別 | 100<p>必須是可篩選的屬性</p> | 是<p>可透過支援要求提高至500個</p> |
| 各Facet選項 | 購物者可在Facet中選取的可篩選產品屬性值數量（例如「紅色」、「藍色」代表顏色；「小」、「Medium」代表大小） | 100 | 是<p>可透過支援要求提高</p> |

{style="table-layout:auto"}

### Recommendations

下列功能適用於產品建議。 [!DNL Adobe Commerce as a Cloud Service]不支援其他Adobe Commerce產品中提供的部分功能。

| **功能** | **描述** | **基底配置** | **可擴充？** |
| --- | --- | --- | --- |
| 使用中的建議單位 | 店面上的即時建議元件數量（例如「已檢視客戶」或「您可能也喜歡」） | 產品推薦的每頁型別50個作用中單位，必要時具有明確的目錄模型範圍 | 否 |

{style="table-layout:auto"}
<!-- Talos complained about this even thought it was copied directly from the ACO version of this page. Commenting out for now, | Category or attribute inclusions/exclusions | Filter products to a specific set that qualifies for recommendations | Not supported | — | -->

### 擴充性

| **功能** | **描述** | **基底配置** | **可擴充？** | **附註** |
| --- | --- | --- | --- | --- |
| Adobe Developer App Builder | 建置雲端原生擴充功能和整合的能力 | 根據GMV層級<p>最小配置：1包/年</p> | 是<p>新增其他套件</p> | 如需每個元件定義的限制，請參閱：<ul><li>[App Builder產品說明](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html)。</li><li>[ *App Builder執行階段指南*&#x200B;中的系統設定和限制](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings)。</li><li>[App Builder儲存需求](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/)</li></ul> |

{style="table-layout:auto"}

<!--
## How to size your solution

Ask your Adobe representative for a list of available packages to determine which most closely matches your project

To accurately size your [!DNL Adobe Commerce as a Cloud Service] solution, follow these steps:

1. Review the available packages, and start with a package that most closely matches your requirements.
1. Review the capabilities and metrics to ensure they align with your business requirements.
1. Purchase add-on packages for any metrics where you require additional capacity.

This approach ensures your solution is accurately sized for your business needs.

### Example use cases

1. **Seasonal Catalog Expansion**

   * Need: +20K SKUs
   * Add-On: 2 × SKU Packs (10K each)

1. **High Traffic Surge**

   * Need: +3M content requests/month
   * Add-On: 3 × content request packs (1M each)

1. **Global Presence**

   * Need: Additional environments for testing
   * Add-On: +1 Production, +2 Sandbox instances

1. **GenAI or Media Needs**

   * Need: +10M dynamic media ops/month
   * Add-On: 10 × dynamic media packs (1M each)
-->
