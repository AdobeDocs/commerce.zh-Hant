---
title: 收集資料
description: 瞭解事件如何收集 [!DNL Product Recommendations]的資料。
feature: Services, Recommendations, Eventing
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 0%

---

# 收集資料

當您安裝及設定SaaS型Adobe Commerce功能（例如[[!DNL Product Recommendations]](install-configure.md)或[[!DNL Live Search]](../live-search/install.md)）時，模組會將行為資料收集部署至您的店面。 此機制會從購物者收集匿名化的行為資料，並支援[!DNL Product Recommendations]。 例如，`view`事件是用來計算`Viewed this, viewed that`建議型別，`place-order`事件是用來計算`Bought this, bought that`建議型別。

>[!NOTE]
>
>以[!DNL Product Recommendations]為目的的資料收集不包含個人識別資訊(PII)。 所有使用者識別碼（例如Cookie ID和IP位址）都需嚴格匿名處理。 瞭解[更多](https://www.adobe.com/privacy/experience-cloud.html)。

## 醫療保健客戶

如果您是醫療保健客戶，且已安裝[Data Services HIPAA擴充功能](../data-connection/hipaa-readiness.md#installation) （屬於[Data Connection](../data-connection/overview.md)擴充功能的一部分），則不會再擷取[!DNL Product Recommendations]使用的店面事件資料。 這是因為店面事件資料是在使用者端產生。 若要繼續擷取和傳送店面事件資料，請重新啟用[!DNL Product Recommendations]的事件收集。 請參閱[一般組態](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general.html#data-services)以瞭解更多資訊。

## 資料型別和事件

Product Recommendations中使用兩種型別的資料：

- **行為** — 購物者在您網站上的參與度資料，例如產品檢視、加入購物車的商品和購買。
- **目錄** — 產品中繼資料，例如名稱、價格、可用性等。

安裝`magento/product-recommendations`模組時，Adobe Sensei會彙總行為和目錄資料，並為每種建議型別建立產品建議。 產品推薦服務會以包含推薦產品&#x200B;_專案_&#x200B;的Widget形式，將這些推薦部署到您的店面。

有些建議型別會使用購物者的行為資料來訓練機器學習模型，以建立個人化建議。 其他建議型別僅使用目錄資料，不使用任何行為資料。 如果您想要在您的網站上快速開始使用產品建議，您可以使用以下僅限目錄的建議型別：

- `More like this`
- `Visual similarity`

### 冷啟動

您何時可以開始使用使用使用行為資料的建議型別？ 視情況而定。 這稱為&#x200B;_冷啟動_&#x200B;問題。

_Cold Start_&#x200B;問題是指模型訓練及生效所需的時間。 對於產品建議，這表示在網站上部署建議單位之前，請等待Adobe Sensei收集足夠的資料以訓練其機器學習模型。 模型擁有的資料越多，建議就越準確和有用。 由於資料收集會在即時網站上進行，因此最好透過安裝和設定`magento/production-recommendations`模組來提前開始此程式。

下錶針對收集每種建議型別的足夠資料所需時間提供一些一般指引：

| 建議型別 | 訓練時間 | 附註 |
|---|---|---|
| 以人氣為基礎(`Most viewed`， `Most purchased`， `Most added to cart`) | 因情況而異 | 視事件數量而定 — 檢視是最常見的檢視，因此學習速度更快；然後新增購物車，然後購買 |
| `Viewed this, viewed that` | 需要更多訓練 | 產品檢視數量相當大 |
| `Viewed this, bought that`，`Bought this, bought that` | 需要最多訓練 | 購買事件是商業網站上最罕見的事件，尤其是與產品檢視次數相比 |
| `Trending` | 需要三天的資料來建立人氣基線 | 趨勢是衡量產品受歡迎程度與其自身受歡迎基線相比的最新動量。 產品的趨勢分數是使用前景集（過去24小時的最近人氣）和背景集（72小時的最近人氣基線）計算。 如果專案的人氣在24小時內比其基準人氣明顯增加，則會獲得高趨勢分數。 每個產品都有此分數，而分數最高的專案會隨時包含最熱門的產品集。 |

其他可能影響訓練所需時間的變數：

- 較高的流量有助於加快學習速度
- 有些建議型別的訓練速度比其他建議型別快
- Adobe Commerce每四小時會重新計算一次行為資料。 在您的網站上使用建議的時間越長，建議就越準確。

為了協助您視覺化每個建議型別的訓練進度，[建立建議](create.md#readiness-indicators)頁面會顯示準備程度指標。

當您的即時網站上正在收集資料且機器學習模型正在進行訓練時，您可以完成設定建議所需的其他測試和設定工作。 當您完成此工作時，模型將擁有足夠的資料來建立有用的建議，可讓您將其部署到店面。

如果您的網站未針對大部分產品SKU取得足夠的流量（檢視、購買、趨勢），則可能沒有足夠的資料來完成學習程式。 這可能會讓管理員中的整備程度指標看起來卡住。 整備程度指標旨在為商家提供另一個資料點，以便選擇哪種推薦型別更適合他們的商店。 數字是參考指標，可能永遠無法達到100%。 [進一步瞭解](create.md#readiness-indicators)整備指標。

### 備份建議 {#backuprecs}

如果輸入資料不足以在一個單位中提供所有請求的建議專案，Adobe Commerce會提供備份建議以填入建議單位。 例如，如果您將`Recommended for you`建議型別部署至首頁，則您網站上的首次購物者未產生足夠的行為資料，因此無法精確建議個人化產品。 在此情況下，Adobe Commerce會根據`Most viewed`建議型別向此購物者顯示專案。

在輸入資料收集不足的情況下，下列建議型別會遞補為`Most viewed`建議型別：

- `Recommended for you`
- `Viewed this, viewed that`
- `Viewed this, bought that`
- `Bought this, bought that`
- `Trending`
- `Conversion (view to purchase)`
- `Conversion (view to cart)`

### 活動

[Adobe Commerce店面事件收集器](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/#quick-start)會列出所有部署到店面的事件。 該清單中有[!DNL Product Recommendations]專屬的事件子集。 當購物者與店面的推薦單位互動時，這些事件會收集資料，並支援量度以分析您的推薦執行狀況。

| 事件 | 說明 |
| --- | --- |
| `impression-render` | 在頁面上轉譯建議單位時傳送。 如果頁面有兩個建議單位（已購買、已檢視），則會傳送兩個`impression-render`事件。 此事件用於追蹤曝光次數的量度。 |
| `rec-add-to-cart-click` | 購物者按一下建議單位中專案的&#x200B;**加入購物車**&#x200B;按鈕。 |
| `rec-click` | 購物者按一下建議單位中的產品。 |
| `view` | 當建議單位變成至少50%可檢視（例如向下捲動頁面）時傳送。 例如，如果建議單位有兩行，當購物者看到一行加上第二行一個畫素時，便會傳送`view`事件。 如果購物者上下捲動頁面數次，則傳送`view`事件的次數會與購物者再次在頁面上看到整個建議單位相同。 |

>[!NOTE]
>
>已針對Luma店面最佳化產品推薦量度。 如果您的店面是透過PWA Studio實作，請參閱[PWA檔案](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/)。 如果您使用自訂前端技術，例如React或Vue JS，請瞭解如何在Headless](headless.md)環境中整合[產品推薦。

#### 必要的儀表板事件

需要下列事件才能填入[[!DNL Product Recommendations] 儀表板](workspace.md)

| 儀表板欄 | 活動 | 加入欄位 |
| ---------------- | --------- | ----------- |
| 曝光數 | `page-view`，`recs-request-sent`，`recs-response-received`，`recs-unit-render` | `unitId` |
| 檢視 | `page-view`，`recs-request-sent`，`recs-response-received`，`recs-unit-render`，`recs-unit-view` | `unitId` |
| 點按次數 | `page-view`，`recs-request-sent`，`recs-response-received`，`recs-item-click`，`recs-add-to-cart-click` | `unitId` |
| 收入 | `page-view`，`recs-request-sent`，`recs-response-received`，`recs-item-click`，`recs-add-to-cart-click`，`place-order` | `unitId`，`sku`，`parentSku` |
| LT收入 | `page-view`，`recs-request-sent`，`recs-response-received`，`recs-item-click`，`recs-add-to-cart-click`，`place-order` | `unitId`，`sku`，`parentSku` |
| CTR | `page-view`，`recs-request-sent`，`recs-response-received`，`recs-unit-render`，`recs-item-click`，`recs-add-to-cart-click` | `unitId`，`sku`，`parentSku` |
| vCTR | `page-view`，`recs-request-sent`，`recs-response-received`，`recs-unit-render`，`recs-unit-view`，`recs-item-click`，`recs-add-to-cart-click` | `unitId`，`sku`，`parentSku` |

以下事件並非產品建議所特有，但Adobe Sensei必須具備，才能正確解譯購物者資料：

- `view`
- `add-to-cart`
- `place-order`

#### 建議型別

此表格說明每種建議型別所使用的事件。

| 建議型別 | 活動 | 頁面 |
| --- | --- | --- |
| 檢視次數最多 | `page-view`<br>`product-view` | 產品詳細資料頁面 |
| 購買最多 | `page-view`<br>`complete-checkout` | 購物車/結帳 |
| 加入購物車次數最多 | `page-view`<br>`add-to-cart` | 產品詳細資料頁面<br>產品清單頁面<br>購物車<br>願望清單 |
| 已檢視這個專案，已檢視那個專案 | `page-view`<br>`product-view` | 產品詳細資料頁面 |
| 已檢視此專案，但購買了其他專案 | 產品推薦 | `page-view`<br>`product-view` | 產品詳細資料頁面<br>購物車/結帳 |
| 已購買此專案，已購買該專案 | 產品推薦 | `page-view`<br>`product-view` | 產品詳細資料頁面 |
| 趨勢 | `page-view`<br>`product-view` | 產品詳細資料頁面 |
| 轉換：檢視以購買 | 產品推薦 | `page-view`<br>`product-view` | 產品詳細資料頁面 |
| 轉換：檢視以購買 | 產品推薦 | `page-view`<br>`complete-checkout` | 購物車/結帳 |
| 轉換：檢視到購物車 | 產品推薦 | `page-view`<br>`product-view` | 產品詳細資料頁面 |
| 轉換：檢視到購物車 | 產品推薦 | `page-view`<br>`add-to-cart` | 產品詳細資料頁面<br>產品清單頁面<br>購物車<br>願望清單 |

#### 警告

- 廣告封鎖程式和隱私權設定可能會防止擷取事件，且可能導致參與和收入[量度](workspace.md#column-descriptions)少報。 此外，由於購物者離開頁面或網路問題，部分事件可能不會傳送。
- [Headless實作](headless.md)必須實作事件以支援產品建議儀表板。
- 對於可設定的產品，「產品建議」會使用建議單位中上層產品的影像。 如果可設定的產品未指定影像，則該特定產品的建議單位將為空白。

>[!NOTE]
>
>如果啟用[Cookie限制模式](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html)，Adobe Commerce不會收集行為資料，直到購物者同意使用Cookie為止。 如果「Cookie限制模式」已停用，Adobe Commerce會依預設收集行為資料。
