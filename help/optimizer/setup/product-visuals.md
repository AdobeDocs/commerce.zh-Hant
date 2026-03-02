---
title: 透過AEM Assets呈現產品視覺效果
description: 瞭解如何在 [!DNL Adobe Commerce Optimizer]中使用產品影像的AEM Assets。
feature: CMS, Media, Configuration, Integration
role: Admin, Developer
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"
source-git-commit: bf1d88ef7daec25872678bb27bce0bb7c97fd296
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---


# 透過AEM Assets呈現產品視覺效果

產品視覺效果可讓[!DNL Adobe Commerce Optimizer]商家透過Adobe Experience Manager (AEM) Assets管理產品影像。 此整合提供順暢的工作流程，可讓您使用目錄圖層，將高品質的產品影像從AEM Assets同步至[!DNL Commerce Optimizer]目錄。

## 主要優點

* **集中式資產管理**：管理企業級數位資產管理解決方案AEM Assets中的所有產品影像。
* **自動同步**：當資產在AEM Assets中核准或更新時，產品影像會自動同步。
* **Dynamic Media傳遞**：利用Dynamic Media與OpenAPI功能，將影像傳遞最佳化。
* **目錄圖層**：產品影像已套用為目錄圖層，可讓您在基本目錄上覆蓋AEM Assets影像。

## 運作方式

整合有兩個主要流程：

* **從AEM Assets**：當資產被核准、拒絕或移除時，事件會透過Adobe Pipeline傳輸至Assets Integration Service。 此服務會使用`match-by-SKU`或自訂比對器策略比對資產與產品，然後將`product-asset`對應傳送至[!DNL Commerce Optimizer]，並儲存為產品層。

* **從ACO**：在[!DNL Commerce Optimizer]中更新產品時，事件會透過Adobe管道傳輸至Assets整合服務。 此服務會將任何相符的資產對應同步回ACO。

更新的影像可透過店面API （目錄服務、即時搜尋、產品推薦）取得。

### Source和圖層設定

AEM Assets中的影像會透過以下來源設定擷取為目錄層：

> 來源設定的範例

```json
{
  "source": {
    "locale": "en-US",
    "layer": "AEM-Assets"
  }
}
```

此設定可確保將AEM Assets影像套用為基本產品目錄上的覆蓋圖。

## 先決條件

在啟用產品視覺效果之前，請確定您符合Commerce Optimizer[的](../../aem-assets-integration/get-started/configure-aco.md#prerequisites)必要條件。

## 設定

若要啟用整合，請[建立支援票證](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket)，其中包含您的[!DNL Commerce Optimizer]和AEM Assets詳細資料。 Adobe支援會設定整合，並在Assets整合服務中註冊您的租使用者。

如需入門資訊，請參閱[設定Commerce Optimizer的AEM Assets](../../aem-assets-integration/get-started/configure-aco.md)。

### 設定AEM Assets中繼資料

若要啟用自動產品比對，請在AEM Assets中使用Commerce中繼資料設定您的資產。

請參閱[設定AEM Assets](../../aem-assets-integration/get-started/configure-aco.md#configure-aem-assets)，以取得必要的中繼資料欄位和步驟。

## 使用產品視覺效果

設定整合後，請透過AEM Assets管理您的產品影像。

### 將影像新增至產品

1. 將影像上傳至您的AEM Assets存放庫。

1. 將Commerce中繼資料新增至資產。 請參閱[將中繼資料套用至資產](../../aem-assets-integration/get-started/configure-aco.md#step-3-apply-metadata-to-assets)。

1. 核准要傳送的資產。 資產必須處於&#x200B;**已核准**&#x200B;狀態才能觸發同步處理。

1. 影像會自動同步至[!DNL Commerce Optimizer]。

### 套用AEM-Assets圖層

若要在店面顯示AEM Assets影像，請[將`AEM-Assets`圖層指派給目錄檢視](catalog-layer.md#assign-the-aem-assets-layer-to-a-catalog-view)。

## 更多相關資訊

* [目錄圖層](catalog-layer.md)
* [目錄檢視](catalog-view.md)
* [AEM Assets整合指南](../../aem-assets-integration/overview.md)
