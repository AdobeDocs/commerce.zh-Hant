---
title: 疑難排解 [!DNL Adobe Commerce Optimizer Connector]的情況
description: 診斷並解決 [!DNL Adobe Commerce Optimizer Connector] 中因設定錯誤或錯誤解讀同步結果所導致的意外行為。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案（Adobe管理的PaaS基礎結構）和內部部署專案的Adobe Commerce 。"
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
source-git-commit: 13c9dae2f2f8442f2d5c7be5f6e3317b94956cf0
workflow-type: tm+mt
source-wordcount: 645
ht-degree: 0%

---


# [!DNL Adobe Commerce Optimizer Connector]的疑難排解案例

此頁面說明在使用[!DNL Adobe Commerce Optimizer Connector]時可能會觀察到的行為，這些行為通常是由設定錯誤或錯誤解讀同步結果所造成。 請依照下列說明找出根本原因並套用適當的解決方法。

## 摘要狀態顯示「成功」，但在[!DNL Adobe Commerce Optimizer]中看不到資料

**問題：** **[!UICONTROL Data Feed Sync Status]**&#x200B;頁面報告同步處理成功，但產品、價格等未如預期在[!DNL Adobe Commerce Optimizer]中顯示。

**原因：**&#x200B;成功的摘要狀態表示擷取端點已接受資料，而不是表示資料已完成透過[!DNL Adobe Commerce Optimizer]的傳播。 內嵌後可能需要幾分鐘的時間才會傳播。

**解決方案：**

- 請稍候幾分鐘，然後重新整理[!DNL Adobe Commerce Optimizer]檢視。
- 確認[!DNL Adobe Commerce]中設定的租使用者ID符合您正在檢查的[!DNL Commerce Optimizer]環境。
- 確認已在[!DNL Commerce Optimizer]中選取正確的[目錄來源](../../optimizer/setup/catalog-sources.md) （商店檢視代碼）或價格簿。

## 匯出的目錄中缺少產品

**問題：**&#x200B;某些產品在完整目錄同步處理之後未出現在[!DNL Adobe Commerce Optimizer]中。

**原因：**&#x200B;如果產品在匯出期間驗證失敗，它們將會從同步中省略。 產品API不會傳回在目錄中停用或不可見的產品。

**解決方案：**

- 確認受影響的產品已指派至用作目錄來源的網站和商店檢視。
- 檢查產品是否已啟用，並設定為包含目錄清單的可見度。
- 在&#x200B;**[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**&#x200B;中檢閱目錄摘要的每專案錯誤詳細資料。

## [!DNL Adobe Commerce Optimizer]中的價格不正確或遺失

**問題：**&#x200B;產品出現在[!DNL Adobe Commerce Optimizer]中，但顯示[產品GraphQL查詢](https://developer.adobe.com/commerce/services/reference/graphql/#products){target="_blank"}未傳回任何價格，或是價格不符合[!DNL Adobe Commerce]中的設定。

**原因：**&#x200B;價格手冊摘要使用的領域對應到特定網站和客戶群組。 錯誤的[目錄檢視](../../optimizer/setup/catalog-view.md)設定可能會導致價格遺失或不正確。

**解決方案：**

- 確認網站已設定為可在聯結器的匯出設定中同步。 請參閱[自訂資料匯出組態](../get-started.md#customize-the-commerce-scopes-export-configuration)。
- 確認用於[!DNL Commerce Optimizer]的價格簿識別碼存在於用於執行產品查詢的[目錄檢視](../../optimizer/setup/catalog-view.md){target="_blank"}組態中。

## Storefront請求傳回存取被拒絕的錯誤，或目錄資料完全消失

**問題：**&#x200B;對於先前傳回資料的目錄檢視，對Merchandising API的請求現在會失敗，並產生`access-key-invalid`錯誤，或是正在運作的店面停止顯示目錄資料。

**原因：**&#x200B;目錄檢視已啟用[目錄保護](../../optimizer/setup/private-catalog-view.md)，而且要求遺漏必要的`AC-Catalog-View-Access-Token`標頭，或指派給檢視的所有受限制存取金鑰已過期。 [!DNL Adobe Commerce Optimizer Connector]不會自動建立、指派或旋轉受限存取金鑰，金鑰管理完全由您的使用者端應用程式處理。

**解決方案：**

- 確認目錄檢視仍至少指派了一個未過期的[受限制存取金鑰](../../optimizer/setup/restricted-access-keys.md)，並視需要旋轉或新增金鑰。
- 驗證storefront或使用者端是否連同每個要求一起傳送有效的已簽署`AC-Catalog-View-Access-Token`標頭。 檢視[私人目錄檢視](../../optimizer/setup/private-catalog-view.md)。

## 同步之後，[!DNL Adobe Commerce Optimizer]中的資料被覆寫或意外修改

**問題：**&#x200B;聯結器執行同步後，外部系統（例如PIM或ERP）直接在[!DNL Adobe Commerce Optimizer]中套用的資料變更會遺失或還原。

**原因：**&#x200B;當[!DNL Adobe Commerce]以外的系統直接寫入[!DNL Adobe Commerce Optimizer] （例如PIM或其他外部系統）時，可能會發生資料衝突。 聯結器會從[!DNL Adobe Commerce]到[!DNL Adobe Commerce Optimizer]單向同步資料&#x200B;*且不會將變更同步回[!DNL Adobe Commerce]。*&#x200B;因此，直接寫入[!DNL Adobe Commerce Optimizer]的資料不會反映在[!DNL Adobe Commerce]中，且可在稍後同步處理時覆寫。


**解決方案：**

不要將目錄修改直接寫入[!DNL Adobe Commerce Optimizer]，請使用[目錄圖層](../../optimizer/setup/catalog-layer.md){target="_blank"}在[!DNL Adobe Commerce]外部套用變更。 目錄層可讓外部系統在[!DNL Adobe Commerce Optimizer]內擴充或覆寫目錄資料，而不會與聯結器同步發生衝突。

## 常見[!DNL SaaS Data Export]問題的疑難排解案例

有關可能影響聯結器的基礎[!DNL SaaS Data Export]的相關問題，請參閱[疑難排解 [!DNL SaaS Data Export]](../../data-export/troubleshooting/troubleshooting-scenarios.md)的情況。
