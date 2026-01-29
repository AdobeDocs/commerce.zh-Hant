---
title: 從搜尋配接卡移轉至PLP Widget
description: 瞭解如何從已棄用的搜尋配接卡移轉至 [!DNL Live Search] 產品清單頁面Widget。
source-git-commit: 8811f0f271928fbc827e5a0164542da473c57224
workflow-type: tm+mt
source-wordcount: '2053'
ht-degree: 0%

---

# 從搜尋配接卡移轉至PLP Widget

搜尋配接器自[&#x200B; 4.0.0起已](release-notes.md#live-search-400)淘汰[!DNL Live Search]，將只接收安全性更新。 [產品清單頁面(PLP) Widget](plp-styling.md)是日後所有[!DNL Live Search]實作的支援解決方案。 本指南可協助您瞭解何時可直接進行移轉，以及何時需要其他工作。

## 先決條件

在開始移轉程式之前，請確認您的環境符合這些需求。

開始移轉前：

**技術需求**：

- Adobe Commerce 2.4.4或更新版本。
- 已安裝[!DNL Live Search]擴充功能。
- 存取命令列(CLI)。
- 存取Commerce管理員。
- 測試或QA環境。

**備份與準備**：

1. 備份您的資料庫和程式碼。
1. 記錄目前的自訂專案。
1. 請檢閱[界限和限制](boundaries-limits.md)，以確保PLP Widget符合您的需求。
1. 在低流量期間排程移轉。
1. 通知利害關係人店面行為的潛在變更。

**檢閱目前的實作**：

- 檢查您目前的[!DNL Live Search]版本。
- 記錄使用中的多面及其組態。
- 測試所有搜尋功能並記錄預期行為。
- 擷取目前搜尋結果簡報的熒幕擷取畫面。

**版本相容性**：

- 執行Adobe Commerce 2.4.4或更新版本。
- 準備升級至[!DNL Live Search] 4.0.0或更新版本。

## 移轉案例

### 直接移轉（無需額外工作）

如果您的實施符合下列所有條件，則可直接移轉至PLP Widget：

**標準Luma型店面**：

- 您正在使用Luma佈景主題或從Luma繼承的佈景主題，且只需最少的自訂。
- 您尚未對PLP配置或範本進行自訂修改。
- 您尚未建立與搜尋結果互動的自訂JavaScript擴充功能。

**標準產品目錄**：

- 所有產品屬性都使用標準來源模型（而非自訂來源模型）。
- 沒有需要特殊轉譯邏輯的自訂產品型別。
- 您的目錄僅使用標準Facet和篩選。

**標準整合**：

- 您沒有使用適用於分析的Google Tag Manager (GTM)。
- 您未使用會修改搜尋行為的協力廠商擴充功能。

如果您的實作符合這些條件，請繼續進行[標準移轉步驟](#standard-migration-steps)。

### 需要額外工作的移轉

如果您的實施有以下任一情況，則需要額外工作：

**自訂主題修改**：

- 覆寫Luma範本的自訂PLP配置。
- 以搜尋配接器特定元素為目標的自訂CSS或JavaScript。
- PLP或相關檔案的自訂範本修改。
- 主題不會繼承自Luma （例如從頭開始的自訂主題）。

**自訂產品屬性**：

- 自訂來源模型用作Facet的產品屬性。
- 具有特殊顯示要求的自訂產品型別。
- 具有`"is_user_defined": false`的程式化屬性。

**進階整合**：

- Google Tag Manager (GTM)現正用於追蹤。
- 與搜尋整合的第三方分析或個人化工具。
- 自訂事件追蹤或資料層實施。
- 與外部搜尋或推薦引擎整合。

**無周邊或PWA實作**：

- 使用Headless架構(例如PWA Studio、Vue Storefront)。
- 自訂前端架構(React、Vue、Angular)。
- 僅針對目錄查詢使用GraphQL。
- 自訂店面事件實施。

**自訂Widget程式碼**：

- 先前自訂搜尋介面卡程式碼。
- 在您自己的CDN上託管自訂版本的Widget。
- 搜尋功能的自訂JavaScript擴充功能。

若您的實作有上述任一情況，請參閱[複雜的移轉情況](#complex-migration-scenarios)。

## 標準移轉步驟

對於沒有特殊自訂的實作，請遵循下列步驟：

### 步驟1：升級[!DNL Live Search]

將您的[!DNL Live Search]擴充功能升級至4.0版或更新版本，以存取PLP Widget。

**角色**：商家或合作夥伴

1. 檢查您目前的[!DNL Live Search]版本：

   ```bash
   composer show magento/live-search | grep version
   ```

1. 若使用3.x版或更舊版本，請先啟用AdvancedSearch模組，再進行升級：

   ```bash
   bin/magento module:enable Magento_AdvancedSearch
   ```

1. 更新`composer.json`以需要[!DNL Live Search] 4.0或更新版本：

   ```json
   "require": {
      "magento/live-search": "^4.0"
   }
   ```

1. 執行升級：

   ```bash
   composer update magento/live-search --with-dependencies
   ```

1. 執行安裝程式升級並重新編譯：

   ```bash
   bin/magento setup:upgrade
   bin/magento setup:di:compile
   ```

1. 視需要部署靜態內容：

   ```bash
   bin/magento setup:static-content:deploy
   ```

### 步驟2：啟用PLP Widget

在Commerce管理員中設定PLP Widget。

**角色**：商人

PLP Widget預設會在[!DNL Live Search] 4.0.0+的新安裝中啟用。 如果從舊版升級：

1. 移至「**[!UICONTROL Stores]** >設定> **[!UICONTROL Configuration]**」。
1. 導覽至&#x200B;**[!UICONTROL Live Search]** > **[!UICONTROL Storefront Features]**。
1. 展開&#x200B;**[!UICONTROL Storefront Features]**&#x200B;區段。
1. 將&#x200B;**[!UICONTROL Enable Product Listing Widgets]**&#x200B;設為&#x200B;**是**。
1. 按一下&#x200B;**[!UICONTROL Save Config]**。
1. 排清快取： **[!UICONTROL System]** >工具> **[!UICONTROL Cache Management]** > **[!UICONTROL Flush Magento Cache]**。

### 步驟3：在中繼環境中測試

上線之前，先在非生產環境中驗證移轉。

**角色**：商家/合作夥伴

在部署到生產環境之前，請徹底測試搜尋功能：

**功能測試**：

- 驗證搜尋結果是否正確顯示。
- 測試所有已設定的多面向。
- 驗證類別導覽是否有效。
- 透過結果測試分頁。
- 確認排序選項如預期運作。
- 測試簡單產品的加入購物車功能。

**視覺測試**：

- 確認產品影像可正確顯示。
- 驗證產品名稱和價格是否正確呈現。
- 測試色票（若有使用）。
- 檢查行動裝置上的回應式行為。
- 驗證樣式是否符合您的品牌。

**效能測試**：

- 測量頁面載入時間。
- 以逼真的目錄大小進行測試。
- 監視伺服器資源使用情況。
- 檢查瀏覽器主控台是否有JavaScript錯誤。

### 步驟4：部署到生產

將驗證的設定移至您的即時店面。

**角色**：商家/合作夥伴

1. 儘可能在維護期間進行部署排程。
1. 遵循您的標準部署程式。
1. 使用[步驟2在生產環境中啟用PLP Widget：啟用PLP Widget](#step-2-enable-the-plp-widget)。
1. 部署後立即監視任何問題。
1. 出現嚴重問題時，請準備好回覆計畫。

### 步驟5：驗證和監視

移轉後追蹤搜尋效能和客戶體驗。

**角色**：商人

部署後，監視關鍵量度：

- 零結果搜尋率
- 搜尋到購物車的轉換率
- 頁面載入效能
- 客戶意見回饋或支援票證
- 瀏覽器主控台中的JavaScript錯誤

## 複雜的移轉案例

下列情況需要超出標準移轉步驟的額外規劃、自訂開發或專業支援。

### 包含版面修改的自訂主題

在此案例中，您有自訂範本或版面配置可覆寫預設的產品清單行為。

**角色**：開發人員/合作夥伴

1. **稽核自訂**：
   - 記錄主題中的所有自訂配置XML檔案。
   - 檢閱對產品清單頁面或相關檔案的任何「自訂」範本修改。
   - 識別用於樣式的自訂CSS類別。
   - 記錄自訂JavaScript互動。

1. **移轉至CSS自訂**：
   - PLP Widget使用特定的CSS類別（請參閱[PLP樣式指南](plp-styling.md)）。
   - 使用PLP Widget CSS類別重新建立視覺化自訂。
   - 測試自訂樣式是否正確套用。

1. **移除衝突的自訂專案**：
   - 移除修改產品清單結構的版面XML。
   - 清除鎖定搜尋配接器特定元素的JavaScript。
   - 更新範本會覆寫與Widget演算衝突的專案。

1. **徹底測試**：
   - 確認所有視覺化自訂都可搭配PLP Widget使用。
   - 確認配置沒有衝突。
   - 測試所有中斷點和裝置。

### 具有自訂來源模型的產品屬性

在此案例中，您有多面向使用自訂來源模型的產品屬性，搜尋配接卡不支援這些模型，但PLP Widget支援這些模型。

**角色**：商人（管理員設定）

1. **識別受影響的屬性**：
   - 檢閱用作Facet的產品屬性。
   - 識別使用自訂來源模型的專案。
   - 記錄目前的Facet設定。

1. **升級並啟用PLP Widget**：
   - 遵循[標準移轉步驟](#standard-migration-steps)。
   - PLP Widget支援自訂來源模型屬性。

1. **重新設定Facet**：
   - 移至「**[!UICONTROL Marketing]** > SEO和搜尋> **[!UICONTROL Live Search]**」。
   - 檢閱受影響屬性的多面向組態。
   - 測試Facet對自訂來源模型正常運作。

1. **驗證**：
   - 使用自訂來源模型Facet測試篩選。
   - 確認所有屬性值皆正確顯示。
   - 確認效能為可接受。

### Google Tag Manager (GTM)整合

此情境中，有一個已知問題啟用PLP Widget可能會導致GTM失敗。

**角色**：開發人員/合作夥伴+客戶工程

**選項1：繼續搜尋配接卡（僅限暫時性）**

- 如果GTM對業務至關重要，請啟用搜尋配接卡。
- 瞭解您只會收到安全性更新。
- 解決GTM相容性時，請規劃進行移轉。
- 如需GTM相容性的更新，請聯絡Adobe支援。

**選項2：將GTM追蹤移轉至替代方法**

1. **實作自訂事件集合**：

   - 使用[Storefront活動SDK](https://developer.adobe.com/commerce/services/shared-services/storefront-events/)。
   - 擷取搜尋和產品互動事件。
   - 手動將事件推送至GTM資料層。

1. **完成下列步驟**：

   - 稽核目前的GTM追蹤需求。
   - 將GTM事件對應至Storefront事件。
   - 實作自訂事件接聽程式。
   - 測試資料流入GTM。
   - 驗證Analytics報表。

**選項3：以Adobe Analytics取代GTM**

- 考慮移轉至[Adobe Analytics](https://business.adobe.com/products/adobe-analytics.html) （如適用）。
- 如需指引，請聯絡客戶工程部門。

**聯絡對象**：提交支援票證，以取得GTM相容性更新或客戶工程協助。

### 案例：Headless或PWA實施

在此案例中，您有Headless或PWA店面需要自訂事件集合，且無法使用標準PLP Widget UI。

**角色**：開發人員/合作夥伴

1. **檢閱參考實作**：
   - 研究[PLP Widget原始程式碼](https://github.com/adobe/storefront-product-listing-page)。
   - 檢閱[[!DNL Live Search] GraphQL](graphql.md)的API檔案。
   - 瞭解[目錄服務查詢](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)。

1. **實作自訂UI**：
   - 使用[!DNL Live Search] GraphQL API進行查詢。
   - 建立自訂產品清單元件。
   - 實作多面向的UI。
   - 處理分頁與排序。

1. **實作事件集合**：
   - 檢閱[Storefront活動檔案](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#live-search)。
   - 實作必要事件：
      - `search-request-sent`
      - `search-response-received`
      - `search-results-view`
      - `product-page-view`
      - `add-to-cart`
   - 測試事件資料流入Adobe Commerce。

1. **設定Facet排序**：
   - 針對Headless實作，Facet可依計數排序。
   - 在&#x200B;**[!UICONTROL Live Search]** > **[!UICONTROL Facets]**&#x200B;工作區中設定。
   - 設定&#x200B;**[!UICONTROL Sort Type]**&#x200B;為&#x200B;**Count**，以獲得較好的UX。

1. **測試及驗證**：
   - 驗證搜尋結果的準確性。
   - 測試多面向功能。
   - 確認已正確追蹤事件。
   - 監視效能測量結果。
   - 驗證智慧型銷售功能是否有效。

### 案例：自訂Widget程式碼修改

在此案例中，您先前已自訂搜尋轉接器或Widget程式碼，且需要移轉自訂。

**角色**：開發人員/合作夥伴

1. **記錄現有的自訂**：
   - 列出對搜尋配接器所做的所有自訂。
   - 識別推動每個自訂化的業務需求。
   - 決定是否仍需要自訂。

1. **檢查內建功能是否符合您的需求**：
   - 檢閱[PLP Widget功能](plp-styling.md#widget-features)。
   - 檢查基於CSS的自訂是否足夠。
   - 測試預設PLP Widget行為。

1. **如果仍需要自訂程式碼**：
   - 複製[PLP Widget存放庫](https://github.com/adobe/storefront-product-listing-page)。
   - 實施您的自訂。
   - 在您自己的CDN上託管。
   - 更新Commerce設定以使用您的自訂Widget。

   >[!WARNING]
   >
   >如果您使用存放庫中的程式碼來自訂PLP Widget，便需自行負責維護與更新。 Adobe的新PLP Widget功能可能與您的自訂不相容。

1. **徹底測試**：
   - 測試所有自訂功能。
   - 確認Commerce更新不會破壞自訂。
   - 記錄您的自訂實作。
   - 規劃進行中的維護作業。

## 已知限制和邊緣案例

移轉時請注意這些限制：

**PLP Widget限制**：

- **排序順序方向**：啟用PLP Widget時，無法變更產品清單頁面上的排序順序方向（遞增/遞減）。
- **加入購物車**： Add to cart按鈕僅適用於Widget中的簡單產品。
- **層級定價**： PLP Widget中不支援。
- **VAT顯示**：價格包含VAT，但VAT不能顯示為個別值。

**與搜尋配接器的功能差異**：

- **色票**： `color`屬性的拼字必須與`color`完全相同（不是「color」或自訂名稱），色票才能正常運作。
- **佈景主題樣式**：自訂佈景主題類別不會由Widget繼承；必須鎖定特定於Widget的CSS類別。
- **自訂產品型別**： Widget中不支援。

**效能考量**：

- 大型目錄（50,000種以上的產品）的初始頁面載入時間可能會更長。
- 具有許多值的多個Facet可能會影響效能。
- 行動裝置效能可能會因目錄大小而異。

**相容性問題**：

- Google Tag Manager相容性問題（請參閱[GTM案例](#google-tag-manager-gtm-integration)）。
- 某些協力廠商擴充功能可能會與PLP Widget發生衝突。
- 自訂簽出擴充功能可能需要更新。

## 取得協助

根據您的特定需求，聯絡適當的資源。

**Adobe支援**&#x200B;可協助：

- 標準即時搜尋移轉程式
- PLP Widget設定問題
- Facet或屬性索引問題
- 預設實施的效能問題
- 升級錯誤

**應該連絡開發夥伴/系統整合經銷商**：

- 自訂主題修改
- 自訂Widget程式碼實作
- 協力廠商擴充功能相容性
- Headless或PWA實作
- 自訂事件追蹤

若要聯絡Adobe支援，請參閱[說明中心使用手冊](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide)。

## 常見問題集

尋找有關從搜尋配接卡移轉至PLP Widget的常見問題解答。

**問：搜尋配接卡是否會收到錯誤修正或功能更新？**

答：不會。 已棄用搜尋配接器，只會接收安全性更新。 只有PLP Widget提供錯誤修正、效能改善和新功能。 如果您遇到搜尋配接卡的問題，建議將移轉至PLP Widget。

**問：移轉是否會破壞我的店面？**

答：如果您在測試中遵循適當的測試程式，移轉程式應該會順暢無礙。 讓復原計畫準備好進行生產部署。

**問：移轉需要多久的時間？**

答：標準實作： 1-2小時。 對於自訂實施：根據複雜度而定，1-4週長。

**問：我的搜尋銷售規則是否仍然有效？**

答：是，在[!DNL Live Search]工作區中設定的所有搜尋銷售規則、同義字和Facet都能繼續與PLP Widget搭配使用。

**問：我是否需要重新設定我的Facet？**

答：通常不會，但如果您受到搜尋配接器的自訂來源模型屬性的限制，現在可以將其與PLP Widget搭配使用。

**問：我的自訂CSS呢？**

答：您需要更新CSS以定位PLP Widget類別。 請參閱[CSS類別參考](plp-styling.md#css-classes)。

**問：這會影響我的搜尋效能嗎？**

答：PLP Widget的設計宗旨是提供優異效能。 大多數商家認為效能相當或更好。 大型目錄應在測試環境中測試。
