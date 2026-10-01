---
title: 管理B2B共用目錄的限制存取金鑰
description: 瞭解如何管理Adobe Commerce Optimizer Connector用來保護B2B共用目錄投影安全的受限制存取金鑰。
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案（Adobe管理的PaaS基礎結構）和內部部署專案的Adobe Commerce 。"
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
    internal-label: Data Transfer
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 0%
---

# 管理B2B共用目錄的限制存取金鑰

[!BADGE Private Beta]{type=Caution tooltip="需要Adobe Commerce Optimizer Connector B2B擴充功能，目前為私人測試版。"}

如果您將[!DNL Adobe Commerce]個B2B共用目錄與[!DNL Adobe Commerce Optimizer Connector B2B extension]搭配使用，擴充功能會在建立目錄檢視時自動產生並指派第一個受限制的存取金鑰。 使用Commerce管理員中的[!UICONTROL Restricted Access Keys]頁面來檢視該金鑰，以及建立、指派或刪除其他金鑰。

![B2B共用目錄檢視的限制存取金鑰](assets/restricted-access-keys.png){width="800" zoomable="yes"}

>[!NOTE]
>
>若要管理您為非B2B使用案例（例如合作夥伴入口網站）手動建立的金鑰，請參閱[受限制的存取金鑰](/help/optimizer/setup/restricted-access-keys.md#create-a-restricted-access-key)。

## 存取頁面 {#access-the-page}

從Commerce Admin移至&#x200B;**[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Restricted Access Keys]**。

您可以從「共用目錄」網格或「公司」網格將索引鍵指派給目錄檢視。 請參閱[將金鑰指派給B2B共用目錄檢視](#assign-keys-to-a-shared-catalog-view)。

>[!NOTE]
>
>如需此頁面上欄位的參考，請參閱&#x200B;*Commerce管理指南*&#x200B;中的[限制存取金鑰管理](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys){target="_blank"}。—>

## 當您需要超過自動金鑰時 {#when-you-need-more-than-the-automatic-key}

[!DNL Adobe Commerce Optimizer Connector B2B extension]產生的自動金鑰涵蓋大多數B2B共用目錄，不需要您採取任何動作。 在這些情況下自行管理金鑰：

- **旋轉金鑰** — 建立新的金鑰，將其與現有金鑰一起指派至目錄檢視，確認其運作正常，然後刪除舊金鑰。 尚無法自動旋轉。
- **索引鍵無法連結** — 如果[目錄檢視同步處理狀態](catalog-view-sync-status.md)顯示索引鍵相關的漂移，請嘗試再次儲存目錄檢視指派，以重試失敗的連結。 如果金鑰仍然失敗，請先執行[!UICONTROL Reconcile & Repair]以復原金鑰或狀態，然後再建立取代。 只有在金鑰過期或失敗永久無法復原時，才建立取代金鑰。
- **尋找公開金鑰** — 在[限制存取金鑰]頁面上，選取&#x200B;**[!UICONTROL View Public Key]**&#x200B;以檢視並複製金鑰的公開金鑰。

目錄檢視一次最多可以有三個指派的索引鍵。 在金鑰輪換期間，[!DNL Adobe Commerce Optimizer]接受由任何指派的未過期金鑰簽署的權杖 — 沒有手動步驟可設定「作用中」金鑰。

## 建立金鑰

在[!UICONTROL Restricted Access Keys]頁面上，選取&#x200B;**[!UICONTROL Create Key]**&#x200B;以建立金鑰。

Commerce會產生新的金鑰組並保留私密金鑰。 「限制存取金鑰」表格會更新為顯示唯一金鑰ID的新金鑰專案。 將金鑰指派給目錄檢視時，請使用此[!UICONTROL Key ID]。

公開金鑰並未向[!DNL Adobe Commerce Optimizer]註冊，直到您將金鑰指派給目錄檢視為止。 註冊之後，會更新「限制存取金鑰」表格專案，以顯示目錄指派與到期日。

## 將索引鍵指派給從B2B共用目錄投影的目錄檢視 {#assign-keys-to-a-shared-catalog-view}

從公司帳戶或共用目錄頁面的目錄檢視指派或取消指派金鑰，而不是從主要[!UICONTROL Restricted Access Keys]格線。

目錄檢視必須至少有一個索引鍵，而且最多可以有三個。

- 如果您嘗試指派第四個索引鍵，當您嘗試儲存值時，會出現錯誤訊息： `A Catalog View can have at most 3 access keys.`
- 如果目錄檢視只有一個索引鍵，則無法刪除或取消指派該索引鍵。

若要更新目錄檢視索引鍵組態，您可以從公司帳戶頁面或共用目錄頁面存取它。

>[!BEGINTABS]

>[!TAB 管理公司帳戶的金鑰]

1. 從Commerce Admin，開啟公司頁面(**[!UICONTROL Customers]** > **[!UICONTROL Companies]**)。

1. 在公司的[!UICONTROL Action]欄中，選取[!UICONTROL Edit]。

1. 若要檢視從指派給公司的共用目錄投影的目錄檢視清單，請展開&#x200B;_[!UICONTROL Catalog Views]_&#x200B;區段。

索引標籤會列出從共用目錄投影的目錄檢視，包括其指派的索引鍵。

1. 在要更新的目錄檢視的[!UICONTROL Actions]欄中，選取&#x200B;**[!UICONTROL Edit Restricted Access Keys]**。

   ![編輯限制存取金鑰下拉式清單，顯示指派給目錄檢視的金鑰](assets/restricted-access-key-selector.png){width="500" zoomable="yes"}

1. 若要指派金鑰，請選取&#x200B;**[!UICONTROL Access Keys]**&#x200B;下拉式清單。 然後，選取[!UICONTROL key ID]未指派的金鑰，例如`#42`。 然後，按一下[!UICONTROL Done]以將其指派給目錄檢視。

   已指派給不同目錄檢視的索引鍵會相應地加上標籤。

1. 若要移除存取權杖，請選取金鑰標籤中的`x`控制項，將其從[!UICONTROL Access Tokens]欄位中移除。

1. 若要儲存並套用組態更新，請選取&#x200B;**[!UICONTROL Save]**。

>[!TAB 從共用目錄管理金鑰]

1. 從Commerce Admin，開啟共用目錄頁面(**[!UICONTROL Catalog]** > **[!UICONTROL Shared catalogs]**)。

1. 在共用的[!UICONTROL Action]欄中，從[!UICONTROL Select]功能表選擇&#x200B;**[!UICONTROL General Settings]**。

1. 若要檢視從共用目錄投影的目錄檢視清單，請從[!UICONTROL Shared Catalog Information]功能表選取&#x200B;**[!UICONTROL Catalog Views]**。

[!UICONTROL Catalog Views]頁面列出每個目錄檢視的目錄檢視識別碼、關聯的存放區檢視以及存取金鑰。

1. 在要更新的目錄檢視的[!UICONTROL Actions]欄中，選取&#x200B;**[!UICONTROL Edit Restricted Access Keys]**。

   ![編輯限制存取金鑰下拉式清單，顯示指派給目錄檢視的金鑰](assets/restricted-access-key-selector.png){width="500" zoomable="yes"}

1. 若要指派金鑰，請選取&#x200B;**[!UICONTROL Access Keys]**&#x200B;下拉式清單。 然後，依預設金鑰標題選取未指派的金鑰，例如`#42`。 然後，按一下[!UICONTROL Done]以將其指派給目錄檢視。

   已指派給不同目錄檢視的索引鍵會相應地加上標籤。

1. 若要移除存取權杖，請選取金鑰標籤中的`x`控制項，將其從[!UICONTROL Access Tokens]欄位中移除。

1. 若要儲存並套用組態更新，請選取&#x200B;**[!UICONTROL Save]**。

>[!ENDTABS]

## 管理金鑰到期和續約

您可以為受限制的存取金鑰設定預設金鑰存留期。 此值決定當[!DNL Adobe Commerce Optimizer Connector B2B]擴充功能產生初始金鑰或手動建立新金鑰時設定的到期日。

到期日會顯示在[!UICONTROL Restricted Access Keys]頁面的[!UICONTROL Expires At]欄中。

若要變更持續時間，請前往&#x200B;**[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL Configuration]** > **[!UICONTROL Services]** > **[!UICONTROL ACO Restricted Access Keys]**。 在[!UICONTROL Provisioning]頁面上，更新&#x200B;**[!UICONTROL Default Key Expiry (days)]**&#x200B;欄位。 預設的系統金鑰存留期最初設定為延長期間（約100年）。 請務必將其更新為符合您安全性原則的值。

### 金鑰續約

當索引鍵到期還不到10天時，[!UICONTROL Restricted Access Keys]頁面會在它的專案旁邊顯示警告圖示。 如果您在金鑰過期之前未更新金鑰，則在您指派新金鑰之前，將無法存取目錄檢視。

您可以隨時建立和指派新金鑰，並在確認新金鑰正常運作後移除舊金鑰。

## 已知限制

尚未提供自動金鑰輪換功能。

>[!MORELIKETHIS]
>
> - [管理受限制的存取金鑰](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys){target="_blank"} — 此頁面的完整欄位參考，在&#x200B;*Commerce管理指南*&#x200B;中 — >
> - [監視目錄檢視同步](catalog-view-sync-status.md) — 監視這些金鑰保護的目錄檢視
> - [私人目錄檢視](/help/optimizer/setup/private-catalog-view.md) — 瞭解什麼是聯結器管理的私人目錄檢視
> - [受限制的存取金鑰](/help/optimizer/setup/restricted-access-keys.md) — 瞭解手動、ACO Studio型金鑰流程如何適用於非B2B使用案例
