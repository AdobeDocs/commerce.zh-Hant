---
title: 開始使用 [!DNL Catalog Service]
description: 瞭解如何存取 [!DNL Catalog Service] 以及與前端應用程式和協力廠商服務整合。
role: Admin, Developer
exl-id: ee178e67-519d-4283-8de8-2634ae1f347a
source-git-commit: 50d8937c903efb1c56ec86e6bc4b947d2f198d49
workflow-type: tm+mt
source-wordcount: '586'
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

適用於Adobe Developer App Builder[&#128279;](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/)的API Mesh可讓開發人員使用Adobe IO將私人或協力廠商API和其他介面與Adobe產品整合。

請參閱[[!DNL Catalog Service] 和API Mesh](mesh.md)主題，以取得安裝和設定詳細資料。

## 監視及疑難排解資料匯出

Commerce管理員提供的工具可監控從Commerce匯出至連線服務的資料，並對其進行疑難排解：

- **[資料管理儀表板](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)** — 監視[!DNL Catalog Service]與您的Adobe Commerce執行個體之間的資料同步處理。 儀表板會顯示整體同步狀態，並列出所有同步的產品。

- **[資料摘要同步狀態頁面](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)** — 追蹤所有資料摘要的匯出狀態，以確保資料的一致性。 此頁面會針對匯出程式期間發生的問題提供警示，以便您快速解決問題。 「成功」狀態表示資料已匯出，當資料同步程式完成時，可在連線的Commerce服務中使用。

>[!NOTE]
>
>如果雲端或內部部署的Commerce的Commerce Admin中沒有資料摘要同步狀態頁面，請依照[擴充功能安裝指示](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status#install-the-extension)加以啟用。
