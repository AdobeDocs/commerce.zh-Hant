---
title: 限制和邊界
description: 瞭解 [!DNL Adobe Commerce Optimizer] 限制與界限，以規劃容量並避免效能問題。
role: Admin, Developer
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"
exl-id: 58d94da9-8d48-4513-8b6a-8e8c7c27a2a5
source-git-commit: f9ac230d448f071e6e8e6368b940f0c415abb02b
workflow-type: tm+mt
source-wordcount: '1350'
ht-degree: 0%

---

# 限制和邊界

[!DNL Adobe Commerce Optimizer]有兩種限制：

- **授許可權制** — 根據您購買的容量；可以購買其他套件來擴充。
- **系統界限** — 已修正限制，可保護系統資源並確保所有使用者的可靠效能。

您的使用量必須維持在這些限制內。 超過上限可能會導致延遲增加並要求節流。

## 請求額外容量

透過購買[授許可權制和系統界限](#license-limits-and-system-boundaries)一節中所述的授權套件，或針對不重複的使用案例協商自訂授權，可增加授許可權制。 請聯絡您的Adobe客戶代表以討論您的需求。

若有關於系統界限的問題，請連絡[Adobe支援](https://experienceleague.adobe.com/home?lang=zh-Hant#support)。

## 避免效能問題

遵循這些最佳實務，以保持在限制內並避免營運問題：

- **檢閱您的限制** — 在啟動新店面或行銷活動之前，請先瞭解您的[容量限制](#license-limits-and-system-boundaries)。
- **追蹤您的使用情形** — 使用內建的量度儀表板或CDN記錄。

## 授許可權制和系統界限

下表按功能區域概述許可證限制和系統邊界，並包含新增額外許可證以擴大適用容量的相關資訊。

### 環境限制

| **環境** | **描述** | **基底配置** | **可擴充？** |
| --- | --- | --- | --- |
| **沙箱環境** | 包含的沙箱環境數量 | 每個執行個體2個 | 是<p>為每個執行個體新增額外的環境授權</p> |
| **生產環境** | 包含的生產環境數量 | 每個執行個體1個 | 授權<p>為每個執行個體新增額外的環境授權</p> |

{style="table-layout:auto"}

### 目錄

| **功能** | **描述** | **基底配置** | **可擴充？** |
| --- | --- | --- | --- |
| 產品擷取率 | 已建立或已更新的產品數 | 每分鐘1K更新<p>每天最多可更新100,000個</p> | 是<p>新增一個授權套件：</p><ul><li>每分鐘5K更新<br>每天最多可更新500K</li> <li>每分鐘10K更新<br>每天最多可更新1M</li></ul><p>資料擷取的最大容量為每天100萬次更新。</p> |
| 產品裝載大小 | 使用API建立、更新或擷取產品資訊時允許的最大資料量 | 200 KB | 否 |
| 目錄變數 | 店面使用者可用的目錄檢視次數。<p>計算為(*目錄檢視次數×價格簿數量*)</p> | 100個變數 | 是<p>新增100個目錄變化授權套件</p> |
| 單一目錄來源中的產品 | 目錄中支援的SKU | 25萬SKU | 是<p>新增100K SKU授權套件</p> |
| 各產品的變體 | 每個產品允許的產品變數（大小、顏色組合）數量 | 10K | 否 |
| 目錄來源 | 目錄資料內容（例如PIM和ERP等地區設定或資料來源）的數量 | 50 | 否 |

{style="table-layout:auto"}

### 價格簿

| **功能** | **描述** | **基底配置** | **可擴充？** |
| --- | --- | --- | --- |
| 價格簿 | 每個執行個體允許的價格簿數量 | 根據[目錄變數](#catalog)的數量 | 是<br>增加目錄變化 |
| 每筆價格記錄的折扣 | 單一價格簿中可套用至產品價格的折扣數 | 10 | 否 |

{style="table-layout:auto"}

### 由AEM Assets支援的產品視覺效果

| **功能** | **描述** | **基底配置** | **可擴充？** |
| --- | --- | --- | --- |
| 產品視覺效果進階使用者 | 具有完整數位資產管理功能(包括AI工具、Adobe Express/Firefly整合和Content Hub共用)的授權使用者，可處理核心DAM任務和進階雲端原生功能以實現最佳效率。 | 2 | 是<p>升級至AEM Assets授權</p> |
| 產品視覺效果共同作業人員使用者 | 透過AEM Commerce整合存取及使用資產、使用Adobe Express和Firefly建立及編輯內容，以及（如果已啟用）透過Content Hub入口網站運用已核准的資產。 | 2 | 是<p>升級至AEM Assets授權</p> |
| 產品視覺效果儲存 | 為資產配置的儲存空間 | 1 TB儲存空間 | 否 |
| Dynamic Media使用情況 | 動態媒體處理作業的裕量，包括：<ul><li>影像傳送</li><li>智慧型影像</li><li>視訊傳送</li></ul><p>如需詳細資訊，請參閱下方的&#x200B;*計算Dynamic Media使用量*。 | 根據GMV<p>最小配置：每月500萬項作業</p> | 是<ul><li>購買其他操作的授權</li><li>升級至AEM Assets授權</li></ul> |
| 視訊傳送 | 視訊傳送或下載的備抵 | 300部影片，每部影片1分鐘 | 是<p>升級至AEM Assets授權</p> |
| 資產產生 | 存取用於建立影像的Adobe Express和Adobe Firefly generative AI | 無 | 單獨購買Generative AI積分 |

{style="table-layout:auto"}


>[!NOTE]
>
>**超級使用者**&#x200B;可以直接存取Adobe Express或在Adobe Commerce Optimizer中存取。 **Collaborator使用者**&#x200B;可以直接存取Adobe Express應用程式。 使用方式受[Adobe Express與Firefly產品特定授權條款](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/PSLT-AdobeExpressWFirefly-WW-2025v1.pdf)所規範。


>[!BEGINSHADEBOX 「計算Dynamic Media使用量」]

Dynamic Media使用方式會追蹤進入Adobe Commerce Optimizer中「產品視覺效果」元件的API請求，以促進下列其中一個動作：

- **影像傳送每次發生下列情況時，都會耗用一個Dynamic Media作業**：
   - 數位資產的&#x200B;**基本影像轉換**，例如調整大小、縮放、格式轉換、壓縮或裁切作業。
   - **靜態影像傳遞或下載**&#x200B;此數位資產或數位資產轉譯（視訊除外）
- **智慧型影像傳遞會針對單一數位資產的每個最佳化傳遞，自動產生最適合一般使用者裝置和瀏覽器的影像轉譯，耗用20個Dynamic Media作業**。
- **視訊傳送會花費20個Dynamic Media作業**，用於單一傳送或下載視訊或視訊的轉換變體。

>[!ENDSHADEBOX]


### 目錄檢視與原則

| **功能** | **描述** | **基底配置** | **可擴充？** |
| --- | --- | --- | --- |
| 目錄檢視 | 主目錄的可設定子集數目 | 根據[目錄變數](#catalog)的數量 | 是<br>增加目錄變化 |
| 每個目錄檢視的原則 | 允許的資料篩選器數 | 10 | 否 |
| 原則中的屬性值 | 可設定為篩選的產品特性數 | 100 | 否 |

{style="table-layout:auto"}

### 目錄店面

目錄店面功能的基本配置是根據GMV層級來決定。 此表格指出每項功能的最小配置。

| **功能** | **描述** | **基底配置** | **可擴充？** |
| --- | --- | --- | --- |
| 目錄擷取率 | 系統（店面、交易系統、ERP或其他）每月呼叫目錄API以從目錄中擷取資料的次數 | 根據GMV層級<p>最小配置：1000萬/月</p> | 是<p>每月新增100萬個授權套件要求</p> |
| 內容請求 | 向Commerce商店請求HTML頁面檢視或JSON API呼叫。 計為1次頁面檢視或5次API呼叫。 | 根據GMV層級<p>最小配置：2M/月</p> | 是<p>每月新增100萬個授權套件</p> |
| 店面GenAI變數 | 允許產生文字式內容 | 根據GMV層級<p>最小配置：1K個變數/月</p> | 是<p>單獨購買Generative AI積分</p> |

{style="table-layout:auto"}

>[!NOTE]
>
>產生影像需要布建至與Adobe Commerce Optimizer相同的IMS組織的Adobe Firefly授權。


### 產品探索

| **功能** | **描述** | **基底配置** | **可擴充？** |
| --- | --- | --- | --- |
| 每個搜尋要求的產品 | 搜尋結果中每頁傳回的最大產品數量 | 100 | 否 |
| 可篩選的屬性 | 可針對分層導覽和多面向啟用的產品特性（如顏色、大小、品牌或材質）數量 | 200 | 否 |
| 可搜尋的屬性 | 可設定為與產品目錄搜尋服務搭配使用的產品特性數 | 200 | 否 |
| 可排序的屬性 | 可設定用於決定搜尋結果值順序的產品特性數 | 50 | 否 |
| 搜尋分頁深度 | 可透過分頁存取的最大產品數量(例如，第100頁×100個產品/頁面) | 10K | 否 |
| Facet | 可篩選的產品屬性數量（例如品牌、顏色、大小、價格），可設定為協助購物者調整搜尋結果和瀏覽類別 | 100<p>必須是可篩選的屬性</p> | 否 |
| 各Facet選項 | 購物者可從清單中選取的可篩選產品屬性值(例如「紅色」、「藍色」代表顏色；「小」、「Medium」代表大小)的數量 | 100 | 是<p>可透過支援要求提高</p> |

{style="table-layout:auto"}

### Recommendations

下列功能適用於產品建議。 [!DNL Adobe Commerce Optimizer]不支援其他Adobe Commerce產品中提供的部分功能。

| **功能** | **描述** | **基底配置** | **可擴充？** |
| --- | --- | --- | --- |
| 使用中的建議單位 | 店面上的即時建議元件數量（例如「已檢視客戶」或「您可能也喜歡」） | 50 | 否 |
| 類別或屬性包含/排除 | 將產品篩選為符合建議資格的特定集合 | 不支援 | |
| 預覽建議 | 發佈前預覽建議在店面上的顯示方式 | 不支援 | |

{style="table-layout:auto"}

### 擴充性

| **功能** | **描述** | **基底配置** | **可擴充？** | **附註** |
| --- | --- | --- | --- | --- |
| Adobe Developer App Builder | 建置雲端原生擴充功能和整合的能力 | 根據GMV層級<p>最小配置：1包/年</p> | 是<p>新增其他套件</p> | 如需每個元件定義的限制，請參閱：<ul><li>[App Builder產品說明](https://helpx.adobe.com/tw/legal/product-descriptions/adobe-developer-app-builder.html)每個套件定義的限制。</li><li>[&#x200B; &#x200B;](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings)App Builder執行階段指南&#x200B;*中的系統設定和限制*。</li><li>[App Builder儲存需求](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/)</li></ul> |

{style="table-layout:auto"}

<!--## How to size your solution

Ask your Adobe representative for a list of available packages to determine which most closely matches your project

To accurately size your Adobe Commerce Optimizer solution, follow these steps:

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
   * Add-On: 10 × dynamic media packs (1M each) -->
