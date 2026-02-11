---
title: 邊界和限制
description: 瞭解 [!DNL Product Recommendations] 的界限和限制，以確保其符合您的業務需求。
role: Admin, Developer
source-git-commit: 66830c9d950a27269aca1bda0dcc7d0d86f05647
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 0%

---

# 邊界和限制

請檢閱下列界限和限制，以確保[!DNL Product Recommendations]符合您的業務需求。 瞭解這些限制可幫助您規劃實作、設定篩選器並避免常見問題。

## 一般

- **產品型別** — 支援的產品型別包括&#x200B;_簡單_、_可設定_、_虛擬_、_可下載_&#x200B;和&#x200B;_禮卡_。 不支援&#x200B;_套件_、_群組_&#x200B;和自訂產品型別。 如果您的目錄包含大量不支援的產品型別，您可能會預期較低[整備分數](create.md#readiness-indicators)。 請參閱[依產品型別篩選](filters.md#type)。
- **含有空格的SKU** — 含有空格的SKU可能會降低建議的相關性，應儘可能避免。
- **購物車頁面** — 當您的商店設定為在將產品新增到購物車後立即[顯示購物車頁面時，購物車頁面不支援產品建議](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/stores-sales/point-of-purchase/cart/cart-configuration)。 請參閱[建立建議](create.md)。
- **子產品** — 可設定產品的子產品（可見度&#x200B;_無法個別顯示_）未顯示在建議單位中。 只能顯示可設定的（父）產品。 請參閱[篩選產品](filters.md#product)。
- **已停用或未顯示的產品** — 已停用或未個別顯示的產品永遠都不會出現在建議中，也不能在產品篩選器中選取。
- **特殊價格** - [特殊價格](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/catalog/products/pricing/product-price-special)不支援在建議單位中使用開始和結束日期。 具有特殊價格的產品可能會出現在建議中，但單位不會顯示特殊價格、開始日期或結束日期。 購物者會看到一般價格（或您的目錄/價格摘要所提供的其他價格資料），直到開啟產品頁面為止。

## 建議單位

- **每個頁面型別的作用中單位** — 您最多可以為每個頁面型別（首頁、類別、產品詳細資料、購物車、確認）建立50個作用中建議單位。 達到上限時，建立流程中的頁面型別會呈現灰色。
- **每單位的產品** — 建議單位中顯示的產品數量可以從5 （預設）設定為最多20。
- **草稿狀態** — 將建議儲存為草稿後，您無法修改該單位的頁面型別或建議型別。 啟用之前可以編輯其他設定。

## 篩選和條件

- **動態條件** — 除了首頁之外，其他每個頁面型別都可使用動態條件（例如「與目前產品屬於相同類別的產品」或「相對價格範圍」）。 透過「頁面產生器」放置建議的頁面也無法使用這些建議。 請參閱[條件](filters.md#conditions)。

## 預覽和非生產環境

- **最近檢視的預覽** — 無法在管理員中預覽&#x200B;_最近檢視的_&#x200B;建議型別，因為資料是根據瀏覽器歷史記錄，無法在管理員內容中使用。 請參閱[預覽建議](create.md#preview)。
- **來自其他資料空間的建議** — 當您從非生產店面中的其他SaaS資料空間[擷取建議](settings.md) （例如，生產環境）時，您可以檢視建議，但無法點進這些建議的產品頁面。 這是專為預覽和測試而設計。
- **GraphQL和替代資料空間** — 透過[GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/)使用產品建議時，`alternateEnvironmentId`引數（用於從其他資料空間擷取建議）無法使用。 使用REST API或管理員設定，在非生產環境中切換建議來源。

## API和設定

- **API金鑰（4.x和更新版本）** — 您必須提供適用於沙箱和生產環境的公開和私人API金鑰。 如果您未提供這兩組API金鑰，將無法在「管理員」中存取「產品建議」功能。 您店面上的資料收集和現有的建議會繼續運作。 請參閱[安裝與設定](install-configure.md)。

## Cookie限制

- 當啟用[Cookie限制模式](setting-cookie.md)且購物者未接受Cookie時，某些依賴行為資料的建議型別可能不會顯示或會顯示有限的結果。
- 啟用Cookie限制時，不依賴行為資料的建議型別（例如&#x200B;_檢視次數最多_、_視覺相似度_）仍可繼續運作。
- 啟用Cookie限制時，在購物者同意前，「產品建議」不會收集或儲存Cookie或本機儲存中的行為資料。

## 頁面產生器

- **量度和存放區檢視** - Page Builder建議單位的量度只會出現在產品建議工作區的預設存放區檢視中。 若要在非預設商店檢視上檢視頁面產生器建議量度，您必須開啟並[編輯](edit.md)該商店檢視中的頁面產生器建議單位並加以儲存；然後該商店檢視會顯示量度。 請參閱[頁面產生器整合](page-builder.md)。

## B2B

- 產品建議遵循[類別許可權](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/category-permissions.html)、[共用類別](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared.html)和客戶群組特定定價。 購物者只會根據自己的區段和目錄指派，看見他們可存取之產品的建議。 請參閱[上線](onboarding.md)。

## 資料與整備

- **行為資料** — 許多建議型別需要足夠的店面行為資料（檢視、加入購物車、購買）。 在收集到足夠的資料之前，新存放區或低流量存放區可能會看到這些型別的有限或無結果。 在管理員中監視[整備指標](create.md#readiness-indicators)。
- **沒有生產資料的測試** — 在沒有行為資料的非生產環境中，唯一可以測試而不從生產擷取的建議型別是&#x200B;_更類似於_，它僅使用目錄型相似度。 請參閱[中繼環境](staging-environment.md)。

## 疑難排解

如需目錄同步、建議未顯示或其他常見問題的說明，請搜尋[Commerce知識庫](https://experienceleague.adobe.com/zh-hant/docs/commerce-knowledge-base/kb/overview)或聯絡[支援](https://experienceleague.adobe.com/zh-hant/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide)。
