---
title: 開始使用 [!DNL Catalog Service]
description: 瞭解如何存取 [!DNL Catalog Service] 以及與前端應用程式和協力廠商服務整合。
role: Admin, Developer
exl-id: ee178e67-519d-4283-8de8-2634ae1f347a
TQID: https://experienceleague.adobe.com/KBdWesEoKJu-qWsY-Ny1Om-msUkyUPfUTQWftEqSg1g
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: c32adafa-ed01-4b31-997e-2413013911b0id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2: id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: e1e0219c-f879-479f-8427-888ed2a6e9c2id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 10a91a91337778648e99078bcbf0c9ef25a49f86
workflow-type: tm+mt
source-wordcount: 437
ht-degree: 0%

---

# 開始使用[!DNL Catalog Service]

[!DNL Catalog Service]啟用後，您就可以存取此服務，並使用它從您的Adobe Commerce執行個體擷取目錄資料，例如產品和類別資訊。 此服務是以GraphQL API的形式提供，您可以從Commerce Admin或從任何支援GraphQL查詢的前端應用程式中存取。

{{aco-merchandising-services}}

## 存取服務

[!DNL Catalog Service]可用作GraphQL API，您可從Commerce管理員或任何支援GraphQL查詢的前端應用程式中存取。 此服務同時適用於SaaS和PaaS環境。

僅[!BADGE 個PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案（Adobe管理的PaaS基礎結構）和內部部署專案的Adobe Commerce 。"}

| 環境 | 端點 |
| ------------ | ----------: |
| **正在測試** | `https://catalog-service-sandbox.adobe.io/graphql` |
| **生產** | `https://catalog-service.adobe.io/graphql` |

僅[!BADGE SaaS]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案（Adobe管理的SaaS基礎結構）。"}

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

如需有關使用目錄服務GraphQL API的詳細資訊，請參閱&#x200B;*Adobe Commerce開發人員*&#x200B;檔案中的[Adobe Commerce目錄服務指南](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)。

## 與Headless店面或協力廠商服務整合

若要與Headless店面整合，您必須更新店面設定以啟用店面與[!DNL Catalog Service]之間的通訊，以擷取產品和類別資料。

如果您在Edge Delivery Services上使用Adobe Commerce店面，請將目錄服務端點新增至店面設定。 如需詳細資訊，請參閱[Edge Delivery Services檔案](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/#storefront-configuration)。

如需其他整合，請參閱專案設定檔案，以取得有關如何設定服務與後端資料來源之間整合的詳細資訊。

### 防火牆設定

若要允許[!DNL Catalog Service]通過防火牆，請新增`commerce.adobe.io`至允許清單。

## 目錄服務和API網格

適用於Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/)的[API Mesh可讓開發人員使用Adobe IO將私人或協力廠商API和其他介面與Adobe產品整合。

請參閱[[!DNL Catalog Service] 和API Mesh](mesh.md)主題，以取得安裝和設定詳細資料。

## 監視及疑難排解資料匯出

{{$include /help/_includes/data-export/verify-commerce-service-data-sync.md}}

必要時使用[Commerce CLI](../data-export/data-export-cli-commands.md)手動重新同步摘要。 如需重新同步選項及其他疑難排解步驟，請參閱&#x200B;_SaaS Data Export Guide_&#x200B;中的[Manage synchronization](../data-export/data-sync-manage.md)。

{{install-data-sync-feed-status}}
