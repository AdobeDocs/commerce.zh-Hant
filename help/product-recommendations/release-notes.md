---
title: '[!DNL Product Recommendations]發行說明'
description: Adobe Commerce中 [!DNL Product Recommendations] 的最新發行資訊。
feature: Services, Recommendations, Release Notes
exl-id: 37404605-5b62-4c71-90d1-4f09e6105c4b
source-git-commit: 6b74580a3135322f222b8cfa5c51277a34e6bb83
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 0%

---

# [!DNL Product Recommendations]發行說明

發行說明包含下列[!DNL Product Recommendations]模組的更新：

* [!DNL Product Recommendations]中繼封裝： `magento/product-recommendations`
* [!DNL Product Recommendations] （選擇性）模組中的Page Builder支援： `magento/module-page-builder-product-recommendations`
* [!DNL Product Recommendations] （選擇性）模組的視覺相似度推薦型別支援： `magento/module-visual-product-recommendations`

支援最新發行的版本。 舊版的發行說明僅供參考。
發行說明包括：

![新](../assets/new.svg)新功能
![修正](../assets/fix.svg)修正和改良
![錯誤](../assets/bug.svg)已知問題

請參閱開發人員檔案以[瞭解產品支援](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability)。

## 託管服務更新

這些附註說明在版本化版本發行之外發佈或發現的更新或已知問題，或對託管服務的改進。

_2025年10月1日_

![新](../assets/new.svg)已新增客戶登入資料名稱為`ds-logged-in`的新資料儲存金鑰。

_2025年1月31日_

![新](../assets/new.svg)測試環境中未查詢的目錄資料有新的資料保留原則。 [了解更多](overview.md#catalog-data-retention-policy)。

_2024年6月28日_

![錯誤](../assets/bug.svg)當購物車頁面重新載入時，從購物車頁面上的[!DNL Product Recommendations]裝置新增到購物車的產品，並未從建議產品清單中移除。
![錯誤](../assets/bug.svg)從購物車移除的產品會繼續保留在`cartSkus`陣列中，直到購物車頁面重新載入為止。

_2023年7月18日_

![新](../assets/new.svg) [!DNL Product Recommendations]現在有GraphQL [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/)查詢。

_2023年4月25日_

![新](../assets/new.svg) [!DNL Product Recommendations]客戶現在可以利用[SaaS價格索引](../price-index/price-indexing.md)。

## 目前的主要版本

### 6.4.0 magento/product-recommendations

_2025年9月17日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![修正](../assets/fix.svg)解決當本機儲存體資料無法使用時，產品建議單位會因JavaScript錯誤而消失的間歇性問題。 此修正可確保PREX在本機存放區中缺少`ds-view-history-time-decay`時不再擲回錯誤。
![新](../assets/new.svg)已將`recommendations-sdk`的CDN URL更新至`adobe.io`網域。

### 舊版

### 6.3.0的magento/product-recommendations

_2025年9月5日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)新增支援，以便顯示在[產品推薦工作區](page-builder.md)的非預設存放區檢視中，[PageBuilder推薦單位](workspace.md)的量度。
![新的](../assets/new.svg)產品建議現在會完全遵守[Cookie限制模式](setting-cookie.md)，方法是在啟用限制時，防止在Cookie/本機存放區中進行資料收集和儲存。

### 6.2.1的magento/product-recommendations

_2025年7月14日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![修正](../assets/fix.svg)已改善[預覽建議](./create.md#preview-recommendations)面板。

### 6.2.0的magento/product-recommendations

_2025年4月4日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)已將`recommendations-admin-ui`的CDN URL更新為`adobe.io`網域。

### 6.1.0的magento/product-recommendations

_2025年3月11日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)已新增PHP 8.4支援。

### 6.0.3的magento/product-recommendations

_2024年11月6日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![修正](../assets/fix.svg)修正[類別篩選器](filters.md#category)包含不屬於目前商店檢閱的類別的問題。
![修正](../assets/fix.svg)已修正`magento/product-recommendations`中繼資料中的相依性問題。

### 6.0.2的magento/product-recommendations

_2024年5月9日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![修正](../assets/fix.svg)修正在Product Recommendations單位內的簡單產品上按一下「**[!DNL Add to Cart]**」按鈕，將購物者重新導向首頁而不是停留在目前頁面的問題。
![錯誤](../assets/bug.svg) `referenceBlock` XML檔案中的`ProductRecommendations Layout`專案發生驗證錯誤。

### 6.0.1的magento/product-recommendations

_2024年3月19日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)已新增PHP 8.3支援。

### 6.0.0的magento/product-recommendations

_2024年2月22日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg) [!DNL Catalog Sync Dashboard]現在是[[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard)。 此改版後的儀表板提供[!DNL Product Recommendations]、[!DNL Live Search]和[!DNL Catalog Service]的資料串流的深入分析。
![修正](../assets/fix.svg)修正造成[!DNL Product Recommendations]簽出錯誤的問題。

+++5.0.0和先前版本

### 5.0.1的magento/product-recommendations

_2023年9月15日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)已新增模組以支援[Saas價格索引器](../price-index/price-indexing.md)。
![新](../assets/new.svg)已新增新的資料匯出模組，以支援匯出更多產品型別，包括套件產品和禮品卡。
![修正](../assets/fix.svg)產品與價格摘要的資料表大小已大幅縮減。 資料表`catalog_data_exporter_products`和`catalog_data_exporter_product_prices`應該會大幅縮減大小。

#### 已知限制

* 如果`websiteCode`值包含底線(_)，則傳回的值不正確。

### 5.0.0的magento/product-recommendations

_2023年3月20日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)已更新[!DNL Product Recommendations]以支援Adobe Commerce 2.4.6。
![新增](../assets/new.svg)這是主要版本發行。 [編輯](install-configure.md#update)專案的根`composer.json`檔案。
![新的](../assets/new.svg) [!DNL Product Recommendations]現在支援Commerce中的完整[Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction)功能(先前稱為多Source詳細目錄，或MSI)。 若要啟用完整支援，您必須[將](install-configure.md#update)相依性模組`commerce-data-export`更新為102.2.0+版。

### 4.0.1的magento/product-recommendations

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![修正](../assets/fix.svg)先前，當顯示貨幣切換為非預設貨幣時，[!DNL Product Recommendations]會顯示錯誤。 現在切換貨幣已可正常運作。

### 4.0.0的magento/product-recommendations

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)已新增[整備指標](create.md)，以協助您視覺化每個建議型別的訓練進度。
![新](../assets/new.svg)此版本為主要版本。 [編輯](install-configure.md#update)專案的根`composer.json`檔案。 此版本也要求您在安裝和設定[!DNL Product Recommendations]時提供兩個API金鑰： [生產金鑰和沙箱金鑰](../landing/saas.md)。

#### 已知限制

* 如果`websiteCode`值包含底線(_)，則傳回的值不正確。

### 3.3.7的magento/product-recommendations

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新](../assets/new.svg)已新增PHP 8.1支援
![新增](../assets/new.svg)改善影像調整大小，讓參考顯示範本中的影像調整大小處理方式更加一致

### 3.3.6的magento/product-recommendations

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新的](../assets/new.svg)已透過明確列出相依性最佳化[!DNL Product Recommendations]中繼套件

### 3.3.5的magento/product-recommendations

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新](../assets/new.svg)已在[中新增](onboarding.md#b2bsupport)B2B支援[!DNL Product Recommendations]
![新](../assets/new.svg)已新增摘要至[透過命令列將目錄資料](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync)同步至Commerce服務

### 3.3.3的magento/product-recommendations

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新](../assets/new.svg)已新增新的[建議型別](type.md)：轉換（檢視到購物車）、轉換（檢視到購買）和最近檢視。 這些新建議型別可在`magento/product-recommendations`模組3.2.2和更新版本中使用。
![修正](../assets/fix.svg)修正Fastly的Web應用程式防火牆(WAF)無法正確封鎖Cookie的問題
![修正](../assets/fix.svg)修正為特定商店檢視建立建議時，指派給非預設商店檢視的產品未顯示在&#x200B;_Recommendations產品預覽_面板中的問題
![修正](../assets/fix.svg)修正頁面產生器中的某些建議單位名稱無法顯示於店面的問題

### 3.3.2的magento/product-recommendations

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![修正](../assets/fix.svg)修正B2B支援的相依性遺失

### 3.3.1的magento/product-recommendations

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新](../assets/new.svg)已新增B2B客戶群組定價的支援。 當您在建議單位上設定[價格篩選器](filters.md)時，已登入的B2B客戶會看到所顯示產品的客戶群組定價集。

### 3.3.0的magento/product-recommendations

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新](../assets/new.svg)已新增對Adobe使用者端資料層的支援，以便標準化跨Adobe Commerce功能與服務的行為資料收集。 請參閱[讀我檔案](https://github.com/adobe/commerce-events/blob/main/packages/storefront-events-collector/README.md)以瞭解更多資訊。

### 3.2.6的magento/product-recommendations

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![修正](../assets/fix.svg)修正JavaScript模組錯誤
![修正](../assets/fix.svg)修正Fastly的Web應用程式防火牆(WAF)無法正確封鎖Cookie的問題

### 3.2.5的magento/product-recommendations

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新](../assets/new.svg)將Magento服務重新命名為[Commerce服務](https://experienceleague.adobe.com/en/docs/commerce/user-guides/integration-services/saas)，並改善管理員的可用性

### 3.2.4的magento/product-recommendations

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![修正](../assets/fix.svg)修正索引產品屬性時發生「無法擷取可設定的產品選項資料」錯誤

### 3.2.3的magento/product-recommendations

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![修正](../assets/fix.svg)修正目錄同步處理期間的「無法擷取可設定的產品選項資料」錯誤
![修正](../assets/fix.svg)修正啟用「將存放區代碼新增至URL」設定時，存放區代碼未正確設定的問題
![修正](../assets/fix.svg)已改善偵測管理員面板組態變更，以確保這些變更會反映在目錄同步處理資料中

### 3.2.2的magento/product-recommendations

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新](../assets/new.svg)已新增在建立時[預覽建議結果](create.md)的功能。 您可能需要將模組更新至最新版本。
![新](../assets/new.svg)已新增從管理員[監視及管理](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync)目錄同步處理程式的功能。
![新](../assets/new.svg)已新增[篩選器](filters.md)，以控制建議中顯示的產品。
![New](../assets/new.svg)已新增[視覺相似度](type.md#visualsim)建議型別。

### 1.2.1適用於Page Builder的magento/module-page-builder-product-recommendations

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新](../assets/new.svg)已新增`magento/product-recommendations`模組3.2.0+版本的支援

### 3.1.0的magento/product-recommendations

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![New](../assets/new.svg)已新增透過命令列[重新同步](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync)您的目錄至SaaS服務的功能。
![新](../assets/new.svg)新增支援資料庫資料表首碼
![修正](../assets/fix.svg)已移除PHP 7.1支援

### 3.0.8個magento/product-recommendations

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![修正](../assets/fix.svg)修正設定模組前，針對資料收集傳送事件，造成流量無效的問題

### 3.0.6的magento/product-recommendations

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新](../assets/new.svg) **(Beta)**&#x200B;包含新[視覺相似度](type.md#visualsim)建議型別的支援。

### 1.0.0 magento/module-visual-product-recommendations

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新的](../assets/new.svg) **(Beta)** [視覺相似度](type.md#visualsim)。 透過&#x200B;_視覺相似度_&#x200B;建議型別，您可以將建議單位部署至產品詳細資料頁面，該頁面會顯示與正在檢視之產品視覺上相似的產品。

### 3.0.5的magento/product-recommendations

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![修正](../assets/fix.svg)修正目錄匯出期間可能發生的「無法擷取產品選項資料」錯誤。
![修正](../assets/fix.svg) _儀表板上_ Revenue _[!DNL Product Recommendations]_&#x200B;欄中的貨幣符號現在正確反映設定的基本貨幣。

### 3.0.4的magento/product-recommendations

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![修正](../assets/fix.svg)已新增對Adobe Commerce 2.4.0的支援

### 3.0.3的magento/product-recommendations

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![修正](../assets/fix.svg)店面範本中改進的符號實作

### 1.0.4 magento/module-page-builder-product-recommendations for Page Builder

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

編輯Page Builder內容型別時新增![New](../assets/new.svg)產品推薦名稱

### 3.0.2 magento/product-recommendations

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

在Page Builder中選取Recommendation單位時，![新增](../assets/new.svg)在格線中新增狀態列
![修正](../assets/fix.svg)修正產品和影像URL中http/https通訊協定不正確的問題

### 3.0.1的magento/product-recommendations

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

此為主要版本發行版本。 [編輯](install-configure.md#update)您專案的根composer.json檔案。

![新的](../assets/new.svg)從備用SaaS資料空間擷取[!DNL Product Recommendations]。 這可讓您在其他非生產環境中使用產品環境中計算的[!DNL Product Recommendations]。 [切換SaaS資料空間](settings.md)進一步說明此功能。

![修正](../assets/fix.svg)修正使用uBlock Origin的購物者無法結帳的問題
![修正](../assets/fix.svg)修正傳送無關的加入購物車事件的問題

### 1.0.3適用於Page Builder的magento/module-page-builder-product-recommendations

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新](../assets/new.svg)頁面產生器支援。 透過頁面產生器整合，您可以準確且詳細地將Recommendation單位放置在Page Builder編寫內容上的任何位置。 您也可以設定標題與建議單位本身的樣式。 如需詳細資訊，請移至[頁面產生器](https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/add-content/recommendations)。

### 2.0.0的magento/product-recommendations

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.x或更新版本

![新](../assets/new.svg)一般可用性版本！

+++

## 檔案

若要進一步瞭解[!DNL Product Recommendations]和[!DNL Product Recommendations]開發：

* [使用手冊](overview.md)
* [開發人員檔案](https://experienceleague.adobe.com/en/docs/commerce/product-recommendations/developer/development-overview)
