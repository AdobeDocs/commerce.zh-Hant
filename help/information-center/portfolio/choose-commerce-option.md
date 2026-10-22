---
title: 選擇Commerce選項
description: 根據交易所有權、部署模式和銷售需求比較Adobe Commerce架構。
role: Admin, Developer, Leader, User
feature: Storefront, Integration, Configuration
recommendations: noCatalog
TQID: 'https://experienceleague.adobe.com/5y0IU5nji50eqfFNQHbVDV-R81Mx0I8v5Y0a6nccL-w'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 6388cf7b-8a81-5248-a1e4-7bb57bbe250f
    internal-label: Install
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 4c3c267873a68560a885c6376cd1137a7503710a
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%
---

# 選擇Commerce選項

首先，識別擁有購物車、結帳、訂單和其他交易之系統。 然後選擇適合該後端的銷售路徑。

## 引導您決策的問題

使用下列問題來識別要評估的選項。 考慮您現有的商務後端、想要保留多少基礎架構責任，以及您是否需改善產品探索和銷售。 Adobe Commerce Optimizer提供探索和銷售功能。 它不會取代處理交易的後端。

1. **您要Adobe以軟體即服務(SaaS)方式管理Commerce平台嗎？**
   - 是：評估Adobe Commerce as a Cloud Service。
   - 否：如果您需要Adobe Commerce且想要保留對雲端或內部部署基礎結構的控制權，請在雲端或內部部署上評估Adobe Commerce。
1. **您是否需要Adobe Commerce來處理購物車、結帳、訂購和其他交易？**
   - 是：在雲端或內部部署，或Adobe Commerce as a Cloud Service上評估Adobe Commerce。 這些選項會使用Commerce Foundation做為交易式後端。
   - 否：保留您現有的或協力廠商交易後端。 如果您還需要Adobe探索和銷售功能，請評估獨立的Adobe Commerce Optimizer。
1. **您是否要使用Adobe Commerce Optimizer來改進現有協力廠商商務後端的產品探索和銷售？**
   - 是：評估獨立的Adobe Commerce Optimizer，同時保留交易的第三方後端。
1. **您是否已在雲端或內部部署執行Adobe Commerce，而且想要更強大的探索和銷售？**
   - 是：評估Adobe Commerce Optimizer聯結器，以便在Adobe Commerce繼續處理交易時同步目錄和定價資料。

使用下表的比較表，將您的答案與起點進行比對。 如需詳細的系統圖表，請參閱[架構選項](../architecture-options/overview.md)。

## 比較Commerce選項

| 您的需求 | 建議的起點 | 擁有交易的系統 | 銷售與探索 |
| --- | --- | --- | --- |
| Adobe以SaaS管理Commerce平台。 | [Adobe Commerce as a Cloud Service](/help/cloud-service/overview.md) | Adobe Commerce as a Cloud Service基礎 | 使用為Adobe Commerce as a Cloud Service布建的Commerce服務。 如需Adobe Commerce Optimizer整合的可用性，請參閱此表格下方的注意事項。 |
| 需要Adobe Commerce，並且想要保留對雲端或內部部署基礎建設的控制。 | 雲端或內部部署上的[Adobe Commerce](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/start/guide-overview) | Adobe Commerce Foundation | 視需要使用支援的Commerce服務。 |
| 在雲端上的Adobe Commerce上或內部部署，並且想要採用Adobe Commerce Optimizer來進行探索和銷售。 | 具有[Adobe Commerce Optimizer Connector](/help/aco-connector/overview.md)的Adobe Commerce | Adobe Commerce仍然是交易的記錄系統。 | 聯結器會將目錄和定價資料同步至Adobe Commerce Optimizer，以提供探索和銷售體驗。 |
| 擁有協力廠商商業後端，且想要Adobe Commerce Optimizer探索與銷售功能而不取代該後端。 | 獨立[Adobe Commerce Optimizer](/help/optimizer/overview.md) | 您的協力廠商商務後端 | 將目錄和價格資料傳送至Adobe Commerce Optimizer。 透過API Mesh、App Builder或直接整合，將購物車、結帳和其他交易式作業與後端整合。 |

>[!NOTE]
>
>Adobe Commerce as a Cloud Service與Adobe Commerce Optimizer的整合已列入Commerce藍圖。 如果您同時需要這兩種平台，請立即規劃使用它們作為個別的架構選項。 請連絡您的Adobe客戶經理，以進一步瞭解整合的時間表。

## 相關指引

- [平台和服務](platform-and-services.md)
- [架構選項](../architecture-options/overview.md)
- [開始使用](../get-started/get-started-by-role.md)
