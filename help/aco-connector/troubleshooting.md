---
title: 疑難排解 [!DNL Adobe Commerce Optimizer Connector]
description: 瞭解如何疑難排解 [!DNL Adobe Commerce] PaaS整合的 [!DNL Adobe Commerce Optimizer Connector] 認證、目錄同步和範圍匯出問題。
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案（Adobe管理的PaaS基礎結構）和內部部署專案的Adobe Commerce 。"
autotag-review: '2026-06-09T19:00:00.000Z'
TQID: 'https://experienceleague.adobe.com/ei86QuJ3nQ2d-6NRoAeJslgDxjGlZRejD-Nx-6SAVdc'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 331
ht-degree: 0%

---

# 疑難排解[!DNL Adobe Commerce Optimizer Connector]

使用本指南來診斷及解決初始設定、目錄摘要同步化及範圍匯出設定期間[!DNL Adobe Commerce Optimizer Connector]的常見問題。 以下各節涵蓋認證和租使用者驗證、資料同步處理失敗以及相關的[!DNL SaaS Data Export]診斷。

## 認證或租使用者驗證失敗

如果`aco:config:init`在認證驗證期間失敗：

- 執行`bin/magento aco:config:show` [!DNL Adobe Commerce] CLI命令以驗證儲存的值。
- 確認租使用者ID屬於用來取得認證的IMS組織。
- 確認OAuth使用者端具有[!DNL Adobe Commerce Optimizer]擷取服務的必要範圍（請參閱[取得IMS認證](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials)）。

## 資料未同步

**檢查專案層級錯誤詳細資料：**

請參閱[確認資料同步正在運作](./data-sync-manage.md#verify-that-the-data-sync-is-working)，以瞭解在Commerce管理中開啟&#x200B;**[!UICONTROL Data Feed Sync Status]**&#x200B;的步驟。 選取失敗的摘要以檢視每個專案的錯誤詳細資料。

錯誤處理的要點：

- 未重試&#x200B;**400個錯誤**。 檢查裝載中是否有格式錯誤或遺漏的必填欄位。 如需預期的格式，請參閱聯結器摘要[&#128279;](reference/field-mapping.md)的欄位對應。
- **5xx錯誤**&#x200B;由`*_resend_failed_items` cron工作自動重試（每5分鐘執行一次）。

**檢查範圍組態：**

如果問題僅影響特定目錄來源（商店檢視代碼）或價格簿，請檢查對應的網站或商店檢視是否已停用同步。 請參閱[自訂Commerce範圍匯出設定](./get-started.md#customize-the-commerce-scopes-export-configuration)。

**解析時：**

聯結器摘要在&#x200B;**[!UICONTROL Data Feed Sync Status]**&#x200B;中顯示成功狀態，而預期的產品、價格和屬性會顯示在[!DNL Commerce Optimizer]的&#x200B;**[!UICONTROL Data Sync]**&#x200B;頁面上。

## 設定錯誤和結果解釋

如需因設定錯誤或誤解同步處理結果所造成的特定行為目錄，例如遺漏產品、不正確的價格或範圍層級的資料差距，請參閱[疑難排解案例](troubleshooting/troubleshooting-scenarios.md)。

## [!DNL SaaS Data Export]診斷

如需底層[!DNL SaaS Data Export]診斷（包括記錄位置與摘要重新同步命令），請參閱[[!DNL SaaS Data Export] 疑難排解指南](https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/troubleshooting/logging){target="_blank"}。
