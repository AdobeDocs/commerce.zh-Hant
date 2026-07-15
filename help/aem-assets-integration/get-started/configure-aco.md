---
title: 設定適用於Commerce Optimizer的AEM Assets
description: 瞭解如何設定 [!DNL Adobe Commerce Optimizer]的AEM Assets整合。
feature: CMS, Media, Configuration, Integration
source-git-commit: 0c2e50338cbf286704239b6d1f628180e85a3bef
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 0%

---


# 為[!DNL Adobe Commerce Optimizer]設定AEM Assets

僅[!BADGE SaaS]{type=Positive tooltip="僅適用於Adobe Commerce Optimizer專案。"}

適用於[!DNL Adobe Commerce Optimizer]的AEM Assets整合可讓商家使用AEM Assets作為產品影像的集中式數位資產管理解決方案。 本指南涵蓋[!DNL Commerce Optimizer]的特定組態。

下圖為[!DNL Adobe Commerce Optimizer]與AEM Assets整合之間的產品同步概觀。

![AEM Assets到[!DNL Commerce Optimizer]流量](../assets/aco-asset-sync-architecture.png){width="700"}

此整合有兩個獨立的事件流程。 兩者都使用[Adobe I/O Events](https://developer.adobe.com/events/docs/)將事件傳輸至Assets Integration Service，但每個方向都使用自己的事件提供者：

* **從AEM Assets到Assets Integration Service**：當資產被核准、拒絕或移除時，事件會傳遞到Assets Integration Service。 此服務會比對資產與使用`match-by-SKU` （中繼資料導向）或[自訂比對器(App Builder)](../synchronize/custom-match.md){target=_blank}的產品，然後將`product-asset`對應傳送至[!DNL Commerce Optimizer]，並在其中儲存為產品層。

  >[!NOTE]
  >
  >整合所使用的`AEM-Assets`目錄層會在上線時自動建立。 您不需要預先建立。 如需目錄圖層如何運作以及AEM-Assets圖層運作方式的背景資訊，請參閱[AEM-Assets圖層](../../optimizer/setup/catalog-layer.md#aem-assets-layer)。

* **從[!DNL Adobe Commerce Optimizer]到Assets Integration Service**：當產品在[!DNL Commerce Optimizer]中更新時，事件會傳遞到Assets Integration Service。 此服務會將任何符合的資產對應同步回[!DNL Commerce Optimizer]。

## 限制

[!DNL Commerce Optimizer]整合有下列限制：

### 圖層相關限制

* 對AEM Assets內容使用專屬圖層。

  從AEM Assets傳送的裝載會填入Commerce Optimizer目錄層。 該圖層中的值會覆寫提供欄位的基本目錄屬性。 當整合忽略裝載中的欄位時，該圖層中的對應值可能會被空值覆寫。 與不相關的Commerce工作流程共用圖層（或重複使用已儲存非AEM-Assets產品資料的圖層）可能會導致&#x200B;**無意資料遺失**&#x200B;或混淆覆寫。 主要為AEM驅動的產品影像同步保留圖層名稱（例如預設的&#x200B;**`AEM-Assets`**）。

* 整合支援每個租使用者一個目錄來源：單一地區設定和一個命名圖層。 目前不支援為相同租使用者設定多個AEM-Assets圖層或多個地區設定。

* 重複使用現有圖層或與不相關的工作流程共用圖層，經常是可預防的支援案例的原因。

### 其他限制

* **僅限影像**：整合在此階段不支援視訊或其他媒體型別。
* **沒有類別影像**：無法使用類別影像同步處理。 不支援AEM Assets中用於Assets選擇器（UI插入）的類別影像。
* **沒有多網站區別**：整合不會處理多網站；與產品相關的影像在所有管道和原則上都顯示相同。
* **影像位置/順序**：不支援影像位置和順序。
* **產品必須存在**：如果產品不存在於[!DNL Commerce Optimizer]中，則不會為該產品 — 資產對應建立圖層。

## 先決條件

在設定整合之前，請確定您具備：

* 具有&#x200B;**產品視覺效果**&#x200B;權益的有效[!DNL Adobe Commerce Optimizer]執行個體（整合Dynamic Media與OpenAPI功能+ [AEM Assets Prime](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-prime)），或客戶提供的AEM Assets授權（例如&#x200B;**AEM Assets Ultimate**）並啟用Dynamic Media。
* 存取AEM Assets as a Cloud Service環境。
* 同一Adobe IMS組織中的[!DNL Commerce Optimizer]和AEM Assets。
* 在您的AEM Assets環境中啟用OpenAPI的Dynamic Media （請參閱[設定AEM Assets專案](configure-aem.md#prerequisites)以取得啟用步驟）。

### 請先設定AEM Assets

若要支援整合，請先設定AEM Assets專案和環境，再開始與[!DNL Commerce Optimizer]進行AEM Assets整合的程式。 這包括以OpenAPI功能啟用Dynamic Media，以及讓Commerce中繼資料結構、事件和UI可在AEM專案中使用。

* [!BADGE 建議]{type=Positive}在AEM版本`2026.5.26309`和更新版本上，啟用無程式碼部署的Cloud Manager整合。 請依照[啟用Commerce整合（自助服務）](configure-aem.md#enable-aem-commerce-self-service)操作。

* 在舊版AEM中，手動部署`assets-commerce`套件。
請依照[手動安裝assets-commerce套件](configure-aem.md#install-the-assets-commerce-package-manually)操作。

>[!TIP]
>
> 您可以從右上角功能表檢視目前的AEM版本： **[!UICONTROL Help]** > **[!UICONTROL About AEM]**。

## 入門

>[!IMPORTANT]
>
>在您提交支援票證以啟用與[!DNL Commerce Optimizer]的整合之前，請先完成此程式以[設定AEM Assets](#configure-aem-assets-first)。 支援需要設定AEM Assets環境和專案以支援AEM Commerce整合，包括部署`assets-commerce`套件（或同等自助服務）的中繼資料和事件。 在設定AEM之前開啟票證可能會延遲上線。

若要使用[!DNL Commerce Optimizer]加入AEM Assets整合，Adobe支援人員必須向Assets整合服務註冊您的Adobe Commerce Optimizer執行個體，並訂閱至：

* AEM Assets事件（資產已核准、更新、已移除）
* [!DNL Commerce Optimizer]個目錄事件（已建立、已更新的產品）

若要啟動此程式，請[建立支援票證](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket)，其中包含下列資訊：

* 在您的[!DNL Commerce Optimizer] URL或Commerce Cloud Manager UI中找到&#x200B;**[!DNL Adobe Commerce Optimizer]租使用者識別碼** （執行個體識別碼）。
* **當您[設定AEM Assets](#configure-aem-assets-first)進行整合時，所設定的AEM方案ID和環境ID**。
* **符合規則**：符合SKU或[外部符合專案(App Builder)](../synchronize/custom-match.md){target=_blank}。
* **階層**：要登入租使用者的目錄階層名稱（請參閱&#x200B;**階層相關限制**）。 只有在刻意的情況下才指定自訂名稱；否則會使用預設&#x200B;**`AEM-Assets`**。
* **地區設定**：要向註冊租使用者的目錄來源地區設定（例如，`en-US`）。 此地區設定必須符合您在目錄檢視和產品目錄資料中使用的地區設定。

### 設定目錄檢視

[!DNL Commerce Optimizer]租使用者註冊之後，請設定您的目錄檢視，讓店面和API顯示AEM驅動影像資料：

* **選取目錄來源（地區）** — 選取您在支援票證中指定的相同地區（例如&#x200B;**`en-US`**）。 整合會為每個租使用者註冊一個地區設定；如果不相符，同步影像就不會出現在預期的目錄檢視中。
* **指派目錄圖層** — 指派&#x200B;**`AEM-Assets`**&#x200B;圖層（或票證中的自訂圖層名稱）給該目錄檢視。

如果未正確指派地區設定或圖層，影像資料會&#x200B;**未出現**&#x200B;或行為異常，即使在上游同步已成功。

## 同步

設定之後，整合會自動同步`product-asset`對應。

如需詳細資訊，請參閱[自訂自動比對](../synchronize/custom-match.md)。

### 依SKU工作流程範例比對

將現有資產新增至新產品時的典型流程：

1. 在[!DNL Commerce Optimizer]中建立產品（透過API或資料擷取）。 產品一開始可能沒有影像。

1. 在AEM Assets中，開啟您要對應至產品的資產。

1. 將產品SKU新增至&#x200B;**commerce:skus**&#x200B;中繼資料並指派影像角色（例如，`thumbnail`、`image`）。

1. 核准要傳送的資產。 這會觸發Assets整合服務處理的事件。

1. Assets整合服務會將產品影像對應傳送至[!DNL Commerce Optimizer]。 [!DNL Commerce Optimizer]中的產品已使用資產中的影像更新。

1. 確認影像可見。 請稍候數分鐘，讓同步處理完成，然後檢查[!DNL Commerce Optimizer] UI中的產品，或查詢店面API以確認影像已傳回。

## 影像角色處理

當產品有多個資產使用相同的影像角色時（例如，兩個資產具有`thumbnail`角色），整合可確保只有一個資產會保留該角色，以避免[!DNL Commerce Optimizer]層中的重複角色和非預期的店面行為。

**行為：**&#x200B;從AEM Assets傳送更新時，最近更新的資產會收到影像角色（例如，`thumbnail`），而該角色會從具有它的先前資產中移除。 這可防止店面中出現重複的影像角色。

## 更多相關資訊

* [產品視覺效果](../../optimizer/setup/product-visuals.md)
* [設定AEM Assets專案](configure-aem.md)
* [自訂自動比對](../synchronize/custom-match.md)
* [AEM Assets整合概述](../overview.md)
