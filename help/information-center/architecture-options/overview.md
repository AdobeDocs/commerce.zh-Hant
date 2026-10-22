---
title: Commerce架構概述
description: 瞭解Adobe Commerce產品模型，以及在何處可以找到詳細的架構選項、店面和API指引。
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T10:11:03.706Z'
TQID: 'https://experienceleague.adobe.com/V9Zp0eS8b45xYEay4EK91tPVnKhRdkWGDj4Vv7hB79U'
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
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
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
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: da3860b0-d637-47df-bef0-273751180266
    internal-label: Digital asset management
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%
---

# Commerce架構概覽

Adobe Commerce架構通常結合三個層：商務後端（[!DNL Adobe Commerce]或[!DNL Adobe Commerce Optimizer]）、店面以及一組連線的服務和整合。 本節將引導您瞭解產品模型，並指出在每個專用頁面中維護的詳細比較、圖表和API參考。

## 快速入門

| 章節 | 使用它可以 |
| ------- | --------- |
| [平台和服務](../portfolio/platform-and-services.md) | 瞭解每個Commerce產品是什麼 — Adobe Commerce、Commerce Foundation、Adobe Commerce Optimizer和Adobe Commerce as a Cloud Service。 |
| [選擇Commerce選項](../portfolio/choose-commerce-option.md) | 根據交易所有權、部署模型和銷售需求比較Commerce選項。 |
| [架構選項](../architecture-options/implementation-architectures.md) | 詳細比較所有四種支援的架構，包括系統圖表和參考連結。 |
| [店面](../storefronts/overview.md) | 瞭解店面選項，以及它們如何連線至每個架構。 |
| [API](../apis/commerce-apis.md) | 比較Commerce Foundation、Storefront Services和Commerce Optimizer所使用的API系列。 |
| Commerce的[AEM Assets整合](../aem-assets/aem-assets-integration.md) | 在任何Commerce或Optimizer架構中新增集中式數位資產管理。 |
| [移轉與採用](../migration-adoption/overview.md) | 規劃在架構之間移動，或分階段採用Adobe Commerce Optimizer。 |

## 術語快速參考

| 偏好的詞語 | 含義 | 避免使用作為目前的架構標籤 |
| --- | --- | --- |
| **Commerce Foundation** | 基本商務和異動功能 | 核心Commerce和PHP基礎層 |
| **店面服務** | 目錄服務、即時搜尋和產品推薦的店面導向API | 標籤限製為只有一個Commerce平台 |
| **Commerce Optimizer銷售服務** | 適用於目錄探索和銷售體驗的Optimizer API | Commerce Foundation API |
| **由Edge Delivery Services提供支援的Commerce店面** | 面向客戶的店面實作 | API系列 |

## 相關指引

- [實施架構](implementation-architectures.md)
- [參考架構](reference-architectures.md)
- [建立新店面](../implementation-guides/build-new-storefront.md)
