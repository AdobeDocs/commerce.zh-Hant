---
title: 開始使用Adobe Commerce Optimizer聯結器
description: 瞭解如何安裝和設定聯結器、自訂匯出設定、連線至Adobe Commerce Optimizer以及監控資料同步狀態。
feature: Personalization, Integration, Configuration
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案（Adobe管理的PaaS基礎結構）和內部部署專案的Adobe Commerce 。"
source-git-commit: f302efcb6c08d5a3c695a47ae16fdac790a8bc24
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 0%

---


# 開始使用

安裝並設定Commerce Optimizer Connector以將您的Adobe Commerce目錄資料與[!DNL Adobe Commerce Optimizer]同步，然後監視資料同步狀態，以確保您的店面為最新狀態。

## 使用整合的需求

* Adobe Commerce 2.4.7+

   * PHP 8.2、8.3或8.4
   * Composer 2.x

* 具有已布建沙箱執行個體的[!DNL Adobe Commerce Optimizer]授權。

* 存取[repo.magento.com](https://repo.magento.com)以使用Composer下載Commerce Connector中繼資料。

* 管理員存取[Adobe Commerce Optimizer沙箱執行個體](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-commerce-optimizer/create-first-instance)。

設定整合的Adobe Commerce使用者必須具備：

* Adobe Commerce管理員的管理員存取權。

* [對Adobe Commerce應用程式伺服器的命令列存取權](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/user-access)。

* 開發人員存取已布建[專案的](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations?)IMS組織[!DNL Adobe Commerce Optimizer]。

>[!BEGINSHADEBOX]

## 先決條件

如果您已安裝下列任何擴充功能，請在安裝Commerce Optimizer Connector前解除安裝它們：

* Adobe Commerce即時搜尋(`magento/live-search`)
* Adobe Commerce產品建議(`magento/product-recommendations`)
* Adobe Commerce目錄服務(`magento/catalog-service`， `magento/catalog-service-installer`)
* 資料管理儀表板(`magento-catalog-sync-admin`)

與這些擴充功能相關聯的資料仍可在Commerce資料庫中使用。 但是，當聯結器啟用時，它不會匯出到[!DNL Adobe Commerce Optimizer]。 若要在啟用聯結器後實作這些擴充功能所提供的搜尋和銷售功能，請從[[!DNL Adobe Commerce Optimizer] 管理UI](https://experienceleague.adobe.com/en/docs/commerce/optimizer/overview#quick-tour)進行設定。

>[!ENDSHADEBOX]

## 設定步驟

請依照下列步驟啟用聯結器，並開始將資料從Commerce同步至您的Adobe Commerce Optimizer執行個體。

1. **[使用Composer安裝Commerce Optimizer聯結器套件](#install-the-commerce-connector-package)**，以將您的Commerce執行個體連線至[!DNL Adobe Commerce Optimizer]。

1. **[從管理員檢閱及自訂資料匯出設定](#customize-commerce-data-export-configuration)**。

1. **[取得在Commerce和Commerce Optimizer之間建立連線所需的API認證](#get-required-values-for-configuring-the-commerce-optimizer-connection)**。

1. **[啟用 [!DNL Adobe Commerce Optimizer] 整合](#enable-the-adobe-commerce-optimizer-integration)**。

1. **[確認資料同步處理正在運作](#verify-that-the-data-sync-is-working)**。


## 安裝Commerce Optimizer聯結器套件

Adobe Commerce Optimizer Connector是以撰寫器中繼資料的形式提供，適用於具有[!DNL Adobe Commerce Optimizer]的有效授權的所有Commerce商家。

### 安裝步驟

1. 使用撰寫器新增`adobe-commerce/commerce-data-export-aco-adapter`模組：

   ```shell
   composer require adobe-commerce/commerce-data-export-aco-adapter
   ```

1. 將變更部署至您的Adobe Commerce中繼環境。

部署完成後，Commerce Optimizer管理功能表會提供Commerce選項。 按一下&#x200B;**[!UICONTROL Commerce Optimizer]**，直接從Commerce管理員開啟您的Commerce Optimizer執行個體。

>[!NOTE]
>
>如需詳細的擴充功能安裝指示，請參閱下列指南：
>
>在雲端基礎結構上的Adobe Commerce上[安裝擴充功能](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions)
>
>[在Adobe Commerce內部部署安裝擴充功能](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions)

### 取得必要的連線詳細資料

從Adobe Developer Console建立啟用[!DNL Adobe Commerce Optimizer]內嵌服務的開發人員專案，並產生OAuth伺服器對伺服器認證。 如需詳細指示，請參閱[銷售開發人員指南](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials)中的&#x200B;*取得IMS認證*。

>[!TIP]
>
>如果您已在與Commerce Optimizer執行個體相同的IMS組織中擁有使用資料擷取API設定的開發人員專案，您可以重複使用現有的OAuth伺服器對伺服器認證。

從證明資料頁面儲存下列值：

* **組織識別碼** (`org_id`)
* **使用者端識別碼** (`client_id`)
* **使用者端密碼** (`client_secret`)

### 取得[!DNL Adobe Commerce Optimizer]執行個體詳細資料

從您的[!DNL Adobe Commerce Optimizer]執行個體儲存執行個體識別碼（也稱為租使用者識別碼）。 您可以在用來存取執行個體的URL中找到它。 例如，在`https://experience.adobe.com/#/@<project-id>/in:TToyu73daQRn66KAYaq8YZ/commerce-optimizer-studio/home`中，執行個體識別碼為`TToyu73daQRn66KAYaq8YZ`。

## 自訂Commerce資料匯出設定

依預設，所有Commerce範圍（網站和商店檢視）的目錄資料同步已啟用。 您可以根據業務需求自訂匯出設定，以僅同步特定範圍的資料。 例如，如果您有多個存放區檢視，但只想匯出其中一個的資料，您可以停用其他存放區檢視的匯出工具。

>[!IMPORTANT]
>
>變更匯出設定會觸發完整的重新編列索引，這可能需要相當長的時間，視您的目錄大小而定。 在低流量期間規劃這些變更，以將對效能的影響降至最低。

### 依範圍匯出資料

下表說明會在每個範圍層級匯出哪些資料：

| 範圍 | 資料已匯出 | 附註 |
| ------- | --------------- | ------- |
| 網站 | 價格與價格手冊 | 每組價格會使用命名慣例[匯出為](../optimizer/setup/pricebooks.md)價格簿`website::customergroupcode`。 包括網站的所有客戶群組。 |
| 存放區檢視 | 產品和產品屬性 | 每個存放區檢視都會在[!DNL Adobe Commerce Optimizer]中建立個別的目錄來源。 |

### 啟用和停用行為

| 動作 | 結果 |
| -------- | -------- |
| 停用商店檢視 | 目錄來源仍保留在[!DNL Adobe Commerce Optimizer]中，但已移除所有資料。 |
| 停用然後重新啟用存放區檢視 | 相同的目錄來源會以完整資料重新同步重新填入。 |

### 更新匯出設定

安裝聯結器套件後，管理員中的商店格線現在會顯示Commerce Optimizer的匯出組態設定。

![具有Commerce Optimizer同步設定的商店格線](./assets/aco-connector-sync-config.png){width="600" zoomable="yes"}

**若要變更網站或商店檢視的設定：**

1. 在Commerce管理員中，導覽至「**[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL All Stores]**」。

1. 選取您要設定的網站或商店檢視。

1. 在&#x200B;**[!DNL Adobe Commerce Optimizer]匯出程式設定**&#x200B;中，視需要使用核取方塊來啟用或停用資料同步處理。

   ![更新資料同步設定](./assets/aco-connector-store-website-export-settings.png){width="500" zoomable="yes"}

1. 儲存您的變更。

## 啟用[!DNL Adobe Commerce Optimizer]整合

>[!IMPORTANT]
>
>資料同步處理會在您執行設定命令後立即開始。 依預設，所有Commerce範圍（網站和商店檢視）的目錄資料同步已啟用。 視目錄大小而定，資料同步程式可能需要幾分鐘到數小時的時間。

使用您在上一步中收集的API認證和執行個體詳細資訊，您現在可以設定Commerce和[!DNL Adobe Commerce Optimizer]執行個體之間的整合。

1. 從Commerce Admin中，選取&#x200B;**[!UICONTROL Adobe Commerce Optimizer]**&#x200B;以顯示包含指示的設定頁面。

   ![[!DNL Adobe Commerce Optimizer]設定頁面](/help/aco-connector/assets/aco-connector-admin-installation.png){width="500" zoomable="yes"}

1. 從命令列，[使用SSH](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections)連線至Commerce中繼環境。

1. 執行下列Commerce CLI命令來設定整合，將預留位置值取代為Commerce Optimizer專案的值：

```terminal
bin/magento aco:config:init --org_id=your-org --tenant_id=your-tenant --client_id=your-client-id --client_secret=your-secret
```

1. 返回Commerce管理員並選取[!UICONTROL Adobe Commerce Optimizer]選項，以驗證連線。

   當您按一下選項時，它會在新索引標籤中開啟[!DNL Adobe Commerce Optimizer] UI。

## 確認資料同步處理運作正常

啟用整合後，資料同步會自動開始。 視目錄大小而定，初始同步可能需要幾分鐘到幾小時的時間。

1. **在Commerce管理員中檢查同步狀態：**

   前往&#x200B;**[!UICONTROL System]** > [!UICONTROL Data Transfer] > **[!UICONTROL Data Feed Sync Status]**。

   ![具有摘要專案狀態報告的[資料摘要同步處理狀態]頁面](./assets/data-feed-sync-status.png){width="500" zoomable="yes"}

   同步執行時，摘要資料會顯示已成功傳送的記錄。 選取摘要以檢視詳細資料或疑難排解同步問題。

1. **確認資料已送達Commerce Optimizer：**

   從[!DNL Adobe Commerce Optimizer]功能表選取&#x200B;**[!UICONTROL Data Sync]**。

   ![資料同步](./assets/data-sync.png){width="500" zoomable="yes"}

   確認已出現預期的產品、價格和屬性。

>[!TIP]
>
>如果您有任何資料同步問題，請參閱[SaaS資料匯出](/help/data-export/troubleshooting-logging.md)檔案中的&#x200B;*疑難排解*&#x200B;一節。

## 後續步驟

1. **[設定 [!DNL Adobe Commerce Optimizer] 目錄檢視與原則](#configure-adobe-commerce-optimizer-stores)**

   在[!DNL Adobe Commerce Optimizer]指南中建立目錄檢視和原則。 請注意，價格簿是從Adobe Commerce客戶群組自動建立的。

1. **[在Edge Delivery Services上設定Commerce店面](#set-up-a-commerce-storefront-on-edge-delivery-services)**

   依照[店面設定檔案](https://experienceleague.adobe.com/developer/commerce/storefront/setup/)將您的店面連線到[!DNL Adobe Commerce Optimizer]執行個體，並開始提供個人化的商務體驗。


