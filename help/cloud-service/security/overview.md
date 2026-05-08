---
title: 安全性概覽
description: 瞭解Adobe Commerce as a Cloud Service的安全性功能。
role: Admin, Developer, Leader
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案（Adobe管理的SaaS基礎結構）。"
source-git-commit: feb48068137c6a63e6594167fe969c3aa4b044c4
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---


# 安全性概覽

[!DNL Adobe Commerce as a Cloud Service]以安全性為核心，提供現代化的SaaS原生商務平台，可為各種規模的企業提供企業級保護、營運復原能力及安心功能。

與傳統的PaaS模型不同，SaaS模型消除了手動修補、基礎架構維護和升級週期的負擔。 安全性內嵌於平台的每個層級 — 從Adobe管理的基礎結構和自動化部署管道，到透過[!DNL Adobe IMS]的識別與存取管理。

[!DNL Adobe Commerce as a Cloud Service]採用Adobe的全球安全與法規遵循架構，確保符合ISO 27001、SOC 2和GDPR等業界標準。 客戶可受益於[共同責任模式](./shared-responsibility.md)，該模式清楚說明Adobe在保護平台安全方面的角色，以及客戶在管理資料和存取權方面的角色。

透過內建的保護功能，例如Web應用程式防火牆(WAF)、減少DDoS、安全布建及持續性弱點掃描，[!DNL Adobe Commerce as a Cloud Service]可讓企業更快創新，而不會影響安全性。

本檔案概述[!DNL Adobe Commerce as a Cloud Service]的安全性架構、運作保障和法規遵循狀態，讓客戶能夠做出明智的決策，並放心地擴展其數位商業作業。

## 內容傳遞網路(CDN)與網頁應用程式防火牆(WAF)

### 店面CDN

商家可選擇部署Adobe管理的CDN，或購買自己的CDN解決方案，以保護其Commerce支援的店面。

>[!IMPORTANT]
>
>如果客戶選擇部署Adobe管理的CDN，將無法設定CDN規則。 自訂快取規則或WAF規則可由客戶在自備CDN時設定，以保護其店面。

### [!DNL API Mesh for Adobe Developer App Builder] CDN

[!DNL API Mesh]的CDN層會終止TLS、以Worker身分執行GraphQL閘道、提供全域邊緣快取和自動DDoS/WAF，並將`edge‑graph.adobe.io`/`edge‑sandbox‑graph.adobe.io`公開為公用網狀端點；客戶可以在前端新增自己的CDN，但[!DNL API Mesh]的CDN是由Adobe修正和管理的，而且客戶無法設定自己的WAF規則。

如需[!DNL API Mesh]安全性功能的詳細資訊，請參閱[API Mesh檔案](https://developer.adobe.com/graphql-mesh-gateway/mesh/security/){target="_blank"}。

### 後端CDN

內建的CDN可保護[!DNL Adobe Commerce as a Cloud Service]。

由於[!DNL Adobe Commerce as a Cloud Service]架構，當商家在複合儲存格（例如`na1`、`eu1`、`au1`或其他地理區域）中布建執行個體時，會公開三個公用表面：

| 表面 | 範例URL模式 |
| --- | --- |
| 管理員UI | `https://<region>.admin.commerce.adobe.com/<tenant-id>/admin/` |
| REST API | `https://<region>.api.commerce.adobe.com/<tenant-id>/<endpoint>` |
| GRAPHQL API | `https://na1.api.commerce.adobe.com/<tenant_id>/graphql/` |

[!DNL Adobe Commerce as a Cloud Service]使用合併的WAF和CDN：

- **WAF** — 所有[!DNL Adobe Commerce as a Cloud Service]公用介面的Web應用程式防火牆保護。
- **CDN** — 靜態資產的Edge快取和可快取的GraphQL回應。

WAF和CDN由[!DNL Adobe Commerce as a Cloud Service]平台管理，客戶無法設定。

### DDoS保護

內建的CDN和WAF提供網路層和HTTP層DDoS保護。 [!DNL Adobe Commerce as a Cloud Service]不會直接向商家公開這些WAF或DDoS記錄。

## 資料儲存與加密

如果資料儲存在[!DNL App Builder]中，則商家可以參考[!DNL App Builder] [儲存選項](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/)。 [!DNL App Builder]會強制租使用者隔離，而且這些服務中儲存的資料存取權被限製為執行動作的執行階段名稱空間。 儲存區中沒有資料加密。

使用[!DNL API Mesh]時，密碼應儲存在網狀組態的`secrets.yaml`檔案中。 [!DNL API Mesh]使用AES-256加密([https://developer.adobe.com/graphql-mesh-gateway/mesh/advanced/secrets/](https://developer.adobe.com/graphql-mesh-gateway/mesh/advanced/secrets/))來加密這些秘密。

儲存在[!DNL Adobe Commerce as a Cloud Service]中的任何資料都會使用AES 256位元加密進行靜態加密，所有資料都會使用TLS 1.2或更新版本的傳輸資料透過HTTPS進行加密。
