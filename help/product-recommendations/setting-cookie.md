---
title: 處理Cookie限制
description: 瞭解產品建議如何處理Cookie限制。
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# 處理Cookie限制

Adobe Commerce和Magento Open Source都會在資料儲存在瀏覽器Cookie中之前要求您同意。 如需詳細資訊，請參閱[Cookie限制模式](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html)。

當您將`magento/product-recommendations`模組部署到生產環境時，它會開始收集店面上的購物者互動事件。 因為這些事件的資料可儲存在瀏覽器Cookie或本機儲存空間中，此功能會在購物者給予Cookie同意前不收集事件，以支援Cookie限制模式。

協力廠商Cookie同意解決方案可能無法使用此功能。 每個商家都有責任確保在取得Cookie同意前不會進行資料收集，因為法律通常會有此規定。 如果您透過自訂程式碼管理Cookie同意，則可以使用名稱為`mg_dnt`的Do-Not-Track Cookie來限制資料收集。

- Cookie的名稱：

  ```text
  `const DNT_COOKIE = "mg_dnt";`
  ```

- 設定do-not-track Cookie以停用資料收集：

  ```text
  `$.mage.cookies.set(DNT_COOKIE, true);`
  ```

- 若要在使用者接受Cookie時清除Cookie：

  ```text
  `$.mage.cookies.clear(DNT_COOKIE);`
  ```
