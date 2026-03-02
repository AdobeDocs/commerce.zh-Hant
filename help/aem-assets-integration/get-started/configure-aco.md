---
title: 設定適用於Commerce Optimizer的AEM Assets
description: 瞭解如何設定 [!DNL Adobe Commerce Optimizer]的AEM Assets整合。
feature: CMS, Media, Configuration, Integration
source-git-commit: bf1d88ef7daec25872678bb27bce0bb7c97fd296
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---


# 為[!DNL Adobe Commerce Optimizer]設定AEM Assets

僅[!BADGE SaaS]{type=Positive tooltip="僅適用於Adobe Commerce Optimizer專案。"}

適用於[!DNL Adobe Commerce Optimizer]的AEM Assets整合可讓商家使用AEM Assets作為產品影像的集中式數位資產管理解決方案。 本指南涵蓋[!DNL Commerce Optimizer]的特定組態。

不同於Adobe Commerce (PaaS)或Adobe Commerce as a Cloud Service (ACCS)，[!DNL Commerce Optimizer]沒有管理員設定UI。 若要啟用整合，請使用您的[!DNL Adobe Commerce Optimizer]和AEM Assets詳細資料建立支援票證。 Adobe支援會設定整合，並在Assets整合服務中註冊您的租使用者。

下圖為[!DNL Adobe Commerce Optimizer]與AEM Assets整合之間的產品同步概觀。

![AEM Assets到[!DNL Commerce Optimizer]流量](../assets/aco-asset-sync-architecture.png){width="700"}

此整合有兩個主要流程：

* **從AEM Assets**：當資產被核准、拒絕或移除時，事件會透過Adobe Pipeline傳輸至Assets Integration Service。 此服務會將資產與使用`match-by-SKU` （中繼資料導向）或[自訂比對器(App Builder)](../synchronize/custom-match.md){target=_blank}的產品比對，然後將`product-asset`對應傳送至Commerce Optimizer，以儲存為產品層。

* **從[!DNL Adobe Commerce Optimizer]**：當產品在[!DNL Commerce Optimizer]中更新時，事件會透過Adobe管道傳輸到Assets整合服務。 此服務會將任何符合的資產對應同步回[!DNL Adobe Commerce Optimizer]。

## 先決條件

在設定整合之前，請確定您具備：

* 具有產品視覺效果權益的有效[!DNL Adobe Commerce Optimizer]執行個體，或具有Dynamic Media的任何AEM Assets授權。
* 存取AEM Assets as a Cloud Service環境。
* 同一Adobe IMS組織中的[!DNL Commerce Optimizer]和AEM Assets。
* 在您的AEM Assets環境中啟用OpenAPI的Dynamic Media 。

## 入門

若要將AEM Assets與[!DNL Commerce Optimizer]整合，您必須[建立支援票證](https://experienceleague.adobe.com/zh-hant/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket)。

Adobe支援會使用您票證中的資訊，向Assets Integration Service註冊您的租使用者，並設定整合。

在您的支援票證中包含下列資訊：

* 在您的&#x200B;**[!DNL Adobe Commerce Optimizer]URL或Commerce Cloud Manager UI中找到**&#x200B;租使用者識別碼[!DNL Commerce Optimizer] （執行個體識別碼）。
* **AEM計畫識別碼**。
* **AEM環境識別碼**。
* **符合規則**：符合SKU或[外部符合專案(App Builder)](../synchronize/custom-match.md){target=_blank}。
* **階層**：要登入租使用者的目錄階層名稱。 視需要指定自訂名稱。 否則，會使用預設`AEM-Assets`。
* **地區設定**：要向註冊租使用者的目錄來源地區設定（例如，`en-US`）。

>[!IMPORTANT]
>
> 整合支援每個租使用者一個來源，也就是一個地區設定和一個圖層的組合。

Adobe支援處理完您的票證後，便會設定整合，並且您的租使用者會向Assets Integration Service註冊。

上線完成後：

1. **向Assets Integration Service註冊**：您的[!DNL Commerce Optimizer]租使用者已使用[!DNL Adobe Commerce Optimizer]租使用者ID、AEM方案ID、AEM環境ID和租使用者向Assets Integration Service註冊。

1. **驗證設定**： IMS服務權杖驗證設定在[!DNL Commerce Optimizer]與Assets整合服務之間，以進行安全通訊。

1. **事件訂閱**： Assets Integration Service訂閱：

   * AEM Assets事件（資產已核准、更新、已移除）
   * [!DNL Commerce Optimizer]個目錄事件（已建立、已更新的產品）

### 限制

[!DNL Commerce Optimizer]整合有下列限制：

* **每個商家一個圖層**—AEM Assets整合支援每個商家一個AEM-Assets圖層（每個租使用者一個來源）。 目前不支援為每個商家設定多個圖層。
* **僅限影像** — 整合不支援視訊或其他媒體型別。
* **沒有類別影像** — 無法使用類別影像同步處理。 不支援AEM Assets中用於Assets選擇器（UI插入）的類別影像。
* **沒有多網站區別** — 整合不會處理多網站；與產品相關的影像在所有管道和原則上都顯示相同。
* **影像位置/順序** — 不支援影像位置和順序。
* **產品必須存在** — 如果產品不存在於[!DNL Commerce Optimizer]中，將不會為該產品 — 資產對應建立圖層。
* **圖層欄位覆寫** — 圖層中的值覆寫基底目錄。 如果欄位沒有在圖層裝載中傳送，則可能會以空值覆寫。 對AEM Assets內容使用專用圖層；若將現有圖層重複用於其他用途，可能會導致非預期的資料遺失。

### 設定您的AEM Assets

[!DNL Commerce Optimizer]的AEM Assets安裝與設定程式與Adobe Commerce as a Cloud Service相同。 如需完整步驟，請參閱[設定AEM Assets專案以支援Commerce中繼資料](configure-aem.md)。

確保您的AEM Assets環境準備就緒：

1. **AEM Assets設定**：設定Commerce中繼資料設定檔。 請參閱[設定中繼資料設定檔](configure-aem.md#configure-a-metadata-profile)。

1. **啟用Dynamic Media**：確認已在您的AEM Assets環境中啟用具有OpenAPI功能的Dynamic Media。

## 設定AEM Assets

若要啟用產品與資產同步化，請設定AEM Assets環境。

### 步驟1：使用OpenAPI啟用Dynamic Media

必須在您的AEM Assets環境中啟用具有OpenAPI的Dynamic Media 。 產品視覺效果和新的AEM Assets授權可讓您透過Cloud Manager以自助方式啟用。 舊版AEM Assets授權需要Adobe支援才能啟用。 如需啟用步驟，請參閱[設定AEM Assets專案](configure-aem.md#prerequisites)。

### 步驟2：選擇性。 設定Commerce中繼資料設定檔

在AEM Assets中設定中繼資料設定檔，以儲存Commerce專屬的中繼資料。

如需詳細指示，請參閱[設定中繼資料設定檔](configure-aem.md#step-2-optional-configure-a-metadata-profile)。

### 步驟3：將中繼資料套用至資產

將Commerce中繼資料新增至AEM Assets中的產品影像。

檢視[AEM Commerce套件內容](configure-aem.md#aem-commerce-assets-commerce-package-contents)以取得欄位定義，以及[設定中繼資料設定檔](configure-aem.md#step-2-optional-configure-a-metadata-profile)以取得設定步驟。

資產必須處於&#x200B;**已核准**&#x200B;狀態，資料同步才會觸發。 單獨儲存中繼資料不會觸發事件。

>[!CAUTION]
>
> 將`AEM-Assets`圖層指派給您的[目錄檢視](https://experienceleague.adobe.com/zh-hant/docs/commerce/optimizer/setup/catalog-view)。 如果未指定圖層，產品影像資料可能會意外覆寫。

## 同步

設定之後，整合會自動同步`product-asset`對應。

如需詳細資訊，請參閱[自訂自動比對](../synchronize/custom-match.md)。

### 依SKU工作流程範例比對

將現有資產新增至新產品時的典型流程：

1. 在[!DNL Commerce Optimizer]中建立產品（透過API或資料擷取）。 產品一開始可能沒有影像。

1. 在AEM Assets中，開啟您要對應至產品的資產。

1. 將產品SKU新增至&#x200B;**commerce:skus**&#x200B;中繼資料並指派影像角色（例如，`thumbnail`、`image`）。

1. 核准要傳送的資產。 這會觸發Assets Integration Service處理的事件。

1. Assets整合服務會將產品影像對應傳送至[!DNL Commerce Optimizer]。 [!DNL Commerce Optimizer]中的產品已使用資產中的影像更新。

1. 確認影像可見。 留出時間讓同步完成（通常在幾分鐘內），然後檢查[!DNL Commerce Optimizer] UI中的產品（例如，資料同步或目錄檢視），或查詢店面API (目錄服務、即時搜尋、店面GraphQL API)以確認傳回影像。

## 影像角色處理

當產品有多個資產使用相同的影像角色時（例如，兩個資產具有`thumbnail`角色），整合可確保只有一個資產會保留該角色，以避免[!DNL Commerce Optimizer]層中的重複角色和非預期的店面行為。

**行為：**&#x200B;從AEM Assets傳送更新時，最近更新的資產會收到影像角色（例如，`thumbnail`），而該角色會從具有它的先前資產中移除。 這可防止店面中出現重複的影像角色。

## 更多相關資訊

* [產品視覺效果](../../optimizer/setup/product-visuals.md)
* [設定AEM Assets專案](configure-aem.md)
* [自訂自動比對](../synchronize/custom-match.md)
* [AEM Assets整合概述](../overview.md)
