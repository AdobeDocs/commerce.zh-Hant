---
title: 安裝 [!DNL Payment Services]
description: 安裝Payments Services擴充功能。
exl-id: babaa91a-9376-4acb-b934-a89f9df52016
role: Admin
feature: Payments, Checkout, Install, Upgrade, Paas
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案(Adobe管理的PaaS基礎結構)和內部部署專案的Adobe Commerce 。"
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---

# 安裝[!DNL Payment Services]

若要開始使用[!DNL Adobe Commerce]和[!DNL Magento Open Source]的支付服務，您必須完成一些入門步驟。

>[!INFO]
>
> 如需詳細資訊，請參閱我們的[為Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-payment-services)設定 [!DNL Payment Services] 影片。

下載並安裝[!DNL Adobe Commerce]和[!DNL Magento Open Source]的[!DNL Payment Services]擴充功能是使用[!DNL Payment Services]的先決條件步驟。

## 下載擴充功能

您必須先從[Commerce Marketplace](https://experienceleague.adobe.com/docs/commerce-admin/start/resources/commerce-marketplace.html)下載擴充功能，才能進行安裝。

1. 導覽至Commerce Marketplace](https://commercemarketplace.adobe.com/magento-payment-services.html)中的[付款服務擴充功能。
1. 若要選擇版本和版本，請將&#x200B;**[!UICONTROL Edition]**&#x200B;和&#x200B;**[!UICONTROL Your store version]**&#x200B;切換為您偏好的選擇。
1. 按一下&#x200B;**[!UICONTROL Add to Cart]**。
1. 完成簽出，然後按一下&#x200B;**[!UICONTROL Place Order]**。
1. 檢查與您的Marketplace下載相關聯的電子郵件，以取得訂單確認和詳細資訊。

>[!NOTE]
>
> 若為Adobe Commerce 2.4.7或更新版本，[!DNL Payment Services]現成可用。

## 安裝擴充功能

您可以在雲端基礎結構和內部部署執行個體上同時安裝[!DNL Adobe Commerce]的[!DNL Payment Services]擴充功能，這些執行個體連結到您在註冊程式中提供的Commerce帳戶[mageid](https://developer.adobe.com/commerce/marketplace/guides/sellers/profile-information/#access-keys)。
[!DNL Magento Open Source]個客戶使用內部部署指示。

Composer在初始安裝[!DNL Adobe Commerce]期間使用這些金鑰，或在先前未將Composer金鑰儲存到`auth.json`檔案的情況下。

請參閱[取得您的驗證金鑰](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)，以取得有關取得Composer金鑰的詳細資訊。

請參閱[安裝擴充功能](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions)，以取得下載和安裝擴充功能前需考量的詳細資訊。

### 雲端基礎結構上的[!DNL Adobe Commerce]

此方法用於安裝Commerce Cloud執行個體的[!DNL Payment Services]擴充功能。

1. 更新您的`composer.json`檔案：

   ```bash
   composer require magento/payment-services --no-update
   ```

1. 更新相依性並安裝擴充功能：

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   使用`composer update`命令更新所有根相依性。

1. 提交並推送您的變更。

### 內部部署和其他設定

此方法用於為內部部署執行個體和[!DNL Magento Open Source]客戶安裝[!DNL Payment Services]擴充功能。

1. 若要取得擴充功能，請執行以下命令：

   ```bash
   composer require magento/payment-services --no-update
   ```

1. 更新相依性並安裝擴充功能：

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   使用`composer update`命令更新所有根相依性。

1. 升級您的執行個體：

   ```bash
   bin/magento setup:upgrade
   ```

1. 清除快取：

   ```bash
   bin/magento cache:clean
   ```

1. 提交變更。
1. 若要確保已部署認可的程式碼，請更新您的執行個體。

>[!NOTE]
>
> [!DNL Payment Services] 1.6.1與PHP 7.x版相容。不過，強烈建議更新至最新的[!DNL Payment Services]版本。

## 升級擴充功能

當新版的[!DNL Payment Services]發行時，您可以輕鬆升級擴充功能。

1. 若要取得最新版本的套件：

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   使用`composer update`命令更新所有根相依性。

1. 在撰寫器更新後，執行：

   ```bash
   bin/magento setup:upgrade
   ```

1. 提交並推送您的變更。

## 疑難排解

嘗試安裝[!DNL Payment Services]擴充功能時，您可能會看到錯誤。 請使用下列疑難排解方法來解決錯誤。

### 存放庫清單

確認`repo.magento.com`存在於您的存放庫清單中。

### 不正確的撰寫器索引鍵

如果您看到下列錯誤，指出您的撰寫器索引鍵不正確：

```
Could not find a matching version of package magento/payment-services. Check the package spelling, your version constraint and that the package is available in a stability which matches your minimum-stability (stable).
```

確認您的撰寫器金鑰有效，且您擁有其他Magento套件的存取權。

若要檢視已設定的撰寫器金鑰：

1. 尋找`auth.json`檔案的位置：

   ```bash
   composer config --global home
   ```

1. 檢視`auth.json`檔案：

   ```bash
   cat /path/to/auth.json
   ```

1. 檢視[哪些金鑰與您的Commerce帳戶`MageID`](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)相關聯。

### PHP的記憶體不足

如果看到以下錯誤，表示您沒有足夠的記憶體來使用PHP：

```
Fatal error: Allowed memory size of 2146435072 bytes exhausted (tried to allocate 4096 bytes) in phar:///usr/local/bin/composer/src/Composer/DependencyResolver/RuleWatchGraph.php on line 52
```

[在`php.ini`中增加環境上PHP的記憶體限制](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/app/php-settings#increase-php-memory-limit)。

或者，您可以使用此命令指定記憶體限制： `php -d memory_limit=-1 [path to composer]/composer require magento/payment-services`。

例如：

```bash
php -d memory_limit=-1 vendor/bin/composer require magento/payment-services
```
