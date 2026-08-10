---
title: 受限制的存取金鑰
description: 瞭解如何建立、指派和旋轉受限制的存取金鑰，以使用已簽署的權杖驗證來保護 [!DNL Adobe Commerce Optimizer] 中的目錄檢視。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 專案（Adobe管理的SaaS基礎結構）。"
TQID: https://experienceleague.adobe.com/Jmze0Pq3kSNMIXqkkML-hmmlZnv-XKgeEgRB8Q8NZ6s
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: e0eb8757-182f-49f3-94a4-1587d16f5094
nudge: true
source-git-commit: 688bc6e28a4c5a94b1fe55c84f7c05401dd651bc
workflow-type: tm+mt
source-wordcount: 791
ht-degree: 0%

---

# 受限制的存取金鑰

受限制的存取金鑰可讓授權的使用者端應用程式存取[私人目錄檢視](catalog-view.md) — 只有從指派的金鑰中攜帶有效已簽署權杖的請求才能擷取目錄資料。 所有其他請求都遭到拒絕，包括來自匿名購物者、未明確獲得此目錄檢視存取權的購物者，以及探索API的指令碼。

## 限制存取的關鍵使用案例

在[!DNL Adobe Commerce Optimizer]中，**[!UICONTROL Price Book ID]**&#x200B;會決定要求可以看到的價格 — 其範圍是定價，而非誰可以提出要求。 任何知道目錄檢視ID和價格簿ID的使用者端都可透過Merchandising API擷取該資料。 限制存取金鑰可新增個別的補充控制：限制存取金鑰可限定存取目錄檢視的使用者範圍，且不受價格簿所套用。

受限制的存取金鑰通常用於：

- **合約式B2B定價** — 限制連結至議價價格簿的目錄檢視，以便只有適用它的買方可以查詢它。 其他購買機構和公眾則不能。
- **合作夥伴與經銷商入口網站** — 將目錄的子集限製為直接與銷售API整合的已核准合作夥伴。
- **發行前預覽** — 讓受信任的內部或合作夥伴系統先預覽即將推出的產品，然後再公開顯示。

>[!IMPORTANT]
>
>金鑰產生、權杖簽署和輪換目前完全由驗證購物者的後端使用者端應用程式管理。 [!DNL Adobe Commerce Optimizer]不會代表您產生或旋轉這些金鑰。

## 受限制的存取金鑰如何運作

受限制的存取金鑰是RSA金鑰組的公開元件。 您的使用者端應用程式會產生並使用此金鑰來證明其已獲得讀取私人目錄檢視的授權。 在此內容中，「使用者端應用程式」是指可驗證購物者的後端系統（例如，[!DNL Adobe Commerce]上的自訂邏輯或第三方後端），而不是店面前端本身。

下列步驟說明金鑰組與簽署的權杖如何從建立移至驗證：

1. 您的使用者端應用程式會產生RSA金鑰組並保留私密金鑰。
1. 您在[!DNL Commerce Optimizer]中將&#x200B;**公用**&#x200B;金鑰註冊為受限制的存取金鑰。
1. 您的使用者端應用程式會使用私密金鑰簽署JSON Web權杖(JWT)，並將其隨每個對私密目錄檢視的請求納入。
1. [!DNL Commerce Optimizer]會根據已登入的公開金鑰驗證權杖的簽章，如果有效，會傳回要求的目錄資料。

## 建立受限制的存取金鑰

若要初次測試私人目錄檢視，請使用[!DNL OpenSSL]之類的工具產生金鑰組。 保留私密金鑰機密 — 僅公開金鑰上傳至[!DNL Commerce Optimizer]。

```bash
openssl genrsa -out private-key.pem 2048
openssl rsa -in private-key.pem -pubout -out public-key.pem
```

金鑰大小必須介於2048到8192位元之間。 `public-key.pem`包含您貼到下列&#x200B;**[!UICONTROL Public key]**&#x200B;欄位中的值。

## 將受限制的存取金鑰新增至[!DNL Commerce Optimizer]

1. 從[!DNL Adobe Commerce Optimizer Studio]的左側功能表，移至&#x200B;**[!UICONTROL Store setup]**，然後按一下&#x200B;**[!UICONTROL Restricted access keys]**。

   ![限制存取金鑰清單，包含[新增限制存取金鑰]按鈕](../assets/restricted-access-keys.png){width="70%" zoomable="yes"}

1. 按一下&#x200B;**[!UICONTROL Add Restricted Access Key]**。

1. 輸入金鑰詳細資料：

   ![新增限制存取金鑰表單，包含[標題]、[到期日]和[公開金鑰]欄位](../assets/restricted-access-keys-add.png){width="70%" zoomable="yes"}

   - **[!UICONTROL Title]** — 識別索引鍵的標籤，顯示在索引鍵清單和目錄檢視索引鍵選擇器中，例如`ACME Corp wholesale portal — Tier 1 pricing`。
   - **[!UICONTROL Expiration date]** — 停止接受金鑰的日期和時間(UTC)，即使對於尚未過期的權杖亦然。
   - **[!UICONTROL Public key]** — 主體公開金鑰資訊(SPKI)格式的PEM編碼RSA公開金鑰，包括`-----BEGIN PUBLIC KEY-----`和`-----END PUBLIC KEY-----`標籤。 在整個環境中必須是唯一的。

1. 按一下&#x200B;**[!UICONTROL Save]**。

建立後，金鑰便不可變動。 若要變更任何值，請刪除索引鍵並建立新值。 請參閱[旋轉金鑰](#rotate-a-key)以在沒有存取中斷的情況下完成此操作。

## 將索引鍵指派給目錄檢視

限制存取金鑰只有在已指派給啟用&#x200B;**[!UICONTROL Catalog Protection]**&#x200B;的目錄檢視後，才會限制存取。 如需設定步驟，請參閱[保護目錄檢視](private-catalog-view.md#protect-a-catalog-view)。

## 刪除金鑰

1. 在&#x200B;**[!UICONTROL Restricted access keys]**&#x200B;頁面上，找到您要移除的金鑰，然後按一下&#x200B;**[!UICONTROL Delete]**。

   如果將索引鍵指派給一或多個目錄檢視，則會出現警告，說明依賴該索引鍵的使用者端應用程式會失去存取權。 目錄檢視本身仍受到保護 — 它們不會公開存取。

1. 確認刪除。

## 旋轉索引鍵

若要在不中斷存取的情況下旋轉金鑰，請注意，目錄檢視最多可同時指派三個金鑰：

1. 產生新的金鑰組，並將新的公開金鑰新增為新的受限制存取金鑰。
1. 將新索引鍵與現有索引鍵一起指派給目錄檢視。
1. 開始使用新的私密金鑰簽署新權杖以完成金鑰變換。
1. 在新金鑰上確認所有使用者端應用程式後，請移除並刪除舊金鑰。

## 限制

檢視[目錄檢視和原則限制](../boundaries-limits.md#catalog-views-and-policies)。

## 更多相關資訊

- [私人目錄檢視](private-catalog-view.md) — 瞭解如何使用受限制的存取金鑰保護目錄檢視。

