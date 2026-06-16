---
title: 設定適用於Commerce Optimizer的AEM Assets
description: 瞭解如何設定 [!DNL Adobe Commerce Optimizer]的AEM Assets整合。
feature: CMS, Media, Configuration, Integration
source-git-commit: 2cc7b70a6923687c74fe3f4b88448eaada6d16af
workflow-type: tm+mt
source-wordcount: '1453'
ht-degree: 0%

---


# 為[!DNL Adobe Commerce Optimizer]設定AEM Assets

僅[!BADGE SaaS]{type=Positive tooltip="僅適用於Adobe Commerce Optimizer專案。"}

適用於[!DNL Adobe Commerce Optimizer]的AEM Assets整合可讓商家使用AEM Assets作為產品影像的集中式數位資產管理解決方案。 本指南涵蓋[!DNL Commerce Optimizer]的特定組態。

與Adobe Commerce (PaaS)或[!DNL Adobe Commerce as a Cloud Service]不同，[!DNL Commerce Optimizer]沒有管理員設定UI。 若要啟用整合，請使用您的[!DNL Adobe Commerce Optimizer]和AEM Assets詳細資料建立支援票證。 Adobe支援會設定整合，並在Assets整合服務中註冊您的租使用者。

**在提交票證之前準備AEM Assets。** 租使用者註冊會假設AEM端可用於Commerce。 例如，在您部署AEM Commerce `assets-commerce`套件後，讓中繼資料和事件如說明般運作。 **在設定AEM之前開啟票證可能會延遲上線。**

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
* 在您的AEM Assets環境中啟用OpenAPI的Dynamic Media （請參閱[設定AEM Assets專案](configure-aem.md#prerequisites)以取得啟用步驟）。

## 請先設定AEM Assets

在&#x200B;**之前，完成AEM Assets步驟**&#x200B;您[開啟支援票證](#onboarding)以進行租使用者註冊。 安裝模式符合Adobe Commerce as a Cloud Service — 請參閱[設定AEM Assets專案以支援Commerce中繼資料](configure-aem.md)。

### 步驟1：部署AEM Commerce套件

在您的AEM專案中安裝並部署`assets-commerce`套件，以便使用Commerce中繼資料結構、事件和UI。

完成[安裝`assets-commerce`封裝](configure-aem.md#step-1-install-the-assets-commerce-package)中的完整程式。 開啟支援票證之前，請依照下列步驟操作：

1. 複製Cloud Manager Git存放庫並將[AEM Assets Commerce存放庫](https://github.com/ankumalh/assets-commerce)程式碼複製到您的專案。

1. 在您的專案的所有`filter.xml`和`pom.xml`檔案中，以您的應用程式名稱取代所有出現的&lt;my-app>。

1. 認可、推播、執行您的部署管道，並驗證&#x200B;**[!UICONTROL Commerce]**&#x200B;索引標籤是否出現在資產屬性上。

請參閱[安裝`assets-commerce`套件](configure-aem.md#step-1-install-the-assets-commerce-package)，以取得Cloud Manager熒幕擷取畫面、管線步驟，以及疑難排解（如果缺少&#x200B;**[!UICONTROL Commerce]**&#x200B;索引標籤）。

### 步驟2：使用OpenAPI啟用Dynamic Media

必須在您的AEM Assets環境中啟用具有OpenAPI功能的Dynamic Media 。 自助式路徑（例如產品視覺效果的Cloud Manager）和Adobe支援路由在[設定AEM Assets專案](configure-aem.md#prerequisites)下說明。

### 步驟3：套用Commerce中繼資料並核准資產

將Commerce中繼資料新增至AEM Assets中的產品影像 — 如需欄位定義，請參閱[AEM Commerce套件內容](configure-aem.md#aem-commerce-assets-commerce-package-contents)。

資產必須處於&#x200B;**已核准**&#x200B;狀態，資料同步才會觸發。 單獨儲存中繼資料不會觸發事件。

### 步驟4：選用 — 設定Commerce中繼資料設定檔

如果您選擇使用AEM中繼資料設定檔來簡化撰寫作業，請在&#x200B;**之後**&#x200B;設定這些設定檔，封裝已部署，且您的團隊瞭解必要的Commerce欄位 — 與&#x200B;**設定AEM Assets專案**&#x200B;相同的選用模式。

請參閱[設定中繼資料設定檔](configure-aem.md#step-2-optional-configure-a-metadata-profile)。

## 限制

[!DNL Commerce Optimizer]整合有下列限制：

### 圖層相關限制

在&#x200B;**之前**&#x200B;閱讀本節，您可以在支援票證中選擇目錄圖層名稱。 在沒有此前後關聯的情況下選擇或共用圖層，經常會造成可預防的支援案例。

**為AEM Assets內容使用專用圖層。** 從AEM Assets傳送的裝載會填入Commerce Optimizer目錄&#x200B;**層**。 該圖層&#x200B;**覆寫**&#x200B;提供欄位之基本目錄屬性的值。 當整合忽略裝載中的欄位時，該圖層中的對應值可能會被空白值覆寫。 與不相關的Commerce工作流程共用圖層（或重複使用已儲存非AEM-Assets產品資料的圖層）可能會導致&#x200B;**無意資料遺失**&#x200B;或混淆覆寫。 在&#x200B;**之前規劃圖層選擇**&#x200B;您開啟支援票證，並保留該圖層名稱（例如預設的&#x200B;**`AEM-Assets`**）主要用於AEM驅動的產品影像同步。

>[!IMPORTANT]
>
>整合支援每個租使用者&#x200B;**一個**&#x200B;目錄來源：單一地區設定和&#x200B;**一個具名圖層**。 目前不支援為相同租使用者設定多個AEM-Assets圖層或多個地區設定。

### 其他限制

* **僅限影像**：整合在此階段不支援視訊或其他媒體型別。
* **沒有類別影像**：無法使用類別影像同步處理。 不支援AEM Assets中用於Assets選擇器（UI插入）的類別影像。
* **沒有多網站區別**：整合不會處理多網站；與產品相關的影像在所有管道和原則上都顯示相同。
* **影像位置/順序**：不支援影像位置和順序。
* **產品必須存在**：如果產品不存在於[!DNL Commerce Optimizer]中，則不會為該產品 — 資產對應建立圖層。

## 入門

若要將AEM Assets與[!DNL Commerce Optimizer]整合，您必須[建立支援票證](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket)。

Adobe支援會使用您票證中的資訊，向Assets Integration Service註冊您的租使用者，並設定整合。

在提交票證之前，請確定您已先完成[設定AEM Assets](#configure-aem-assets-first)。

在您的支援票證中包含下列資訊：

* 在您的[!DNL Commerce Optimizer] URL或Commerce Cloud Manager UI中找到&#x200B;**[!DNL Adobe Commerce Optimizer]租使用者識別碼** （執行個體識別碼）。
* **AEM計畫識別碼**。
* **AEM環境識別碼**。
* **符合規則**：符合SKU或[外部符合專案(App Builder)](../synchronize/custom-match.md){target=_blank}。
* **階層**：要登入租使用者的目錄階層名稱（請參閱&#x200B;**階層相關限制**）。 只有在刻意的情況下才指定自訂名稱；否則會使用預設&#x200B;**`AEM-Assets`**。
* **地區設定**：要向註冊租使用者的目錄來源地區設定（例如，`en-US`）。 這必須符合您在目錄檢視和產品目錄資料中使用的地區設定。

Adobe支援處理完您的票證後，便會設定整合，並且您的租使用者會向Assets Integration Service註冊。

上線完成後：

1. **向Assets Integration Service註冊**：您的[!DNL Commerce Optimizer]租使用者已使用票證中提供的[!DNL Adobe Commerce Optimizer]租使用者ID、AEM方案ID、AEM環境ID、比對規則、地區設定和圖層名稱，向Assets Integration Service註冊。

1. **事件訂閱**： Assets Integration Service訂閱：

   * AEM Assets事件（資產已核准、更新、已移除）
   * [!DNL Commerce Optimizer]個目錄事件（已建立、已更新的產品）

設定您的[目錄檢視](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/catalog-view)，讓店面和API顯示AEM驅動的影像資料：

* **目錄來源（地區）** — 選取您在支援票證中指定的相同地區（例如&#x200B;**`en-US`**）。 整合會為每個租使用者註冊一個地區設定；如果不相符，同步影像就不會出現在預期的目錄檢視中。
* **目錄圖層** — 將&#x200B;**`AEM-Assets`**&#x200B;圖層（或票證中的自訂圖層名稱）指派給該目錄檢視。

如果未正確指派地區設定或圖層，影像資料可能會&#x200B;**未出現**&#x200B;或出現意外行為 — 即使在上游同步已成功。

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

1. 確認影像可見。 留出時間讓同步完成（通常在幾分鐘內），然後檢查[!DNL Commerce Optimizer] UI中的產品（例如，資料同步或目錄檢視），或查詢店面API （目錄服務、即時搜尋、店面GraphQL API）以確認傳回影像。

## 影像角色處理

當產品有多個資產使用相同的影像角色時（例如，兩個資產具有`thumbnail`角色），整合可確保只有一個資產會保留該角色，以避免[!DNL Commerce Optimizer]層中的重複角色和非預期的店面行為。

**行為：**&#x200B;從AEM Assets傳送更新時，最近更新的資產會收到影像角色（例如，`thumbnail`），而該角色會從具有它的先前資產中移除。 這可防止店面中出現重複的影像角色。

## 更多相關資訊

* [產品視覺效果](../../optimizer/setup/product-visuals.md)
* [設定AEM Assets專案](configure-aem.md)
* [自訂自動比對](../synchronize/custom-match.md)
* [AEM Assets整合概述](../overview.md)
