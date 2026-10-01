---
title: B2B共用目錄投影
description: 瞭解B2B聯結器如何將Adobe Commerce B2B共用目錄專案至受保護的Commerce Optimizer目錄檢視中，以及店面如何解析並授權購買者存取權。
feature: Integration, Configuration
role: Admin, Developer
level: Intermediate
TQID: 'https://experienceleague.adobe.com/b37PBjcVQXRSLrB6c7nEf3A3U5cuLs1lQzwPUbp9fdA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
feature_v2:
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
subfeature_v2:
  - id: 3c398179-d35a-51ba-b317-6c5b95feef5e
    internal-label: Logs
  - id: a1d22079-48b9-5e69-9ee6-eb236068ef34
    internal-label: Search
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%
---
# B2B共用目錄投影

[!DNL Adobe Commerce Optimizer Connector for B2B]專案[!DNL Adobe Commerce]共用目錄和公司指派到受保護的[!DNL Adobe Commerce Optimizer]目錄檢視。

## 基礎同步化與B2B投影

基底[!DNL Adobe Commerce Optimizer Connector]同步目錄和定價摘要，將商店檢視對應到目錄來源，將網站對應到價格簿，並將客戶群組對應到價格簿。

[!DNL Adobe Commerce Optimizer Connector for B2B]會將每個自訂共用目錄的分類和價格專案到受保護的檢視中。 Adobe Commerce會使用購買者的公司指派來選取檢視。 受限制的存取金鑰會驗證已簽署的請求，但不會決定目錄存取權。 Adobe Commerce是聯結器管理目錄、定價和B2B投影資料的記錄系統。 在[!DNL Adobe Commerce Optimizer]設定中管理產品探索和建議。

## 資料對應

B2B投影將同步化的目錄內容與訂價與「共用目錄分類」及公司指派內容結合在一起。

![圖表將[!DNL Adobe Commerce]存放區檢視、定價、共用目錄和公司指派對應到[!DNL Adobe Commerce Optimizer]](./assets/b2b-catalog-projection-mapping.svg){width="800"}中預計的私人目錄檢視

| [!DNL Adobe Commerce]資料 | [!DNL Adobe Commerce Optimizer]個結果 | 用途 |
| --- | --- | --- |
| 啟用商店檢視和產品資料 | 目錄來源 | 提供本地化產品內容。 |
| 網站與客戶群組定價 | 價格簿 | 提供適用的價格，但不授權存取 |
| 自訂共用目錄分類 | 原則 | 將目錄檢視篩選為共用目錄分類。 |
| 自訂共用目錄和已啟用的存放區檢視 | 私人目錄檢視 | 為每個組合建立一個受保護的檢視，並附上適用的目錄來源、原則和價格簿。 |
| 將公司指派給共用目錄 | 已解析的購買者內容 | 允許已驗證後端解析與購買者公司關聯的目錄檢視。 |
| 指派給受保護檢視的受限制存取金鑰 | 目錄保護 | 授權請求到受保護的目錄檢視，但不選取定價。 |

每個私人型錄檢視只能參考一個價格簿。 使用不同當地語系化目錄來源時，具有相同網站和客戶群組定價內容的商店檢視可以共用價格簿。 聯結器不會為每個共用目錄建立價格簿。

預設的共用目錄不會投影為B2B私人目錄檢視。

## 執行階段授權

採購員登入後，Commerce後端會驗證工作階段，並使用採購員的公司指定與存放區檢視來解析適當的型錄檢視與價格簿。

店面會傳送目錄檢視ID、價格簿ID以及與每個銷售API請求簽署的權杖。 [!DNL Adobe Commerce Optimizer]會根據指派給目錄檢視的受限制存取金鑰，驗證JWT的RS256簽章。 只有在權杖和金鑰有效且未過期時，才會傳回目錄資料。

從購物者透過店面和Commerce後端到[!DNL Adobe Commerce Optimizer]](./assets/b2b-catalog-runtime-authorization.svg){width="700"}的B2B目錄請求的![執行階段授權流程

對於私人目錄請求，傳送以下標頭：

| 頁首 | 用途 |
| --- | --- |
| `AC-View-ID` | 識別目錄檢視。 |
| `AC-Price-Book-ID` | 識別要使用的價格簿。 |
| `AC-Catalog-View-Access-Token` | 攜帶已簽署的JWT，該JWT授權對受保護目錄檢視的存取權。 |

如需完整要求與權杖需求，請參閱[銷售API驗證](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api#authentication)以及[驗證對私人目錄檢視的存取權](/help/optimizer/setup/private-catalog-view.md#verify-access-is-enforced)。

## 保護範圍

目錄保護僅涵蓋目錄和搜尋要求。 它不會保護購物車、結帳或訂單作業的安全。 在Adobe Commerce或連線交易系統中強制執行購買資格。

## 投影設定和監視

B2B聯結器會專案來自[!DNL Adobe Commerce]的私人目錄檢視、原則、價格簿參考和受限制的存取金鑰組態。 您不需要手動建立這些聯結器管理的投影物件。 如需安裝指示，請參閱[開始使用B2B聯結器](get-started-b2b-shared-catalogs.md)。

若要監視預計的目錄檢視並調解組態漂移，請參閱[監視目錄檢視同步處理](catalog-view-sync-status.md)。 若要管理指派的金鑰，請參閱[管理B2B共用目錄的限制存取金鑰](restricted-access-keys.md)。
