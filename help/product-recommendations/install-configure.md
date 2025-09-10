---
title: 安裝與設定
description: 瞭解如何安裝、更新及解除安裝 [!DNL Product Recommendations]。
role: Admin, Developer
exl-id: 2e7f6454-d4cb-44bc-982f-354a179e8e59
source-git-commit: 3821893c3df01e2e36ab0142616e52c1c92b4d51
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# 安裝與設定

將[!DNL Product Recommendations]部署至您的店面和管理員，需要您安裝模組並設定[Commerce Services Connector](../landing/saas.md)。 發佈更新時，您可以輕鬆將安裝更新為最新版本。

- [安裝](#install)
- [設定](#configure)
- [更新](#update)
- [解除安裝](#uninstall)

## 安裝[!DNL Product Recommendations] {#install}

由於[!DNL Product Recommendations]模組是獨立的中繼套件，因此比Adobe Commerce更頻繁地發行更新。 若要確定您使用最新的錯誤修正和功能，請參閱[發行說明](release-notes.md)。

>[!IMPORTANT]
>
>請確定您擁有使用產品建議的正確[權益](../landing/saas.md#credentials)。

使用撰寫器安裝`magento/product-recommendations`模組：

```bash
composer require magento/product-recommendations
```

### 新增頁面產生器支援 {#pbsupport}

Page Builder的[!DNL Product Recommendations]為選用模組，需另行安裝。 若要搭配Page Builder使用[!DNL Product Recommendations]，請執行以下命令來安裝模組：

```bash
composer require magento/module-page-builder-product-recommendations
```

透過在頁面產生器中啟用[!DNL Product Recommendations]，您可以將現有的作用中[建議單位](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/page-builder/add-content/recommendations)新增到頁面產生器中建立的任何內容，例如頁面、區塊和動態區塊。

如需進一步說明，請參閱[搭配頁面產生器內容 [!DNL Product Recommendations] 使用](page-builder.md)。

### 新增視覺相似度推薦型別 {#vissimsupport}

_視覺相似度_&#x200B;建議型別可讓您將建議單位部署至產品詳細資料頁面，該頁面會顯示與正在檢視的產品[視覺上類似](type.md#visualsim)的產品。 當產品的影像和視覺方面是購物體驗的重要部分時，此建議型別最有用。 執行下列命令，安裝&#x200B;_視覺相似度_&#x200B;建議型別：

```bash
composer require magento/module-visual-product-recommendations
```

## 設定[!DNL Product Recommendations] {#configure}

1. 安裝`magento/product-recommendations`模組後，請指定API金鑰並選取SaaS資料空間，以設定[Commerce Services Connector](../landing/saas.md)。

   設定此連線會啟用Commerce執行個體、目錄服務和其他支援服務之間的資料同步和通訊。 資料同步處理由[SaaS Data Export擴充功能](../data-export/overview.md)處理。

1. 若要確保目錄匯出可以正確執行，請確認[cron](https://experienceleague.adobe.com/zh-hant/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs)工作和[索引子](https://experienceleague.adobe.com/zh-hant/docs/commerce-operations/configuration-guide/cli/manage-indexers)正在執行，且`Product Feed`索引子設定為`Update by Schedule`。

當您成功將Commerce應用程式連結至Commerce Services並指定[SaaS資料空間](../landing/saas.md#saas-configuration)後，目錄同步作業就會開始。 然後，您可以[驗證](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/)行為資料正在傳送至您的店面。

## 監控資料同步並疑難排解

透過Commerce Admin，您可以使用[資料管理控制面板](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/systems/data-transfer/data-dashboard)來監視同步化程式。 使用[Commerce CLI](../data-export/data-export-cli-commands.md#troubleshooting)和記錄檔來管理和疑難排解程式。

然後，您可以[驗證](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/)行為資料正在傳送至您的店面。

## 更新您的[!DNL Product Recommendations]安裝 {#update}

如同所有的Adobe Commerce，[!DNL Product Recommendations]使用Composer進行安裝和更新。 若要更新`magento/product-recommendations`模組，請執行下列動作：

```bash
composer update magento/product-recommendations --with-dependencies
```

若要更新為主要版本，例如從5.0到6.0，您必須編輯專案的根`composer.json`檔案。 （如需最新版本的相關資訊，請參閱[發行說明](release-notes.md)。） 例如，讓我們開啟主要`composer.json`檔案並搜尋`magento/product-recommendations`模組：

```json
"require": {
    ...
    "magento/product-recommendations": "^5.0",
    ...
}
```

讓我們將主要版本從`5.0`增加到`6.0`：

```json
"require": {
    ...
    "magento/product-recommendations": "^6.0",
    ...
}
```

儲存`composer.json`檔案並執行：

```bash
composer update magento/product-recommendations --with-dependencies
```

或者，如果您已安裝`magento/module-visual-product-recommendations`與`magento/module-page-builder-product-recommendations`模組：

```bash
composer update --with-dependencies magento/product-recommendations magento/module-visual-product-recommendations magento/module-page-builder-product-recommendations
```

>[!NOTE]
>
> 在3.x.x版的Product Recommendations中，您只需要單一API金鑰。 在4.x.x版和更新版本中，您必須提供適用於沙箱和生產環境的公開和私人API金鑰。 如果您未提供這兩組API金鑰，將無法在「管理員」中存取「產品建議」功能。 不過，資料收集會在您的店面中持續進行，而現有的建議會持續向您的購物者顯示。

## 防火牆

若要讓產品建議通過防火牆，請將`commerce.adobe.io`新增至允許清單。

## 解除安裝[!DNL Product Recommendations] {#uninstall}

如有必要，您可以[解除安裝](https://experienceleague.adobe.com/zh-hant/docs/commerce-operations/installation-guide/tutorials/uninstall-modules)產品建議模組。
