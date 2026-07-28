---
title: 驗證移轉服務存取權
description: 瞭解如何驗證Commerce資料移轉服務API的端對端存取權、確認網路可及性、IMS驗證和租使用者授權。
feature: Cloud
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案（Adobe管理的SaaS基礎結構）。"
role: Developer
level: Intermediate
autotag-review: '2026-07-22T19:18:53.554Z'
TQID: 'https://experienceleague.adobe.com/csDq2Bbha2IieqxsDDG0iS1IHhAJ02fD-cwd8KFIsSk'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2: id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 670b6214b28be93a16130552a226a8cadb487324
workflow-type: tm+mt
source-wordcount: 452
ht-degree: 1%

---

# 驗證移轉服務存取權

{{bulk-data-early-access}}

使用本指南來驗證從您的環境端對端存取Commerce Data Migration Service (CDMS) API。 成功的呼叫會同時驗證來自您的輸出IP （IP允許清單）、IMS驗證和租使用者授權的網路可達性。

完成[客戶整備檢查清單](readiness-checklist.md)中的所有專案之後，以及執行[移轉指南](migration-guide.md)中所述的移轉之前，請完成本指南。

## 先決條件

- 在[Adobe Developer Console](https://developer.adobe.com/console/)中建立的OAuth 2.0伺服器對伺服器認證（使用者端ID和使用者端密碼）。
- 您的IMS組織識別碼，格式為`<org>@AdobeOrg`。 組織必須擁有目標租使用者。
- 目標`tenantId`，22個字元的英數IMS租使用者ID。
- 送出輸出IP位址已提交給Adobe並由CDMS閘道加入允許清單。 如果您不確定IP位址或其狀態，請與Adobe團隊協調。
- [服務主機（依環境和區域](#service-hosts-by-environment-and-region)資料表）的區域特定服務主機。

## 產生IMS存取權杖

使用具有`client_credentials`授權的OAuth 2.0伺服器對伺服器認證產生存取權杖。 所有資料區域在此步驟中的IMS主機都相同。 只有每個區域的CDMS主機會變更。

```bash
curl -X POST "https://ims-na1.adobelogin.com/ims/token/v3" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -H "x-org-id:<your-org-id>@AdobeOrg" \
  -d "grant_type=client_credentials" \
  -d "client_id=<your-ims-client-id>" \
  -d "client_secret=<your-ims-client-secret>" \
  -d "scope=AdobeID,openid,read_organizations,additional_info.projectedProductContext,additional_info.roles,adobeio_api,read_client_secret,manage_client_secrets"
```

## 呼叫清單移轉API

以下請求會擷取租使用者的移轉清單，並需要上一步驟的存取權杖。 從[依環境和地區](#service-hosts-by-environment-and-region)區分的服務主機表格中，選取您所在地區的主機。 `-i`旗標會列印HTTP狀態行和回應標題，以便您確認結果。

```bash
curl -i "https://<host>/<tenantId>/v1/migrations" \
  -H "Authorization: Bearer <your IMS access token>"
```

## 解讀回應

| HTTP程式碼 | 含義 | 範例回應內文 |
| --- | --- | --- |
| 200 | 成功。 連線、驗證和租使用者授權全部通過。 回應本文包含租使用者的移轉清單。 | `{"migrations":[...]}` |
| 401 | 遺失或無效的持有人權杖，在到達服務前遭拒。 [重新產生權杖](#generate-an-ims-access-token)。 | 視情況而定（閘道產生） |
| 403 | 已驗證的使用者沒有此租使用者的移轉許可權。 | `{"error":"access_denied","message":"You do not have permission to access this tenant"}` |
| 500 | 內部伺服器錯誤。 | `{"error":{"message":"Internal Server Error","status":500}}` |

>[!NOTE]
>
>如果要求逾時或連線遭拒，且未傳回HTTP狀態，表示您的輸出IP可能並未加入允許清單，或您使用錯誤的主機。 確認下表中的區域主機和您的允許清單IP。

## 依環境和地區區分的服務主機

| 區域或環境 | 主機 |
| --- | --- |
| 沙箱或預先生產 | `https://na1-sandbox.api.commerce.adobe.com` |
| 北美 | `https://na1.api.commerce.adobe.com` |
| 歐洲 | `https://eu1.api.commerce.adobe.com` |
| 印度 | `https://in1.api.commerce.adobe.com` |
| UK | `https://uk1.api.commerce.adobe.com` |
| 澳洲和紐西蘭 | `https://au1.api.commerce.adobe.com` |

## 後續步驟

在您確認存取權後，請繼續參閱[移轉指南](migration-guide.md)以開始環境設定和移轉執行。
