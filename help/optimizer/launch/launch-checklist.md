---
title: 啟動檢查清單
description: 瞭解如何驗證 [!DNL Adobe Commerce Optimizer] 生產環境的設定、店面、SEO、CDN、整合、安全性、分析和測試。
solution: Commerce
feature: Integration, Storefront, Search, Catalog Management, Personalization
feature-set: Commerce
role: Admin, Developer
level: Intermediate
topic: Administration
recommendations: noCatalog
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 專案（Adobe管理的SaaS基礎結構）。"
source-git-commit: 37b8b8a334ca11daacfd3da03b0441e77329e2e1
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 0%

---


# 啟動檢查清單

使用此檢查清單來驗證您的生產[!DNL Adobe Commerce Optimizer]專案是否已設定、測試並準備好啟動。 與您的團隊一起處理每個區段，並在您自己的專案計畫或追蹤器中追蹤完成。 如需下列參考的產品功能和UI區域，請參閱[[!DNL Adobe Commerce Optimizer] 檔案](../overview.md)。

## 使用案例和架構 {#use-case}

當您傳送結合[!DNL Adobe Commerce Optimizer]和Edge Delivery Services (EDS)的B2C體驗與雲端例項上的現有Adobe Commerce時，請使用此檢查清單。

您的解決方案通常包含下列元件：

- **雲端** — 雲端上的Adobe Commerce可管理目錄資料、客戶、資產和購買流程（結帳、訂單管理、配送等）。
- **最佳化程式**—[!DNL Adobe Commerce Optimizer]提供銷售體驗。
- **店面**—Edge Delivery Services上的Adobe Commerce店面提供UI。
- **協力廠商服務** — 付款、送貨及稅捐提供者。
- **App Builder** — 擴充性。
- **API網格** — 要求路由。

## 驗證雲端上的Adobe Commerce {#verify-cloud}

確認雲端環境上的Adobe Commerce已準備好投入生產。

▢雲端執行個體為[已布建](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/start/new-project)。
▢測試與虛擬資料已從執行個體移除。
▢生產資料已載入執行個體上。
▢您知道[GraphQL端點](https://developer.adobe.com/commerce/webapi/graphql/)。
▢執行個體符合[準備啟動](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/launch/checklist)需求。

## 驗證Commerce Optimizer執行個體 {#verify-optimizer}

確認您的[!DNL Adobe Commerce Optimizer]生產執行個體已正確設定。

▢生產執行個體作用中。 請參閱[開始使用](../get-started.md)以瞭解如何布建它。
▢執行個體在正確的區域中。
▢環境型別為「生產」。
▢您知道組織ID、使用者端ID、擷取URL和Commerce Optimizer URL。 請參閱[開始使用](../get-started.md)。
▢設定的限制和界限符合您的Adobe客戶技術顧問(CTA)所確認的值。
▢測試成品和虛擬資料已從執行個體中移除。

## 驗證店面網站 {#verify-storefront-site}

確認您的Edge Delivery Services店面網站存在，並且存取許可權受限。

▢店面網站已存在。 請參閱[建立店面](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/)。
▢您知道網站名稱。
▢只有授權人員才有[許可權可發佈](https://tools.aem.live/tools/user-admin/index.html)。
▢只有授權人員才有[製作者的許可權](https://docs.da.live/administrators/guides/permissions)。

## 驗證Cloud和Optimizer整合 {#cloud-optimizer-integration}

確認Adobe Commerce on Cloud和[!DNL Adobe Commerce Optimizer]正確交換資料。

### 在Adobe Commerce上

在雲端專案中完成這些檢查。

▢ Commerce Optimizer聯結器已[安裝及設定](../../aco-connector/get-started.md)。
▢ `aco:conf:show` CLI命令會確認與生產Commerce Optimizer執行個體的連線。 組織ID、使用者端ID、擷取URL和Commerce Optimizer URL符合生產環境。
▢匯出設定[中的](../../aco-connector/get-started.md)同步處理範圍符合您的需求。
▢ [資料摘要同步狀態](../../aco-connector/get-started.md)會確認從雲端執行個體匯出資料。

### 在Commerce Optimizer中

在[!DNL Adobe Commerce Optimizer] UI中完成這些檢查。

▢ [資料同步儀表板](../setup/data-sync.md)會顯示收到的資料。 產品、價格和屬性會出現在目錄服務、產品探索和建議中。
▢ [價格簿](../setup/pricebooks.md)是從雲端上的客戶群組自動建立的。
▢ [目錄檢視](../setup/catalog-view.md)存在，而且您知道它們的ID。
▢ [原則](../setup/policies.md)存在，而且您知道它們的ID。
已設定▢ [Facet](../merchandising/facets/overview.md)。
已設定▢ [同義字](../merchandising/synonyms/overview.md)。
已設定▢ [銷售規則](../merchandising/rules/overview.md)。
▢ [價格方面和搜尋語言](../settings.md)符合您使用這些功能的需求。
▢ [產品建議](../merchandising/recommendations/create.md)存在，且行為與預覽中預期的一樣。
▢ [搜尋效能資料](../manage-results/search-performance.md)出現在&#x200B;*管理員*中。
▢ [Recommendations效能資料](../manage-results/recommendation-performance.md)出現在&#x200B;*管理員*&#x200B;中。

## 驗證店面和雲端整合 {#storefront-cloud-integration}

確認店面可讀取正確的Adobe Commerce GraphQL端點。

### 在Adobe Commerce上

▢店面相容性套件已[安裝](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility/install/)。

### 在店面

▢店面`commerce-core-endpoint`設定指向您的[雲端GraphQL端點](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/)。
▢如果您使用API Mesh做為Cloud GraphQL的Proxy，`commerce-core-endpoint`會指向API Mesh端點，而非Cloud GraphQL端點。

## 驗證店面與Optimizer整合 {#storefront-optimizer-integration}

確認店面設定中的Commerce Optimizer設定。

▢您的店面使用正確的[Commerce Optimizer設定](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/)。
▢ `adobe-commerce-optimizer`是`true`。
▢ `commerce-endpoint`指向生產Commerce Optimizer GraphQL端點，或您使用API Mesh時的API Mesh端點。
▢ `headers.cs.AC-view-ID`儲存您生產Commerce Optimizer執行個體的目錄檢視ID。

## 驗證雲端上的協力廠商服務 {#third-party-services}

確認在您的主機商務系統上執行的整合（不在[!DNL Adobe Commerce Optimizer]中）。

▢ **付款：**&#x200B;付款閘道已上線並經過測試（Stripe、PayPal、Adyen等）。
▢ **送貨：**&#x200B;送貨API連線有效（UPS、FedEx等）。
▢ **送貨：** Fulfillment平台已連線並測試（例如ShipStation）。
▢ **稅捐：**&#x200B;已驗證稅捐計算整合（Avalara、TaxJar等）。
▢ **稅捐：**&#x200B;帳戶處理軟體同步處理（QuickBooks等）。
▢ **詳細目錄：** PIM、ERP或詳細目錄管理整合已測試並同步。
▢ **架構：**&#x200B;主商務系統處理付款、運送、稅金和存貨（非[!DNL Adobe Commerce Optimizer]）。
▢ **架構：** API Mesh與App Builder在主機商務系統與[!DNL Adobe Commerce Optimizer]之間保持同步。
▢ **電子郵件：**&#x200B;異動電子郵件傳送可正常運作（訂單確認、送貨等）。
▢ **電子郵件：**&#x200B;電子郵件範本符合您的品牌，並使用正確的連結。

## 驗證App Builder和API Mesh {#app-builder-mesh}

確認生產的可擴充性設定。

### App Builder

▢生產工作區包含所有必要的設定和服務。
▢生產應用程式通過了組建案例測試。
已根據▢Adobe Developer App Builder產品說明[和](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html){target="_blank"}App Builder系統設定和限制[，檢閱及確認](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings){target="_blank"}產品限制和界限。
▢生產應用程式使用App Builder生產端點。
▢自訂&#x200B;*Admin*&#x200B;面板擴充功能已部署至生產工作區。

### API網格

▢設定和來源已準備就緒可供生產。

### 活動

已設定▢個Adobe I/O Events並驗證訂閱。

## 最終確定店面體驗 {#finalize-storefront}

啟動前的波蘭文內容、SEO、效能、安全性和CDN行為。

### 內容與製作

確認編寫工作流程和Storefront元件。

▢ [AEM/EDS上線檢查清單](https://www.aem.live/docs/go-live-checklist)檢閱已完成。
▢編寫來源是檔案式或通用編輯器（且已設定）。
使用預覽→發佈週期發佈▢內容。
▢網域上的`.aem.live`內容和設計QA已完成。
▢網站已正確設定並提供Favicon。
▢ da.live和產品視覺效果使用[已設定的](https://docs.da.live/administrators/guides/permissions)專用認證。
▢個下拉式清單（購物車、結帳、PDP、PLP、auth、帳戶）為[自訂](../storefront.md)並已測試。
▢店面品牌反映CSS設計權杖、印刷樣式和顏色。

### SEO和索引

確認中繼資料、URL和抓取行為。

關鍵頁面（尤其是PDP和PLP）有▢個檔案標題中繼資料。 請參閱[Adobe Commerce店面](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/metadata/){target="_blank"}檔案中的&#x200B;_SEO中繼資料_。
▢個PDP包含[個中繼資料和結構化資料](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/metadata/){target="_blank"} （例如JSON-LD）。
▢產品URL格式一致（例如，`domain/product-name`）。
▢個虛名URL會重新導向至標準URL。
▢專案包含`robots.txt`，可讓您在適當時編制索引、參考Sitemap，以及封鎖您不想編制索引的路徑（例如，`/drafts`）。
▢ [重新導向](https://www.aem.live/docs/redirects)檔案涵蓋來自移轉的URL變更（例如，移除`.html`之後）。
▢ Sitemap已存在，並已視需要提交至Google搜尋主控台。
▢規範URL傳回`2xx`狀態（不是`3xx`或`4xx`）。
▢多語言網站在網站地圖中包含`hreflang`標籤。
▢ Google Search Console涵蓋範圍報告為最新狀態。

### 預先呈現

確認啟用伺服器端轉譯。

關鍵頁面的▢預先呈現已開啟。 請參閱[AEM店面](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-prerender/){target="_blank"}檔案中的&#x200B;_Adobe Commerce預先呈現_。
▢個URL使用小寫，所以預先呈現不會中斷連結。
▢ HTML來源包含確認預先轉譯有效性的中繼資料和內文內容。
▢地區設定顯示適用的正確翻譯頁面。
▢其他HTML標籤已視需要[設定](https://www.aem.live/docs/redirects)。

### 效能與監控

確認效能基準和分析配線。

▢您的店面遵循[Adobe Commerce店面](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/performance/){target="_blank"}檔案中的&#x200B;_效能最佳做法_。
已設定▢ （選用） Google Analytics和Google Tag Manager。
▢ [Storefront事件](https://github.com/adobe/commerce-events/tree/main/examples/events/snowplow-debugger)實作有效，資料會顯示在Adobe Commerce [!DNL Live Search]Admin[!DNL Product Recommendations]的&#x200B;*和*儀表板中。
▢ `environment`Commerce組態[中的](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/){target="_blank"}分析引數在開發期間為`"Testing"`，在上線時為`"Production"`。 請參閱[Analytics檢測](https://experienceleague.adobe.com/developer/commerce/storefront/setup/analytics/instrumentation/){target="_blank"}。
根據此主題的指引，▢ Lighthouse分數符合您的目標（例如，關鍵頁面上的`100`）。

### 安全性與存取權

確認許可權和密碼。

▢已為DA內容和EDS網站設定適當的許可權。 請參閱[DA.live許可權](https://da.live/docs/administration/permissions)和[製作驗證設定](https://www.aem.live/docs/authentication-setup-authoring)。
▢已布建產品視覺效果整合。 請參閱[AEM Cloud Service存取總覽](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/overview#)。
電子郵件範本中的▢密碼重設連結符合您的Edge Delivery Services設定。 請參閱店面常見問題集：[如果移轉至Edge Delivery Services或Helix後我的電子郵件範本連結失效，怎麼辦？](https://experienceleague.adobe.com/developer/commerce/storefront/troubleshooting/faq/#what-should-i-do-if-my-email-template-links-are-broken-after-migrating-to-edge-delivery-services-or-helix){target="_blank"}。
整合和付款提供者的▢生產金鑰已準備就緒。
▢網域已加入允許清單，後端Webhook可正常運作。

### cdn和快取

確認CDN、DNS和快取行為。

▢ CDN設定會針對Sidekick擴充功能和指令碼（例如Sitemap產生和影像匯入工具）使用生產GraphQL端點(`yourproject.com/graphql`)。
▢當您使用Adobe Commerce Fastly時，可使用CDN清除權杖，且[網站設定](https://tools.aem.live/tools/cdn-setup/index.html)包含`authToken`和`serviceId`。
▢ [CDN組態](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/content-delivery-network/){target="_blank"}驗證快取與失效。
▢對於[多存放區設定](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/indexing/#multi-store-setups){target="_blank"}，目錄服務和[!DNL Live Search]要求包含存放區特定的快取匯出工具（例如，查詢引數或CDN規則）。
▢個推播失效工作端對端進行（發佈變更，然後在生產網域上驗證）。
▢個DNS TTL在切換前已足夠低。
所有網域和主機名稱的▢個DNS A和CNAME記錄都正確。
▢已為生產網域布建及驗證SSL/TLS憑證。
▢ `www`和Apex重新導向行為正確。

## 安全性與合規性 {#security-compliance}

確認安全性狀態與法規遵循任務。

▢ **SSL：**&#x200B;已安裝信任的SSL/TLS憑證。
▢ **SSL：** HTTPS已在整個網站強制執行。
▢ **存取：**&#x200B;預設&#x200B;*管理員*&#x200B;密碼已變更，而且已設定強式密碼原則。 請參閱[!DNL Adobe Commerce Optimizer] [使用者和識別管理](../user-management.md)。
▢ **存取：** *管理員* URL不是預設值。
已針對所有▢管理員&#x200B;**使用者啟用** *存取：*雙因素驗證。
▢ **存取：**&#x200B;沒有非使用中或未使用的管理員使用者與專案相關聯。
▢ **防火牆：** Web應用程式防火牆(WAF)已設定並驗證。
▢ **PCI：**&#x200B;生產環境的安全性滲透測試（PCI範圍）已完成。
▢ **掃描：** Adobe安全性掃描工具已登入，且初始掃描已完成。
▢ **存取：** CORS僅允許核准的原始項。
▢ **法規遵循：** [的](../shared-responsibility.md)共用責任模式[!DNL Adobe Commerce Optimizer]為最新狀態，且已清楚定義Adobe與客戶責任的比較。
▢ **法規遵循：**&#x200B;已驗證隱私權原則、Cookie同意以及GDPR或CCPA要求。

## 分析和監視 {#analytics-monitoring}

確認測量與基準線。

▢ **RUM：**&#x200B;實際使用者監控(RUM)是針對前後比較而檢測的。
已設定▢ **Analytics：** Adobe Experience Platform資料集合（如果適用）。
▢ **Analytics：**&#x200B;已驗證MarTech標籤是否會在生產主機名稱上引發。
▢ **分析：**&#x200B;已記錄基準線分析；預期會在啟動後波動（頁面檢視、跳出率等）。
▢ **事件：**&#x200B;轉換追蹤工作端對端進行（新增到購物車→結帳→確認）。

## 測試 {#testing}

啟動前後確認品質。

▢ **功能：**&#x200B;核心流程工作端對端：瀏覽→搜尋→篩選器→新增到購物車→結帳→建立帳戶。
▢ **功能：**&#x200B;付款閘道接受實際和測試交易。
▢ **功能：**&#x200B;訂單位置、確認電子郵件及訂單追蹤工作。
▢ **功能：**&#x200B;送貨選項與稅捐計算正確。
▢ **功能：**&#x200B;優惠券、折扣和熟客方案如預期般運作。
▢ **UAT：**&#x200B;使用者驗收測試已在中繼及生產環境中完成。
▢ **效能：**&#x200B;負載和壓力測試已完成，且Adobe CTA或CSE已有結果。
▢ **效能：**&#x200B;在桌上型電腦和行動裝置上的頁面載入時間少於3秒。
▢ **效能：** Lighthouse分數達到關鍵頁面上的目標（例如，透過PageSpeed Insights）。
已最佳化▢ **效能：**&#x200B;影像、指令碼和資產。
▢ **相容性：** Chrome、Firefox、Safari和Edge的行為如預期。
▢ **相容性：**&#x200B;回應式配置適用於行動裝置、平板電腦和案頭。
▢ **相容性：**&#x200B;在3G、4G和Wi-Fi上可接受的效能。
▢ **協助工具：**&#x200B;協助工具稽核已完成（WCAG、熒幕閱讀器、鍵盤導覽）。
▢ **功能：**&#x200B;已制定啟動後404監視計畫。
▢ **UAT：**&#x200B;復原計畫已存在，如果發生啟動問題，則會通過測試。

## 啟動日和啟動後 {#launch-post-launch}

確認通訊、支援和後續工作。

▢ **啟動協調：** Adobe已確認啟動日期；已透過電子郵件通知CTA。
▢ **支援：**&#x200B;已記錄P1熱線號碼： US (+1) 800-497-0335，然後按下Commerce的6。
▢ **支援：**&#x200B;您的團隊在呼叫P1熱線前&#x200B;**已接受開啟支援票證**&#x200B;的訓練。
▢ **啟動後：**&#x200B;驗證生產網域上的Lighthouse分數。
▢ **啟動後：**&#x200B;監視Google搜尋主控台以建立索引並抓取錯誤。
▢ **啟動後：**&#x200B;監視404報告，並為高流量的舊版URL新增重新導向。
▢ **啟動後：**&#x200B;確認生產環境中的MarTech與分析資料。
▢ **啟動後：**&#x200B;請要求您的CTA、CSE或AM啟用高SLA監視。
▢有災難回覆計畫存在，且已通過測試。
▢已制定程式來追蹤及升級範本和擴充功能套件至目前版本。
