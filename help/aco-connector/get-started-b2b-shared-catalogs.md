---
title: 設定B2B Commerce的聯結器
description: 瞭解如何安裝B2B聯結器、選取Commerce範圍、同步處理共用目錄資料、驗證目錄檢視及監視投影健康情況。
feature: Integration, Configuration
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案（Adobe管理的PaaS基礎結構）和內部部署專案的Adobe Commerce 。"
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
  - id: e126554b-28f9-4290-b58c-10b888b88174
    internal-label: IMS integration
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
    internal-label: Data Transfer
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
last-update: 2026-10-01
source-git-commit: 9ed3a09bc4e26e2ef787909700f51e25de0a18fa
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 0%
---

# 設定B2B Commerce的聯結器

使用[!DNL Adobe Commerce] B2B共用目錄的商戶可以使用[!DNL Adobe Commerce Optimizer Connector for B2B]將自訂共用目錄資料和設定同步到[!DNL Adobe Commerce Optimizer]。

{{aco-integration-environment-alignment}}

## 使用整合的需求 {#requirements-to-use-the-integration}

* 已安裝並啟用[Adobe Commerce B2B 1.5.3+](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/b2b/install)版的Commerce 2.4.8+。

* [!DNL Commerce Optimizer]授權包含已布建的沙箱執行個體。

* [驗證金鑰](https://experienceleague.adobe.com/zh-hant/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)以使用Composer下載聯結器中繼封裝。

* 管理員存取[[!DNL Commerce Optimizer] 沙箱執行個體](../optimizer/get-started.md)。

設定整合的[!DNL Adobe Commerce]使用者必須具有：

* Commerce管理員的管理員存取權。

* [對 [!DNL Adobe Commerce] 應用程式伺服器](https://experienceleague.adobe.com/zh-hant/docs/commerce-on-cloud/user-guide/project/user-access)的命令列存取權。

* 開發人員存取已布建[!DNL Commerce Optimizer]專案的[IMS組織](https://experienceleague.adobe.com/zh-hant/docs/core-services/interface/administration/organizations？)。

### 應用程式需求

* Commerce cron和索引器正常運作。
* 為匯出識別的所需網站和商店檢視。
* 共用目錄、公司指派、分類和B2B定價已設定或可在Adobe Commerce中設定。

>[!BEGINSHADEBOX]

## 移除衝突的擴充功能 {#remove-conflicting-extensions}

{{$include /help/_includes/aco-connector/remove-conflicting-extensions.md}}

>[!ENDSHADEBOX]

## 設定步驟 {#configuration-steps}

若要啟用[!DNL Adobe Commerce Optimizer Connector for B2B]並開始將自訂共用目錄組態從[!DNL Adobe Commerce]同步至您的[!DNL Commerce Optimizer]執行個體，請遵循下列步驟。

1. **[使用Composer安裝 [!DNL Adobe Commerce Optimizer Connector for B2B] 封裝](#install-the-adobe-commerce-optimizer-connector-for-B2B-package)**，以將您的[!DNL Adobe Commerce]執行個體連線到[!DNL Commerce Optimizer]。

1. **[從管理員自訂Commerce範圍匯出設定](#data-export-and-scope-mapping)**。

1. **[啟用 [!DNL Commerce Optimizer] 整合](#enable-the-adobe-commerce-optimizer-integration)**。

1. **[確認資料同步處理正在運作](#verify-that-the-data-sync-is-working)**。

## 安裝[!DNL Adobe Commerce Optimizer Connector for B2B]封裝 {#install-the-adobe-commerce-optimizer-connector-for-B2B-package}

[!DNL Adobe Commerce Optimizer Connector for B2B]會以Composer中繼套件的形式傳送，適用於所有具有[!DNL Commerce Optimizer]有效授權的Commerce商家。

### 安裝步驟

1. 使用撰寫器新增`adobe-commerce/commerce-data-export-aco-adapter-b2b`模組：

   ```shell
   composer require adobe-commerce/commerce-data-export-aco-adapter-b2b
   ```

1. 將變更部署至您的[!DNL Adobe Commerce]中繼環境。

   部署完成後，「Commerce管理員」功能表中會提供[!DNL Commerce Optimizer]選項。 選取&#x200B;**[!UICONTROL Commerce Optimizer]**&#x200B;以直接從Commerce管理員開啟您的[!DNL Commerce Optimizer]執行個體。

{{install-extension-links}}

### 資料匯出和範圍對應

選取要同步的網站和商店檢視，然後驗證初始摘要。 對於B2B，聯結器在將共用目錄資料專案到[!DNL Commerce Optimizer]時，會使用啟用的範圍。

* **存放區檢視** →目錄來源具有當地語系化的產品內容
* **網站與客戶群組**&#x200B;網站與客戶群組定價的→價手冊
* **共用的目錄**→受保護的私人目錄檢視和強制原則

共用目錄會定義產品分類，而每個啟用的存放區檢視都會提供本地化的目錄來源。 網站與客戶群組會決定適用的價格簿。 聯結器會針對每個已啟用的存放區檢視投影每個自訂共用目錄，因此您不需要B2B投影的個別範圍設定。

自訂共用目錄可產生多個受保護的私人目錄檢視，每個啟用的存放區檢視各一個。 預設的公用共用目錄不會投影為B2B私人目錄檢視。 如需詳細的物件對應和執行階段授權流程，請參閱[B2B共用目錄投影](b2b-shared-catalog-projection.md)。

>[!IMPORTANT]
>
>變更匯出設定會觸發完整的重新編列索引，這可能需要相當長的時間，視您的目錄大小而定。 先設定Commerce範圍，再啟用整合併開始初始資料同步。

### 若要變更範圍匯出設定

1. 在Commerce Admin中，前往&#x200B;**[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL All Stores]**。

1. 選取您要設定的網站或商店檢視。

1. 在&#x200B;**[!DNL Commerce Optimizer]匯出程式設定**&#x200B;中，視需要使用核取方塊來啟用或停用資料同步處理。

   ![更新資料同步設定](./assets/aco-connector-b2b-storeview-list.png){width="500" zoomable="yes"}

1. 儲存您的變更。

### 啟用和停用行為

| 動作 | 結果 |
| -------- | -------- |
| 停用商店檢視 | **停用同步會從B2B店面移除目錄資料。** 目錄來源仍保留在[!DNL Adobe Commerce Optimizer]中，但所有同步資料在下次cron執行時都會被移除。 |
| 停用然後重新啟用存放區檢視 | 相同的目錄來源會以完整資料重新同步重新填入。 |

### 監視B2B共用目錄變更

聯結器會監視共用目錄和公司指派的變更。 當您在Commerce管理員中移除共用目錄時，聯結器會在可設定的寬限期後移除對其私人目錄檢視的存取權。

>[!NOTE]
>
>刪除寬限期預設為七天。 您可以更新目錄檢視同步設定組態來變更它。 請參閱[目錄檢視同步處理狀態組態](catalog-view-sync-status.md#configure-aco-catalog-view-sync-settings)。

## 啟用[!DNL Commerce Optimizer]整合 {#enable-the-adobe-commerce-optimizer-integration}

您透過執行`aco:config:init` CLI命令來啟用整合，並起始資料同步處理。 此指令會完成下列步驟：

1. 使用作為命令列引數提供的憑證取得IMS存取權杖。
1. 呼叫位於`https://ccm.api.commerce.adobe.com/api/v1/tenants/{tenantId}/owner/{orgId}`的Commerce Cloud Manager (CCM)服務以驗證租使用者並擷取內嵌URL和[!DNL Commerce Optimizer] Studio URL。
1. 將所有設定（使用者端密碼已加密）儲存至`core_config_data`。
1. 讓所有[!DNL Commerce Optimizer]摘要索引器失效，以排程初始完整同步。

{{aco-data-sync-processing-note}}

## 取得必要的連線詳細資料

{{$include /help/_includes/aco-connector/connection-details.md}}

### 取得[!DNL Commerce Optimizer]執行個體詳細資料

{{$include /help/_includes/aco-connector/configure-connection.md}}

## 確認資料同步處理運作正常 {#verify-that-the-data-sync-is-working}

{{$include /help/_includes/aco-connector/verify-optimizer-data-sync.md}}

## 後續步驟

1. **監視B2B目錄檢視投影**

在初始摘要同步之後，使用[目錄檢視同步狀態](catalog-view-sync-status.md)來驗證預計的私人目錄檢視、原則、價格簿參考和受限制的存取金鑰組態。 如需投影模型與執行階段授權流程，請參閱[B2B共用目錄投影](b2b-shared-catalog-projection.md)。

1. **在[!DNL Edge Delivery Services]**&#x200B;設定Commerce店面

   若要將店面連線到[!DNL Commerce Optimizer]執行個體並開始提供個人化的商務體驗，請依照[店面設定檔案](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/){target="_blank"}操作。
