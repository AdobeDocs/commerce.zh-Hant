---
title: 收集資料
description: 瞭解事件如何收集 [!DNL Product Recommendations]的資料。
feature: Services, Recommendations, Eventing
exl-id: 0d5317e3-c049-4fcd-a8e4-228668d89386
TQID: https://experienceleague.adobe.com/efHRMj3u3w-xvUgMnEYDpX0D-BDCUyjhhrkMaa3n-xg
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 88a0b1a238090dec85e0f79082d264b720999fee
workflow-type: tm+mt
source-wordcount: 937
ht-degree: 0%

---

# 收集資料

當您安裝和設定[[!DNL Product Recommendations]](install-configure.md)時，模組會將行為資料收集部署到您的店面。 此機制會從購物者收集匿名化的行為資料，並支援[!DNL Product Recommendations]。 例如，`view`事件是用來計算`Viewed this, viewed that`建議型別，`place-order`事件是用來計算`Bought this, bought that`建議型別。

若要深入瞭解[!DNL Product Recommendations]事件所收集的行為資料，請參閱[開發人員檔案](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#product-recommendations)。

>[!NOTE]
>
>以[!DNL Product Recommendations]為目的的資料收集不包含個人識別資訊(PII)。 所有使用者識別碼（例如Cookie ID和IP位址）都需嚴格匿名處理。 瞭解[更多](https://www.adobe.com/privacy/experience-cloud.html)。

## 醫療保健客戶

如果您是醫療保健客戶，且已安裝[資料服務HIPAA擴充功能](../data-connection/hipaa-readiness.md#installation) （包含在[資料連線](../data-connection/overview.md)擴充功能中），則[!DNL Product Recommendations]會停止收集店面事件資料，因為資料是在使用者端產生。

若要繼續收集和傳送店面事件資料，請重新啟用[!DNL Product Recommendations]的事件收集。 如需詳細資訊，請參閱[一般組態](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/config/general/general#data-services)。

## 資料型別和事件

Product Recommendations中使用兩種型別的資料：

- **行為** — 購物者在您網站上的參與度資料，例如產品檢視、加入購物車的商品和購買。
- **目錄** — 產品中繼資料，例如名稱、價格、可用性等。

安裝`magento/product-recommendations`模組時，Adobe AI會彙總行為和目錄資料，並為每種建議型別建立產品建議。 產品推薦服務會以包含推薦產品&#x200B;_專案_&#x200B;的Widget形式，將這些推薦部署到您的店面。

有些建議型別會使用購物者的行為資料來訓練機器學習模型，並產生個人化建議。 其他則僅依賴目錄資料。 若要快速開始使用產品建議，請從下列僅目錄建議型別中選擇：

- `More like this`
- `Visual similarity`

### 冷啟動

您何時可以開始使用使用使用行為資料的建議型別？ 視情況而定。 此情況稱為&#x200B;_冷啟動_&#x200B;問題。

_冷開始_&#x200B;問題是機器學習模型訓練所需的時間，之後才能產生有效的建議。 針對產品建議，Adobe AI必須先收集足夠的資料以訓練其模型，才能部署建議單位。 更多資料通常會改善建議的準確性和實用性。 因為資料收集會在您的即時網站上進行，請透過安裝和設定`magento/product-recommendations`模組來提前開始此程式。

下錶針對收集每種建議型別的足夠資料所需時間提供一些一般指引：

| 建議型別 | 訓練時間 | 附註 |
|---|---|---|
| 以人氣為基礎(`Most viewed`， `Most purchased`， `Most added to cart`) | 因情況而異 | 視事件數量而定 — 檢視是最常見的檢視，因此學習速度更快；然後新增購物車，然後購買 |
| `Viewed this, viewed that` | 需要更多訓練 | 產品檢視數量相當大 |
| `Viewed this, bought that`, `Bought this, bought that` | 需要最多訓練 | 購買事件是商業網站上最罕見的事件，尤其是與產品檢視次數相比 |
| `Trending` | 需要三天的資料來建立人氣基線 | 趨勢是衡量產品受歡迎程度與其自身受歡迎基線相比的最新動量。 產品的趨勢分數是使用前景集（過去24小時的最近人氣）和背景集（72小時的最近人氣基線）計算。 如果專案的人氣在24小時內比其基準人氣明顯增加，則會獲得高趨勢分數。 每個產品都有此分數，而分數最高的專案會隨時包含最熱門的產品集。 |

其他可能影響訓練所需時間的變數：

- 較高的流量有助於加快學習速度
- 有些建議型別的訓練速度比其他建議型別快
- Adobe Commerce每四小時會重新計算一次行為資料。 在您的網站上使用建議的時間越長，建議就越準確。

為了協助您視覺化每個建議型別的訓練進度，[建立建議](create.md#readiness-indicators)頁面會顯示準備程度指標。

當您的即時網站收集資料並訓練機器學習模型時，請完成其餘的測試和設定工作。 當模型擁有足夠的資料以產生有用的建議後，將建議單位部署到您的店面。

如果您的網站未收到適用於大部分產品SKU的足夠流量（檢視、購買或趨勢），則學習流程可能無法完成，導致管理員中的整備程度指標顯示為卡住。 整備程度指標可協助商家為其商店選擇最佳建議型別，但僅作為指南，且永遠無法達到100%。 進一步瞭解整備程度指標。 [進一步瞭解](create.md#readiness-indicators)整備指標。

### 備份建議 {#backuprecs}

當輸入資料不足導致建議單位無法傳回所有請求的專案時，Adobe Commerce會以備份建議填入。 例如，您在首頁上部署`Recommended for you`建議型別後，首次購物者可能無法針對個人化建議產生足夠的行為資料。 在此案例中，Adobe Commerce會根據`Most viewed `建議型別顯示專案。

如果輸入資料收集不足，下列建議型別會遞補為`Most viewed`建議型別：

- `Recommended for you`
- `Viewed this, viewed that`
- `Viewed this, bought that`
- `Bought this, bought that`
- `Trending`
- `Conversion (view to purchase)`
- `Conversion (view to cart)`

#### 警告

- 廣告封鎖程式和隱私權設定可能會防止擷取事件，且可能導致參與和收入[量度](workspace.md#column-descriptions)少報。 此外，由於購物者離開頁面或網路問題，部分活動未傳送。
- [Headless實作](headless.md)必須實作事件以支援產品建議儀表板。
- 對於可設定的產品，「產品建議」會使用父產品的影像。 如果父級產品沒有影像，則該產品不會出現在建議單位中。

>[!NOTE]
>
>如果啟用[Cookie限制模式](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law)，Adobe Commerce不會收集行為資料，直到購物者同意使用Cookie為止。 如果「Cookie限制模式」已停用，Adobe Commerce會依預設收集行為資料。
