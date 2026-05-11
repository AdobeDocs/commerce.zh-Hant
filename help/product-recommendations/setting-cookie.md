---
title: 處理Cookie限制
description: 瞭解產品建議如何處理Cookie限制和隱私權法規遵循。
exl-id: 7e7342db-b903-4105-93c0-e4022c81673b
TQID: https://experienceleague.adobe.com/qqgwO4KI4koSBcYu9mdrjb6AQFW4guxk6dfLDBEwVb8
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 454
ht-degree: 0%

---

# 處理Cookie限制

Adobe Commerce和Magento Open Source都會在資料儲存在瀏覽器Cookie中之前要求您同意。 如需詳細資訊，請參閱[Cookie限制模式](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html?lang=zh-Hant)。

## 產品建議如何處理Cookie限制

當您將`magento/product-recommendations`模組部署到生產環境時，它會開始收集店面上的購物者互動事件。 此資料可儲存在瀏覽器Cookie或本機儲存中，以支援建議演演算法。

>[!IMPORTANT]
>
>啟用Cookie限制時，產品建議現在會遵守Cookie限制模式，不會在Cookie或本機儲存空間中收集或儲存任何資料。 其中包括用於個人化推薦的行為資料。

### 受Cookie限制影響的資料

啟用Cookie限制模式時，不會收集下列產品建議資料：

- **行為資料**：產品檢視、加入購物車的動作、購買，以及其他購物者互動。
- **工作階段資料**：購物者工作階段資訊與建議單位互動。
- **Personalization資料**：用於建議型別（例如「最近檢視」和「最常購買」）的資料。

### 對建議型別的影響

當啟用Cookie限制模式且購物者未接受Cookie時，某些建議型別可能不會顯示或會顯示有限的結果：

- **最近檢視的產品**：需要工作階段資料儲存在Cookie/本機儲存體中。
- **為您推薦**：需要行為資料才能進行個人化。
- **已購買，已購買**：需要購買歷程記錄資料。

>[!NOTE]
>
>即使啟用Cookie限制，不依賴行為資料（例如「檢視次數最多」和「視覺相似度」）的建議型別仍會繼續正常運作。

## 協力廠商Cookie同意解決方案

產品Recommendations可能不會自動整合協力廠商Cookie同意解決方案。 商家有責任確保資料收集符合適用的隱私權法規。

如果您使用自訂Cookie同意解決方案，則可實作do-not-track Cookie機制來控制資料收集。

### 實作do-not-track cookie

您可以使用`mg_dnt` Cookie以程式設計方式控制資料收集：

#### Cookie名稱

```javascript
const DNT_COOKIE = "mg_dnt";
```

#### 停用資料收集

當使用者拒絕Cookie時，請設定do-not-track Cookie：

```javascript
$.mage.cookies.set(DNT_COOKIE, true);
```

#### 啟用資料收集

當使用者接受Cookie時，請清除Do-not-track Cookie：

```javascript
$.mage.cookies.clear(DNT_COOKIE);
```

## 測試Cookie限制模式

若要測試Product Recommendations在Cookie限制下的行為方式：

1. 在您的Adobe Commerce設定中啟用Cookie限制模式。
1. 造訪您的店面而不接受Cookie。
1. 確認建議單位顯示適當的遞補內容。
1. 接受Cookie並確認建議開始收集資料。

## 隱私權法規遵循

產品Recommendations資料收集不包含個人識別資訊(PII)。 所有使用者識別碼（例如Cookie ID和IP位址）都會進行匿名處理。 如需詳細資訊，請參閱[Adobe隱私權原則](https://www.adobe.com/privacy/policy.html)。

>[!TIP]
>
>若醫療保健客戶使用資料服務HIPAA擴充功能，則可能需要額外設定。 如需詳細資訊，請參閱[HIPAA整備](../data-connection/hipaa-readiness.md)。
