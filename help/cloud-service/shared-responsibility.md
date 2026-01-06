---
title: 共擔責任
description: 瞭解您 [!DNL Adobe Commerce as a Cloud Service] 專案中各參與者的安全性責任。
feature: Cloud, Security
role: Admin, Architect, Leader
level: Intermediate
exl-id: 424fe5cd-5d54-425d-97ce-024476d18dde
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"
source-git-commit: 1ce3b6b6b94b1b4e94c0d34c081dec2884d7f0f8
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# 共擔責任安全性與營運模式

[!DNL Adobe Commerce as a Cloud Service]是隨選服務，需仰賴共擔責任安全性與運作模型。 Adobe和客戶共同承擔這些責任，各方在保護和運作Adobe Commerce應用程式方面各有各的責任。

>[!BEGINSHADEBOX]

下列摘要表使用RACI模型來顯示Adobe和客戶之間共用的安全性責任。

**R** — 負責
**A** — 負責
**C** — 已諮詢
**I** — 已通知

>[!ENDSHADEBOX]

| 任務 | Adobe | 客戶 |
| --- | --- | --- |
| 套用Adobe Commerce基礎結構修補程式 | RA | |
| 將修補程式套用至支援服務（例如Nginx或MySQL） | RA | |
| 定義後端來源WAF規則 | RA | |
| 定義後端CDN WAF規則 | RA | |
| 部署後端平台WAF規則 | RA | |
| 部署後端CDN WAF規則 | RA | |
| 修正[!DNL Adobe Commerce as a Cloud Service]中的核心錯誤 | RA | I |
| 正在釋放[!DNL Adobe Commerce as a Cloud Service]個基礎結構修補程式 | RA | |
| 擴充（基礎架構） | RA | |
| 縮放（核心應用程式） | RA | |
| 整合外部應用程式 | | RA |
| 安裝App Builder應用程式 | | RA |
| 測試所有App Builder應用程式的效能 | | RA |
| 自訂App Builder應用程式的主題設定和設計 | | RA |
| 設定後端DNS | RA | I |
| 入門後端CDN | RA | I |
| 支援後端CDN | RA | I |
| 取得後端DNS提供者 | RA | |
| 布建生產和沙箱環境 | A | R |
| 在雲端基礎結構上存取Dynamics for Adobe Commerce | R | C |
| 解決後端客戶的安全問題 | RA | I |
| 解決後端CDN安全性問題 | RA | |
| 協助Adobe進行安全性研究（掃描/稽核） | RA | |
| 執行PCI ASV掃描 | RA | I |
| 正在修復Adobe Commerce基礎結構PCI掃描 | R | |
| 管理作業系統和平台機密 | RA | |
| 監控後端安全性記錄 | RA | |
| 控制客戶支援與存取 | A | R |
| Adobe DR計畫及備份與還原的年度測試和檔案 | RA | |
| 災難回覆計畫的年度測試與檔案 | RA | |
| 偵錯和問題隔離 | R | R |
| 及時支援偵錯和問題隔離流程 | R | R |
| 將更新和修補程式發佈至Adobe Commerce核心 | RA | I |
| 安裝Adobe Commerce核心的更新和修補程式 | RA | I |
| 核心Adobe Commerce應用程式品質 | RA | |
