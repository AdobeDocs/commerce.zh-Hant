---
title: 設定您的店面
description: 瞭解如何執行支架工具來設定您的 [!DNL Adobe Commerce as a Cloud Service] 店面。
feature: Storefront
role: Developer
level: Beginner
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"
source-git-commit: 6eda2197fde2e88292e58b2bb4fc4759f24da558
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# 設定您的店面

若要為[!DNL Adobe Commerce Storefront] (SaaS)設定由[!DNL Edge Delivery Services]提供支援的[!DNL Adobe Commerce as a Cloud Service]，請完成下列步驟。

如需更可自訂且更詳細的逐步解說，請參閱[店面檔案](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=zh-Hant)。

1. 開啟[網站建立者工具](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator)。

1. 選取&#x200B;**[!UICONTROL Create New Site (Code & Content)]**。

1. 輸入您要在其中建立店面程式碼存放庫的&#x200B;**[!UICONTROL Github Organization/Username]**。

1. 輸入&#x200B;**[!UICONTROL Site Name]**。

1. 在&#x200B;**[!UICONTROL Commerce GraphQL Endpoint (optional)]**&#x200B;欄位中，輸入您的[!DNL Adobe Commerce as a Cloud Service] (SaaS) GraphQL端點，您可以在[建立您的執行個體](./getting-started.md#create-an-instance)後，在Commerce Cloud Manager中存取該端點。

   或者，如果您使用[[!DNL API Mesh]](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic)，請在[!DNL API Mesh]欄位中輸入您的&#x200B;**[!UICONTROL Commerce GraphQL Endpoint (optional)]** GraphQL端點。 如需詳細資訊，請參閱[建立網格](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/create-mesh)。

1. 按一下&#x200B;**[!UICONTROL Create Site]**。 依照畫面上的指示，授權存取您的GitHub存放庫。

程式完成後，您可以使用以下方法自訂店面：

* 自訂您的程式碼： `https://github.com/<username or org>/<repo name>`
* 編輯您的內容： `https://da.live/#/<username or org>/<repo name>`
* 管理您的設定： `https://da.live/sheet#/<username or org>/<repo name>/configs-stage`
* 預覽您的店面： `https://main--<repo name>--<username or org>.aem.page/`

## 後續步驟

如需詳細資訊，請參閱下列文章：

* 若要進一步瞭解如何管理和顯示店面中的內容和資料，請參閱[更新店面內容](./use-cases.md#update-storefront-content)。
* 如需內容實驗功能的詳細資訊，請參閱[內容實驗](./use-cases.md#contextual-experimentation)。
* 如需使用Generative AI自動產生高品質內容的詳細資訊，請參閱[產生變數](./use-cases.md#generate-variations)。
* 若要進一步瞭解如何更新網站內容以及與Commerce前端元件和後端資料整合，請參閱[[!DNL Adobe Commerce Storefront documentation]](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=zh-Hant)。
