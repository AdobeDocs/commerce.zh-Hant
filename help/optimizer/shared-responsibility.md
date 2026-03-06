---
title: 共擔責任
description: 瞭解您 [!DNL Adobe Commerce Optimizer] 專案中各參與者的安全性責任。
role: Admin, Architect, Leader
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 專案(Adobe管理的SaaS基礎結構)。"
exl-id: 9e09790f-832d-43ab-b2df-6389ad52b43d
source-git-commit: c7c21df464685783b5fae1c99d60ca91e0c334d2
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# 共擔責任安全性與營運模式

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
| 將修補程式套用至支援服務 | RA | |
| 定義後端來源WAF規則 | RA | |
| 定義後端CDN WAF規則 | RA | |
| 部署後端平台WAF規則 | RA | |
| 部署後端CDN WAF規則 | RA | |
| 修正[!DNL Adobe Commerce Optimizer]中的錯誤 | RA | I |
| 正在釋放[!DNL Adobe Commerce Optimizer]基礎結構修補程式 | RA | |
| 擴充（基礎架構） | RA | I |
| 整合外部應用程式 | | RA |
| 安裝App Builder應用程式 | | RA |
| 測試所有App Builder應用程式的效能 | | RA |
| 自訂App Builder應用程式的主題設定和設計 | | RA |
| 設定後端DNS | RA |  |
| 入門後端CDN | RA |  |
| 支援後端CDN | RA |  |
| 取得後端DNS提供者 | RA | |
| 布建生產和沙箱環境 | A | R |
| 正在存取[!DNL Adobe Commerce Optimizer]的Dynamics | R | C |
| 解決後端客戶的安全問題 | RA | I |
| 解決後端CDN安全性問題 | RA | |
| 協助Adobe進行安全性研究（掃描/稽核） | RA | |
| 執行PCI ASV掃描 | RA | I |
| 正在修復[!DNL Adobe Commerce Optimizer]基礎架構PCI掃描 | R | |
| 管理作業系統和平台機密 | RA | |
| 監控後端安全性記錄 | RA | |
| 控制客戶支援與存取 | A | R |
| Adobe DR計畫及備份與還原的年度測試和檔案 | RA | |
| 災難回覆計畫的年度測試與檔案 | RA | |
| 偵錯和問題隔離 | R | R |
| 及時支援偵錯和問題隔離流程 | R | R |
| 正在安裝[!DNL Adobe Commerce Optimizer]的更新和修補程式 | RA | I |
| 核心[!DNL Adobe Commerce Optimizer]應用程式品質 | RA | |
