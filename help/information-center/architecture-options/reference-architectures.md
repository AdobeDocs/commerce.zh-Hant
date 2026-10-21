---
title: 參考架構
description: 瞭解常見Adobe Commerce實作（例如店面、服務和目錄同步管道）的參考架構模式。
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T11:42:09.021Z'
TQID: 'https://experienceleague.adobe.com/GVbGyRZz8llMWcUykcXXZwWnTaAomHVCTcV3ft49IEc'
product_v2:
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 8dc0e58b-adf0-51bb-8db5-bb36e3e656fb
    internal-label: Inventory
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
    internal-label: Commerce ecosystem
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
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%
---

# 參考架構

下列檔案提供跨不同部署模式和使用案例的Adobe Commerce平台和服務參考架構模式。

- [Adobe Commerce as a Cloud Service架構](/help/cloud-service/overview.md#architecture)
- [Adobe Commerce企業參考架構](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/architecture/enterprise-blueprint){target="_blank"}
- [Adobe Commerce店面架構](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/architecture/){target="_blank"}
- [雲端基礎結構架構上的Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/architecture/cloud-architecture){target="_blank"}

## 由Edge Delivery Services提供支援的店面

在Adobe Commerce展示板上建立的店面，使用插入式元件和內容區塊，連線到Adobe Commerce或[!DNL Adobe Commerce Optimizer]作為後端。 檢視[Adobe Commerce店面總覽](https://experienceleague.adobe.com/en/tools/commerce-storefront/)。

- [Adobe Commerce店面架構](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/architecture/)

## 目錄同步管道

用於在Adobe Commerce與Adobe Commerce服務（Commerce Optimizer、即時搜尋、目錄服務、產品建議和其他連線的[Commerce服務](../../landing/home.md)）之間保持目錄、價格和存貨資料同步的資料流程。

- 如需Adobe Commerce as a Cloud Service、雲端基礎結構或內部部署的相關資訊，請參閱[使用SaaS資料匯出同步資料](/help/data-export/sync-overview.md)

- 對於雲端基礎結構或使用Adobe Commerce Optimizer Connector設定的內部部署上的Adobe Commerce，請參閱[聯結器同步管道](/help/aco-connector/connector-sync-pipeline.md)。


## 相關指引

- [實施架構](implementation-architectures.md)
