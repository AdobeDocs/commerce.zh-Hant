---
title: 大量資料移轉工具
description: 瞭解如何使用大量資料移轉工具，將資料從雲端執行個體上的現有Adobe Commerce移轉至 [!DNL Adobe Commerce as a Cloud Service]。
feature: Cloud
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案（Adobe管理的SaaS基礎結構）。"
role: Developer
level: Intermediate
exl-id: 81522de9-df54-4651-b8ed-58956376af86
autotag-review: '2026-07-22T19:18:39.433Z'
TQID: 'https://experienceleague.adobe.com/tkCFabZpBKu-W34wsufHlVIWzCUE8FKm4kK7qZahxBU'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2:
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 4c0eca0039bab7d015144dd9ac3885a0b2be0563
workflow-type: tm+mt
source-wordcount: 924
ht-degree: 0%

---

# 大量資料移轉工具

>[!IMPORTANT]
>
>大量資料移轉工具目前正在搶先使用。 存取權完全透過Commerce部署工程(CDE)參與程式提供。

大量資料移轉工具可讓系統整合經銷商將第一方核心商務資料從[!DNL Adobe Commerce on Cloud]或內部部署安裝移轉到[!DNL Adobe Commerce as a Cloud Service]。

大量資料移轉工具是以Docker為基礎的CLI，系統整合經銷商可在自己的移轉機器上執行。 它會連線至來源例項、擷取第一方核心商務資料、將其上傳至Adobe的移轉服務（Commerce資料移轉服務），並監控完成進度。

所有命令都會在本機執行，因此您可以控制何時開始移轉、何時套用維護模式以及何時執行每個階段。

## 移轉工作流程

此工具會端對端管理下列階段：

- **資料擷取** — 從來源執行個體（[!DNL Adobe Commerce on Cloud]或內部部署）擷取第一方核心商務資料。
- **資料載入** — 將擷取的資料載入目標[!DNL Adobe Commerce as a Cloud Service]執行個體。
- **資料完整性驗證** — 執行自動化的移轉後檢查，包括REST與GraphQL API比較及記錄計數驗證。

>[!NOTE]
>
>目前，大量資料移轉工具僅支援移轉第一方核心商務資料。 目前不支援自訂資料移轉。 組態設定（存放區設定、系統組態）不會自動移轉，且必須在移轉前於目標執行個體上獨立設定。

## 架構

大量資料移轉工具採用分散式架構，可安全且有效率地移轉資料。 此工具可協助系統整合經銷商將資料從現有的[!DNL Adobe Commerce on Cloud or on-premises instance]移轉至[!DNL Adobe Commerce as a Cloud Service]。 如需移轉程式的詳細資訊，請參閱[移轉概觀](../overview.md)。

下圖詳細說明使用大量資料移轉工具的架構和端對端資料流程。

![大量資料移轉工具架構圖，顯示PaaS至SaaS資料流程](../../assets/bulk-data-diagram.png){zoomable="yes"}

### 元件

| 元件 | 角色 |
| --------- | ---- |
| **大量資料移轉工具** | 系統整合商在移轉機器上執行的Docker式CLI，可從來源讀取結構描述和資料，將擷取的資料上傳至Adobe的移轉服務，並驅動狀態轉換，藉此協調整個管道。 |
| **Source執行個體（雲端或內部部署上的Commerce）** | 移轉來源。 此工具會透過REST和GraphQL API，以及透過SSH通道([!DNL Adobe Commerce on Cloud])或透過直接資料庫連線（內部部署）進行連線，以擷取資料。 |
| **Commerce資料移轉服務(CDMS) API** | Adobe管理的REST API可註冊移轉、協調狀態轉換，並提供安全端點來上傳擷取的資料。 移轉工具會使用您`.env`設定中的CDMS端點URL和IMS認證，連線至此API。 |
| **Commerce資料移轉服務(CDMS)背景工作** | Adobe管理的背景服務，可將擷取的資料載入目標例項中，並執行載入後完整性驗證。 |
| **[!DNL Adobe Commerce as a Cloud Service]** | Adobe Commerce的SaaS型版本以及您的移轉目標。 接收載入的資料，並公開在完整性驗證期間使用的目錄、即時搜尋和定價規則服務。 |

### 資料流程

資料會依下列順序移動元件：

1. 大量資料移轉工具會透過[!DNL Adobe Commerce on Cloud]的SSH通道或內部部署的直接資料庫連線，從來源執行個體讀取資料庫結構描述和資料。
1. 此工具會註冊移轉，並透過CDMS API上傳擷取的資料。
1. CDMS背景工作將資料載入目標[!DNL Adobe Commerce as a Cloud Service]租使用者。
1. [!DNL Adobe Commerce as a Cloud Service]會擷取載入的目錄資料並建置目錄索引。
1. Commerce資料移轉服務(CDMS)背景工作透過資料庫總和檢查碼比較、REST和GraphQL （跨下列服務）驗證載入的資料：

   - **目錄** (GraphQL) — 產品和類別資料。
   - **即時搜尋** (REST) — 搜尋索引正確。
   - **定價規則** (REST) — 價格和規則資料。

1. 工具會在整個過程中輪詢移轉狀態，並在完成時擷取最終的移轉報告。


## 參與生命週期

大量資料移轉工具的存取權是透過Commerce Deployed Engineering (CDE)專案獨家提供。 此工具無法公開存取。

典型的參與生命週期為：

1. **CDE Discovery** — 完成初始範圍設定呼叫、評估資料足跡和複雜性，並完成範圍設定問卷。
1. **交易簽章** — 已簽署商業合約，並已確認移轉範圍。 在此階段，您有權存取移轉工具。
1. **CDE Co-Innovation and Support** — 與Adobe合作，在您的環境中安裝此工具並執行測試移轉。
1. **上線** — 執行生產轉換移轉並完成資料完整性驗證。

## 工具分佈

此工具是作為CDE參與的一部分來分發。 您的Adobe代表提供工具套件，包括：

- 基於Docker的CLI和構建配置
- 包含所有必要環境變數檔案的`.example.env`設定範本
- 涵蓋工具架構、設定參考資料、自訂轉換和測試架構及疑難排解指南的完整技術檔案

有關詳細的設定和操作指示，請參閱工具散發套件中包含的檔案。

## 移轉指南

以下頁面示範從準備到執行的完整移轉生命週期。 如需完全瞭解移轉程式，請依照下列順序檢閱：

1. [客戶整備檢查清單](readiness-checklist.md) — 在您要求工具存取權之前，請先確認參與、移轉機器、來源及目標先決條件。
1. [驗證移轉服務存取權](cdms-access.md) — 取得工具的存取權後，針對Commerce資料移轉服務(CDMS) API驗證網路連線能力、IMS驗證及租使用者授權。
1. [執行大量資料移轉](migration-guide.md) — 設定工具、準備網路和執行個體，然後開始移轉。

如需完整設定參考資料、自訂轉換和測試架構，以及疑難排解指南，請參閱工具發佈套件中包含的檔案。
