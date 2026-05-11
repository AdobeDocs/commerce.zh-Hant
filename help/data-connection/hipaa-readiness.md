---
title: ' [!DNL Commerce] 服務的HIPAA整備'
description: 瞭解如何使用 [!DNL Data Connection] 擴充功能與Experience Platform共用 [!DNL Commerce] 資料並維持HIPAA法規遵循。
role: Admin, Leader
feature: Security, Compliance
exl-id: 8851e6d2-c466-4d8e-bfa4-20d0ad6522b5
TQID: https://experienceleague.adobe.com/PxrtL1nHtJsRJuAehDVKRk0ZuJz0ta7i84j1K6An1QU
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2:
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 601
ht-degree: 1%

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

如果您已購買Adobe [!DNL Commerce]的醫療保健附加元件，表示您已安裝[HIPAA-Ready擴充功能](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/hipaa-ready-service/overview#installation)。 若要確保您的[!DNL Commerce]後台事件資料已可使用HIPAA，您還需要安裝[!DNL Data Connection]擴充功能搭配額外的&#x200B;**資料服務HIPAA**&#x200B;擴充功能。 **Data Services HIPAA**&#x200B;擴充功能可確保您傳送至Experience Platform的所有後台資料都可使用HIPAA。 瞭解[如何安裝擴充功能](install.md#install-the-data-services-hipaa-extension)。

>[!IMPORTANT]
>
>安裝&#x200B;**Data Services HIPAA**&#x200B;擴充功能時，將不再擷取「即時搜尋」和「產品推薦」所使用的店面事件資料。 這是因為店面事件資料是在使用者端產生。 若要繼續擷取和傳送店面事件資料，請重新啟用這些服務的事件收集。 請參閱[一般組態](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general#data-services)以瞭解更多資訊。

## 如何確保傳送至Experience Platform的資料已可使用HIPAA

在[!DNL Commerce]中，[!DNL Data Connection]擴充功能傳送至Experience Platform的所有後台事件資料都視為敏感。 不過，商家有責任將資料使用標籤套用至其Experience Platform中的[!DNL Commerce]結構描述，以明確識別敏感性特定資料。 當您直接將資料使用標籤套用至結構描述時，這些標籤會傳播至以該結構描述為基礎的所有現有和未來資料集。

如需資料使用標籤及其在資料控管架構中角色的概觀，請參閱Experience Platform檔案中的[資料使用標籤概觀](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/data-governance/labels/overview)。

### 套用資料使用標籤至[!DNL Commerce]欄位

請依照[管理結構描述](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/labels)的資料使用標籤教學課程中的步驟，瞭解如何將標籤套用至您的[!DNL Commerce]結構描述。

請參閱敏感標籤的[字彙表](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/labels/reference#sensitive)，瞭解您可以套用至[!DNL Commerce]結構描述中欄位的可用標籤。 例如，標籤`RHD`會識別Adobe合約准許您上傳的受保護健康資訊(PHI)或病人相關資訊。

當您的[!DNL Commerce]資料標籤為敏感時，您可以強制實行原則以防止構成原則違規的資料作業。 深入瞭解Experience Platform中的[原則執行](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/enforcement/overview)。

## Commerce中的資料加密

Adobe [!DNL Commerce]使用區塊層級加密。 針對儲存，[!DNL Commerce]使用Amazon彈性區塊存放區(EBS)。 所有EBS磁碟區都使用AES-256演演算法加密，這表示資料會靜態加密。 傳輸中的[!DNL Commerce]資料是透過使用HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246)的安全加密連線進行。

>[!IMPORTANT]
>
>當資料不在伺服器之間傳輸或不在伺服器之間傳輸時，Commerce不支援欄或列層級的加密或加密。

### Experience Platform中的資料加密

當商家將資料傳送至Experience Platform時，該資料會使用HTTPS TLS v1.2傳送。 深入瞭解[Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/landing/governance-privacy-security/encryption)如何加密資料。

## [!DNL Commerce]如何處理隱私權要求

瞭解[!DNL Commerce] [如何處理隱私權要求](handle-privacy-request.md)。
