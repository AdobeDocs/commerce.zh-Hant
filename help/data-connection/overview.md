---
title: 指南概觀
description: 瞭解如何使用 [!DNL Data Connection] 擴充功能整合Adobe Commerce資料與Adobe Experience Platform。
recommendations: noCatalog
exl-id: 660f9337-cad8-47fb-a959-0770f0fd813c
source-git-commit: a3e19940e2a3d8a240bb17703cfdd9903df311aa
workflow-type: tm+mt
source-wordcount: '1762'
ht-degree: 0%

---

# [!DNL Data Connection]簡介

>[!IMPORTANT]
>
>Experience Platform聯結器已重新命名為[!DNL Data Connection]。

[!DNL Data Connection]擴充功能會將您的Adobe Commerce Web執行個體連線至Adobe Experience Platform和Edge Network。 對於行動應用程式開發人員而言，您可以搭配使用Adobe Experience Platform Mobile SDK與Commerce，擷取Commerce資料並將其傳送至Experience Platform。 [了解更多](./mobile-sdk-epc.md)。

您的Commerce商店包含豐富的資料。 有關您的購物者如何瀏覽、檢視及最終在您網站上購買產品的資訊，可揭示建立更個人化購物體驗的機會。 雖然這些資料可通知購物車價格規則等原生Commerce功能和動態區塊，但資料仍會定位於您的Commerce執行個體中。

Adobe Experience Platform提供了一套技術，可在與Commerce商店中的資料結合後，透過Edge Network將該資料發佈到其他Adobe DX產品，以解鎖有關購物者購買行為的洞察資訊。 透過這些深入分析，您可以跨所有管道建立更加個人化的購物體驗。

下圖顯示當已安裝並設定[!DNL Data Connection]擴充功能時，您的Commerce資料如何從您的商店傳輸至其他Adobe DX產品。

![資料如何流向Experience Platform Edge](assets/commerce-edge.png)

在上圖中，您的行為、後端辦公室和客戶設定檔資料會使用SDK、API和來源聯結器傳送至Experience Platform Edge。 您不需要完全瞭解這些元件的運作方式，因為擴充功能可處理資料共用的複雜性。 當事件資料位於邊緣時，您可以將該資料提取到其他Experience Platform應用程式中。 例如：

| 應用 | 用途 | 使用案例 |
|---|---|---|
| [Adobe [!DNL Real-Time CDP]](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html) | 設定檔管理和細分服務 | **購買記錄細分**：商家可以根據特定時段（每月、每季、每年等）識別購買專案的客戶。 然後，商家可以建立這些客戶的區段，並針對促銷活動、行銷活動鎖定這些客戶，以及作為訂閱服務之潛在客戶的&#x200B;_頂端_&#x200B;資料。<br> **類別型細分**：商戶可以檢視購買的產品類別。<br> **以優惠方案為基礎的細分**：商家可以識別持續傳回產品的客戶。 提供給他們的優惠和折扣現在可能更具智慧。 例如，對於一直退貨的客戶，可以移除免運費。<br> **相似對象鎖定目標**： _相似對象_&#x200B;是商家為了促銷活動而採用的方法，可觸及可能會對其業務感興趣的新客戶，因為他們與現有客戶具有相似的特性。 可以根據行為和異動資料建立相似區段。<br> **客戶傾向**：可以從交易資料建立更深入的客戶設定檔，以識別客戶行為中的變更。 由於有更多資料流入計算，例如產品退貨和產品組態，傾向分數會有較高的信賴度。<br> **交叉銷售**：商家可以從Commerce中擷取的細微資訊找出強大的交叉銷售和追加銷售機會。 |
| [客戶 [!DNL Journey Analytics]](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html) | 完整Commerce歷程的深入分析 | **季節性趨勢**：商家可以識別季節性趨勢，這有助於他們為特定產品的週期性需求變化做好準備。 此外，商家可以識別任何產品在不同年份的整體人氣變化。<br> **轉換分析**：商戶只要知道購買產品的時間，並存取店面印象事件，就可以建立客戶的豐富個人檔案，以執行轉換分析。 |
| [Adobe [!DNL Analytics]](https://experienceleague.adobe.com/docs/analytics/analyze/admin-overview/analytics-overview.html) | 深入分析客戶行為與行銷活動績效 | **訂單退貨**：商戶可以識別具有退貨模式的客戶和較大型客戶區段。 這有助於商戶改善他們的商業策略，因為他們瞭解他們的客戶基礎行為是什麼樣的。<br> **訂單地址**：根據送貨地址，商家可以瞭解訂單是由客戶自己下單，還是由其他個人或實體下單。<br> **季節性趨勢**：商家可以識別季節性趨勢，這有助於他們準備特定產品的週期性需求變化。 此外，商家可以識別任何產品在不同年份的整體人氣變化。<br> **轉換分析**：商戶只要知道購買產品的時間，並存取店面印象事件，就可以建立客戶的豐富個人檔案，以執行轉換分析。 **注意** Adobe Analytics僅支援行為（店面）事件資料。 Adobe Analytics不支援異動(Backoffice)事件資料。 |
| [Adobe [!DNL Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html) | 跨管道的行銷活動協調 | **行為型歷程**：商戶可建議購買新機型，藉此鎖定兩年前購買行動電話的客戶。 商戶可為這些客戶建立個人化的行銷活動和促銷活動，並使用電子郵件和簡訊功能來聯絡。 此外，商家可以使用歷史順序和行為資料來識別趨勢。 例如，如果客戶過去曾購買具有特定設定的專案，而現在又希望再次購買相同的產品，則可透過賦予他們可見度並存取相同的產品設定，來增強其購買歷程。<br> **Personalization**：透過存取客戶設定檔資訊，[!DNL Journey Optimizer]可以解鎖高度個人化的歷程，讓商家透過多個不同管道聯絡客戶。<br> **已建立新設定檔**：歡迎電子郵件和促銷活動可鼓勵並影響新客戶的購物歷程。<br> **已刪除設定檔**：商家可以選擇停止傳送促銷電子郵件給已關閉帳戶的使用者端。 或者，商家也可以建立行銷活動，以贏回失去的客戶。 |

## 將Experience Platform資料提取回Commerce

使用[!DNL Data Connection]擴充功能將Commerce資料傳送至Experience Platform是Commerce資料共用功能的一面。 另一邊是選用的擴充功能，稱為[Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html)。 此擴充功能可讓您在Real-Time CDP中建立受眾，並將這些受眾部署至您的Commerce商店，以告知購物車價格規則、相關產品規則及動態區塊。

從高層面來看，從Commerce存放區到Experience Platform，然後透過Audience Activation擴充功能回頭的資料流程如下所示：

![[!DNL Data Connection]流量](assets/data-connection.png)

在您設定Commerce與Experience Platform以及Experience Platform與Commerce之間的連線後，資料會繼續流動。 除非升級時需要，否則您不需要重新連線。

## 概念

在這兩個系統之間共用資料需要您瞭解數個概念。

- **資料** — 與Experience Platform共用的資料是從店面上的瀏覽器事件、伺服器上的後台事件和設定檔記錄資料收集而得。 店面活動是從網站上的購物者互動擷取的，並包括`addToCart`、`pageView`、`createAccount`、`editAccount`、`startCheckout`、`completeCheckout`、`signIn`、`signOut`等事件。 如需店面活動的完整清單，請參閱[店面活動](events.md#storefront-events)。 伺服器端或後台事件包含[訂單狀態](events-backoffice.md#order-status)資訊，例如[`orderPlaced`](events-backoffice.md#orderplaced)、[`orderReturned`](events-backoffice.md#orderitemreturncompleted)、[`orderShipped`](events-backoffice.md#ordershipmentcompleted)、[`orderCancelled`](events-backoffice.md#ordercancelled)等。 如需後台事件的完整清單，請參閱[後台事件](events-backoffice.md)。 個人資料記錄資料包含建立、更新或刪除新個人資料時的資訊。 檢視[個人資料記錄資料](events-profilerecord.md)以深入瞭解。

- **Experience Platform和Edge Network** — 大部分Adobe DX產品的資料倉儲。 傳送至Experience Platform的資料會透過Experience Platform Edge Network傳播至Adobe DX產品。 例如，您可以啟動Journey Optimizer、從邊緣擷取您的特定Commerce事件資料，以及在Journey Optimizer中建立捨棄的購物車電子郵件。 如果Commerce商店中有任何放棄的購物車，Journey Optimizer就可以傳送該電子郵件。 深入瞭解[Experience Platform和Edge Network](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/overview.html)。

- **結構描述** — 結構描述描述正在傳送的資料結構。 在Experience Platform可以擷取Commerce資料之前，您必須撰寫結構描述資料結構，並為每個欄位可包含的資料型別提供限制。 結構描述包含一個基底類別和零個或多個結構描述欄位群組。 此結構描述會使用XDM結構，所有Adobe DX產品都可以讀取此結構。 結構描述可確保所有DX產品都能瞭解傳送至Experience Platform的資料。 深入瞭解[結構描述](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html)。

- **資料集** — 資料集合的儲存和管理結構，通常是包含結構描述（欄）和欄位（列）的表格。 資料集也包含中繼資料，可說明其儲存資料的各個層面。 所有成功擷取至Adobe Experience Platform的資料都包含在資料集中。 深入瞭解[資料集](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html)。

- **資料串流** — 可讓資料從Adobe Experience Platform流向其他Adobe DX產品的ID。 此ID必須與您特定Adobe Commerce執行個體中的特定網站相關聯。 當您建立此資料流時，請指定您在上面建立的XDM結構描述。 深入瞭解[資料串流](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html)。

## 支援的架構

[!DNL Data Connection]擴充功能適用於下列架構：

- PHP/Luma
- [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/integrations/adobe-commerce/aep/)
- [AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/integrations/aep.html)

>[!BEGINSHADEBOX]

## 先決條件

若要使用[!DNL Data Connection]擴充功能，您必須具備下列條件：

- Adobe Commerce 2.4.4或更新版本
- Adobe ID和組織ID
- 收集店面事件資料所需的[Adobe使用者端資料層(ACDL)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/client-data-layer/overview.html)
- 其他Adobe DX產品的權益。

>[!ENDSHADEBOX]

## 入門步驟

從高層面來看，啟用[!DNL Data Connection]擴充功能包含下列步驟：

1. [安裝](install.md) [!DNL Data Connection]延伸模組。
1. [登入](https://helpx.adobe.com/manage-account/using/access-adobe-id-account.html)您的Adobe帳戶，並[檢視以確認](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255)您的組織識別碼。 組織ID是與已布建Experience Cloud公司相關聯的ID。 此ID是24個字元的英數字串，後面接著（而且必須包含） `@AdobeOrg`。
1. 確定您擁有Experience Platform[中資料收集的](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html)許可權。
1. 檢閱您可以收集及傳送的[資料型別](data-ingestion.md)。
1. 使用Commerce特定的欄位群組建立或更新您的[時間序列事件結構描述](update-xdm.md)或[設定檔記錄資料結構描述](profile-data.md)。
1. [根據您建立或更新的結構描述建立資料集](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset)。 此資料集包含傳送至Experience Platform Edge的Commerce資料。
1. [建立資料流](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html)並選取包含Commerce特定欄位群組的XDM結構描述。
1. [連線到Commerce服務](../landing/saas.md)。
1. [連線到Adobe Experience Platform](connect-data.md)。

本指南的其餘部分將更詳細地引導您完成所有這些步驟，以便您快速入門，並開始在您的Commerce商店中使用Adobe DX產品的強大功能。

>[!NOTE]
>
>針對行動開發人員瞭解如何[整合](./mobile-sdk-epc.md) Adobe Experience Platform Mobile SDK與Commerce。

## HIPAA整備

[!DNL Data Connection]擴充功能可讓您與Experience Platform共用[!DNL Commerce]個後台資料，並維持HIPAA合規性。 [了解更多](hipaa-readiness.md)。

## 客群

本指南是專為想要豐富及個人化Commerce商店，以提升客戶購物體驗的Adobe Commerce商家所設計。

## 支援

如果您需要本指南未涵蓋的資訊或問題，請使用下列資源：

- [說明中心](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/overview.html){target="_blank"}
- [支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket){target="_blank"} — 提交票證以接收其他說明。
