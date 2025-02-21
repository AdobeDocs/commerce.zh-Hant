---
title: 安裝 [!DNL Data Connection]
description: 瞭解如何從Adobe Commerce安裝、更新及解除安裝 [!DNL Data Connection] 擴充功能。
role: Admin, Developer
feature: Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# 安裝[!DNL Data Connection]

安裝擴充功能之前，[請先檢閱必要條件](overview.md#prereqs)。

## 安裝擴充功能

[!DNL Data Connection]擴充功能可從[Adobe Marketplace](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html)取得。 當您從伺服器的命令列安裝此擴充功能時，會以[服務](../landing/saas.md)的形式連線至您的Adobe Commerce安裝。 程式完成時，**[!DNL Data Connection]**&#x200B;和&#x200B;**Commerce Services Connector**&#x200B;會顯示在Commerce _管理員_&#x200B;中&#x200B;**服務**&#x200B;下的&#x200B;**系統**&#x200B;功能表中。

![[!DNL Data Connection]延伸模組管理員檢視](assets/epc-adminui.png)

>[!IMPORTANT]
>
>雖然擴充功能的名稱已從Experience Platform聯結器變更為[!DNL Data Connection]，但封裝名稱仍為`experience-platform-connector`以支援回溯相容性。

1. 若要下載`experience-platform-connector`套件，請從命令列執行以下命令：

   ```bash
   composer require magento/experience-platform-connector
   ```

   此中繼資料包含以下模組和擴充功能：

   - `magento/orders-connector`
   - `magento/data-services`
   - `magento/customers-connector`
   - `magento/module-experience-connector`
   - `magento/module-experience-connector-admin`
   - `magento/module-experience-connector-admin-graph-ql`
   - `magento/module-experience-connector-aep-integration`

1. （選擇性）若要包含[!DNL Live Search]資料（包含[搜尋事件](events.md#search-events)），請安裝[[!DNL Live Search]](../live-search/install.md)擴充功能。

1. （選擇性）若要包含[請購單事件](events.md#b2b-events)的B2B資料，請安裝[B2B擴充功能](#install-the-b2b-extension)。

1. （選擇性）若您是醫療保健業者，請安裝[資料服務HIPAA](#install-the-data-services-hipaa-extension)擴充功能，讓您的[!DNL Commerce]後台資料可使用HIPAA。

### 安裝Adobe I/O Events並設定客戶聯結器模組

安裝`experience-platform-connector`擴充功能後，您必須安裝適用於Adobe Commerce的Adobe I/O Events並設定`customers-connector`模組。

下列步驟適用於雲端基礎結構上的Adobe Commerce和內部部署安裝。

1. 如果您執行Commerce 2.4.4或2.4.5，請使用以下命令載入事件模組：

   ```bash
   composer require magento/commerce-eventing=^1.0 --no-update
   ```

   Commerce 2.4.6及更新版本會自動載入這些模組。

1. 更新專案相依性。

   ```bash
   composer update
   ```

1. 啟用新模組：

   ```bash
   bin/magento module:enable Magento_AdobeCommerceEventsClient Magento_AdobeCommerceEventsGenerator Magento_AdobeIoEventsClient Magento_AdobeCommerceOutOfProcessExtensibility
   ```

根據部署型別完成安裝：雲端基礎結構或內部部署上的Adobe Commerce 。

#### 在雲端基礎結構上

在雲端基礎結構上的Adobe Commerce中，啟用`.magento.env.yaml`中的`ENABLE_EVENTING`全域變數。 [深入瞭解](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-global.html#enable_eventing)。

```bash
stage:
   global:
      ENABLE_EVENTING: true
```

提交更新檔案並將其推播到雲端環境。 部署完成後，使用以下命令啟用傳送事件：

```bash
bin/magento config:set adobe_io_events/eventing/enabled 1
```

#### 內部部署

在內部部署環境中，您必須手動啟用程式碼產生和Adobe Commerce事件：

```bash
bin/magento events:generate:module
bin/magento module:enable Magento_AdobeCommerceEvents
bin/magento setup:upgrade
bin/magento setup:di:compile
bin/magento config:set adobe_io_events/eventing/enabled 1
```

### 安裝B2B擴充功能

針對B2B商家，安裝下列擴充功能以包含[請購單清單](events.md#b2b-events)事件資料。

從命令列執行下列動作來下載`magento/experience-platform-connector-b2b`擴充功能：

```bash
composer require magento/experience-platform-connector-b2b
```

### 安裝資料服務HIPAA擴充功能

對於醫療保健商家，請安裝下列擴充功能，以確保後端辦公室事件資料可隨時使用HIPAA。

從命令列執行下列動作來下載`magento/module-data-services-hipaa`擴充功能：

```bash
composer require magento/module-data-services-hipaa
```

## 更新[!DNL Data Connection]副檔名 {#update}

若要更新[!DNL Data Connection]擴充功能，請從命令列執行下列動作：

```bash
composer update magento/experience-platform-connector --with-dependencies
```

或者，對於B2B商家：

```bash
composer update magento/experience-platform-connector-b2b --with-dependencies
```

若要更新到主要版本，例如從2.0.0到3.0.0，請編輯專案的根[!DNL Composer] `.json`檔案，如下所示：

1. 開啟根`composer.json`檔案並搜尋`magento/experience-platform-connector`。

1. 在`require`區段中，更新版本號碼，如下所示：

   ```json
   "require": {
      ...
      "magento/experience-platform-connector": "^3.0",
      ...
    }
   ```

1. **儲存** `composer.json`。 然後，從命令列執行下列動作：

   ```bash
   composer update magento/experience-platform-connector –-with-dependencies
   ```

   或者，對於B2B商家：

   ```bash
   composer update magento/experience-platform-connector-b2b --with-dependencies
   ```

## 解除安裝[!DNL Data Connection]延伸模組 {#uninstall}

若要解除安裝[!DNL Data Connection]擴充功能，請參閱[解除安裝模組](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/uninstall-modules.html)。
