---
title: '[!DNL Manage the Data Export extension]'
description: 瞭解如何升級 [!DNL Data Export] 擴充功能，以及移除或停用不需要的資料匯出服務。
role: Admin, Developer
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# 管理SaaS資料匯出擴充功能

SaaS服務的[!DNL data export]擴充功能是啟用Adobe Commerce與連線的Commerce服務之間的資料收集與同步化的模組集合。

Adobe Commerce服務擴充功能的中繼包含特定模組，例如
作為[即時搜尋](/help/live-search/overview.md)、[產品建議](/help/product-recommendations/overview.md)和[目錄服務](/help/catalog-service/overview.md)。 如果您使用這些服務，則不需要個別安裝即可啟用Data Export擴充功能。

## 移除或停用Commerce資料匯出功能

如果您不需要其中一個已安裝的商務資料匯出模組，請使用`magento:module:disable` CLI命令加以停用。

例如，有一個[類別API](https://developer.adobe.com/commerce/services/graphql/catalog-service/categories/)在內部使用類別許可權摘要資料。 如果您未使用此API，可以停用類別許可權摘要的資料匯出。

```shell script
bin/magento module:disable Magento_CategoryPermissionDataExporter Magento_SaaSCategoryPermissions
```

### 將模組更新至特定版本

您可以使用Composer更新任何已安裝的商務資料匯出模組。 例如，您可以將模組更新至指定版本，也可以更新任何必要的相依性。

1. 登入Commerce應用程式伺服器。

1. 從命令列，使用撰寫器更新模組：

   ```bash
   composer require magento/module-saas-price:103.3.1 --with-all-dependencies
   ```

如果已在雲端基礎結構上部署Commerce執行個體，請從您的雲端專案目錄更新擴充功能。 請參閱&#x200B;_雲端基礎結構上的Adobe Commerce指南_&#x200B;中的[升級擴充功能](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/extensions#upgrade-an-extension)。
