---
title: Commerce資訊中心控管
description: 瞭解Commerce資訊中心的內部治理模式。 未發佈至Experience League。
source-git-commit: a91925091da28cd0745923894a3faab0374f0a0c
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%
---

# Commerce資訊中心控管

`TOC.md`中未列出檔案團隊的內部參考，因此未發佈至Adobe Experience League。

## 所有權

Adobe Commerce檔案團隊擁有資訊中心。 它是在`Adobe-Enterprise-Docs/commerce.en`中撰寫，存放庫在`metadata.md`中列為`git-repo`。

沒有單一產品團隊擁有它，因為它是跨產品的。 將產品特定的更正升級至擁有產品團隊的檔案聯絡人，而不是在此處修正。

## 資訊中心的內容

| 屬於此處 | 屬於產品存放庫 |
| --- | --- |
| 涵蓋多個產品或服務的內容，例如產品選擇指南、跨產品實施歷程、架構模式和白皮書 | 單一產品內容，例如逐步設定、API/CLI/設定參考和疑難排解 |
| 連結至授權產品檔案的簡短組織頁面 | |

- 如果這裡的頁面累積了單一產品的詳細資訊，請將其移至產品指南並連結。
- 資訊中心不會合併或遷移產品檔案，也不會記錄個別產品功能。 在撰寫新內容之前，先連結到現有的授權內容。

## 新增內容

### 現有區段中的文章

1. 將檔案新增至符合區段的資料夾。
1. 新增專案至該區段下的`TOC.md`。

除了正常的PR稽核以外，不需要核准。

| 目錄區段 | 資料夾 |
| --- | --- |
| 探索Commerce平台和服務 | `portfolio/`, `storefronts/`, `aem-assets/`, `apis/` |
| 角色快速入門 | `get-started/` |
| 深入分析和指引 | `guidance-and-insights/` |
| 架構 | `architecture-options/` |
| 移轉與採用 | `migration-adoption/` |
| 實作指南 | `implementation-guides/` |

### 深入分析和指導文章

1. 將`whitepaper-template.md`或`security-guidance-template.md`從`guidance-and-insights/templates/`複製到`guidance-and-insights/`。 範本未發佈。 如需完整撰寫程式，包括COMDOX輸入票證，請參閱[readme.md](guidance-and-insights/readme.md)。
1. 刪除範本的預留位置註解。
1. 當內容準備發佈時，在深入分析和指引下新增`TOC.md`專案。

### 最上層區段

`TOC.md`中的新頂層群組變更了指南的導覽，因此需要IA檢閱。 請連絡擁有Commerce IA評論的人員。 先重複使用現有的區段，例如合作夥伴或啟用內容的由角色開始使用。

### 已發佈的URL

URL是從指南ID、`TOC.md`中的區段ID （例如，`{#insights-and-guidance}`）和檔案名稱建置的。 資料夾名稱未出現在URL中。 為每個區段指定唯一的ID，並確定沒有兩篇文章可解析為相同的URL。

## 評論步調

- **事件導向** — 檢閱「探索Commerce平台和服務」、「透過角色開始使用」、「架構、移轉和採用」以及「實作指南」章節。當Commerce產品重新命名、啟動、棄用，或其可用性變更時。 例如，檢閱Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer是否獲得整合。 這些頁面會先過期。
- **已排程** — 若要取得過時的術語、品牌或技術上的不準確之處，請每六個月執行一次自動內容稽核和檢閱。

## 與說明/登陸/的關係

`help/landing/` (「Adobe Commerce Services Guides」)是獨立的指南，不屬於資訊中心。 它著重於Commerce服務，如目錄服務、即時搜尋、產品建議和支付服務，以及它的資訊中心連結，以取得詳細資訊。 重新處理或合併兩者是本指南未解決的後續決定。
