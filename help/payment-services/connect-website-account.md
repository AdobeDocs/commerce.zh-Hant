---
title: 為網站連線其他PayPal帳戶
description: 在管理員中完成網站範圍內的PayPal上線，將不同的PayPal商家帳戶連結至個別網站。
role: Admin, User
level: Intermediate
feature: Payments, Checkout, Configuration, Paas, Saas
TQID: 'https://experienceleague.adobe.com/U1zGAU6vYKjk2tc2KXnvyqnYdbA2HKTCNZSKhHdS0Vw'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: bd989d82-1e15-4534-88db-f1f51dd77ffaid: dac87252-6066-4d6e-a9d2-f6d84c323de7
source-git-commit: d754c71e287d7d9ff297dd7d95efbaaae7ffc2fc
workflow-type: tm+mt
source-wordcount: 393
ht-degree: 0%

---

# 為網站連線其他PayPal帳戶

針對具有&#x200B;**多個網站**&#x200B;的Commerce執行個體，您可能需要&#x200B;**不同的PayPal商家帳戶**。 [!DNL Payment Services]在&#x200B;**全域**&#x200B;上線後啟用&#x200B;**網站範圍** PayPal上線。

>[!NOTE]
>
> 此功能僅支援連線新帳戶。

## 網站範圍內上線的先決條件

只有當您的商店符合以下要求時，才可使用網站層級的上線：

- [Commerce Services Connector](https://experienceleague.adobe.com/en/docs/commerce/user-guides/integration-services/saas)安裝完成。
- PayPal帳戶已連線至全域（預設設定）範圍。

您可以檢查下列欄位是否已填入預設範圍，以確認此動作：

- [!UICONTROL Payment Services Sandbox ID]
- [!UICONTROL Payment Services Production ID]
- [!UICONTROL PayPal Merchant ID]

如果這些欄位是空的，您必須先[完成全域上線](configure-admin.md)。 在您完成必要條件之前，**[!UICONTROL Connect different account]**&#x200B;按鈕會停用。

## 啟動網站層級連線

1. 在&#x200B;_Admin_&#x200B;側邊欄上，前往&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**>**[!UICONTROL Sales]**並選擇&#x200B;**[!UICONTROL Payment Methods]**。
1. 在左上角的範圍選取器中，從&#x200B;**[!UICONTROL Default Config]**&#x200B;切換至您想要上線的&#x200B;**[!UICONTROL Website]**。
1. 按一下&#x200B;**[!UICONTROL Connect different account]**。

   如果停用此按鈕，表示您的存放區不符合上述[必要條件](#prerequisites-global-scope)。

## 完成入門強制回應視窗

隨即開啟快顯視窗。

1. 從下拉式清單中選取您的&#x200B;**[!UICONTROL Country]**。
1. 選擇您的上線型別： **[!UICONTROL Basic]**&#x200B;或&#x200B;**[!UICONTROL Advanced]**。
1. 按一下&#x200B;**[!UICONTROL Next]**。

>[!NOTE]
>
> 如果您正在匈牙利、西班牙或奧地利上線，則必須開啟並檢視條款與條件連結，然後才能按一下&#x200B;**[!UICONTROL I Accept]**&#x200B;按鈕。 在您開啟條款與條件之前，按鈕為停用狀態。

## 登入PayPal

在您重新導向到PayPal登入後，請登入並完成PayPal中的上線步驟。

>[!IMPORTANT]
>
> 按一下&#x200B;**[!UICONTROL Confirm and Continue]**&#x200B;後，您全域範圍的工作階段就會結束，網站層級的連線就會開始。 如果您不小心按了&#x200B;**[!UICONTROL Connect different account]**，可以選取&#x200B;**[!UICONTROL Cancel]**&#x200B;或在確認前按一下&#x200B;**X**&#x200B;圖示來取消。

## 完成並返回管理員

1. 完成PayPal步驟之後，請關閉PayPal視窗。
1. 按一下&#x200B;**[!UICONTROL Finish]**&#x200B;或右上角的&#x200B;**X**&#x200B;以關閉入門快顯視窗。
1. Commerce設定頁面會自動重新整理。

## 確認結果

頁面重新整理後，請檢查網站範圍設定頁面：

- 已更新該網站的&#x200B;**[!UICONTROL PayPal Merchant ID]**。
- 顯示上線結果的狀態標籤：

| 狀態 | 含義 |
| --- | --- |
| `ACTIVE` | 成功完成上線 |
| `PENDING` | 上線仍在處理中 |
| `ERROR` | 上線未成功完成 |

如果您看到`ERROR`狀態，則會顯示說明問題的錯誤訊息。 您可以再次按一下「**[!UICONTROL Connect different account]**」以重試上線程式。
