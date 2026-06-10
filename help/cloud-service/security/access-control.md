---
title: 識別與存取管理
description: 瞭解Adobe Commerce as a Cloud Service的身分和存取管理功能。
role: Admin, Developer, Leader
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案（Adobe管理的SaaS基礎結構）。"
TQID: 'https://experienceleague.adobe.com/lbI3nsLtafel6GtquXnkZmXD2Z3b-rRGPOyr8EqzrjE'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: ef32511703a96b5f4db32d54229e9a7cbe961f12
workflow-type: tm+mt
source-wordcount: 419
ht-degree: 0%

---


# 身分和存取管理

[!DNL Adobe Commerce as a Cloud Service]利用Adobe的企業級身分基礎結構，確保所有環境都具備安全、可擴充和集中的存取控制。 [!DNL Adobe Commerce as a Cloud Service]中的識別與存取管理(IAM)旨在簡化使用者布建、強制最低許可權存取，以及支援符合全域安全性標準。

- **[!DNL Adobe Identity Management Services (IMS)]**： [!DNL Adobe Commerce as a Cloud Service]使用[Adobe Identity Management Services (IMS)](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/start/admin/ims/adobe-ims-integration-overview)驗證使用者和管理權益。 這包括支援同盟識別服務提供者和[角色型存取控制](../user-management.md)。

- **Admin Console控管**：管理員透過[!DNL Adobe Admin Console]管理對店面和後端的存取。 許可權可限定於特定功能和角色，以確保最低許可權的存取權。

## Adobe Identity Management Services (IMS)

[!DNL Adobe Commerce as a Cloud Service]使用[!DNL Adobe Identity Management Services (IMS)]驗證使用者並管理整個平台的權益。 IMS提供：

- **同盟身分支援**：使用SAML或OIDC與企業身分服務供應商（例如Azure AD和Okta）整合。
- **單一登入(SSO)**：順暢存取[!DNL Adobe Commerce]和其他[!DNL Adobe Experience Cloud]產品。
- **多重驗證(MFA)**：已在組織層級強制執行，以提供增強式安全性。
- **全域備援**：身分資料儲存在多區域、負載平衡的雲端基礎結構中。

## Admin Console存取控制

[!DNL Adobe Admin Console]是管理[!DNL Adobe Commerce as a Cloud Service]使用者存取權的中心樞紐：

- **角色型存取控制(RBAC)**：根據使用者的角色（例如開發人員、管理員和分析人員）指派精細許可權給使用者。
- **產品設定檔**：為不同的環境（例如測試和生產）定義存取範圍。
- **委派管理**：系統管理員和產品管理員可以管理使用者存取權而無需IT人員介入。

如需詳細資訊，請參閱[使用者管理](https://experienceleague.adobe.com/zh-hant/docs/commerce/cloud-service/user-management)。

## API驗證和整合安全性

[!DNL Adobe Commerce as a Cloud Service]的REST API驗證已透過Adobe的[!DNL Adobe Identity Management Services (IMS)]使用標準化的OAuth 2通訊協定處理。 此驗證系統支援互動式使用者工作流程與自動化伺服器對伺服器整合，確保不同使用案例的安全與適當存取。

>[!NOTE]
>
>SaaS環境中不支援[!DNL Adobe Commerce]的PaaS版本中的管理及整合權杖產生方法。 而是必須透過OAuth驗證取得IMS管理權杖。

- **OAuth 2.0支援**：整合和協力廠商服務的安全權杖式驗證。
- **範圍的API存取**：限制API存取特定資源與作業。
- **稽核記錄**：追蹤驗證事件和存取變更，以進行規範及疑難排解。

如需詳細資訊，請參閱[REST驗證](https://developer.adobe.com/commerce/webapi/rest/authentication/)。
