---
title: 商店履行需求
description: 布建和上線 [!DNL Store Fulfillment solution]的需求。
role: Leader, Admin, Developer
level: Intermediate
feature: Shipping/Delivery, Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Adobe Commerce的商店履行需求

以下小節詳細說明安裝和啟用Adobe Commerce的「商店履行」解決方案的技術和業務需求。

## 平台與軟體版本需求

[!DNL Store Fulfillment]解決方案適用於下列平台上的Adobe Commerce客戶。

- 雲端基礎結構上的Adobe Commerce (ECE)
- Adobe Commerce內部部署(EE)

在安裝或升級之前，請參閱發行說明和Adobe Commerce系統需求，以取得有關版本相容性、更新或可能影響安裝或升級需求的變更的最新資訊。

- [Store Fulfillment發行說明](release-notes.md)

- *Adobe Commerce發行資訊*&#x200B;中的[Adobe Commerce發行說明](https://experienceleague.adobe.com/docs/commerce-operations/release/versions.html)。

- *Adobe Commerce安裝指南*&#x200B;中的[Adobe Commerce系統需求](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html)。


## 商店協助應用程式需求

管理商店取貨訂單的端對端程式，可透過安裝在行動裝置上的Store Assist應用程式進行管理。 這些裝置（由零售商或商店員工使用其個人智慧型手機所提供）必須符合下列需求：

**最低作業系統需求**

- ANDROID 6
- iOS 12

**最低硬體需求**

- 1 GB RAM
- 600 MB可用磁碟空間

## 業務需求

您的企業必須符合下列最低條件，才能實作「商店履行」解決方案：

- 僅限美國企業

- 企業對消費者(B2C)零售商、消費性包裝商品(CPG)製造商直接銷售給消費者(D2C)，或是直接銷售給消費者或小型企業的經銷商

- 至少一個實體商店或倉儲

- 使用適用於Adobe Commerce的Inventory management （亦稱為MSI）管理您的產品詳細目錄

- 財團化商家庫存的能力

- 在支援「商店履行」解決方案的所有位置，都可使用Wi-Fi：最低網際網路速度為3 Mbps

- 商店和倉儲關聯員在輪班期間可存取iOS或Android行動裝置，無論為個人或由商家提供

- 使用「商店履行」解決方案管理的產品必須具有包含SKU或UPC產品代碼的產品屬性
