---
title: Commerce產品解決方案
description: 瞭解如何使用徽章來識別適用於不同Adobe Commerce解決方案（SaaS、PaaS、內部部署）的檔案。
feature: Paas, Saas
recommendations: noDisplay, noCatalog
hide: true
hidefromtoc: true
exl-id: 5ba1fa65-391f-4af7-8c40-d8314ec9d3e5
source-git-commit: 5e4481dfd7259a07bda58a1e945b086e9f1c1805
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---

# Adobe Commerce產品解決方案

Adobe提供數種解決方案來滿足電子商務業務的需求。 有關[Experience League](https://experienceleague.adobe.com/zh-hant/docs/commerce)和[Adobe Developer](https://developer.adobe.com/commerce/docs/)網站的Adobe Commerce檔案為客戶提供自助服務資源，以支援所有解決方案。 但是，如果沒有指引，導覽如此大量的內容可能具有挑戰性。

>[!NOTE]
>
>如需[!DNL Adobe Commerce as a Cloud Service] (SaaS)中可用功能的詳細資訊，以及這些功能如何與其他版本的Adobe Commerce (例如[!DNL Adobe Commerce on Cloud]和[!DNL Adobe Commerce on Premises] (PaaS))一致，請參閱[功能比較](../cloud-service/feature-comparison.md)。

## 徽章

徽章可協助您快速識別在傳統網站導覽或網際網路搜尋中尋找的Commerce檔案，是否與您使用的Commerce產品解決方案有關。 當內容僅套用至一個解決方案時，這一點尤其重要。

如果顯示徽章，表示內容僅套用至指定的解決方案。 如果未顯示徽章，則表示內容適用於所有Adobe Commerce解決方案。

例如，如果您使用Adobe Commerce as a Cloud Service，您應該忽略關於[安裝](../product-recommendations/install-configure.md#install-product-recommendations) Product Recommendations擴充功能和[設定](../product-recommendations/install-configure.md#configure-product-recommendations) Commerce Services聯結器的內容。 當您建立執行個體時，Adobe會自動完成這些步驟。

### 定義

下表定義在Adobe Commerce檔案中顯示的徽章：

>[!BEGINSHADEBOX]

![資訊](../cloud-service/assets/Smock_InfoOutline_18_N.svg)此處說明的徽章特別適用於Adobe Commerce檔案。 它們不代表檔案在其他Adobe Experience Cloud產品中如何使用徽章。

>[!ENDSHADEBOX]

#### 僅[!BADGE SaaS]{type=Positive tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"}

此徽章僅識別[Adobe Commerce as a Cloud Service](../cloud-service/overview.md)和[Adobe Commerce Optimizer](../optimizer/overview.md)專案的檔案。 這些專案在雲端原生、完全受管理的軟體即服務(SaaS)解決方案上進行控管，其中Adobe負責大部分的營運層面，例如持續更新、安全性監控和擴充能力，因此客戶可以聚焦於商業而非基礎架構。

#### 僅[!BADGE 個PaaS]{type=Informative tooltip="僅適用於雲端專案(Adobe管理的PaaS基礎結構)和內部部署專案的Adobe Commerce 。"}

此徽章只會識別與Cloud[和內部部署專案上的](https://experienceleague.adobe.com/zh-hant/docs/commerce-on-cloud/user-guide/overview)Adobe Commerce相關的檔案。 雲端上的Adobe Commerce專案在預先布建的環境中於雲端原生、完全受管理的平台即服務(PaaS)解決方案上託管，該解決方案具有Adobe Commerce的所有核心功能。 內部部署專案在客戶管理的基礎架構上託管。

>[!NOTE]
>
>除非另有說明，否則這也包括根據Magento Open Source程式碼庫自行託管的專案。

### 規則

請使用下列規則來瞭解適用於各個Adobe Commerce解決方案的內容：

- **頁面層級徽章**：顯示在頁面頂端（頁面標題上方）。 指出頁面上的&#x200B;_所有_&#x200B;內容僅套用至指定的解決方案。

- **區段層級徽章**：顯示在頁面上所有其他標題的正下方（頁面標題除外）。 表示該區段中的內容僅適用於指定的解決方案。

- **內嵌徽章**：顯示在所有非標題頁面元素內，例如表格、段落和清單。 表示該元素中的內容僅套用至指定的解決方案。

>[!NOTE]
>
>徽章旨在互斥。 這表示您不會在同一頁面或區段中看到多個頁面或區段層級徽章。 不過，同一頁面或同一區段中有多個內嵌徽章是可能的。
