---
title: '[!DNL SaaS Data Export Guide]'
description: 瞭解如何將 [!DNL data export] 擴充功能用於Adobe Commerce SaaS服務，以在Adobe Commerce與連線的Commerce服務之間同步資料。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 8a0067ba-90a4-48a6-8276-208d09abe6fc
TQID: https://experienceleague.adobe.com/OHE1GBUEd8hHFPwFlO9fJa3Y0wK2xZ0HOYnwUn0-DSk
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: c1256247-af4b-46d8-9dca-0c654ecfa157id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 402
ht-degree: 0%

---

# [!DNL SaaS Data Export] 指南

[!DNL SaaS data export]會在Adobe Commerce執行個體和連線的Commerce Services之間同步資料。 當您將Live Search、Product Recommendations、目錄服務或[!DNL Adobe Commerce Optimizer Connector]新增至Adobe Commerce安裝時，[!DNL Data Export]擴充功能會自動安裝。

>[!NOTE]
>
>如果您安裝[!DNL Adobe Commerce Optimizer Connector]，相同的[!DNL Data Export]擴充功能會從[!DNL Adobe Commerce]收集目錄和定價摘要。 聯結器接著會使用可撰寫目錄資料模型(CCDM)將這些摘要對應並提交給[!DNL Adobe Commerce Optimizer]。 如需設定和架構，請參閱[[!DNL Adobe Commerce Optimizer Connector] 概觀](../aco-connector/overview.md)，如需匯出後的同步行為，請參閱[聯結器同步管道](../aco-connector/connector-sync-pipeline.md)。

SaaS資料匯出會收集並匯出各種型別的資料，稱為&#x200B;_摘要_，用於彙總特定型別的資訊。 視安裝的Commerce服務而定，SaaS資料匯出摘要包含：

- **目錄實體摘要**&#x200B;彙總產品資料。 資料包括產品、產品屬性、產品價格、產品變化、類別、類別許可權和產品許可權。
- **範圍摘要**&#x200B;會彙總客戶群組、網站、商店和商店檢視的資料。
- **銷售訂單摘要**&#x200B;會彙總訂單資料，包括其相關實體，例如商業發票、出貨、銷退折讓單等。
- **多Source庫存摘要**&#x200B;會彙總有關庫存狀態專案的資料。

SaaS資料匯出會以PHP擴充功能提供，支援自動和手動同步處理：

- **自動同步處理** — 當您連線Commerce服務時，在初始完整同步處理之後，cron工作會使用部分同步處理以及自動重試失敗的專案，讓連線的服務保持最新狀態，而不需要管理員使用者或系統整合員採取任何動作。

- **手動同步** — 從Commerce Admin或[Commerce CLI](data-export-cli-commands.md)執行完整的重新同步或重新同步選取的摘要。

- **監視** — 從Commerce管理員的[!UICONTROL Data Feed Sync Status]頁面和資料管理儀表板追蹤摘要健康狀態、狀態和傳遞。 請參閱[管理同步處理](data-sync-manage.md)，以取得驗證和重新同步處理步驟。

如需同步化行為、模式和匯出流程圖，請參閱[同步化的運作方式](sync-overview.md)。

SaaS資料匯出還提供工具，用於規劃和疑難排解同步化程式：

- **排程與效能** — 預估同步處理時間，以排程處理並避免網站中斷，以及自訂匯出處理以提升效能。 請參閱[預估資料量和傳輸時間](estimate-data-volume-sync-time.md)和[改善資料匯出效能](customize-export-processing.md)。

- **追蹤和疑難排解** — 使用資料匯出和saas-export記錄檔來檢閱同步處理狀態和摘要裝載。 檢視[檢閱記錄檔及疑難排解](troubleshooting/logging.md)。

>[!MORELIKETHIS]
>
> - [延伸與自訂SaaS資料匯出摘要](extensibility-and-customizations.md) — 新增或修改摘要資料。
> - [疑難排解狀況](troubleshooting/troubleshooting-scenarios.md) — 診斷設定錯誤和意外的同步處理結果。
> - [發行說明](release-notes.md) — 擴充功能更新和已知問題。
