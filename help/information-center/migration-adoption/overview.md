---
title: 移轉與採用
description: 瞭解採用Adobe Commerce Optimizer、將現有店面現代化或完全移轉至Adobe Commerce as a Cloud Service的途徑。
role: Admin, Developer, Leader
feature: Storefront, Integration, Configuration
recommendations: noCatalog
TQID: 'https://experienceleague.adobe.com/2iEJ6fA-wLr18bi9C8l-w3srx1AWlAtiGt1cG9RPv0Q'
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
  - id: 1783ae9f-7157-5aeb-a915-91e260301e46
    internal-label: Routes
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
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
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 4c3c267873a68560a885c6376cd1137a7503710a
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%
---

# 移轉與採用

採用不需要單一、一次性的平台變更。 根據您的直接目標是店面現代化、銷售改進、後端現代化，還是完全移至「受管理的軟體即服務」(SaaS)來選擇路線。

## 採用路徑

### 最新化現有的Adobe Commerce部署

- 將現有的Commerce Foundation保留為交易式後端。
- 採用由[!DNL Edge Delivery Services]提供支援的Commerce店面。
- 使用Storefront Services、App Builder、API Mesh和選用的AEM Assets整合。

### 使用Commerce Optimizer作為Bridge

- 使用[!DNL Adobe Commerce Optimizer Connector]連線[!DNL Adobe Commerce]雲端或內部部署。
- 採用銷售服務、探索、建議和Edge Delivery Services店面。
- 保留[!DNL Adobe Commerce]作為產品、價格、目錄結構、購物車、結帳、客戶和訂單的主要記錄系統。
- 使用此架構作為向[!DNL Adobe Commerce as a Cloud Service]的可能轉換。

### 完全移轉至Adobe Commerce as a Cloud Service

- 評估目前的應用程式、自訂、整合、店面和資料。
- 使用SaaS相容的擴充性模式將自訂內容現代化。
- 重建或調整店面與整合。
- 移轉及驗證目錄、客戶、訂單、設定和支援的自訂資料。
- 測試、切換及操作新的SaaS環境。

### 採用獨立式Adobe Commerce Optimizer

- 從協力廠商Commerce平台、PIM、ERP或其他來源擷取目錄和價格資料。
- 使用[!DNL Adobe Commerce Optimizer]銷售服務進行目錄擷取、探索、建議和銷售。
- 使用由[!DNL Edge Delivery Services]提供支援的Commerce店面。
- 將購物車、結帳、客戶、訂單、付款、稅捐、送貨和履行保留在連線的協力廠商系統中。

## 建議的順序

1. 評估目前狀態並定義系統擁有權。
1. 建立API優先整合界限。
1. 打造最新的店面與體驗層。
1. 同時採用銷售服務和AEM Assets。
1. 必要時移轉Commerce Foundation。
1. 驗證、切換、監控和最佳化。

## 相關指引

- [選擇Commerce選項](../portfolio/choose-commerce-option.md)
- [架構選項](../architecture-options/overview.md)
- [更新現有的店面](../implementation-guides/modernize-storefront.md)
- [啟用Adobe Commerce Optimizer](../implementation-guides/enable-aco.md)
