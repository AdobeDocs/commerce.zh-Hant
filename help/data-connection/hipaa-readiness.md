---
title: ' [!DNL Commerce] 服務的HIPAA整備'
description: 瞭解如何使用 [!DNL Data Connection] 擴充功能與Experience Platform共用 [!DNL Commerce] 資料並維持HIPAA法規遵循。
role: Admin, Leader
feature: Security, Compliance
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# [!DNL Commerce]服務的HIPAA整備

[!DNL Data Connection]擴充功能可讓您與Experience Platform共用[!DNL Commerce]個後台事件資料，並維持HIPAA法規遵循。

>[!IMPORTANT]
>
>由於店面事件是在使用者端產生，因此商家應負責[不要將店面事件資料](connect-data.md#data-collection)傳送至Experience Platform。

在本文章中，您將瞭解：

- 安裝內容
- 如何確保傳送至Experience Platform的資料已可使用HIPAA
- [!DNL Commerce]中的資料加密

## 安裝

如果您已購買Adobe [!DNL Commerce]的醫療保健附加元件，表示您已安裝[HIPAA-Ready擴充功能](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/start/compliance/hipaa-ready-service/overview#installation)。 若要確保您的[!DNL Commerce]後台事件資料已可使用HIPAA，您還需要安裝[!DNL Data Connection]擴充功能搭配額外的&#x200B;**資料服務HIPAA**&#x200B;擴充功能。 **Data Services HIPAA**&#x200B;擴充功能可確保您傳送至Experience Platform的所有後台資料都可使用HIPAA。 瞭解[如何安裝擴充功能](install.md#install-the-data-services-hipaa-extension)。

>[!IMPORTANT]
>
>安裝&#x200B;**Data Services HIPAA**&#x200B;擴充功能時，將不再擷取「即時搜尋」和「產品推薦」所使用的店面事件資料。 這是因為店面事件資料是在使用者端產生。 若要繼續擷取和傳送店面事件資料，請重新啟用這些服務的事件收集。 請參閱[一般組態](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general.html#data-services)以瞭解更多資訊。

## 如何確保傳送至Experience Platform的資料已可使用HIPAA

在[!DNL Commerce]中，[!DNL Data Connection]擴充功能傳送至Experience Platform的所有後台事件資料都視為敏感。 不過，商家有責任將資料使用標籤套用至其Experience Platform中的[!DNL Commerce]結構描述，以明確識別敏感性特定資料。 當您直接將資料使用標籤套用至結構描述時，這些標籤會傳播至以該結構描述為基礎的所有現有和未來資料集。

如需資料使用標籤及其在資料控管架構中角色的概觀，請參閱Experience Platform檔案中的[資料使用標籤概觀](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/data-governance/labels/overview)。

### 套用資料使用標籤至[!DNL Commerce]欄位

請依照[管理結構描述](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/tutorials/labels)的資料使用標籤教學課程中的步驟，瞭解如何將標籤套用至您的[!DNL Commerce]結構描述。

請參閱敏感標籤的[字彙表](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/data-governance/labels/reference#sensitive)，瞭解您可以套用至[!DNL Commerce]結構描述中欄位的可用標籤。 例如，標籤`RHD`會識別Adobe合約准許您上傳的受保護健康資訊(PHI)或病人相關資訊。

當您的[!DNL Commerce]資料標籤為敏感時，您可以強制實行原則以防止構成原則違規的資料作業。 深入瞭解Experience Platform中的[原則執行](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/data-governance/enforcement/overview)。

## Commerce中的資料加密

Adobe [!DNL Commerce]使用區塊層級加密。 針對儲存，[!DNL Commerce]使用Amazon彈性區塊存放區(EBS)。 所有EBS磁碟區都使用AES-256演演算法加密，這表示資料會靜態加密。 傳輸中的[!DNL Commerce]資料是透過使用HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246)的安全加密連線進行。

>[!IMPORTANT]
>
>當資料不在伺服器之間傳輸或不在伺服器之間傳輸時，Commerce不支援欄或列層級的加密或加密。

### Experience Platform中的資料加密

當商家將資料傳送至Experience Platform時，該資料會使用HTTPS TLS v1.2傳送。深入瞭解[Experience Platform](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/landing/governance-privacy-security/encryption)如何加密資料。

## [!DNL Commerce]如何處理隱私權要求

瞭解[!DNL Commerce] [如何處理隱私權要求](handle-privacy-request.md)。
