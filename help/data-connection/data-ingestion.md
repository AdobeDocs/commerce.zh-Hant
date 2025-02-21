---
title: Commerce資料型別
description: 瞭解您可以收集並傳送至Experience Platform的資料型別。
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Commerce資料型別

[Data Connection擴充功能](overview.md)會將您的Commerce資料連線到Experience Platform。 打算用於Experience Platform的資料會分組為兩種行為型別：屬於&#x200B;**體驗事件**&#x200B;類別的時間序列資料，以及屬於&#x200B;**個人設定檔**&#x200B;類別的記錄資料。

深入瞭解Experience Platform中的[資料行為](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html#data-behaviors)和[類別](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html#class)。

## 時間序列資料

時間序列資料提供記錄主體直接或間接執行動作時的系統快照。 例如，當購物者瀏覽您網站上的產品時、新增產品至購物車、下訂單等等。 使用類別設為&#x200B;**體驗事件**&#x200B;的結構描述將時間序列資料擷取到Experience Platform。

### 已擷取的時間序列資料

請參閱[行為事件](events.md)和[後台事件](events-backoffice.md)，以瞭解在產生時間序列事件時擷取了哪些資料。

### 擷取時間序列事件資料所需的結構描述

瞭解如何[建立結構描述](update-xdm.md)，以擷取行為和後台時間序列事件資料。

## 記錄資料

記錄資料提供有關主旨屬性的資訊。 主旨可以是組織或個人。 例如，您網站上的購物者會建立帳戶，並產生記錄資料。 此資料是使用類別設定為&#x200B;**個別設定檔**&#x200B;的結構描述擷取到Experience Platform中。 您可以將該記錄資料傳送至Adobe的設定檔管理和細分服務： [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html)。

### 已擷取的設定檔記錄資料

檢視[客戶個人檔案記錄資料](events-profilerecord.md)，以瞭解產生個人檔案記錄時所擷取的資料。

### 擷取設定檔記錄資料所需的結構描述

瞭解如何[建立可內嵌設定檔記錄資料的結構描述](profile-data.md)。
