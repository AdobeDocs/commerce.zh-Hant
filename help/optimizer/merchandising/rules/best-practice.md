---
title: 銷售規則最佳實務
description: 瞭解針對搜尋、預設清單和類別頁面實作銷售規則的最佳實務。
role: Admin, Developer
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 專案（Adobe管理的SaaS基礎結構）。"
exl-id: cc8d0879-c253-4ad4-8e7d-e066dff9112d
TQID: https://experienceleague.adobe.com/DrdrBBXeMyqQr16h1LrlSoet3F6ihn57LBmPFBUXmTs
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 70f219ca854a0df0ac16ed31116ba9c510eebec2
workflow-type: tm+mt
source-wordcount: 398
ht-degree: 0%

---

# 銷售規則最佳實務

若要最佳化轉換和收入，請實作有效的&#x200B;**搜尋規則**、強大的&#x200B;**預設清單**&#x200B;規則和&#x200B;**[類別規則](add.md#rule-types)**。 使用銷售資料、庫存、促銷活動和[智慧型排名](add.md#intelligent-ranking)調整排名。

建立深思熟慮的&#x200B;**預設規則**&#x200B;至關重要。 您的[預設規則](overview.md#default-rule)會決定搜尋結果在未套用特定搜尋規則時的初始排序方式，這可以改善探索和購買的可能性。 請定期檢閱，以符合購物者需求和行銷活動。

## 最佳化搜尋規則的提示

- 釘選或提升高銷量或近期銷售活動的產品。
- 優先處理高評等和正面評論的產品。
- 確保庫存專案排名較高。
- 稍微優先處理利潤率較高的產品，而不會影響關聯性。
- 標示在銷售中或屬於特別促銷的產品。
- 使用促銷期間的日期範圍，在促銷期間或銷售期間自動設定搜尋規則。
- 根據使用[智慧型排名](add.md#intelligent-ranking)的個別購物者行為量身打造搜尋結果，例如「為您推薦」、「檢視次數最多」等。
- 當選取&#x200B;**無**&#x200B;以外的智慧策略時，針對每個規則調整&#x200B;**[智慧排名提升](add.md#intelligent-ranking-boost)**，並在發佈前於&#x200B;**測試您的規則**&#x200B;進行驗證。
- 請一律使用「測試規則」面板來預覽您的智慧排名策略如何影響不同查詢的實際搜尋結果。

## 類別規則的提示

- 在高流量或高利潤的&#x200B;**類別頁面**&#x200B;上使用[類別規則](add.md#rule-types)，其中已組織的訂單與搜尋一樣重要，例如，季節性系列或精選部門。
- 將&#x200B;**智慧型排名** （例如，趨勢、檢視次數最多）與購物者瀏覽該類別的方式對齊；類別頁面不會像搜尋規則那樣使用搜尋查詢文字。 請參閱[智慧型排名](add.md#intelligent-ranking)。 對於&#x200B;**無**&#x200B;以外的智慧方法，請使用&#x200B;**[智慧排名提升](add.md#intelligent-ranking-boost)**&#x200B;和類別預覽來調整該類別規則的行為強度。
- 套用&#x200B;**圖釘**、**提升**&#x200B;和&#x200B;**埋藏**&#x200B;的方式與您的行銷活動計劃一致；請記住，只有當購物者對清單使用&#x200B;**預設排序**&#x200B;時，才會套用手動位置。 請參閱[手動排名](add.md#manual-ranking)。
- 在編輯器中預覽&#x200B;**類別**&#x200B;規則流程，並在發佈後在店面進行驗證，這與您在搜尋時「測試您的規則」面板使用的規則相同。
