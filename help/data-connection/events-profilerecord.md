---
title: 設定檔記錄
description: 瞭解設定檔記錄擷取哪些資料。
role: Admin, Developer
feature: Personalization, Integration, Eventing
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# [!DNL Data Connection]個設定檔記錄

以下說明安裝[!DNL Data Connection]擴充功能時可用的Commerce設定檔記錄資料。 設定檔記錄中的資料會傳送至Adobe Experience Platform。

## 設定檔記錄

建立、更新或刪除新設定檔時，可在Experience Platform中使用設定檔記錄更新。

### 從設定檔記錄收集的資料

以下說明為設定檔記錄擷取的資料。

| 欄位 | 說明 |
|---|---|
| `channel` | 包含資料來源的相關資訊。 `_id`和`_type`都包含[名稱空間值](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/namespaces)。 |
| `channel._id` | 管道的唯一識別碼，例如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 識別管道資料的來源，例如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `person` | 包含有關客戶的資訊。 |
| `person.name` | 包含客戶名稱的相關資訊。 |
| `person.name.firstName` | 包含客戶的名字。 |
| `person.name.lastName` | 包含客戶的姓氏。 |
| `person.birthDate` | 購物者的出生日期。 |
| `personalEmail` | 個人電子郵件地址。 |
| `personalEmail.address` | 技術地址，例如，RFC2822和後續標準中通常定義的`name@domain.com`。 |
| `billingAddress` | 帳單郵寄地址。 |
| `billingAddress.street1` | 主要街道層級資訊、公寓號碼、街道號碼和街道名稱。 |
| `billingAddress.street2` | 選用的街道資訊第二行。 |
| `billingAddress.city` | 城市的名稱。 |
| `billingAddress.state` | 狀態的名稱。 此為自由格式的欄位。 |
| `billingAddress.country` | 政府管理的領土的名稱。 除了`xdm:countryCode`，這是自由格式的欄位，可以有任何語言的國家名稱。 |
| `billingAddress.primary` | 指出這是否為主要帳單地址。 值一律為`False`。 |
| `billingAddressPhone` | 與帳單地址相關聯的電話號碼。 |
| `billingAddressPhone.number` | 電話號碼。 請注意，電話號碼為字串，並可能包含有意義的字元，例如括弧`()`、連字型大小`-`或表示次撥接識別碼的字元，例如分機號碼`x`，例如`1-353(0)18391111`或`+613 9403600x1234`。 |
| `billingAddressPhone.primary` | 表示這是否為帳單地址的主要電話號碼。 值一律為`False`。 |
| `shippingAddress` | 郵寄地址。 |
| `shippingAddress.street1` | 主要街道層級資訊、公寓號碼、街道號碼和街道名稱。 |
| `shippingAddress.street2` | 選用的街道資訊第二行。 |
| `shippingAddress.city` | 城市的名稱。 |
| `shippingAddress.state` | 狀態的名稱。 此為自由格式的欄位。 |
| `shippingAddress.country` | 政府管理的領土的名稱。 除了`xdm:countryCode`，這是自由格式的欄位，可以有任何語言的國家名稱。 |
| `shippingAddress.primary` | 指出這是否為主要送貨地址。 值一律為`False`。 |
| `shippingAddressPhone` | 與送貨地址關聯的電話號碼。 |
| `shippingAddressPhone.number` | 電話號碼。 請注意，電話號碼為字串，並可能包含有意義的字元，例如括弧`()`、連字型大小`-`或表示次撥接識別碼的字元，例如分機號碼`x`，例如`1-353(0)18391111`或`+613 9403600x1234`。 |
| `shippingAddressPhone.primary` | 指出這是否為送貨地址的主要電話號碼。 值一律為`False`。 |
| `userAccount` | 表示任何熟客方案細節、偏好設定、登入流程和其他帳戶偏好設定。 |
| `userAccount.startDate` | 首次建立設定檔的日期。 |

>[!NOTE]
>
>每個設定檔記錄也包含[`identityMap`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/identitymap)欄位，其中包含系統產生的Commerce客戶ID作為設定檔的主要識別碼，以及用作次要識別碼的電子郵件ID。

瞭解如何[建立設定檔記錄特定的結構描述](profile-data.md)，以便從您的設定檔記錄擷取資料。
