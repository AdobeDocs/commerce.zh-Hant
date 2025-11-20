---
title: 開始使用 [!DNL Catalog Service]
description: 瞭解如何存取 [!DNL Catalog Service] 以及與前端應用程式和協力廠商服務整合。
role: Admin, Developer
exl-id: ee178e67-519d-4283-8de8-2634ae1f347a
source-git-commit: ae672ed3f2693e2f14e8c7f379e59ef117a34fc3
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# 開始使用[!DNL Catalog Service]

[!DNL Catalog Service]啟用後，您就可以存取此服務，並使用它從您的Adobe Commerce執行個體擷取目錄資料，例如產品和類別資訊。 此服務是以GraphQL API的形式提供，您可以從Commerce Admin或從任何支援GraphQL查詢的前端應用程式中存取。

## 存取服務

[!DNL Catalog Service]可用作GraphQL API，您可從Commerce管理員或任何支援GraphQL查詢的前端應用程式中存取。 此服務同時適用於SaaS和PaaS環境。

僅[!BADGE 個PaaS]{type=Informative url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案(Adobe管理的PaaS基礎結構)和內部部署專案的Adobe Commerce 。"}

| 環境 | 端點 |
| ------------ | ----------: |
| **正在測試** | `https://catalog-service-sandbox.adobe.io/graphql` |
| **生產** | `https://catalog-service.adobe.io/graphql` |

僅[!BADGE SaaS]{type=Positive url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"}

| 環境 | 端點 |
| ----------- | --------:|
| 測試 | `https://na1-sandbox.api.commerce.adobe.com/{{tenant-id}}/graphql` |
| 生產（尚未提供） | `https://na1.api.commerce.adobe.com/{{tenant-id}}/graphql` |

SaaS端點的&#x200B;**URL結構**

```text
https://<region>-<environment>.api.commerce.adobe.com/<tenantId>/graphql
```

- `<region>`是部署執行個體的雲端區域。
- `<environment>`是環境型別，例如`sandbox`。 如果環境是生產環境，則會忽略此值。
- `<tenantId>`是Adobe Experience Cloud中貴組織特定執行個體的唯一識別碼。

如需有關使用目錄服務GraphQL API的詳細資訊，請參閱[Adobe Commerce開發人員](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)檔案中的&#x200B;*Adobe Commerce目錄服務指南*。

## 與Headless店面或協力廠商服務整合

若要與Headless店面整合，您必須更新店面設定以啟用店面與[!DNL Catalog Service]之間的通訊，以擷取產品和類別資料。

如果您在Edge Delivery Services上使用Adobe Commerce店面，請將目錄服務端點新增至店面設定。 如需詳細資訊，請參閱[Edge Delivery Services檔案](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/?lang=zh-Hant#storefront-configuration)。

如需其他整合，請參閱專案設定檔案，以取得有關如何設定服務與後端資料來源之間整合的詳細資訊。

### 防火牆設定

若要允許[!DNL Catalog Service]通過防火牆，請新增`commerce.adobe.io`至允許清單。

## 目錄服務和API網格

適用於Adobe Developer App Builder[的](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/)API Mesh可讓開發人員使用Adobe IO將私人或協力廠商API和其他介面與Adobe產品整合。

請參閱[[!DNL Catalog Service] 和API Mesh](mesh.md)主題，以取得安裝和設定詳細資料。

## 使用資料管理控制面板

使用[資料管理儀表板](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)監視[!DNL Catalog Service]與您的Adobe Commerce執行個體之間的資料同步。 控制面板提供資料傳輸流程的深入分析，包括資料匯出的狀態和同步產品的清單。