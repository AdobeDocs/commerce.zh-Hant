---
title: 設定AEM Assets整合的IMS使用者許可權
description: 瞭解IMS身分和Admin Console設定檔如何啟用AEM Assets傳送存取、資產選擇器和自動填入的Commerce設定欄位。
feature: CMS, Media, Configuration
source-git-commit: 0fd98bf86555c914f7a5b1e177c31c37764dbf84
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---

# 使用者許可權和IMS

**IMS** (Adobe Identity Management System)是驗證層。 對於Adobe Commerce as a Cloud Service，Admin預設為啟用IMS驗證。 對於雲端或內部部署的Adobe Commerce，IMS是選用專案；[啟用Commerce的IMS](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/ims/adobe-ims-config.html?lang=zh-Hant){target=_blank}提供增強的設定UI （資產選擇器、自動填入的下拉選單），但您可以手動輸入&#x200B;**方案ID**&#x200B;和&#x200B;**環境ID**，設定不使用IMS的整合。

使用IMS時，AEM Assets整合也需要特定的&#x200B;**Adobe Admin Console產品設定檔**。 在Commerce管理員中設定整合的使用者需要&#x200B;**AEM Assets DM OpenAPI使用者 — 傳遞**&#x200B;產品設定檔，或是&#x200B;**作者**&#x200B;產品設定檔作為遞補。 這可透過使用者IMS組織中的Admin Console產品設定檔控制，並啟用：

* **Asset Selector**&#x200B;可在管理類別影像或頁面產生器內容時，從AEM Assets選取影像。
* **自動填入設定欄位**，例如&#x200B;**方案ID**、**環境ID**&#x200B;和&#x200B;**網域對應**&#x200B;下拉式清單，這些下拉式清單會根據使用者的Admin Console產品設定檔（傳遞或作者）從使用者的IMS工作階段提取值。

若沒有正確的許可權，「資產選擇器」便無法使用，且這些欄位會顯示為空白或需要手動輸入。
>[!BEGINSHADEBOX]

**IMS和許可權如何搭配運作**

Adobe IMS提供使用者身分和組織內容，而Adobe Admin Console定義其擁有哪些&#x200B;**產品設定檔**（許可權）。 AEM Assets整合會使用IMS詳細資訊和指派的設定檔，以判斷其能否自動填入設定欄位及啟用「資產選擇器」。

>[!ENDSHADEBOX]

## 為什麼需要產品設定檔

整合只能載入對應到設定檔的網域。 因此，使用者可以擁有以下產品設定檔：

* **AEM傳遞產品設定檔**。 當使用者同時擁有作者和傳送設定檔時，資產選擇器和設定UI的必要專案。 整合會使用可用的AEM傳遞產品設定檔。

* **作者產品設定檔**。 需要才能存取AEM Assets UI。 當使用者的Admin Console中沒有AEM傳遞產品設定檔時，也可作為資產選擇器和設定UI的備援。

網域（包括方案ID、環境ID和網域對應）會指派給AEM傳遞產品設定檔。 整合會從&#x200B;**AEM傳遞產品設定檔**&#x200B;載入網域（可用時），或在AEM傳遞產品設定檔不在使用者的Admin Console中時，退回給&#x200B;**作者產品設定檔**。 使用者需要這些設定檔之一來：

* 在Commerce管理設定中填入&#x200B;**方案識別碼**、**環境識別碼**&#x200B;和&#x200B;**網域對應**&#x200B;下拉式清單。
* 使用「資產選擇器」，從AEM Assets中瀏覽及選取資產。

如果兩個設定檔均未設定，使用者可以手動輸入&#x200B;**方案ID**&#x200B;和&#x200B;**環境ID**，但將無法使用資產選擇器。

## 依部署型別授與許可權

>[!BEGINTABS]

>[!TAB Adobe Commerce as a Cloud Service]

僅[!BADGE SaaS]{type=Positive tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案（Adobe管理的SaaS基礎結構）。"}

IMS驗證預設為啟用。 將使用者新增至&#x200B;**Adobe Admin Console**&#x200B;中的[AEM Assets DM OpenAPI使用者 — 傳遞](https://adminconsole.adobe.com/)產品設定檔，或新增至&#x200B;**作者**&#x200B;產品設定檔（例如，`<environment-name> - author - <program-id> - <environment-id>`），當使用者的Admin Console中沒有AEM傳遞產品設定檔時，作為遞補。

>[!NOTE]
>
> 使用者也必須新增至Commerce和AEM Assets。 如需完整設定，請參閱「[使用者和AEM Assets](https://experienceleague.adobe.com/zh-hant/docs/commerce/cloud-service/user-management#add-a-user-to-aem-assets-or-product-visuals){target=_blank}指南」中的&#x200B;_新增使用者至Identity Management或產品視覺效果_。

適用於Admin Console傳遞的![AEM Assets產品設定檔](../assets/aem-assets-delivery-product-profile.png){width="600" zoomable="yes"}

>[!TAB 雲端或內部部署上的Adobe Commerce]

僅[!BADGE 個PaaS]{type=Informative tooltip="僅適用於雲端專案上的Adobe Commerce （Adobe管理的PaaS基礎結構）。"}

Paa需要&#x200B;**IMS使用者端ID**&#x200B;才能啟用資產選擇器。 如需先決條件，請參閱[設定AEM Assets專案](configure-aem.md#prerequisites)，包括使用OpenAPI啟用Dynamic Media時如何取得IMS使用者端ID。

若要使用資產選擇器和自動填入的設定欄位（方案ID、環境ID、網域對應）：

1. [為Commerce啟用Adobe IMS](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/ims/adobe-ims-config.html?lang=zh-Hant){target=_blank}，讓Commerce管理員使用IMS驗證，並可讀取使用者的Admin Console產品設定檔。

1. [開啟支援票證](https://experienceleague.adobe.com/zh-hant/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-cases)以要求資產選擇器的自訂IMS使用者端ID。

1. 從[Adobe Admin Console](https://adminconsole.adobe.com/)，將使用者新增至&#x200B;**AEM Assets DM OpenAPI使用者 — 傳遞**&#x200B;產品設定檔，或新增至&#x200B;**作者**&#x200B;產品設定檔（例如，`<environment-name> - author - <program-id> - <environment-id>`），當使用者的Admin Console中沒有AEM傳遞產品設定檔時，作為遞補。

如果沒有IMS，您仍然可以在Commerce管理員中手動輸入方案ID和環境ID來設定整合。

>[!ENDTABS]

## 相關檔案

* [設定AEM Assets整合的IMS使用者許可權](setup-synchronization.md) — 將Commerce連線至AEM Assets並設定比對規則。
* [手動選取資產](../synchronize/asset-selector-integration.md) — 使用類別影像和頁面產生器的資產選擇器。
* [將使用者新增至AEM Assets或產品視覺效果](https://experienceleague.adobe.com/zh-hant/docs/commerce/cloud-service/user-management#add-a-user-to-aem-assets-or-product-visuals){target=_blank} — 針對ACCS，請先將使用者新增至Commerce和AEM Cloud Manager （業務負責人、部署管理員）。 **AEM Assets DM OpenAPI使用者 — 傳遞**&#x200B;設定檔（或作為遞補的&#x200B;**作者**&#x200B;設定檔）是「資產選擇器」和自動填入功能的額外需求。
* [將團隊成員指派給AEM傳遞層](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem#add-team-members){target=_blank}。 傳遞存取許可權的AEM檔案。
