---
title: 檢視和管理記錄檔
description: 瞭解在何處尋找及管理Commerce的AEM Assets整合記錄。
feature: CMS, Media, Integration
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案(Adobe管理的PaaS基礎結構)和內部部署專案的Adobe Commerce 。"
exl-id: 9c6c8694-6ded-4cc8-a3ab-d1dfb50e3583
source-git-commit: 202eca18c71a211cbbf1d210be00543049170c3f
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# 檢視和管理記錄檔

AEM Assets整合在您的Commerce執行個體中提供下列記錄檔：

- `/var/log/aem-assets-integration.log`
- `/var/log/aem-assets-integration-errors.log`

請要求您的系統管理員檢查這些記錄的記錄檔輪換排程，以防止它們變得太大。 在某些環境中，記錄會自動輪換；在其他環境中，您必須手動設定記錄輪換。  如需詳細資訊，請參閱下列主題：

- 若為Adobe Commerce內部部署安裝，請要求系統管理員設定[記錄輪換](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html?lang=zh-Hant#server-settings)。
- 如需雲端基礎結構專案上的Adobe Commerce，請參閱[檢視及管理記錄檔](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html?lang=zh-Hant)。
