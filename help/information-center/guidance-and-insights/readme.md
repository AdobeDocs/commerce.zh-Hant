---
title: 見解和指引控管
description: 瞭解用於見解和指引的內部治理模型。 未發佈至Experience League。
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: a91925091da28cd0745923894a3faab0374f0a0c
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%
---

# 見解和指引控管

這是說明檔案團隊的內部參考。 `TOC.md`中未列出它，因此它並未建置或發佈至Experience League。 請將其保留在此處，使其靠近它所控管的內容。 如需資訊中心的整體管理，請參閱[governance.md](../governance.md)。

## 所有權

前瞻分析和指引文章歸負責維護文章正確性和貨幣的發佈作者或團隊所有。 這些文章目前託管於`commerce.en`存放庫。 Commerce檔案團隊協助確保內容品質並將文章發佈到生產環境。

## 深入分析和指引的內容

- **屬於此處**—Commerce解決方案的策略指引和白皮書，涵蓋根據真實世界情境提供的實作指引。 納入相關Commerce檔案頁面的連結以取得支援。

- **改為屬於產品存放庫** — 逐步設定、教學課程、參考資料（API/CLI/設定參考）和疑難排解。 如果這裡的貼文開始累積此類細節，請將其移至相關的產品指南，並改為連結至該指南。

## 新增內容

為要發佈的文章建立COMDOX JIRA票證。 將`[templates/comdox-intake-template.md](templates/comdox-intake-template.md)`複製到票證說明中並填入 — 它會要求請求者識別對象、標幟內容是否為暫時（附帶到期日），並確認其屬於見解和指南，而非Commerce產品檔案。

在限定票證的範圍後，從`templates/`中的範本開始撰寫文章（`whitepaper-template.md`、`security-guidance-template.md`、`insight-perspective-template.md` — 未發佈、將相關文章複製到目標檔案中，並刪除範本自己的frontmatter預留位置註解）。 在內容準備好發佈後，在深入分析和指引下將專案新增至`help/information-center/TOC.md`。

- **新增最上層區段** （例如「深入分析>目錄管理」）在新增之前需要IA稽核，因為它會變更指南的導覽形狀。 在擁有該劇本或任務之Commerce IA評論的人中重複此程式。

- **新增至目錄** — 在發佈前新增主題至目錄。 如有需要，請使用隱藏中繼資料，發佈只有擁有連結的人才能存取的隱藏文章。 請參閱ExL作者指南中的[隱藏內容](https://experienceleague.adobe.com/en/docs/authoring-guide/using/authoring/hiding-files)。

## 評論步調

當新的Commerce解決方案重新命名或更新時，或見解不再相關時，檢閱文章內容。
