---
title: ' [!DNL Commerce] 服務如何處理隱私權要求'
description: 瞭解 [!DNL Commerce] 服務如何處理存取和刪除資料的請求。
role: Admin, Leader
feature: Security, Compliance
exl-id: 1408ca77-6956-4519-93a6-bc9be9bffeff
source-git-commit: c6725fc524e9d239ccc0f16701e92ad5d2fc7729
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# 隱私權請求

Adobe Experience Platform Privacy Service提供RESTful API和使用者介面，協助您管理客戶資料請求。 透過Privacy Service，您可以提交存取和刪除Adobe Experience Cloud應用程式中個人客戶資料的請求，協助促進法律資訊和組織隱私法規的自動合規性。

如需Privacy Service以及如何建立和管理隱私權請求的詳細資訊，請參閱Adobe Experience Platform檔案：

* [Privacy Service概觀](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/privacy/home)
* [在Privacy Service UI中管理隱私權工作](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/privacy/ui/user-guide)

## 管理個別資料隱私權請求

您可以透過兩種方式提交個別請求，以從[!DNL Commerce]存取和刪除消費者資料：

* 透過&#x200B;**Privacy Service UI**。 請參閱檔案[這裡](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/privacy/ui/user-guide#_blank)。
* 透過&#x200B;**Privacy Service API**。 請參閱檔案[這裡](https://developer.adobe.com/experience-platform-apis/references/privacy-service/#_blank)和API資訊[這裡](https://developer.adobe.com/experience-platform-apis/#_blank)。

Privacy Service支援兩種請求： **資料存取**&#x200B;和&#x200B;**資料刪除**。

>[!NOTE]
>
>本文著重於提出[!DNL Commerce]的隱私權要求。 如果您打算針對[Platform Data Lake](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/catalog/privacy)、[即時客戶設定檔](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/profile/privacy)或[身分識別服務](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/identity/privacy)提出隱私權要求，請參閱其各自的使用手冊。 請注意，刪除和存取請求必須個別向每個系統發出，因為Commerce的隱私權請求不會從所有這些系統中移除資料。

## 資料存取

針對&#x200B;**存取要求**，請從UI指定「Commerce (Personalization)」 （或在API中將`commerceMarketingData`指定為產品程式碼）。

## 資料刪除

針對刪除請求，Privacy Service會出於行銷目的刪除儲存在Commerce SaaS服務中的[!DNL Commerce]資料，這表示資料主體的設定檔和訂單將不再傳送至Adobe行銷應用程式，以用於行銷活動和客戶歷程。 不過，Privacy Service不會刪除[!DNL Commerce]應用程式中的資料，因為商家交易需求可能需要該資料。 商家需負責[!DNL Commerce]應用程式中的任何資料刪除/存取要求。 請參閱[共用職責安全性與運作模型](https://experienceleague.adobe.com/zh-hant/docs/commerce-operations/security-and-compliance/shared-responsibility)以瞭解更多資訊。

[!DNL Commerce]會將資料主體請求刪除特定資料的資訊，傳送給商家，通知他們刪除請求。

## 如何建立存取及刪除請求

### 先決條件

若要請求存取和刪除Adobe [!DNL Commerce]的資料，您必須擁有：

* IMS組織ID
* 您要對其採取動作之人員的身分識別碼以及對應的名稱空間。 如需Adobe [!DNL Commerce]和Experience Platform中身分識別名稱空間的詳細資訊，請參閱[身分識別名稱空間概觀](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/identity/features/namespaces)。

### GDPR請求/刪除存取權範例：

針對&#x200B;**存取請求**，請從UI指定「Commerce (Personalization)」 （或「commerceMarketingData」作為API中的產品程式碼）。

對於&#x200B;**刪除請求**，請確定已啟用「Commerce (Personalization)」核取方塊。 此外，如果客戶設定檔和訂單資料已從[!DNL Commerce]傳送至Adobe Experience Platform，您必須提交刪除請求給下列下游服務。

* 設定檔（產品代碼：「profileService」）
* AEP Data Lake （產品代碼：「AdobeCloudPlatform」）
* 身分（產品代碼：&quot;identity&quot;）

若要透過隱私權API傳送存取和刪除請求，您必須驗證和管理Privacy Service的許可權：

* [驗證及存取Privacy Service API](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/privacy/api/getting-started)
* [管理Privacy Service的許可權](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/privacy/permissions)

**必要的標頭**

```bash
curl --location --request POST 'https://platform.adobe.io/data/core/privacy/jobs' \
--header 'Content-Type: application/json' \
--header 'x-api-key: {{CLIENT_ID}}' \
--header 'x-gw-ims-org-id: {{IMS_ORGID}}' \
--header 'Authorization: Bearer {{ACCESS_TOKEN}}' \
```

**要求**

```json
{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{{IMS_ORGID}}"
      }
    ],
    "users": [
      {
        "key": "sampleUserKey1",
        "action": ["access"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "dsmith@sample.com",
            "type": "standard"
          }
        ]
      },
      {
        "key": "sampleUserKey2",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "ajones@sample.com",
            "type": "standard"
          }
        ]
      }
    ],
    "include": ["commerceMarketingData"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "gdpr"
}
```

**回應**

```json
{
    "requestId": "17284033173196154RX-223",
    "totalRecords": 3,
    "jobs": [
        {
            "jobId": "a52ca032-858e-11ef-bbb4-27391388a0a6",
            "customer": {
                "user": {
                    "key": "sampleUserKey1",
                    "action": [
                        "access"
                    ],
                    "userIDs": [
                        {
                            "namespace": "email",
                            "value": "dsmith@sample.com",
                            "type": "standard",
                            "namespaceId": 6,
                            "isDeletedClientSide": false
                        }
                    ]
                }
            }
        },
        {
            "jobId": "a52ca034-858e-11ef-bbb4-d5d952d69769",
            "customer": {
                "user": {
                    "key": "sampleUserKey2",
                    "action": [
                        "delete"
                    ],
                    "userIDs": [
                        {
                            "namespace": "email",
                            "value": "ajones@sample.com",
                            "type": "standard",
                            "namespaceId": 6,
                            "isDeletedClientSide": false
                        }
                    ]
                }
            }
        },
        {
            "jobId": "a52ca033-858e-11ef-bbb4-8361a5022341",
            "customer": {
                "user": {
                    "key": "sampleUserKey2",
                    "action": [
                        "access"
                    ],
                    "userIDs": [
                        {
                            "namespace": "email",
                            "value": "ajones@sample.com",
                            "type": "standard",
                            "namespaceId": 6,
                            "isDeletedClientSide": false
                        }
                    ]
                }
            }
        }
    ]
}
```
