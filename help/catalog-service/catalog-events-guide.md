---
title: 目錄事件和Adobe I/O Events整合指南
description: 瞭解如何驗證目錄資料、為Adobe Commerce設定 [!DNL Adobe I/O Events] 、訂閱目錄事件型別，以及驗證消費者的傳遞。
level: Intermediate
recommendations: noCatalog
role: Admin, Developer
feature: Services, Catalog Service
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 15aaeadde61b9d70ec107db2ed4c118d1f8ee731
workflow-type: tm+mt
source-wordcount: 1567
ht-degree: 0%

---

# 目錄事件和[!DNL Adobe I/O Events]整合指南

目錄事件是電腦產生的通知，說明可透過[!DNL Catalog Service]使用的受支援目錄變更。 它們可啟用事件導向的工作流程，例如：

* 讓外部快取或服務與目錄更新保持同步。
* 產品、變體、價格或類別變更時觸發下游流程。
* 支援Experience Edge和需要近乎即時目錄更新的[!DNL Edge Delivery Services]使用案例。

如需從[!DNL Adobe Commerce]到您的事件消費者的端對端路徑，請參閱[透過 [!DNL Adobe I/O Events]](#event-delivery-through-adobe-io-events)的事件傳遞。

## 支援的事件型別 {#supported-event-types}

目錄活動著重於透過[!DNL Adobe Developer Console]公開的店面相關變更。 目前支援的訂閱如下。

| 訂閱 | 活動 |
| --- | --- |
| 產品更新 | 產品建立、更新和刪除透過[!DNL Catalog Service]提供的產品變更 |
| 價格更新 | 價格建立、更新和刪除影響店面目錄資料的變更 |

每個事件包含：

* 描述變更型別的事件識別碼。
* 實體和環境內容，例如例項ID和SKU。
* 說明已變更的實體和相關範圍資訊的裝載。


## 範例事件裝載

**ProductUpdated事件**

```json
{
  "imsOrgId": "aaa-0",
  "instanceId": "instance-9",
  "eventCode": "productUpdated",
  "sku": "1234",
  "links": [
    {"type":  "variantOf", "sku": "5678"}
   ],
  "scope": [
    { "storeViewCode": "US-us" },
    { "storeViewCode": "FR-fr" },
    { "storeViewCode": "DE-de" }
  ]
}
```

**PriceUpdated事件**

```json
{
  "imsOrgId": "aaa-0",
  "instanceId": "instance-9",
  "eventCode": "priceUpdated",
  "sku": "1234",
  "scope": [
    {
      "websiteCode": "website1",
      "customerGroupCode": "customer-group-code1"
    },
    {
      "websiteCode": "website2",
      "customerGroupCode": "customer-group-code2"
    }
  ]
}
```

## 透過[!DNL Adobe I/O Events]傳遞事件 {#event-delivery-through-adobe-io-events}

[!DNL Adobe I/O Events]會將目錄事件傳送給您的整合。 下圖顯示從[!DNL Adobe Commerce]到[!DNL Catalog Service]和[!DNL Adobe I/O Events]的目錄變更高層級流向已訂閱的消費者：

![從Adobe Commerce透過目錄服務和Adobe I/O Events到訂閱消費者的目錄事件高階流程](assets/catalog-service-event-pipeline.png)

下列步驟將更詳細地說明每次移交：

1. **Adobe Commerce →目錄服務**

[!DNL Adobe Commerce]使用支援的SaaS Data Export延伸模組將目錄資料匯出至[!DNL Catalog Service]。

1. **目錄服務正在處理**

   * [!DNL Catalog Service]個處理支援的目錄變更，並為事件傳遞準備這些變更。

1. **→目錄服務**

* 目錄事件已發佈至[!DNL Adobe I/O Events]。
* 消費者使用日誌、webhook、[!DNL Adobe I/O Runtime]、Amazon EventBridge或其他支援的傳遞機制來訂閱。

[!DNL Adobe I/O Events]提供：

* *每個訂閱者至少傳送一次* （可能有重複的事件）。
* 不同傳遞之間不提供訂購保證。

您的消費者必須處理重複事件和順序錯亂的傳遞。 如需實作指南，請參閱[Idempotency](#idempotency)。

## 使用案例 {#use-cases}

您可在多個案例中使用目錄事件。

### 靜態網站和邊緣傳送

* 目錄資料變更時，重新產生或失效目錄頁面和店面片段。
* 避免頻繁輪詢[!DNL Catalog Service] API。

### 搜尋索引和快取

* 觸發下游搜尋索引中的累加更新。
* 當產品或類別資料變更時，更新快取圖層或目錄的外部檢視。

### 與外部系統整合

* 將目錄變更轉寄給外部系統，例如PIM、訂價引擎或其他業務線系統。
* 保持下游應用程式同步化而不需直接存取資料庫。

### 監視和可觀察性

將目錄事件與現有的監視（例如，[!DNL Grafana]與[!DNL Prometheus]）結合為：

* 監視事件輸送量。
* 偵測目錄更新磁碟區中的異常。

## 啟用目錄事件 {#enable-catalog-events}

若要啟用端對端的目錄事件，請依照下列步驟操作。

>[!PREREQUISITES]
>
>在啟用目錄事件之前，請確定您具備下列條件：
>
>* 支援的Adobe Commerce環境已啟用[!DNL Catalog Service]。
>* [已為Adobe Commerce](https://developer.adobe.com/commerce/extensibility/events/configure-commerce)設定 [!DNL Adobe I/O] 連線。
>* 存取布建Commerce環境的相同IMS組織中的[!DNL Adobe Developer Console]。
>* 若要確認同步處理至Commerce SaaS服務，請在[管理]中使用&#x200B;**[!UICONTROL Data Management Dashboard]**。
>* 儀表板驗證需要Product Recommendations v6.0、[!DNL Live Search] v4.1.0+或[!DNL Catalog Service] v1.17+。 Adobe建議將您的Commerce專案更新至這些服務的最新支援版本。 對於舊版服務，請使用[目錄同步](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync)進行同步驗證。


>[!NOTE]
>
>若要使用目錄事件，請先設定[!DNL Adobe I/O Events]的Commerce環境，然後在[!DNL Adobe Developer Console]中註冊事件訂閱。
>
>如果您的環境在設定後未出現在[!DNL Adobe Developer Console]中，請確認您已登入正確的IMS組織，且您的帳戶擁有必要的存取權。 如果環境仍未顯示，請聯絡Adobe支援。

### 驗證目錄資料 {#verify-catalog-data}

在設定之前，請先確認[!DNL Catalog Service]擁有您[!DNL Commerce]執行個體目前的目錄資料。 目錄事件取決於[!DNL SaaS Data Export]完成兩個階段 — 確認&#x200B;**兩者**：

1. 確認成功從Commerce **匯出**&#x200B;摘要。

   從[!DNL Adobe Commerce] Admin開啟[資料摘要同步狀態](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)頁面(**[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**)，並確認每個[!DNL Catalog Service]摘要的最後匯出狀態都成功。

1. 確認從[!DNL Adobe Commerce]管理員成功&#x200B;**同步處理至連線的Commerce服務**。

   從[!DNL Adobe Commerce]管理員開啟[資料管理儀表板](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) (**[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Management Dashboard]**)，然後確認同步的產品資料包含預期的產品。

### 註冊並訂閱[!DNL Adobe I/O Events] {#register-events}

定義要訂閱的Commerce事件，然後在專案中註冊這些事件。

如果您的執行個體不在選取專案清單中，則它未連線到[!DNL Adobe I/O]。 如需修正問題的指示，請參閱&#x200B;*Adobe Commerce Developer*&#x200B;檔案中的[設定 [!DNL Adobe I/O] 連線](https://developer.adobe.com/commerce/extensibility/events/configure-commerce#configure-the-adobe-io-connection)。

1. 從[!DNL Adobe Developer Console]，登入用於Commerce專案的相同IMS組織。

1. 為Commerce目錄事件建立專案，或將事件API新增至現有專案。

   * 在頂端導覽列中選取&#x200B;**[!UICONTROL APIs and services]**。

   * 在&#x200B;**[!UICONTROL Browse APIs and services]**&#x200B;頁面上，選取&#x200B;**[!UICONTROL Events]**&#x200B;索引標籤。

   * 快速尋找Commerce Catalog Events API。 在搜尋方塊中輸入&#x200B;_目錄_，或依&#x200B;**[!UICONTROL Commerce]**&#x200B;產品篩選。

   * 在&#x200B;**[!UICONTROL Commerce Catalog Events]**&#x200B;卡片上，選取&#x200B;**[!UICONTROL Project]**。

   在[瀏覽API和服務]頁面上選取的![Commerce目錄事件提供者](assets/catalog-event-select-provider.png){width="600" zoomable="yes"}

1. 設定事件註冊。

   選取要從中接收事件通知的Commerce執行個體。 然後，選取&#x200B;**[!UICONTROL Next]**。

   在事件註冊畫面上選取![個Commerce執行個體](assets/catalog-event-registration.png){width="600" zoomable="yes"}

1. 選擇要訂閱的事件。

   選取您想要接收的支援事件訂閱，例如&#x200B;**[!UICONTROL Product Update]**&#x200B;或&#x200B;**[!UICONTROL Price Update]**。 然後，選取&#x200B;**[!UICONTROL Next]**。

   在註冊畫面上選取要訂閱的![事件類別](assets/catalog-event-subscription.png){width="600" zoomable="yes"}

1. 新增OAuth伺服器對伺服器認證。

   輸入&#x200B;**[!UICONTROL Credential name]**。 然後，選取&#x200B;**[!UICONTROL Next]**。

1. 輸入&#x200B;**[!UICONTROL Event registration name]**&#x200B;和&#x200B;**[!UICONTROL Event registration description]**。 然後，選取&#x200B;**[!UICONTROL Next]**。

1. 在最後的註冊畫面中，接受預設消費者，即Journaling API。

   預設日誌API取用者可讓您測試事件註冊，並確認已傳送事件。 如果您已設定webhook或[!DNL Adobe I/O Runtime]動作使用者，請在此處選取它。 否則，稍後當您的消費者準備好時，請編輯事件註冊。

   ![在事件註冊完成畫面上選取的日誌API消費者預設值](assets/catalog-event-consumer.png){width="600" zoomable="yes"}

1. 選取&#x200B;**[!UICONTROL Complete registration]**。

### 設定事件取用者 {#configure-consumer}

1. 設定取用者，例如：

   * webhook端點
   * [!DNL Adobe I/O Runtime]動作
   * 另一個支援的目的地

1. 如果您未在註冊期間選取消費者，請編輯事件註冊以新增消費者詳細資訊。

   * 從[!DNL Adobe Developer Console]編輯您的專案。 然後，選取您建立的事件註冊。

   * 在事件註冊詳細資訊頁面上，選取&#x200B;**[!UICONTROL Edit Events Registration]**。

   * 選取&#x200B;**[!UICONTROL Next]**，直到您到達消費者選取畫面為止。 然後，選取您設定的消費者。

   * 將消費者更新至您設定的目的地。 然後，選取&#x200B;**[!UICONTROL Save configured events]**。

### 驗證事件流程 {#validate-event-flow}

已為您的環境啟用目錄事件。 當[!DNL Commerce]中的目錄資料變更時，更新會流經[!DNL Catalog Service]至[!DNL Adobe I/O Events]，而您訂閱的消費者會收到對應的目錄事件。 在建立生產整合之前，請檢閱[限制和最佳實務](#limits-and-best-practices)。
1. 進行簡單的支援目錄變更，例如更新產品名稱或變更價格。

1. 確認下列結果：

   * 透過[!DNL Catalog Service] API可以看到變更。
   * 您的[!DNL Adobe I/O Events]消費者會收到對應的產品或價格事件。


## 限制和最佳實務 {#limits-and-best-practices}

在建立目錄事件時，請遵循這些最佳實務。

### 冪等性 {#idempotency}

[!DNL Adobe I/O Events]可以傳遞相同目錄事件多次，而單一產品的事件可能會未依順序送達。 設計等冪的消費者，方法如下：

* 搭配版本或時間戳記欄位使用實體ID。
* 安全地忽略相同變更的重複通知。

### 輸送量和背壓

更新率高的大型目錄可能會產生大量的事件量。 請確定：

* 消費者可以在尖峰輸送量處理事件。
* 您可以視需要使用緩衝、批次處理或佇列。

### 安全性與隔離

* [!DNL Adobe I/O Events]強制執行&#x200B;*租使用者隔離*。
* 您的組織只會接收其自身環境和權益的事件。

### 結構描述演變

目錄事件裝載遵循與[!DNL Catalog Service] API相同的概念模型。 若要保持向前相容：

* 儘可能避免嚴格執行結構描述。
* 忽略未知的欄位而不是失敗。

## 疑難排解目錄事件 {#troubleshoot-catalog-events}

如果目錄事件遺失或延遲，請完成以下步驟。

1. **檢查目錄服務資料**

   [使用 [!DNL Catalog Service] API](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/)確認已成功儲存目錄變更。

1. **驗證[!DNL SaaS Data Export]**

   目錄事件需要[!DNL Catalog Service]中的目前資料。 確認匯出路徑的兩個階段：

   * 從Commerce匯出&#x200B;**摘要** — 在[資料摘要同步狀態](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)頁面或`var/log/saas-export.log`中，確認[!DNL Catalog Service]摘要已成功從[!DNL Commerce]匯出。

   * **同步處理至連線的Commerce SaaS服務** — 在[資料管理儀表板](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)、[目錄同步](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync)或匯出記錄檔中，確認資料已成功同步處理至[!DNL Catalog Service]。

   如需疑難排解匯出和同步處理工作，請參閱[使用SaaS資料匯出同步處理資料](../data-export/data-sync-manage.md)和[記錄及疑難排解](../data-export/troubleshooting/logging.md)。

1. **驗證[!DNL Adobe I/O Events]組態**

   確認：

   * 您已在[!DNL Adobe Developer Console]中登入正確的IMS組織。
   * **[!UICONTROL Commerce Catalog Events]**&#x200B;提供者已啟用。
   * 預期的&#x200B;**[!UICONTROL Commerce Catalog Events]**&#x200B;提供者和環境是可見的。
   * 訂閱為作用中。
   * 您的端點、動作或日誌取用者可以接收及處理測試事件。

1. **連絡Adobe支援**

   開啟支援票證時，請選取與&#x200B;**Adobe Commerce應用程式**&#x200B;對應的問題原因，並包含下列資訊：

   * 目錄服務詳細資料（環境、地區）。
   * [!DNL Adobe I/O Events]訂閱詳細資料。
   * 遺失事件的近似時間和說明。

   如需其他說明，請參閱[支援票證](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#support-case)。

>[!MORELIKETHIS]
>
>
>* [上線和安裝](installation.md)
>* [開始使用目錄服務](get-started.md)
>* [使用SaaS資料匯出同步處理資料](../data-export/data-sync-manage.md)
>* [使用GraphQL API擷取目錄資料](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/){target="_blank"}
>* [[!DNL Catalog Service] 和API Mesh](mesh.md)
>* [設定 [!DNL Adobe I/O] 連線](https://developer.adobe.com/commerce/extensibility/events/configure-commerce#configure-the-adobe-io-connection){target="_blank"}
>* [[!DNL Adobe I/O Events]](https://developer.adobe.com/events/docs/guides/){target="_blank"}
