---
title: 設定您的店面
description: 瞭解如何執行支架工具來設定您的 [!DNL Adobe Commerce as a Cloud Service] 店面。
feature: Storefront
role: Developer
level: Beginner
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案（Adobe管理的SaaS基礎結構）。"
TQID: https://experienceleague.adobe.com/LoeNTJ-evBJB-TaJV0mEQpD2G2MwxHX7cYHx67kP0cA
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2: id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: bcc5edb5-84c3-4940-9f84-ed88b6c16274
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 300
ht-degree: 0%

---

# 設定您的店面

若要為[!DNL Adobe Commerce as a Cloud Service] (SaaS)設定由[!DNL Edge Delivery Services]提供支援的[!DNL Adobe Commerce Storefront]，請完成下列步驟。

如需更可自訂且更詳細的逐步解說，請參閱[店面檔案](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/)。

1. 開啟[網站建立者工具](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator)。

1. 選取&#x200B;**[!UICONTROL Create New Site (Code & Content)]**。

1. 輸入您要在其中建立店面程式碼存放庫的&#x200B;**[!UICONTROL Github Organization/Username]**。

1. 輸入&#x200B;**[!UICONTROL Site Name]**。

1. 在&#x200B;**[!UICONTROL Commerce GraphQL Endpoint (optional)]**&#x200B;欄位中，輸入您的[!DNL Adobe Commerce as a Cloud Service] (SaaS) GraphQL端點，您可以在[建立您的執行個體](./getting-started.md#create-an-instance)後，在Commerce Cloud Manager中存取該端點。

   或者，如果您使用[[!DNL API Mesh]](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic)，請在&#x200B;**[!UICONTROL Commerce GraphQL Endpoint (optional)]**&#x200B;欄位中輸入您的[!DNL API Mesh] GraphQL端點。 如需詳細資訊，請參閱[建立網格](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/create-mesh)。

1. 按一下&#x200B;**[!UICONTROL Create Site]**。 依照畫面上的指示，授權存取您的GitHub存放庫。

程式完成後，您可以使用以下方法自訂店面：

* 自訂您的程式碼： `https://github.com/<username or org>/<repo name>`
* 編輯您的內容： `https://da.live/#/<username or org>/<repo name>`
* 管理您的設定： `https://da.live/sheet#/<username or org>/<repo name>/configs-stage`
* 預覽您的店面： `https://main--<repo name>--<username or org>.aem.page/`

## 後續步驟

如需詳細資訊，請參閱下列文章：

* [正在更新店面內容](./use-cases.md#update-storefront-content) — 管理和顯示店面上的內容和資料。
* [情境式實驗](./use-cases.md#contextual-experimentation) — 在您的店面建立和管理實驗。
* [產生變數](./use-cases.md#generate-variations) — 使用Generative AI自動產生高品質的內容。
* [Adobe Commerce Storefront檔案](https://experienceleague.adobe.com/developer/commerce/storefront/) — 取得有關更新網站內容以及與Commerce前端元件和後端資料整合的詳細資訊。
* [組態服務](https://www.aem.live/docs/config-service-setup) — 瞭解如何從`config.json`移轉您的店面組態以使用組態服務，此服務支援進階使用案例，例如重複設定和覆蓋。
