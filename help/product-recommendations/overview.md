---
title: 什麼是產品建議？
description: 瞭解Adobe Commerce中的產品推薦。 探索AI驅動的店面單元、隱私、管理和店面路徑以及關鍵資料保留。
recommendations: noCatalog
exl-id: 72850cfd-555c-4e0e-ac3e-097e6dac2030
source-git-commit: 6bfc2c0ed53b44fb30a142dc87f87dca8a601a33
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 0%

---

# 什麼是[!DNL Product Recommendations]？

[!DNL Product Recommendations]會使用[Adobe AI](https://business.adobe.com/tw/ai.html)，以及針對彙總購物者行為和目錄進行機器學習，協助您在Adobe Commerce店面上顯示個人化產品推薦。 此概觀涵蓋服務限制（包括HIPAA）、資料和隱私權、建議單位出現的位置、店面實作路徑、建議如何補充產品關係，以及目錄資料保留。

>[!IMPORTANT]
>
>**[!DNL Product Recommendations]不是HIPAA就緒的服務。** 請勿在使用HIPAA就緒的產品或以其他方式處理受保護的健康情況資訊(PHI)的任何Adobe Commerce實作中啟用或使用[!DNL Product Recommendations]。 [!DNL Product Recommendations]屬於目前分類為不符合HIPAA標準的Commerce SaaS服務。
>
>如需哪些是HIPAA就緒的Adobe Commerce功能以及哪些服務不可搭配PHI使用的詳細資訊，請參閱Adobe Commerce[&#128279;](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/start/compliance/hipaa-ready-service/overview)和[作業](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/start/compliance/hipaa-ready-service/operations#adobe-commerce-services)上的HIPAA就緒性。

## 資料處理與隱私權

[!DNL Product Recommendations]的資料收集不含任何個人識別資訊(PII)。 所有使用者識別碼（例如Cookie ID和IP位址）都需嚴格匿名處理。 若要進一步瞭解，請參閱[Adobe隱私權原則](https://www.adobe.com/privacy/policy.html)。

如需資料同步的詳細資訊，請參閱[資料管理儀表板](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html?lang=zh-Hant)。

## 建議出現的位置

Recommendations會以有標籤的單位的形式出現在店面上，例如「檢視過此產品的客戶也檢視過」。 您可以透過Adobe Commerce管理員在商店檢視中建立、管理和部署建議。 如果您的Commerce專案使用[Adobe Commerce Optimizer Connector](https://experienceleague.adobe.com/zh-hant/docs/commerce/aco-optimizer-connector/overview)，您可以透過[Adobe Commerce Optimizer](../optimizer/overview.md)建立、管理和部署建議。

## 店面實施

選擇與店面相符的檔案：

- **PWA Studio** — [PWA檔案](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/)
- **自訂前端（例如React或Vue.js）** — [整合 [!DNL Product Recommendations]](headless.md)於Headless店面
- **Commerce Edge Delivery Services (EDS)** — [EDS的Adobe Commerce Storefront檔案](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=zh-Hant)

>[!NOTE]
>
>Headless和自訂設定因棧疊而異。 本產品區域會記錄PWA Studio路徑和一般Headless整合模式；但不會涵蓋所有協力廠商或自訂案例。

## 產品建議與產品關係

考慮到線上購物不斷變化的複雜性，最適合店面的往往是多種關鍵技術的組合。 同時使用[!DNL Product Recommendations]和[產品關係](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-relationships.html?lang=zh-Hant)可讓您在促銷產品時擁有更多彈性。 您可以運用Adobe AI支援的[!DNL Product Recommendations]，以智慧化方式大規模自動化您的建議。 然後，當您必須手動介入並確保向目標購物者區段提出特定建議，或當必須達成某些業務目標時，您可以運用[相關產品規則](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-related-rules.html?lang=zh-Hant)。

產品建議可讓您：

- 根據下列區域，從9種不同的智慧型建議型別中進行選擇：購物者型、專案型、人氣型、趨勢型和相似度型
- 在整個購物者的店面歷程中使用行為資料來個人化建議
- 測量與每個建議相關的關鍵量度，協助您瞭解建議的影響

## 產品推薦示範

觀看此影片以瞭解[!DNL Product Recommendations]：

>[!VIDEO](https://video.tv.adobe.com/v/343991?quality=12)

## 目錄資料保留原則

[!DNL Product Recommendations]服務取決於與您的Adobe Commerce環境保持同步的目錄資料。 停止查詢資料的非使用中目錄或環境可以進入休眠，這會影響在您重新啟用之前服務會傳回的內容。

如果您連續90天未在&#x200B;**測試**&#x200B;環境中提交目錄資料的查詢，則目錄資料會設定為休眠模式，且不會傳回任何查詢的資料。 **生產**&#x200B;環境中的目錄資料不受90天規則影響。

如果您的環境在建立後45天內有&#x200B;**空白的目錄**，則目錄資料會設定為休眠模式，且不會傳回任何查詢的資料。 這同時適用於生產環境和測試環境。

### 重新啟用目錄資料

若要在休眠後還原目錄資料，[提交標題為「重新啟用[!DNL Product Recommendations]」的支援請求](https://experienceleague.adobe.com/zh-hant/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page)並包含環境ID。 目錄資料應會在數小時內還原。
