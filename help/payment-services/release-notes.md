---
title: '[!DNL Payment Services]發行說明'
description: 檢閱發行說明，瞭解所有 [!DNL Payment Services] 發行版本的相關資訊。
exl-id: 104aa2c7-7735-4ac2-8ed1-a03cd9911273
feature: Payments, Release Notes
source-git-commit: 55b342895be0fc81511644a95c52a79bdd34fc98
workflow-type: tm+mt
source-wordcount: '3968'
ht-degree: 0%

---


# 發行說明

這些版本說明說明[!DNL Payment Services]的初始版本，包括：

![新](../assets/new.svg)新功能
![已修正問題](../assets/fix.svg)修正和改良
![已知問題](../assets/bug.svg)已知問題

如需在功能發行版本之外發行的功能變更和修正，請檢閱&#x200B;_託管服務更新_&#x200B;區段。

深入瞭解即將發行的版本、產品支援，以及哪些Adobe Commerce版本支援[!DNL Payment Services]擴充功能，請參閱Adobe Commerce [發行排程](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/schedule)和[產品可用性](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability)主題。

## 託管服務更新

這些發行說明說明說明所發生的功能變更和修正，這些變更和修正是在託管服務的定期功能發行之外發行的。

+++託管服務更新

_2025年4月25日_

![新問題](../assets/new.svg)<!-- Issue PAY-6051 -->現在，[!DNL Payment Services]儀表板會顯示目前的擴充功能版本和儀表板版本。

_2024年8月30日_

![新問題](../assets/new.svg)<!-- Issue PAY-5658 -->現在，商戶可以在[交易報表](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html)中依付款詳細資訊篩選交易，以取得更詳細且精確的付款方式資料。

_2024年7月15日_

![新問題](../assets/new.svg)<!-- Issue PAY-5571 -->現在，商戶可以在[交易報表](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html)中依Commerce客戶電子郵件篩選交易。 輸入客戶電子郵件，以篩選該特定電子郵件的交易。

_2024年7月9日_

![新問題](../assets/new.svg)<!-- Issue PAY-5488 -->現在，商戶可以在[交易報表](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html)中以欄的形式檢視Commerce客戶ID，以協助識別特定客戶所下的交易。 此外，商戶可依據此Commerce客戶ID來篩選關聯訂單的交易報表。

_2024年3月5日_

![已修正問題](../assets/fix.svg)<!-- Issue PAY-5252 -->現在，商家可以選取單一儲存格的內容，從控制面板網格複製資料。

_2023年10月10日_

![新簽發](../assets/fix.svg)<!-- Issue PAY-4888 -->現在，商家可以在[交易報表](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html)中依卡號的最後4位數篩選信用卡與借記卡交易。

_2023年7月12日_

![已修正問題](../assets/fix.svg)<!-- Issue PAY-4587 --> [!DNL Payment Services] 2.1.0版本中發生的問題，使得先前的擴充功能版本無法設定授權失效，現在已解決。 使用任何版本[!DNL Payment Services]的商家都可能使授權無效。

_2023年6月9日_

![新增](../assets/new.svg)<!-- Issue PAY-4288 -->現在，商戶只能[設定&#x200B;_個_ PayPal付款按鈕](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html#use-only-paypal-payment-buttons) — 而&#x200B;_不能_&#x200B;使用PayPal信用卡付款選項。 這可讓商家提供各種付款選項，包括Venmo和PayPal付款按鈕，並使用現有的信用卡提供者，而非PayPal信用卡付款選項。

![新](../assets/new.svg)<!-- Issue PAY-4050 -->已新增出現在付款服務首頁的[資料視覺化檢視](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html#order-payment-status-data-visualization-view)，以取得訂單付款狀態報告。

![已修正問題](../assets/fix.svg)<!-- Issue PAY-4486-->之前，英國商戶的結帳功能中並未顯示PayPal PayLater按鈕。 該問題已解決。

![已修正問題](../assets/fix.svg)<!-- Issue PAY-4485-->當停用[!DNL Payment Services]時，[!DNL Payment Services]首頁現在會出現報告資料視覺效果檢視。

_2023年1月25日_

![已知問題](../assets/bug.svg)<!-- Issue PAY-4102 --> [!DNL Payment Services]的新安裝無法設定Commerce服務，導致[!DNL Payment Services]無法操作。 若要修正此問題，請將您的[!DNL Payment Services]擴充功能更新至1.5.3版。

_2022年9月12日_

![新](../assets/new.svg)<!-- Issue PAY-3705 --> `increment_id`現在可用於調節外部ERP系統中的付款。 它會傳播到[`custom_id` _和_ `invoice_id`](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/data.html#reconcile-with-erp-system)，在PayPal webhook和商家活動詳細資訊中都可以看到付款。

_2022年8月31日_

![已修正問題](../assets/fix.svg)<!-- Issue PAY-3629 -->當新商家首次存取[!DNL Payment Services]首頁時，頁面現在會立即載入以顯示內容，而不需要重新整理頁面。

_2021年8月9日_

![新的](../assets/new.svg)<!-- Issue PAY-3420 --> Apple Pay現在可以作為PayPal智慧型按鈕使用。 此[付款選項](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-options.html#apple-pay-button)可讓客戶在其iOS或macOS裝置上使用觸控式ID功能，以選取Apple Pay。 Apple Pay會使用儲存在裝置上的信用卡和扣帳卡付款憑證來處理付款。

_2021年6月28日_

![新的](../assets/new.svg)<!-- Issue PAY-1720 -->商店訂單糾紛現在可在[訂單付款狀態報表](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html#view-disputes)中取得。 您可以從[!DNL Payment Services]直接導覽至PayPal解決中心來解決爭議。

![新](../assets/new.svg)<!-- Issue PAY-2854 --> [!DNL Payment Services]首頁的使用者體驗改善專案包含修改目前繼承層級組態的功能，以及標頭與導覽的顯示改善。

![新增](../assets/new.svg)<!-- Issue PAY-2854 -->您現在可以從沙箱模式切換至生產模式，以及嘗試離開檢視時看到警告，其中顯示尚未儲存的更新。

![新增](../assets/new.svg)<!-- Issue PAY-2761 -->您現在可以使用[資料行]設定控制項來顯示或隱藏資料行，以自訂[訂單付款狀態報表](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html#show-and-hide-columns)與[付款報表](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/payouts.html#show-and-hide-columns)中顯示的資料。

+++

>[!NOTE]
>
> 經常發行以視需要提供新功能和修正。 發行排程未修正。

## v2.11.1

_2025年3月14日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![已修正問題](../assets/fix.svg)<!-- PAY-5849 -->已修正簽出期間影響[條列專案](line-items.md)的問題。 現在，[!DNL Payment Services]已改善&#x200B;**條列專案**&#x200B;的結帳程式可靠性。 如果您遇到類似問題，請連絡您的[!DNL Payment Services]銷售代表以尋求協助。

## v2.11.0

_2025年3月13日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本


![新增](../assets/new.svg)<!-- PAY-5938 -->現在，[!DNL Payment Services]可讓商家管理付款設定，以最大化其業務的彈性。 此版本改善為商家支援的地區和品牌附加[多個PayPal帳戶](https://experienceleague.adobe.com/en/docs/commerce/payment-services/configure/settings#use-multiple-paypal-accounts)的能力。 我們的銷售團隊可提供入門連結，以設定您的網站和商店檢視範圍。

![新](../assets/new.svg)<!-- PAY-5968 -->現在，[!DNL Payment Services]會以&#x200B;**PayPal商家識別碼**&#x200B;和&#x200B;**PayPal商家狀態**&#x200B;值更新管理員設定。 這些值可讓商家更清楚瞭解其PayPal帳戶狀態。

![已修正問題](../assets/fix.svg)<!-- PAY-5816 -->已解決v2.9.0版中導致所有訂購位置發生錯誤的問題，藉此還原[!DNL Payment Services]中的正常訂購功能。

![已修正問題](../assets/fix.svg)<!-- PAY-5825 -->已修正Apple Pay迷你購物車對登入的客戶使用的預估總計URL不正確的問題。 現在，[!DNL Payment Services]可確保計算的總計準確。

![已修正問題](../assets/fix.svg)<!-- PAY-5826 -->解決將報價狀態變更為`inactive`時造成HTTP 500錯誤的問題，進而改善訂單管理的可靠性。

![已修正問題](../assets/fix.svg)<!-- PAY-5849 -->修正`LineItemProvider`擲回小數點數量低於1的例外狀況的問題。 現在，[!DNL Payment Services]為分數數量提供更好的支援。

![已修正問題](../assets/fix.svg)<!-- PAY-5868 -->已修正結帳時的禮品卡金額錯誤。 [!DNL Payment Services]現在可確保結帳程式中的值準確。

![已修正問題](../assets/fix.svg)<!-- PAY-5911 -->已解決使用非[!DNL Payment Services]個線上付款方式下訂單建立出貨時的錯誤，提升整體可靠性。

![已修正問題](../assets/fix.svg)<!-- PAY-5954 --> [!DNL Payment Services]現在解決在錢包中選取其他信用卡時Apple Pay無法下訂單的問題，提供更順暢的結帳體驗。

![已修正問題](../assets/fix.svg)<!-- PAY-5971 --> 當Apple Pay失敗時，[!DNL Payment Services]不再將客戶重新導向至訂單檢閱頁面，以防止不必要的結帳中斷。

## v2.10.3

_2025年2月24日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![已修正問題](../assets/fix.svg)<!-- PAY-xxxx -->已改善整體穩定性和效能。

![已修正問題](../assets/fix.svg)<!-- PAY-xxxx -->一般改良與最佳化。 修正v2.10.2的重大錯誤。

## v2.10.2

_2025年2月21日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![已知問題](../assets/bug.svg)<!-- PAY-xxxx -->包含可能影響穩定性和效能的重大錯誤。 Adobe建議升級至v2.10.3，而不要使用此版本(v2.10.2)。

## v2.10.1

_2025年2月5日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)<!-- PAY-5813 -->已新增對Adobe Commerce 2.4.8和PHP 8.4的支援。

## v2.10.0

_2024年12月13日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新增](../assets/new.svg)<!-- PAY-5702 --> [!DNL Payment Services]現在支援GraphQL端點進行儲存而不購買，讓客戶儲存其付款方式而不完成交易。

![新增](../assets/fix.svg)<!-- PAY-5789 --> [!DNL Payment Services]現在支援[使用Google Pay的3D安全驗證](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/payment-services/security-compliance/security#3ds)，在付款交易期間增強商家和客戶的安全性。

![修正](../assets/fix.svg)<!-- PAY-5703 --> [!DNL Payment Services]新增了[客戶直接將卡片儲存在其&#x200B;**我的帳戶**](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting)中的功能，改善了便利性，並簡化了未來的結帳。`Vault without purchase functionality might not be 100% compatible with Adobe Commerce 2.4.4 due to a known issue with` [`GraphQL authorization mechanisms`](https://developer.adobe.com/commerce/webapi/graphql/usage/authorization-tokens/)。

![修正](../assets/fix.svg)<!-- PAY-5762 -->修正從產品詳細資料頁面(PDP)起始訂單時，未在訂單稽核頁面上套用優惠券代碼的問題。

![修正](../assets/fix.svg)<!-- PAY-5792 --> [!DNL Payment Services]現在會在結帳頁面[&#128279;](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting)上顯示儲存卡的說明和帳單地址，讓客戶更清楚瞭解他們儲存的付款方式。

![修正](../assets/fix.svg)<!-- PAY-5793 --> [!DNL Payment Services]可讓商戶直接從結帳頁面儲儲存儲存儲存儲存存庫存卡的帳單地址，以確保正確且完整的付款資訊。

## v2.9.0

_2024年11月7日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新增](../assets/new.svg)<!-- PAY-5629 --> [!DNL Payment Services]現在支援Apple Pay **的**&#x200B;升級SDK URL，改善使用Apple Pay的商家整合。 此功能與macOS 14和更新版本相容，執行舊版macOS的裝置將不會顯示此功能。

![全新](../assets/new.svg)<!-- PAY-5630 -->已更新&#x200B;**結帳**、**產品**、**購物車**&#x200B;和&#x200B;**迷你購物車**&#x200B;頁面，以支援Apple Pay的&#x200B;**已升級SDK URL**，為提供Apple Pay付款選項的商家改善使用者體驗。

![新](../assets/new.svg)<!-- PAY-5635 -->改善以Apple付款地址&#x200B;**為基礎的運送預估**，讓客戶在結帳時檢視準確的運送成本。

![修正](../assets/fix.svg)<!-- PAY-5661 -->修正結帳&#x200B;**的各種**&#x200B;[!DNL Payment Services]&#x200B;問題，改善商家和購物者付款程式的可靠性。

![修正](../assets/fix.svg)<!-- PAY-5692 -->修正使用&#x200B;**智慧型按鈕進行快速簽出**&#x200B;時，**客戶的名字和姓氏**&#x200B;未新增至訂單的問題。

![修正](../assets/fix.svg)<!-- PAY-5712 -->解決當總金額為免費時，商家無法&#x200B;**使用「零小計結帳」付款選項**&#x200B;完成結帳的問題。

## v2.8.1

_2024年9月13日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![修正](../assets/fix.svg)<!-- PAY-5644 -->修正在[!DNL Payment Services]中使用多個範圍時，SDK引數快取的問題。 現在會針對每個範圍分別快取SDK設定，而非使用單一索引鍵。 這樣可確保每個範圍的快取獨立失效，進而在管理多個範圍時提高可靠性。

## v2.8.0

_2024年9月13日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新增](../assets/new.svg)<!-- PAY-5499 --> 在Adobe Commerce中輸入[追蹤號碼](track-shipment.md)時，[!DNL Payment Services]現在支援傳送追蹤號碼資訊至PayPal。

![修正](../assets/fix.svg)<!-- PAY-5626 --> 當客戶造訪Commerce結帳頁面時，[!DNL Payment Services]已針對商家登入最佳化要求流程。 之前，使用者會針對每種支付方式(託管欄位、Google Pay、Apple Pay和智慧型按鈕)分別提出要求。 這項改善會減少呼叫次數，提高結帳程式期間的效能和效率。

![修正](../assets/fix.svg)<!-- PAY-5645 --> 如果購物者不同意商家在結帳頁面上建立自訂條款與條件，[!DNL Payment Services]現在會阻止開啟PayPal/Google Pay快顯視窗。

![修正](../assets/fix.svg)<!-- PAY-5648 -->  [!DNL Payment Services]已解決與PayPal入口網站上的明細專案稅捐劃分相關的問題。 如果訂單的送貨成本有關聯稅捐，則稅捐會納入送貨成本中，並顯示在PayPal入口網站顯示的明細專案詳細資訊中。

## v2.7.0

_2024年8月2日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新增](../assets/new.svg)<!-- PAY-4844 --> [!DNL Payment Services]現在支援訂單層級[&#128279;](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/payment-services/payments-checkout/manage/line-items)的條列專案資料。 此功能可讓商家檢視訂單中專案的詳細資訊，例如產品詳細資料、數量及價格（包括銷售稅、折扣及其他相關資訊）。

![新增](../assets/new.svg)<!-- PAY-5380 --> [!DNL Payment Services]改善商家在Admin[&#128279;](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/payment-services/configure/configure-admin#general-configuration)體驗中的設定，以更簡單且更直覺的方式上線流程。 此功能可讓商家重設其[!DNL Payment Services] ID。

![新增](../assets/new.svg)<!-- PAY-5255 --> [!DNL Payment Services]包含[付款失敗通知](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/checkout/checkout-payment-failed-emails)。 此功能會近乎即時地通知商戶付款失敗，因此您可以聯絡購物者，並有可能改善問題解決方案，以儲存訂單。

![修正](../assets/fix.svg)<!-- PAY-5469 -->修正Safari **封鎖** Google Pay快顯視窗的問題。 購物者現在可以在Safari上完成其Google Pay付款交易。

![修正](../assets/fix.svg)<!-- PAY-5492 -->修正商家將自訂條款與條件新增至結帳頁面時的問題。 在[快速結帳](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options#standard-vs-advanced-payments-experience)期間，購物者現在可以接受這些條款與條件，順利完成結帳。

![修正](../assets/fix.svg)<!-- PAY-5532 -->已改善店內接送(ISPU)功能，包含&#x200B;**InstantPurchase**。 當購物者以&#x200B;**InstantPurchase**&#x200B;下訂單時，**ISPU傳遞方法**&#x200B;不再顯示。

![修正](../assets/fix.svg)<!-- PAY-5606 -->修正當商家的國家設定為&#x200B;**德國**&#x200B;時，**設定頁面**&#x200B;國家選擇器中發生的問題。

## v2.6.0

_2024年6月4日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新的](../assets/new.svg)<!-- PAY-4877 -->現在，[!DNL Payment Services]支援[L2/L3定價功能](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/levels-card-payment-transactions.html)。 此功能僅適用於已啟用IC++定價的[!DNL Payment Services]客戶。 如果您想要使用L2/L3處理[!DNL Payment Services]的資料，請連絡您的[!DNL Payment Services]帳戶管理員。

![修正](../assets/fix.svg)<!-- PAY-5455 -->[!DNL Payment Services]可讓您直接從擴充功能啟用Apple Pay，而不需下載及主控[網域關聯檔案](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain)。

## v2.5.0

_2024年4月23日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![修正](../assets/fix.svg)<!-- Issue PAY-5396 -->[!DNL Payment Services]現在支援Adobe Commerce 2.4.7或更新版本中`--db-prefix`引數[&#128279;](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/advanced#install-from-the-command-line)的Adobe Commerce准則。

## v2.4.3

_2024年4月16日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![修正](../assets/fix.svg)<!-- Issue PAY-5106 -->修正在PayPal與Adobe Commerce之間結帳時，不正確填入訂單金額總計的問題。 現在，商家可以在下訂單時確保訂單金額總計正確無誤。

## v2.4.2

_2024年4月11日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)<!-- Issue xxx -->已新增對Adobe Commerce 2.4.7的支援。

## v2.4.1

_2024年4月4日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![修正](../assets/fix.svg)<!-- PAY-5322 -->已修正較新Adobe Commerce發行版本的PCI相容性問題。 現在，[!DNL Payment Services]已改編為Adobe Commerce中的付款選項結帳要求。

在Adobe Commerce中正確顯示![Fix](../assets/fix.svg)<!-- PAY-5323 --> PayLater和Venmo。 修正管理員無法顯示PayLater和Venmo切換選項的錯誤。

## v2.4.0

_2024年3月20日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新的](../assets/new.svg)<!-- PAY-4868 -->商戶可透過管理員成功[設定Google Pay的整個購買體驗](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html)，類似於[!DNL Payment Services]中的其他付款按鈕。

![新增](../assets/new.svg)<!-- PAY-4381 --> [Payment Services透過GraphQL支援Google Pay](https://developer.adobe.com/commerce/webapi/graphql/payment-services/)，讓商戶可以使用Google Pay付款方式取得Headless Commerce體驗。

![新增](../assets/new.svg)<!-- PAY-4878 -->現在，[!DNL Payment Services]基本簽出功能已針對Adobe Commerce和Magento Open Source商家整合。[!DNL Payment Services]現在可以支援業務遍及全球200個地區的商家。[!DNL Payment Services]基本結帳在自助服務上線中提供借記/貸記、PayPal、Venmo （可用時）和PayLater （可用時）選項。

![修正](../assets/fix.svg)<!-- PAY-5291 -->某些交易的收款確認可能延遲。 在這種情況下，商家現在可以獲得訂單的更新付款狀態。 [付款服務會偵測訂單中付款交易](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html)的暫緩狀態，方法是偵測暫緩交易並主動監視這些交易，並在擷取暫緩狀態時進行更新。

## v2.3.4

_2024年3月1日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)<!-- PAY-5244 -->修正非同步簽出相容性。

![修正](../assets/fix.svg)<!-- PAY-5253 -->修正無法刪除不屬於[!DNL Payment Services]的儲存庫權杖的錯誤。

## v2.3.3

_2024年2月14日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)<!-- PAY-5048 -->已新增對PHP 8.3的支援

![修正](../assets/fix.svg)<!-- PAY-5048 -->修正`is_deleted`標幟的錯誤。 現在，訂單不會因為擴充功能傳送的`Rejected`狀態而失敗。

## v2.3.2

_2024年1月26日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![修正](../assets/fix.svg)<!-- PAY-5183 -->已修正REST/GraphQL效能問題。 現在，透過API擷取時，信用卡按鈕會呈現。

## v2.3.1

_2023年12月7日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新增](../assets/new.svg)<!-- PAY-5047 -->現在可從下列位置取得信用/扣帳卡品牌或付款方式型別：
- 店面的客戶訂單頁面
- 訂單確認電子郵件已傳送給購物者
- 從Commerce管理員的[訂單詳細資料檢視](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/order-management/orders/order-processing.html#view-an-order)。

## v2.3.0

_2023年12月1日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新增](../assets/new.svg)<!-- PAY-4381 --> [付款服務現在支援GraphQL整合](https://developer.adobe.com/commerce/webapi/graphql/payment-services/)。 透過GraphQL對PayPal付款按鈕、託管欄位和Apple Pay的支援，[!DNL Payment Services]現在可支援Headless Commerce設定。

## v2.2.1

_2023年9月27日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![修正問題](../assets/fix.svg)<!-- Issue PAY-4870 -->修正傳送具有最新版本的擴充功能版本時，Storefront中新標題屬性填入錯誤的問題。 之前，隨著Commerce服務聯結器的`1.3.0`發行，您無法從[!DNL Payment Services]擴充功能擴充`User-Agent header`。

## v2.2.0

_2023年8月30日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![New](../assets/new.svg)<!-- PAY-4638 -->已新增與Signifyd[&#128279;](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/security-compliance/fraud-protection.html)的整合，此整合提供自動化的詐騙防護服務。

![新增](../assets/new.svg)<!-- PAY-3981 --> [將Apple Pay升級為單獨的付款選項](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html?lang=en#apple-pay-button) （在PayPal付款按鈕之外），以增加購物者對付款選項的可見度，並允許商家控制Apple Pay的放置和樣式。

![新增](../assets/new.svg)<!-- PAY-4002 -->改善信用卡欄位結帳的使用者體驗，包括樣式增強功能，例如新增付款圖示，以降低購物者的認知負荷並提高轉換率。

![新增](../assets/new.svg)<!-- PAY-4002 -->新增功能，可讓商家[排序付款選項順序](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#payment-buttons)，以優先處理特定付款選項。 此功能可提高結帳對話率。

![新](../assets/new.svg)<!-- PAY-4035 -->商戶現在可以使用[!DNL Payment Services] Admin首頁提供的新[交易報告](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html)，有效監控其商店的健康狀況，並識別任何交易問題。 此報表也會顯示有關交易授權率及負數交易趨勢的資料。

## v2.1.0

_2023年6月9日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)<!-- Issue xxx -->已新增對Adobe Commerce 2.4.7-beta1的支援。

![新](../assets/new.svg)<!-- Issue xxx -->已在下列國家和相關貨幣中新增[可用性](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/overview.html#availability)：澳洲、法國、英國。

![新](../assets/new.svg)<!-- Issue PAY-4296 -->已新增管理員角色的[擴充資源](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#configure-roles)，以確保管理員使用者可以建立和管理客戶的訂單，並能在銷售功能表中看到[!DNL Payment Services]。

![新](../assets/new.svg)<!-- Issue PAY-4236 -->已針對結帳期間發生錯誤的訂單新增[自動作廢](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/checkout.html#order-auto-voided-if-error)。

![新](../assets/new.svg)<!-- Issue PAY-4183 -->已建立功能，可在結帳頁面上顯示[信用卡/扣帳卡付款選項按鈕](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html#debit-or-credit-card-button)。

## v2.0.0

_2023年3月10日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)<!-- Issue PAY-4152 -->已新增對PHP 8.2和Adobe Commerce 2.4.6的支援。與PHP 7.x不相容。

## v1.6.1

_2023年3月10日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.4或更新版本

![修正](../assets/fix.svg)<!-- Issue PAY-4226 -->修正新[!DNL Payment Services]商家無法在Admin中使用簽出功能的問題。[!DNL Payment Services]先前曾使用Commerce客戶ID，新客戶不存在此ID。

![修正](../assets/fix.svg)<!-- Issue PAY-4205 -->修正使用[PayPal選項](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html#paypal-smart-buttons)結帳時，指定的送貨地址狀態被預設稅捐設定中的狀態取代的問題。 現在，客戶可以將訂單運送至商戶稅捐設定中設定為預設狀態以外的其他狀態。

![修正](../assets/fix.svg)<!-- Issue PAY-4202 -->修正客戶無法使用`Authorize and Capture`付款動作[&#128279;](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/production.html#set-payment-services-as-payment-method)，使用卡儲存庫完成購買或刪除商店的儲存庫付款方式的問題。 以前，當客戶嘗試使用或修改其存放的信用卡時，會出現「找不到提供者儲存庫ID」錯誤。

## v1.6.0

_2023年2月17日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.0或更新版本

![新](../assets/new.svg)<!-- Issue PAY-3540 -->已針對在歐盟(EU)及英國[&#128279;](security.md#3ds)進行交易的商戶新增PCI 3DS法規遵循功能。 此額外的安全性層級要求購買者必須向其信用卡簽發者進行驗證，有助於防止線上詐騙，並且是歐盟(EU)法規要求的一部分。

![新](../assets/new.svg)<!-- Issue PAY-3609 -->已新增在Admin[&#128279;](vaulting.md#use-vaulting-in-the-admin)中啟用卡儲存的功能。 這可讓商戶使用存放的付款方式，為「管理員」中的客戶建立訂單。

## v1.5.4

_2023年1月29日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.0或更新版本

![已修正問題](../assets/fix.svg)<!-- Issue PAY-4110 -->修正買家無法使用產品頁面、迷你購物車及購物車上的付款按鈕下單的問題。 買家現在可以成功完成訂單。

## v1.5.3

_2023年1月25日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.0或更新版本

![已修正問題](../assets/fix.svg)<!-- Issue PAY-4102 -->已發佈回溯不相容已知問題的修正。 此發行版本會將服務ID延伸版本鎖定至最新穩定版本，這會重新啟用新的[!DNL Payment Services]安裝以設定Commerce Services。

## v1.5.2

_2022年12月22日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.0或更新版本

![已修正問題](../assets/fix.svg)<!-- Issue PAY-3992 -->已改善拒絕付款方式時[!DNL Payment Services]中的開立商業發票。

![已修正問題](../assets/fix.svg)<!-- Issue PAY-3999 -->[!DNL Payment Services]現在已針對使用[Fire Checkout的](https://commercemarketplace.adobe.com/swissup-firecheckout.html){target=_blank}結帳頁面自訂範本的商家，正確顯示PayPal付款按鈕。 之前，迷你圖會斷斷續續地顯示按鈕。

## v1.5.1

_2022年11月23日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.0或更新版本

![新](../assets/new.svg)<!-- Issue PAY-3923 -->[!DNL Payment Services]現在包含使用者代理程式標題中的版本號碼，以便要求可以追蹤、篩選或淘汰未使用的端點。

![已修正問題](../assets/fix.svg)<!-- Issue PAY-3968 -->[!DNL Payment Services]現在當使用付款按鈕從產品頁面下訂單時，可正確顯示訂單資料。

## v1.5.0

_2022年11月18日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.0或更新版本

![新](../assets/new.svg)<!-- Issue PAY-3880 -->購物者現在可以在結帳時[儲存其信用卡資訊](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting.html)，以便稍後為相同商家帳戶內的相同或其他商店購買。

![新](../assets/new.svg)<!-- Issue PAY-3950 -->商戶現在可以為其商店啟用[立即購買Commerce功能](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/point-of-purchase/checkout-instant-purchase.html)，讓購物者可以（使用[保管式信用卡資訊](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting.html)）加快結帳速度。

## v1.4.1

_2022年10月14日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.0或更新版本

![修正](../assets/fix.svg)<!-- Issue PAY-3766 -->當客戶的付款方式遭到拒絕時，可見的錯誤訊息更具描述性。 它建議客戶重新輸入付款資訊，然後再試一次、嘗試其他付款方式，或就拒絕的交易聯絡其銀行。

## v1.4.0

_2022年9月30日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.0或更新版本

![新](../assets/new.svg)<!-- Issue PAY-784 -->[!DNL Payment Services]現在包含設定商家帳戶以[使用多個PayPal企業帳戶](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#use-multiple-paypal-accounts)的功能。 這可讓商家使用不同的貨幣在多個國家經營您的商店，或是將Adobe Commerce用於您的一部分業務。

![新的](../assets/new.svg)<!-- Issue PAY-3231 -->商戶可以[將[!UICONTROL Soft Descriptor]](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#add-soft-descriptor)新增至客戶交易銀行對帳單上顯示的網站或個別商店檢視設定，以描述品牌、商店或產品線。

![新增](../assets/new.svg)<!-- Issue PAY-3707 --> [啟用或停用信用卡欄位和PayPal付款按鈕](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#configure-payment-options)，以便在[!DNL Payment Services]設定中結帳。

![已修正問題](../assets/fix.svg)<!-- Issue PAY-3546 -->當客戶按一下&#x200B;**[!UICONTROL Edit cart]**&#x200B;時，頁面會重新導向至購物車頁面並顯示更新的專案，而非顯示空的購物車。

## v1.3.1

_2022年9月6日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.0或更新版本

![已修正問題](../assets/fix.svg)<!-- Issue PAY-3663 -->現在，當商戶的商店擷取授權為非全域貨幣的訂單時，擷取處理作業會完成，且不會顯示任何錯誤。

## v1.3.0

_2022年8月9日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.0或更新版本

![新的](../assets/new.svg)<!-- Issue PAY-XX -->一般可用性版本 — [!DNL Payment Services]現在[由 [!DNL Adobe Commerce] 和 [!DNL Magento Open Source] 版本2.4.0到2.4.5](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability)支援。

![已修正問題](../assets/fix.svg)<!-- Issue PAY-x --> Apple Pay現在相容於行動裝置和案頭上的Safari瀏覽器v15.5。

## v1.2.0

_2022年6月29日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.0或更新版本

![已知問題](../assets/bug.svg)<!-- Issue PAY-x --> Apple Pay與行動裝置和桌上型電腦上的Safari瀏覽器v15.5不相容。 使用Safari 15.5版時，您無法透過Apple Pay完成結帳。

![已修正問題](../assets/fix.svg)<!-- Issue PAY-3264 -->之前，當登入使用者為其帳戶選取預設地址以外的帳單/運送地址時，簽出失敗。 現在會傳送選取的帳單/運送地址（而不是預設的儲存地址），並成功完成結帳。

![已修正問題](../assets/fix.svg)<!-- Issue PAY-3314 -->如果您停用PayPal付款按鈕以進行結帳，則不會顯示任何錯誤。

![已修正問題](../assets/fix.svg)<!-- Issue PAY-3330 -->當訪客使用者輸入包含破折號的電話號碼時，結帳期間付款不再失敗。

![已修正問題](../assets/fix.svg)<!-- Issue PAY-3338 PAY-2502 -->當Commerce Services認證無效時，[!DNL Payment Services]現在會從Admin的[!DNL Payment Services]首頁顯示認證錯誤，以警示您。

![已知問題](../assets/bug.svg)<!-- Issue PAY-0 --> [!DNL Payment Services]與`commerce-data-export` v101.20和更新版本不相容，這會使其與[[!DNL Channel manager] 擴充功能](https://experienceleague.adobe.com/docs/commerce-channels/channel-manager/guide-overview.html)不相容。

## v1.1.0

_2022年3月31日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.0或更新版本

![新的](../assets/new.svg)<!-- Issue PAY-2127 -->一般可用性版本 — [!DNL Payment Services]現在[由 [!DNL Adobe Commerce] 和 [!DNL Magento Open Source] 版本2.4.0到2.4.4](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability)支援。

![新](../assets/new.svg)<!-- Issue PAY-2682 -->加拿大商戶現在可以使用[!DNL Adobe Commerce]和[!DNL Magento Open Source]的[!DNL Payment Services]延伸模組。 商戶可以使用[法文](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/overview.html?lang=fr#carte-de-cr%C3%A9dit-et-devises-accept%C3%A9es)或[英文](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/overview.html#accepted-credit-cards-and-currencies)檢視付款組態。

![新增](../assets/new.svg)<!-- Issue PAY-2681 --> [!DNL Payment Services]在信用卡與PayPal交易上支援[加幣(CAD)](introduction.md#accepted-credit-cards-and-currencies)。

![新的](../assets/new.svg)<!-- Issue PAY-2680 -->商戶可以[以英文或法文加入 [!DNL Payment Services]](onboard.md)延伸功能。

![新](../assets/new.svg)<!-- Issue PAY-2678 -->商戶現在可以檢視加拿大元(CAD)的財務報表，包括[訂單付款狀態](order-payment-status.md)和[付款報表](payouts.md)。

![已修正的問題](../assets/fix.svg)<!-- Issue PAY-2710 -->[!DNL Payment Services]現在與[PHP 8.1](https://www.php.net/releases/8.1/en.php)相容。

![已修正問題](../assets/fix.svg)<!-- Issue PAY-3017 -->已改善沙箱模式警報，以在多個存放區中顯示適當的警報。

![已修正問題](../assets/fix.svg)<!-- Issue PAY-2742 -->您現在可以在商店檢視層級啟用和停用可用的付款方法，例如Venmo。 之前，您只能為每個網站設定付款方法。

![已修正問題](../assets/fix.svg)<!-- Issue PAY-2277 -->您現在可以選擇性地啟用或停用個別PayPal付款按鈕[&#128279;](settings.md#payment-buttons)。

![已修正問題](../assets/fix.svg)<!-- Issue PAY-2561 -->先前移除的產品未出現在&#x200B;_檢閱訂單_&#x200B;頁面的購物車中。

![已知問題](../assets/bug.svg)<!-- Issue PAY-2842 -->在沙箱環境中處理付款時，透過PayPal測試信用卡交易[可能會失敗](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-cc-sandbox-failure.html)。

## v1.0.0

_2021年11月29日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.0或更新版本

![新的](../assets/new.svg)<!-- Issue PAY-2127 -->一般可用性版本 — [[!DNL Payment Services]](https://commercemarketplace.adobe.com/magento-payment-services.html)現在由[!DNL Adobe Commerce]和[!DNL Magento Open Source]版本2.4.0到2.4.3-p1支援。

![新](../assets/new.svg)<!-- Issue PAY-124 -->可在雲端基礎結構[&#128279;](install.md#adobe-commerce-on-cloud-infrastructure)或[內部部署](install.md#on-premises)執行個體上為[!DNL Adobe Commerce] 安裝[!DNL Adobe Commerce]和[!DNL Magento Open Source]的[!DNL Payment Services]延伸模組。 這些方法需要使用指令行介面。

![新增](../assets/new.svg)<!-- Issue PAY-1986 --> [!DNL Payment Services]支援[沙箱帳戶](sandbox.md)，可讓商家在測試模式中評估擴充功能。

![新的](../assets/new.svg)<!-- Issue PAY-666 -->商戶可以[以基本付款行為設定付款服務](settings.md)延伸模組，例如利用[`Authorize and Capture`](production.md#set-payment-services-as-payment-method)在沙箱或生產環境之間切換。

![新](../assets/new.svg)<!-- Issue PAY-780 -->您的購物者可以使用[!DNL Payment Services]或透過[手動建立訂單](create-order.md)結帳。

![新的](../assets/new.svg)<!-- Issue PAY-1856 -->透過[訂單付款狀態](order-payment-status.md)和[付款報告](payouts.md)提供的綜合報告可供[!DNL Payment Services]使用，讓您清楚瞭解商店的訂單和相關付款。

![新增](../assets/new.svg)<!-- Issue PAY-311 --> [!DNL Payment Services]支援彈性階層式定價（根據總處理量），適用於任何商家。

![新增](../assets/new.svg)<!-- Issue PAY-1443 -->您可以輕鬆[自訂[!DNL Payment Services]分機的PayPal付款按鈕和信用卡欄位的外觀與風格](payments-options.md)。

![已知問題](../assets/bug.svg)<!-- Issue PAY-2473 -->在安裝擴充功能期間使用[不正確的撰寫器金鑰](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-install.html)，會導致使用者無法[使用正確的`MAGEID`驗證](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)。

![已知問題](../assets/bug.svg)<!-- Issue PAY-2474 --> [!DNL Payment Services]報告[可能無法立即同步](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-report-info-delayed.html)。

![已知問題](../assets/bug.svg)<!-- Issue PAY-2475 -->如果您在上線期間建立您的[!DNL Payment Services]的[PayPal沙箱帳戶](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-paypal-acct.html)，則無法驗證該帳戶。
