---
title: 設定您的店面
description: 瞭解如何設定您的 [!DNL Adobe Commerce Optimizer] 店面。
role: Developer
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 專案(Adobe管理的SaaS基礎結構)。"
exl-id: 2b4c9e98-a30c-4a33-b356-556de5bd721a
source-git-commit: c00cb55bd7b61d6506ee8b9b81d28118c1adde00
workflow-type: tm+mt
source-wordcount: '1303'
ht-degree: 0%

---

# 設定您的店面

本指南將引導您使用Adobe Edge Delivery Services為[!DNL Adobe Commerce Optimizer]執行個體設定店面。 您的店麵包含程式碼、範例內容，以及產品詳細資訊頁面和產品探索（搜尋和篩選）的支援。

**預計完成時間：** 30-45分鐘

## 先決條件

* **GitHub帳戶**，可以建立存放庫並設定為本機開發(github.com)
* **[!DNL Adobe Commerce Optimizer]執行個體**，包含範例資料及已設定的目錄檢視和原則
   * 如需安裝程式指示，請參閱[新增範例資料](get-started.md#add-sample-data)。

### 必要的執行個體資料

開始之前，請先從您的[!DNL Adobe Commerce Optimizer]執行個體收集下列資訊：

* **租使用者識別碼** （也稱為執行個體識別碼）
   * 可從[執行個體詳細資訊頁面](get-started.md#manage-instances)取得
* 您執行個體的&#x200B;**GraphQL端點**
   * 可從[執行個體詳細資訊頁面](get-started.md#manage-instances)取得
* 全域目錄檢視的&#x200B;**目錄檢視識別碼**
   * 可從[目錄詳細資料頁面](./setup/catalog-view.md#manage-catalog-view)取得
* 目錄檢視的&#x200B;**Source地區設定**
   * 範例資料的預設值為`en_US`

>[!NOTE]
>
>試用存取客戶可在建立執行個體時收到的歡迎電子郵件中找到GraphQL端點。 試用例項已預先設定範例資料、目錄檢視和原則。

## 設定步驟

1. **[建立您的店面專案](#create-your-storefront-project)** — 使用[網站建立工具](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator)建立新的店面專案，其中包含樣版程式碼、範例內容和設定檔。

1. **[自訂店面設定](#customize-the-storefront-configuration)** — 更新存放庫中的`config.json`檔案，以連線至您的[!DNL Adobe Commerce Optimizer]執行個體。

1. **[驗證您的設定](#verify-your-setup)** （10分鐘）
   * 預覽您的店面網站
   * 測試產品詳細資料頁面和搜尋功能

## 建立您的店面專案

「場地建立者」工具會建立包含下列元件的完整店面專案：

* **網站**：包含樣版內容的店面登陸頁面
* **代碼**：儲存庫包含樣版來源檔案
* **Content**：具有網站內容檔案的檔案製作環境
* **Commerce設定**：執行個體特定設定的`config.json`檔案

### 步驟1：產生專案

1. 開啟[網站建立者工具](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator)

   ![[!DNL Site Creator tool]](./assets/storefront-setup-site-creator.png){width="700" zoomable="yes"}

1. 選取&#x200B;**建立新網站（程式碼與內容）**。

1. 完成站台設定：

   * **GitHub組織/使用者名稱**：輸入您的GitHub使用者名稱或組織名稱
   * **網站名稱**：選擇店面的描述性名稱
   * **Commerce GraphQL端點（選用）**：輸入您[!DNL Adobe Commerce Optimizer]執行個體的GraphQL端點

1. 按一下&#x200B;**建立網站**，使用店面樣板程式碼建立GitHub存放庫。

   建立存放庫時，網站建立者會更新並提示您安裝程式碼同步應用程式。

### 步驟2：安裝程式碼同步應用程式

1. 按一下&#x200B;**[!UICONTROL Install AEM Code Sync App]**&#x200B;以在新索引標籤中開啟程式碼同步處理安裝程式。

1. 設定程式碼同步應用程式：
   * 選取您的GitHub組織，然後按一下&#x200B;**[!UICONTROL Configure]**。
   * 在程式碼同步處理介面中，按一下&#x200B;**[!UICONTROL Only select repositories]**。
   * 按一下&#x200B;**[!UICONTROL Select repositories]**&#x200B;功能表，然後選擇您建立的店面程式碼存放庫。
   * 按一下&#x200B;**[!UICONTROL Save]**&#x200B;註冊您的存放庫。

1. 返回開啟網站建立者的瀏覽器視窗，然後按一下&#x200B;**建立網站**。

   「網站建立者」會將店面樣板內容複製到檔案製作環境。 此程式需要1-2分鐘。

### 步驟3：儲存專案連結

1. 在網站詳細資訊區段中，檢閱店面專案的連結：

   ![[!DNL Storefront setup complete]](./assets/storefront-setup-complete.png){width="700" zoomable="yes"}

   使用這些連結來管理您的店面程式碼、內容和設定。

1. 複製並儲存這些連結以供日後參考：按一下**[!UICONTROL Copy]。

## 設定您的店面

更新您的店面設定以連線至您的[!DNL Adobe Commerce Optimizer]執行個體。

1. 使用您先前儲存的連結開啟設定管理員：

   `https://da.live/sheet#/<username or org>/<repo name>/config.json`

1. 找到組態中的`cs` （目錄服務）區段。

1. 將預留位置值取代為您的例項值。 請參閱[必要條件](#prerequisites)。

   ```json
   "cs": {
      "AC-View-ID": "{catalogViewId}",
      "AC-Environment-ID": "{tenantId}",
      "AC-Source-Locale": "en_US"
   }
   ```

1. 儲存組態檔。

>[!NOTE]
>
>組態變更可能需要幾分鐘的時間才能傳播。 如果您沒有立即看到資料，請等待2-3分鐘再進行疑難排解。

## 驗證您的設定

測試您的店面，以確保它已正確連線到您的[!DNL Adobe Commerce Optimizer]執行個體。

### 步驟1：檢視您的店面首頁

1. 導覽至您的即時預覽URL：

   `https://main--{SITE}--{ORG}.aem.live`

   將`{ORG}`和`{SITE}`取代為您的GitHub組織和網站名稱。

1. **成功標準**：您應該會看到包含樣版內容的店面首頁。

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

### 步驟2：測試產品詳細資料頁面

檢視預設產品詳細資料頁面，以驗證產品資料是否正確載入。

1. 導覽至範例產品頁面：
   `https://main--{SITE}--{ORG}.aem.live/products/placeholder/{sku}`

   使用範例資料中的任何SKU，例如：
   `https://main--{SITE}--{ORG}.aem.live/products/placeholder/aur-flu-tir-std-2017`

   對於預設店面，您可以使用路由中的`placeholder`值來檢視產品。 當您開始自訂店面時，您可以自訂店面程式碼，以根據目錄中定義的產品路由設定產品詳細資料頁面的路徑。

   >[!TIP]
   >
   >從您[執行個體中的](./setup/data-sync.md)資料同步[!DNL Adobe Commerce Optimizer]頁面檢視可用的SKU。

1. **成功標準**：頁面應顯示：
   * 產品名稱、說明和定價
   * 產品影像
   * 加入購物車功能
   * 從您的[!DNL Adobe Commerce Optimizer]執行個體擷取的資料

   ![[!DNL Default product detail page showing a product from the sample data]](./assets/storefront-boilerplate-product-page.png){width="700" zoomable="yes"}

### 步驟3：測試預設搜尋功能

測試預設的產品功能，包括搜尋和篩選。

1. 在店面首頁上，按一下標題中的放大鏡圖示。

1. 輸入搜尋字串`tires`並按&#x200B;**Enter**。

1. **成功標準**：您應該會看到：
   * 包含輪胎產品的搜尋結果頁面
   * 側欄中的篩選選項
   * 包含影像和定價的產品清單

   ![[!DNL View search results page]](./assets/storefront-with-aco-search-results-page.png){width="675" zoomable="yes"}

1. 按一下任何輪胎產品以檢視其詳細資訊頁面。

   ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

## 疑難排解

如果您在設定期間遇到問題，請使用網頁檢視窗主控台來檢查錯誤。 此外，請嘗試清除瀏覽器快取或使用其他瀏覽器。

使用下列指南檢查常見問題：

### 常見問題

| 問題 | 症狀 | 解決方案 |
|-------|----------|----------|
| **程式碼同步安裝失敗** | 無法完成程式碼同步處理設定 | <ul><li>確保您擁有GitHub組織的管理員存取權。</li><li>嘗試使用個人存放庫而非組織。</li><li>請檢查GitHub許可權，然後再試一次。</li></ul> |
| **網站未載入** | 404或連線錯誤 | <ul><li>驗證您的網站URL格式： `https://main--{SITE}--{ORG}.aem.live`</li><li>檢查是否已正確安裝程式碼同步應用程式。</li><li>確儲存放庫是公用或正確設定的。</li></ul> |
| **未顯示任何產品資料** | 產品頁面顯示預留位置或錯誤 | <ul><li>驗證`config.json`中的設定值</li><li>在[!DNL Adobe Commerce Optimizer]執行個體中，檢查[資料同步]頁面以確認是否已載入範例產品。 如果沒有可用的產品，請重新載入範例資料，或使用[資料擷取API](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/using-the-api/#make-your-first-request)新增產品。 請稍候幾分鐘，讓設定變更傳播出去。</li><li>嘗試使用[檔案中設定的相同標頭，使用銷售服務](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/use-cases/#return-product-details)產品查詢`config.json`擷取產品詳細資料。 如果您可以擷取資料，則可能是目錄檢視設定發生問題或索引錯誤。</li></ul> |
| **搜尋未傳回任何結果** | 空白的搜尋結果頁面 | <ul><li>確認您可以使用[檔案中設定的相同標頭，使用Merchandising Services &#x200B;](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/use-cases/#product-search)productSearch查詢`config.json`擷取產品搜尋結果。 如果您可以擷取資料，則可能是目錄檢視設定發生問題或索引錯誤。</li><li>確認`config.json`檔案中的目錄檢視識別碼符合[!DNL Adobe Commerce Optimizer]中的目錄檢視識別碼。</li><li>在Adobe Commerce Optimizer中，驗證您在店面頁首設定中所使用的原則、地區設定和價格簿的設定。</li><li>確認已正確設定搜尋的[屬性中繼資料設定](https://developer.adobe.com/commerce/services/reference/rest/#operation/createProductMetadata)。</li></ul> |

### 驗證檢查清單

在繼續下一步之前，請確認下列事項，確定您的店面運作正常：

![檢查清單](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg)組態值符合您的執行個體設定<br>
![檢查清單](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg)店面首頁載入無錯誤<br>
![檢查清單](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg)至少一個產品詳細資料頁面顯示完整資訊<br>
![檢查清單](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg)搜尋功能傳回相關結果<br>
![檢查清單](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg)產品影像載入正確<br>
![檢查清單](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg)組態值符合您的執行個體設定<br>

### 取得協助

如果問題仍然存在：

* 檢閱[Adobe Commerce Storefront檔案](https://experienceleague.adobe.com/developer/commerce/storefront/)
* 檢視[Adobe Commerce Optimizer開發人員指南](https://developer.adobe.com/commerce/services/optimizer/)
* 造訪[Adobe Commerce支援資源](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview)

## 後續步驟

設定並驗證店面後，您可以：

1. **[安裝Sidekick](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/#install-and-configure-sidekick)** — 直接從您的網站編輯、預覽和發佈內容的瀏覽器延伸模組

2. **[設定本機開發環境](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/#set-up-local-environment)** — 建立本機環境，以自訂您的店面程式碼和內容

### 學習與探索

* **[完成端對端使用案例](./use-case/admin-use-case.md)** — 深入瞭解使用[!DNL Adobe Commerce Optimizer]的店面設定和目錄管理

* **[探索店面自訂](https://experienceleague.adobe.com/developer/commerce/storefront/setup/)** — 瞭解進階設定和組態選項

* **[使用Commerce下拉式功能表來自訂店面體驗](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/all/introduction/)** — 新增預先建立的元件以強化您的店面體驗

>[!MORELIKETHIS]
>
> 請參閱[Adobe Commerce Storefront檔案](https://experienceleague.adobe.com/developer/commerce/storefront/)，深入瞭解如何更新網站內容以及整合Commerce前端元件和後端資料。
