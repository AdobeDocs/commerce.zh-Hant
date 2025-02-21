---
title: 安裝
description: 使用適用於PHP的撰寫器為Adobe Commerce店面安裝 [!DNL Store Fulfillment solution] 。
role: Admin, Developer
level: Intermediate
feature: Shipping/Delivery, Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---


# 安裝

在非生產環境中完成[!DNL Store Fulfillment for Adobe Commerce by Walmart Commerce Technologies]擴充功能的初始安裝，且佇列管理員正在執行且快取設定為允許例外狀況處理。 確保您的開發環境包含開發工具，以確保操作和維護您的Adobe Commerce執行個體的最佳實務。

>[!TIP]
>
>依照&#x200B;_Adobe Commerce升級指南_&#x200B;中的[升級指示](https://experienceleague.adobe.com/docs/commerce-operations/upgrade-guide/modules/upgrade.html)，升級Adobe Commerce內部部署的Store Fulfillment擴充功能。 如需雲端基礎結構上的Adobe Commerce，請參閱&#x200B;*雲端基礎結構上的Commerce指南*&#x200B;中的[升級擴充功能](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/extensions.html#upgrade-an-extension)。

## 先決條件

檢閱Store Fulfillment解決方案的[需求](solution-requirements.md)，並收集必要的資訊，然後再安裝或升級Adobe Commerce的[!DNL Store Fulfillment]擴充功能。

如果您已安裝搶鮮版或Beta版的Adobe Commerce適用的Store Fulfillment擴充功能，請在安裝目前版本之前使用以下命令將其移除。

```bash
rm -rf composer.lock vendor/walmart &&
composer require walmart/magento-bopis-metapackage:1.0.0
```

## 安裝需求

- **存取Walmart Commerce Technologies軟體封存（.zip檔案）的Store Fulfillment** — 在上線和啟用程式期間，請與您的客戶經理合作，存取Store Fulfillment擴充功能的安裝檔案。

- **Adobe Commerce帳戶資訊** — 安裝[!DNL Store Fulfillment]解決方案需要[[!DNL Commerce] 帳戶](https://experienceleague.adobe.com/en/docs/commerce-admin/start/commerce-account/commerce-account-create){target="_blank"}。 您需要帳戶ID和認證，且擁有[!DNL Adobe Commerce]專案的擁有者或管理員存取權。

- 對於雲端基礎結構專案上的[!DNL Adobe Commerce]，軟體安裝程式必須擁有雲端專案的管理員存取權。 請參閱[管理使用者存取權](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/user-access)。

- **使用Composer與[!DNL Commerce CLI]**&#x200B;的體驗 — 請參閱[一般CLI安裝](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions){target="_blank"}，瞭解如何使用這些工具在[!DNL Adobe Commerce]平台上安裝和管理擴充功能。

- **在Adobe Commerce上安裝協力廠商擴充功能體驗** — 如需參考資訊，請參閱Adobe Commerce檔案。

   - [在雲端基礎結構執行個體上安裝Adobe Commerce的擴充功能](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/extensions#install-an-extension)。

   - [安裝Adobe Commerce內部部署執行個體的擴充功能](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions)。

### 步驟1：下載擴充功能套件組合

按照您的帳戶代表提供的指示，下載包含Composer套件的封存檔案，以安裝Store Fulfillment Services擴充功能。

### 步驟2：將擴充功能成品擷取至您的應用程式

解壓縮包含整合套件的封存檔案，以安裝Store Fulfillment Services擴充功能。

1. 為擷取的檔案建立目標目錄。

   - 從命令列，移至網頁伺服器doc根目錄。

   - 建立`artifacts`目錄。

1. 將封存檔案解壓縮至新目錄。

1. 檢閱檔案清單，確認檔案已成功擷取。

   ```
   ../var/www/html/artifacts]$ ls -a
   .
   ..
   bopis-sdk.zip
   module-magento-bopis-alternate-pickup-contact-admin-ui.zip
   module-magento-bopis-alternate-pickup-contact-api.zip
   ```

### 步驟3：使用撰寫器設定您的應用程式

使用Composer設定安裝的來源目錄，並安裝Store Fulfillment Services擴充功能。

1. 設定Composer安裝的來源存放庫。

   ```bash
   composer config repositories.artifacts artifact artifacts/
   ```

1. 將Store Fulfillment Services擴充功能新增至`composer.json`。

   ```bash
   composer require walmart/magento-bopis-metapackage:1.0.0
   ```

>[!NOTE]
>
>若要在Adobe Commerce內部部署執行個體上取得更好的效能，您可以[更新自動載入設定](https://experienceleague.adobe.com/docs/commerce-operations/performance-best-practices/deployment-flow.html#update-the-autoloader)： `composer dump-autoload --optimize`

### 步驟4：升級資料庫架構和資料

使用`bin/magento setup:upgrade`更新資料庫結構描述和資料，並使用變更來支援Store Fulfillment解決方案以完成安裝。

>[!NOTE]
>
>對於雲端基礎結構專案上的Adobe Commerce ，您不需要註冊擴充功能。 請改為提交上一步驟中的程式碼變更，並將它們推送至您的環境分支。 更新資料庫架構和資料的命令會在雲端建置和部署過程中自動執行。

### 步驟5：完成安裝

1. 使用`setup:upgrade` Magento CLI命令在Adobe Commerce中註冊擴充功能。

   ```bash
   bin/magento setup:upgrade
   ```

1. 如果出現提示，請重新編譯您的[!DNL Commerce]專案。

   ```bash
   bin/magento setup:di:compile
   ```

1. 清除快取。

   ```bash
   bin/magento cache:clean
   ```

1. 停用維護模式。

   ```bash
   bin/magento maintenance:disable
   ```

### 步驟6：驗證安裝

從Adobe Commerce伺服器，確認Store Fulfillment Services擴充功能的模組已安裝並啟用。

1. 登入伺服器。

   若為雲端基礎結構上的Adobe Commerce安裝，[請使用SSH登入遠端環境](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/secure-connections#ssh)。

1. 確認「商店履行服務」模組已啟用。

   ```bash
   bin/magento module:status  --enabled | grep Walmart
   ```

   輸出應包括下列模組：

   ```
   Walmart_BopisBase
   Walmart_BopisAlternatePickupContact
   Walmart_BopisAlternatePickupContactFrontend
   Walmart_BopisApiConnector
   Walmart_BopisAlternatePickupContactAdminUi
   Walmart_BopisCheckoutPickInStoreApi
   Walmart_BopisInventorySourceAdminUi
   Walmart_BopisCheckoutPickInStore
   Walmart_BopisInventoryCatalogApi
   Walmart_BopisPreferredLocationApi
   Walmart_BopisHomeDeliveryApi
   Walmart_BopisHomeDelivery
   Walmart_BopisPreferredLocation
   Walmart_BopisInventoryCatalog
   Walmart_BopisPreferredLocationFrontend
   Walmart_BopisCheckoutPickInStoreAdminUi
   Walmart_BopisInventorySourceApi
   Walmart_BopisInventorySourceFaasSync
   Walmart_BopisInventorySourceReservation
   Walmart_BopisLocationCheckInApi
   Walmart_BopisLogging
   Walmart_BopisStoreAssociateApi
   Walmart_BopisLocationCheckInFrontend
   Walmart_BopisStoreAssociate
   Walmart_BopisOperationQueue
   Walmart_BopisOperationQueueAdminUi
   Walmart_BopisOperationQueueApi
   Walmart_BopisOrderFaasSync
   Walmart_BopisOrderUpdateApi
   Walmart_BopisLocationCheckIn
   Walmart_BopisInventoryCatalogAdminUi
   Walmart_BopisPreferredLocationAdminUi
   Walmart_BopisDeliverySelection
   Walmart_BopisCheckoutPickInStoreFrontend
   Walmart_BopisLocationCheckInAdminUi
   Walmart_BopisStoreAssociateAdminUi
   Walmart_BopisOrderUpdate
   Walmart_BopisStoreAssociateTfa
   Walmart_BopisStoreAssociateTfaApi
   ```

### 其他步驟

如有需要，請使用[setup:static-content:deploy](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/cli-reference/commerce-on-premises){target="_blank"} CLI命令，將靜態檢視檔案部署至您的生產環境。

```bash
php bin/magento setup:static-content:deploy -f
```

如果使用空白主題，則需要`-f`選項。

>[!NOTE]
>
>如需詳細資訊，請參閱Adobe Commerce說明中心的[Adobe Commerce中的靜態內容部署最佳實務](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/development/static-content-deployment.html)文章。


