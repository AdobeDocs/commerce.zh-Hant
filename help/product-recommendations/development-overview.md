---
title: 產品Recommendations管理員開發
description: 產品Recommendations架構和開發功能的概觀。
exl-id: 5967259e-c531-4fc7-9abd-cc18433fab33
TQID: https://experienceleague.adobe.com/DtPYY7DaB-A7-VyTeXkjL9Y2My-WOQx-9CD-TgrcTmk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bbbea26f-9621-49eb-9ab8-e06fb3bbce8c
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 319
ht-degree: 0%

---

# 產品Recommendations管理員開發

產品推薦是強大的行銷工具，可用來增加轉換率、增加收入及刺激購物者參與。 產品推薦會以單位的形式出現在商店中，例如「檢視過此產品的客戶也檢視過」、「購買此產品的客戶也購買了」、「為您推薦」等。 Adobe Commerce產品推薦由[Adobe AI](https://business.adobe.com/tw/ai.html)提供技術支援，其使用人工智慧和機器學習演演算法來對彙總的購物者資料執行深入分析。 此資料與您的Commerce目錄結合後，可為購物者提供極為引人入勝、相關且個人化的體驗。

>[!NOTE]
>
>如果您的店面是使用PWA Studio實作，請參閱[PWA檔案](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/)。 如果您使用自訂前端技術，例如React或Vue JS，請參閱使用指南以瞭解如何在[headless](headless.md)環境中整合產品建議。 Headless執行個體必須實作事件，才能支援產品推薦工作區。

## 架構概觀

從高層面來看，Commerce產品建議會部署為SaaS。 Commerce端包括店面（其中包含事件收集器和建議版面配置範本）和後端（其中包含資料服務、SaaS匯出模組和管理UI）。 Adobe AI情報服務會在SaaS端運用。

![產品建議架構圖](assets/arch-diag-sensei.svg)

安裝及設定建議模組後，您的店面就會開始收集行為資料。 Adobe AI會處理此行為資料與目錄資料，並計算Recommendations服務所利用的產品關聯。 此時，商家可以直接從管理UI建立、管理產品推薦單位，並將其部署至店面。

## 後續步驟

請閱讀下列主題，以開始使用產品建議：

- [如何實作產品建議](implementation-workflow.md)

- [安裝及設定產品推薦](install-configure.md)

- [建立產品推薦](create.md)
