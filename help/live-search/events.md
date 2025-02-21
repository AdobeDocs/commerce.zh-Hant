---
title: '[!DNL Live Search]個事件'
description: 瞭解事件如何收集 [!DNL Live Search]的資料。
feature: Services, Eventing
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# [!DNL Live Search]個事件

[!DNL Live Search]會使用事件來增強搜尋演演算法，例如「檢視次數最多」和「已檢視這個專案，已檢視那個專案」。 雖然[Commerce範例Luma佈景主題](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/design/themes/themes#the-default-theme)已可立即使用事件，但Headless和其他自訂實作必須根據自己的需求實作事件。

此表格說明[!DNL Live Search] [排名策略](rules-add.md#intelligent-ranking)所使用的事件。

| 排名策略 | 活動 | 頁面 |
| --- | --- | --- |
| 檢視次數最多 | `page-view`<br>`product-view` | 產品詳細資料頁面 |
| 購買最多 | `page-view`<br>`complete-checkout` | 購物車/結帳 |
| 加入購物車次數最多 | `page-view`<br>`add-to-cart` | 產品詳細資料頁面<br>產品清單頁面<br>購物車<br>願望清單 |
| 已檢視這個專案，已檢視那個專案 | `page-view`<br>`product-view` | 產品詳細資料頁面 |

>[!NOTE]
>
>以[!DNL Live Search]為目的的資料收集不包含個人識別資訊(PII)。 所有使用者識別碼（例如Cookie ID和IP位址）都需嚴格匿名處理。 [深入瞭解](https://www.adobe.com/privacy/experience-cloud.html)。

## 必要的儀表板事件

有些事件需要填入[即時搜尋儀表板](performance.md)

| 儀表板區域 | 活動 | 加入欄位 |
| ------------------- | ------------- | ---------- |
| 不重複搜尋 | `page-view`，`search-request-sent`，`search-response-received` | `searchRequestId` |
| 零結果搜尋 | `page-view`，`search-request-sent`，`search-response-received` | `searchRequestId` |
| 零結果率 | `page-view`，`search-request-sent`，`search-response-received` | `searchRequestId` |
| 熱門搜尋 | `page-view`，`search-request-sent`，`search-response-received` | `searchRequestId` |
| 平均 按一下位置 | `page-view`，`search-request-sent`，`search-response-received`，`search-results-view`，`search-product-click` | `searchRequestId` |
| 點進率 | `page-view`，`search-request-sent`，`search-response-received`，`search-results-view`，`search-product-click` | `searchRequestId`，`sku`，`parentSku` |
| 轉換率 | `page-view`，`search-request-sent`，`search-response-received`，`search-results-view`，`search-product-click`，`product-view`，`add-to-cart`，`place-order` | `searchRequestId`，`sku`，`parentSku` |

### 必要內容

所有事件都需要`Page`和`Storefront`內容。 這應該發生在頁面層級/店面應用程式層，而不是產生個別事件時（例如，在PHP店面中，PHP應用程式容器負責在執行階段設定它們）。

## 使用情況

以下是`search-request-sent`事件的實作範例：

```javascript
const mse = window.magentoStorefrontEvents;

/* set in application container */
// mse.context.page(pageCtx);
// mse.context.setStorefrontInstance(storefrontCtx);

/* set before firing event */
mse.context.setSearchInput(searchInputCtx);
mse.publish.searchRequestSent("search-bar");
```

## 警告

- 廣告封鎖程式和隱私權設定可能會防止擷取事件，且可能導致參與和收入[量度](performance.md)少報。 此外，由於購物者離開頁面或網路問題，部分事件可能不會傳送。
- Headless實作必須實作事件來推動智慧型銷售。

>[!NOTE]
>
>如果啟用[Cookie限制模式](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html)，Adobe Commerce不會收集行為資料，直到購物者同意使用Cookie為止。 如果「Cookie限制模式」已停用，Adobe Commerce會依預設收集行為資料。
