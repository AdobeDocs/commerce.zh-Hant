---
title: 測試並部署商店履行
description: 測試計畫以驗證「商店履行」功能。 測試涵蓋「存貨同步API」、已取消訂單的端對端履行工作流程、「商店履行」應用程式使用者管理，以及「客戶簽入」體驗。
role: User, Admin
level: Intermediate
feature: Shipping/Delivery, User Account, Roles/Permissions
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '2661'
ht-degree: 0%

---

# 測試並部署Adobe Commerce的商店履行

在開發環境中完成入門流程後，您可以開始該流程，以測試並將Store Fulfillment解決方案部署到生產環境。

**必要條件**

在測試或同步任何資訊、儲存區或訂單之前，請先確認您已完成下列工作：

- 已完成Store Fulfillment服務的[一般設定](enable-general.md)。

- [新增並驗證沙箱和生產環境的帳戶憑證和連線詳細資訊](connect-set-up-service.md#configure-store-fulfillment-account-credentials)

- 確認Store Fulfillment解決方案的[Adobe Commerce整合](connect-set-up-service.md#configure-store-fulfillment-account-credentials)可用且已獲得授權。

## 準備測試

必須先完成連線設定，然後才能建立任何測試訂單或執行整合測試。 在測試之前，您也必須驗證您的存放區資料是否已同步。

1. 同步化存放區履行來源。

   - 移至&#x200B;**[!UICONTROL Stores > Sources]**。

   - 選取&#x200B;**[!UICONTROL Synchronize Store Fulfillment Sources]**。

1. 在建立測試訂單之前，從商店網格確認商店已標示為`Synced`。

## 範例測試計畫

零售商會在部署的組態與測試階段，驗證「商店履行」解決方案的基本功能。 此範例測試計畫提供測試的起點。 根據您的需求新增其他案例。

>[!NOTE]
>
>完成Store Fulfillment解決方案的初始入門或更新現有安裝後，一定要先在非生產環境中測試應用程式，然後再部署到生產環境。

此範例測試計畫涵蓋下列功能區域：

| 功能區域 | 函式 | 角色 |
|-------------------------------------|------------------------------------------|----------------------------------|
| 存貨與訂單同步化 | 庫存API同步 | Adobe Commerce管理員 |
| 端對端 | 訂單取消工作流程 | 客戶、管理員、商店關聯 |
| 管理員 | 商店履行應用程式許可權 | 管理員 |
| Adobe Commerce前端 | 產品型別 | 客戶、管理員 |
| 前端簽出</br>簽入表單 | 簽到體驗 | 客戶、管理員 |
| 商店協助應用程式 | 訂單</br>挑選</br>階段</br>和移交 | 存放區關聯 |

### 庫存API同步

測試計畫的這個區段涵蓋存貨與訂單同步化，以確認取貨來源與存貨的更新在Adobe Commerce與「商店履行」解決方案之間已正確同步。

**功能區域**：庫存與訂單同步處理</br>
**角色：**&#x200B;管理員</br>
**測試型別：**&#x200B;全部為正數

<table>
<thead>
<tr>
<th>函式</th>
<th>測試案例</th>
<th>預期結果</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>新增取車庫存來源</strong></td>
<td>儲存新的取車庫存來源。</td>
<td>即時同步會在5分鐘內將來源詳細資料傳送至Walmart GIF服務。</td>
</tr>
<tr>
<td><strong>更新現有的取貨存量來源</strong></td>
<td>將更新儲存至現有的取車庫存來源。</td>
<td>即時同步作業會在5分鐘內將詳細資料傳送至Walmart GIF</td>
</tr>
<tr>
<td><strong>取貨庫存來源</br><code>Is Synced</code>狀態</strong></td>
<td>將更新儲存至現有的取車庫存來源。</td>
<td>成功作業後，「管理Source」頁面的<code>Is Synced</code>欄會從<code>No</code>更新為<code>Yes</code>。</td>
</tr>
<tr>
<td><strong>已修改的庫存預留程式</strong></td>
<td>建立並提交產品的新訂單。</td>
<td>產品的可銷售數量會因此減少。</td>
</tr>
<tr>
<td><strong>新訂單推送、API同步 — 客戶訂單</strong></td>
<td>客戶提交商店取貨訂單。</td>
<td><ul><li>在「管理員訂單」檢視中，<strong>Adobe Commerce管理員使用者</strong>看到「訂單同步」狀態更新為 <code>Sent</code></li><li>訂單詳細資訊記錄包含訊息 <code>Order was sent to BOPIS solution for sync, it's not yet acknowledged yet.</code></li></ul></td>
</tr>
<tr>
<td><strong>新訂單推送、API同步 — 管理員提交訂單</strong></td>
<td>Adobe Commerce <strong>管理員</strong>提交取車訂單。</td>
<td><ul><li>在「管理訂單」檢視中，「訂單同步」狀態會更新為<code>Sent</code>。</li><li>訂單詳細資訊記錄包含訊息 <code>Order was sent to BOPIS solution for sync, it's not yet acknowledged yet.</code></li></ul></td>
</tr>
<tr>
<td><strong>新訂單推送，例外佇列<strong></td>
<td>識別Adobe Commerce管理員中的多項虛擬和可下載產品，可透過Adobe Commerce完成，無需與Fulfillment服務(FaaS)互動。</td>
<td>這些產品在匯出時會適當地移除或加上標籤，以防止下游與FaaS發生衝突。</td>
</tr>
</tbody>
</table>

### 訂單取消工作流程

測試計畫的這個區段包含案例，用於測試透過Adobe Commerce取消的訂單的端對端工作流程。

**功能區域：** Adobe Commerce管理員</br>
**角色：**&#x200B;端對端（管理員、商店關聯、客戶）</br>
**測試結果型別：**&#x200B;所有案例皆為正數

<table style="table-layout:fixed">
<tr>
<th>函式</th>
<th>情境</th>
<th>預期結果</th>
</tr>
<tr>
<td><strong>完整訂單取消</strong></td>
<td><ol>
<li>下單。</li>
<li>等候訂單同步處理。</li>
<li>驗證發票電子郵件的收據建立（若授權並擷取）。</li>
<li>從「商業發票」檢視表，建立包含所有訂購產品的「銷退折讓單」。</li>
</ol>
</td>
<td>
<ul>
<li>已使用<code>We refunded $X online. Transaction ID: transactionID</code>和更新訂單歷史記錄 <code>Received Cancel acknowledgment from the BOPIS solution.</code></li>
<li>訂單狀態為<code>Closed</code>。 （我們已設定「立即付款稽核」。）</li>
<li>在Adobe Commerce中建立的銷退折讓單。 （等到cron運作為止。）</li>
<li>如果選取所有專案，則準備接收電子郵件<code>DISPLAY COMMENT HISTORY</code>會顯示<code>Order is ready for pickup</code> （<code>CUSTOMER NOTIFIED</code>旗標為<code>true</code>）。</li>
<li>如果未挑選所有專案，則會顯示取消電子郵件與顯示註解歷程記錄 <code>Order has been canceled - all items were not available</code></li>
<li><code>CUSTOMER NOTIFIED</code> 標幟是<code>true</code>。)</li>
</ul>
</td>
</tr>
<tr><td><strong>部分訂單取消<strong></td>
<td>
<ol>
<li>訂購至少兩種產品。</li>
<li>等候訂單同步處理。</li>
<li>檢查是否已建立發票（如果授權並擷取）以及是否收到發票電子郵件。</li>
<li>等候兩小時進行交易結算。</li>
<li>從「商業發票」檢視中，建立僅含部分訂購產品的「銷退折讓單」。</li>
</td>
<td>
<ul>
<li>訂單歷史記錄更新： <code>We refunded $X online. Transaction ID: transactionID</code></li>
<li>訂單歷史記錄更新： <code>Order notified as partly canceled at: Date and Hour</code></li>
<li>收到訂單退款電子郵件： <code>$x amount was refunded</code></li>
<li>訂單狀態為<code>Processing</code>。</li>
<li>在Adobe Commerce中建立的銷退折讓單（等待cron運作）。</li>
<li>如果未挑選某些專案，請確認已顯示包含nil挑選或退款區段的[!UICONTROL Ready for Pickup]電子郵件。 <code>DISPLAY COMMENT HISTORY</code>顯示<code>Order is ready for pickup, but some items not available.</code>。</li>
<li><code>CUSTOMER NOTIFIED</code> 標幟是<code>true</code>。</li>
</ul>
</td>
</tr>
<td><strong>準備取貨</br></br>完全取消</br> （所有產品都設定為0數量取貨）</strong></td>
<td>
<ol>
<li>下訂單。</li>
<li>等候訂單同步處理。</li>
<li>檢查是否已建立發票（如果授權並擷取）以及是否收到發票電子郵件。</li>
<li>移至Postman，並使用所有設定為<code>picked</code>且有<code>0 qty</code>的產品執行「準備好取貨」請求。</li>
</ol>
</td>
<td>
<ul>
<li>已更新訂單歷史記錄： <code>We refunded $X offline</code></li>
<li>訂單狀態為<code>CLOSED</code>。
<li>已建立銷退折讓單。 （等到cron運作為止。）</li>
<li>已收到退款電子郵件： <code>$x amount was refunded</code></li>
<li>已傳送訂單取消電子郵件。</li>
</ul>
</td>
</tr>
<tr>
<td><strong>準備取貨 — 部分取消</strong></br></br><strong>（部分產品已取貨，部分產品已使用<code>0 qty</code>取貨）</strong>
</td>
<td>
<ol>
<li>下訂單。</li>
<li>等候訂單同步處理。</li>
<li>檢查是否已建立發票（如果授權並擷取）以及是否收到發票電子郵件。</li>
<li>前往Postman並執行「準備取貨」請求，將部份產品設定為0數量，其餘產品則已取貨。</li>
</ol>
</td>
<td>
<ul>
<li><code>Your order is ready for pickup</code> [!UICONTROL Ready for Pickup Items]和[!UICONTROL Canceled Items]資料表。 </li>
<li>訂單狀態為準備取貨。 </li>
<li>已更新訂單歷史記錄： <code>We refunded $X offline.</code>
<li>已更新訂單歷史記錄： <code>Order notified as partly canceled at: Date and hour</code>
<li>已收到退款電子郵件： <code>$x amount was refunded</code>
<li>已建立銷退折讓單。 （等到cron運作為止。）</li>
</ul>
</td>
</tr>
<tr>
<td><strong>準備取貨 — 部分取消</br></br>部分產品已取貨，部分產品已使用<code>0 qty</code>取貨</strong>
</td>
<td><ol>
<li>下訂單。</li>
<li>等候訂單同步處理。</li>
<li>檢查是否已建立發票（如果授權並擷取）以及是否收到發票電子郵件。</li>
<li>前往Postman並執行「準備取貨」請求，將部份產品設定為0數量，其餘產品則已取貨。</li>
</ol>
</td>
<td><ul>
<li><code>Your order is ready for pickup</code> [!UICONTROL Ready for Pickup Items]和[!UICONTROL Canceled Items]資料表。 </li>
<li>訂單狀態為準備取貨。 </li>
<li>已更新訂單歷史記錄： <code>We refunded $X offline.</code>
<li>已更新訂單歷史記錄： <code>Order notified as partly canceled at: Date and hour</code>
<li>已收到退款電子郵件： <code>$x amount was refunded</code>
<li>已建立銷退折讓單。 （等到cron運作為止。）</li>
</ul>
</td>
</tr>
<tr>
<td><strong>已發放（在發放期間） </br></br>完全取消（所有產品都設定為已拒絕）</strong>
</td>
<td>
<ol>
<li>下訂單。</li>
<li>等候訂單同步處理。</li>
<li>檢查是否已建立發票（如果授權並擷取）以及是否收到發票電子郵件。</li>
<li>前往Postman並執行「準備好取貨」請求，將所有產品設定為「已取貨」。</li>
<li>開啟您的信箱，找到[準備好取件]電子郵件。 然後，按一下&#x200B;**[!UICONTROL Confirm Arrival]**。</li>
<li>簽入。</li>
<li>前往Postman並使用設定為已拒絕的所有產品執行Dispensed請求。</li>
</ol>
<td><ul>
<li>已更新訂單歷史記錄： <code>We refunded $X offline.</code></li>
<li>已收到退款電子郵件： <code>$x amount was refunded</code></li>
<li>狀態已設定為<code>CLOSED</code>。</li>
<li>已建立銷退折讓單。 （等到cron運作為止。）</li>
</ul>
</td>
</tr>
<tr>
<td><strong>已分配（分配期間）</br></br>部分取消</br>（已分配部分產品；已拒絕部分產品。）</strong>
</td>
<td>
<ol>
<li>下訂單。</li>
<li>等候訂單同步處理。</li>
<li>檢查是否已建立發票（如果授權並擷取）以及是否收到發票電子郵件。</li>
<li>前往Postman，執行「準備好取貨」請求，並將所有產品設定為「已取貨」。</li>
<li>開啟您的信箱。 尋找「準備好取貨」電子郵件，並選取<code>Confirm Arrival</code>。</li>
<li>簽入。</li>
<li>前往Postman，執行Dispensed請求，並將部分產品設定為dispensed，並將部分產品設定為rejected</li>
</ol>
</td>
<td>
<li>已更新訂單歷史記錄： <code>We refunded $X offline</code></li>
<li><code>Order notified as partly canceled at: Date and Hour</code>
<li>已收到退款電子郵件： <code>$x amount was refunded</code>
<li>訂單狀態已設定為<code>Ready for pickup Dispensed</code>
<li>已建立銷退折讓單。 （等到cron運作為止。）</li>
</td>
</tr>
<tr>
<td> 傳回後的<strong>新RMA （完整）</strong>
</td>
<td>
<ol>
<li>下訂單。</li>
<li>等候訂單同步處理。</li>
<li>如果已設定授權與擷取選項，請確認已建立商業發票，且客戶已收到商業發票電子郵件。</li>
<li>選擇所有具有Postman的產品。</li>
<li>簽入。</li>
<li>進行分配。</li>
<li>前往訂單，然後選取<strong>[!UICONTROL Create returns]=
<li>建立RMA。</li>
</ol>
</td>
<td>
<ul>
<li>已建立RMA，並顯示在「訂單」檢視的<strong>[!UICONTROL Returns]</b>標籤下方。</li>
<li>客戶已收到RMA確認電子郵件。</li>
</ul>
</td>
</tr>
<tr>
<td>傳回後的<strong>新RMA — 部分</strong>
</td>
<td>
<ol>
<li>下訂單。</li>
<li>等候訂單同步處理。</li>
<li>檢查是否已建立發票（如果授權並擷取）以及是否收到發票電子郵件。</li>
<li>選擇所有具有Postman的產品。</li>
<li>簽入。</li>
<li>進行分配。</li>
<li>移至順序，然後選取「 」  <strong>[!UICONTROL Create returns]</strong></li>
<li>使用部分訂購產品建立RMA。</li>
</ol>
<td>
<ul>
<li>RMA已建立並顯示在訂單檢視的<strong>[!UICONTROL Returns]</strong>標籤下方。</li>
<li>客戶已收到RMA確認電子郵件。</li>
<li>建立RMA之後，取得RMA授權：從管理員移至<strong>[!UICONTROL Sales > Returns]</strong>。 選取您建立的RMA並加以授權。</li>
<li>確認客戶已收到RMA授權確認電子郵件。</li>
<li>檢查退款是否已新增至交易與訂單歷史記錄。</li>
</ul>
</td>
</tr>
</table>


### 商店履行應用程式許可權

測試計畫的這個區段涵蓋「商店履行」應用程式使用者的帳戶管理。

- 確認商店關聯可使用從Adobe Commerce管理員建立的新使用者帳戶進行驗證。
- 確認已成功套用現有帳戶的更新。

**功能區域：** Adobe Commerce管理員</br>
**角色：**&#x200B;管理員，商店關聯</br>
**測試型別：**&#x200B;全部為正數

<table style="table-layout:auto">
<tr>
<th>函式</th>
<th>情境</th>
<th>預期結果</th>
</tr>
<tr>
<td><strong>使用者帳戶管理 — 建立帳戶</strong></br></br>
</td>
<td>
<ol>
<li><strong>管理員</strong> — 登入Adobe Commerce管理員</li>
<li>移至<strong>[!UICONTROL System] &gt; Store Fulfillment App Permissions &gt;所有Store Fulfillment App使用者</strong></li>
<li><strong>新增使用者。</strong></li>
</ol>
<td>
<ul>
<li>已成功建立帳戶。</li>
<li>新的使用者帳戶會顯示在[!UICONTROL Store Fulfillment Users]儀表板上。</li>
<li><strong>市集關聯</strong>使用新的使用者帳戶登入市集協助應用程式。</li>
</ul>
</td>
</tr>
<tr>
<td><strong>使用者帳戶管理 — 更新現有的使用者帳戶</strong>
</td>
<td>
<ol>
<li>使用管理員使用者帳戶登入Adobe Commerce管理員。</li>
<li>移至<strong>[!UICONTROL System] &gt; Store Fulfillment App許可權&gt;所有Store Fulfillment App使用者</strong>。</li>
<li>在使用者帳戶清單中，選取<strong>[!UICONTROL Edit]</strong>以開啟現有的使用中使用者帳戶。
<li>將<strong>[!UICONTROL Is Active]</strong>變更為<strong>否</strong>以停用帳戶。</li>
</ol>
</td>
<td>
<ul>
<li>在<strong>[!UICONTROL Store Fulfillment App Users]</strong>儀表板上，已更新帳戶的狀態變更為<strong>[!UICONTROL Inactive]</strong>。</li>
<li>Store Associate無法使用非使用中的帳戶認證登入Store Assist應用程式。</li>
</ul>
</td>
</tr>
</table>

## Adobe Commerce產品型別

Adobe Commerce產品型別的測試案例會驗證客戶是否看到不同產品型別的正確產品、庫存和傳遞方法資訊：

- [!UICONTROL Configurable]
- [!UICONTROL Grouped]
- [!UICONTROL Virtual]
- 在Adobe Commerce店面中的[!UICONTROL Bundle products]。

**功能區域：** Adobe Commerce前端</br>
**角色：**&#x200B;商店協助應用程式使用者（商店關聯）</br>
**測試型別：**&#x200B;全部為正數

<table style="table-layout:auto">
<tr>
<th>函式</th>
<th>情境</th>
<th>註解</th>
</tr>
<tr>
<td><strong>可設定的產品</strong>
</td>
<td>
<ul>
<li>確認使用者只能看到這些可設定的選項，包括已啟用來源、已指定庫存以及庫存中有某些專案 — 檢查子產品。</li>
<li>確認選取其他存放區時，不可用的選項會顯示為已勾選。</li>
<li>確認如果使用者選取不同的商店，則會取消選取可設定的選項。</li>
<li>確認如果可設定的產品已經在購物車中，並且使用者選擇不同的商店，則產品顯示為無庫存。</li>
</ul>
</td>
<td></td>
</td>
</tr>
<tr>
<td><strong>已分組的產品</strong>
</td>
<td>
<ul>
<li>確認當所有子產品都具備時，已針對客戶停用傳遞方法和[!UICONTROL Add to cart]按鈕
<code>qty</code>已設定為<code>0</code>。</li>
<li>確認至少有一個子產品將<code>qty</code>設定為時，客戶已啟用傳遞方法 <code>0.</code></li>
<li>確認[!UICONTROL Store Pickup Delivery]方法僅對啟用[!UICONTROL Available for Store Pickup]的產品可見且有效。 （檢查子產品。）</li>
</ul>
</td>
<td></td>
</tr>
<tr>
<td><strong>虛擬產品</strong>
</td>
<td>
確認虛擬產品未提供[!UICONTROL In-store Pickup]傳遞方法。
<td></td>
</td>
</tr>
<tr>
<td><strong>套裝產品</strong>
</td>
<td>
<ul>
<li>確認如果至少有一個子項產品停用[!UICONTROL Available for Store Pickup]，則客戶無法使用「商店見面交貨」選項。</li>
<li>確認如果至少有一個子項產品停用[!UICONTROL Available for Home Delivery]，則客戶無法使用「首頁遞送」選項。</li>
<li>驗證套件組合中是否有至少一個子產品無庫存，套件組合（父產品）也會顯示
作為[!UICONTROL Out of stock]。</li>
</ul>
</td>
<td></td>
</tr>
<tbody>
</table>

## 簽到體驗

測試計畫的這個區段涵蓋下列功能的商店取貨訂單簽到體驗：

- 備用取貨聯絡人 — 驗證新增[!UICONTROL Alternate Pickup Contact]及選取商店取貨訂單上[!UICONTROL Preferred Contact]的工作流程。

- 簽到表單 — 驗證提交「商店取貨」訂單簽到請求的工作流程。

**功能區域：**&#x200B;購物車結帳、商店取貨訂單的簽到表單</br>
**角色：**&#x200B;管理員、客戶、商店關聯</br>
**測試型別：**&#x200B;全部為正數

### 替代取車連絡人


**功能區域：**&#x200B;購物車結帳</br>
**角色：**&#x200B;客戶</br>
**測試型別：**&#x200B;全部為正數

<table style="table-layout:auto">
<tr>
<th>函式</th>
<th>情境</th>
<th>預期結果</th>
</tr>
<tr>
<td><strong>備用代答連絡人</br>
簽入<strong>
</td>
<td>
客戶提交具有「店內取貨」選項的訂單。</td>
<td>在結帳過程中，客戶會在送貨步驟中看到[!UICONTROL Alternate Pickup Contact]選項。
</td>
</tr>
<tr>
<td><strong>備用代答慣用連絡人，簽到</strong>
<td>
客戶提交具有「店內取貨」選項的訂單。 結帳期間，客戶新增[!UICONTROL Alternate Pickup Contact]。</td>
<td>在結帳過程中，客戶在送貨步驟中看到[!UICONTROL Preferred Contact]選項。</td>
</td>
</tr>
<tr>
<td><strong>備用接機聯絡詳細資料，簽到</strong>
</td>
<td>
客戶提交具有「店內取貨」選項的訂單。 結帳期間，客戶在送貨步驟中選取[!UICONTROL Alternate Pickup Contact]。
</td>
<td>客戶看到輸入選項以輸入連絡人詳細資料： [!UICONTROL First name]、[!UICONTROL Last name]、[!UICONTROL Phone]和[!UICONTROL Email]。</td>
</tr>
<tr>
<td><strong>備用接送，簽到電子郵件</strong>
</td>
<td>客戶提交具有「店內取貨」選項的訂單。 結帳期間，客戶在送貨步驟中選擇[!UICONTROL Alternate Pickup Contact]、新增聯絡人詳細資料，然後提交訂單。</td>
<td>客戶與替代連絡人都會收到訂單的「簽到電子郵件」。</td>
</tr>
<td><strong>替代取貨，訂單明細</strong></td>
<td>客戶提交具有「店內取貨」選項的訂單。 結帳期間，客戶在送貨步驟中選擇[!UICONTROL Alternate Pickup Contact]、新增聯絡人詳細資料，然後提交訂單。</td>
<td>管理員會看到已儲存訂單的其他聯絡資訊。</td>
</tr>
<tr>
<td><strong>備用取車連絡人，商店相關訂單檢視</strong>
</td>
<td>客戶提交具有「店內取貨」選項的訂單。 結帳期間，客戶在送貨步驟中選擇[!UICONTROL Alternate Pickup Contact]、新增聯絡人詳細資料，然後提交訂單。</td>
<td>「商店關聯」可以在FaaS/ChaaS中檢視訂單的其他聯絡資訊。</td>
</td>
</tr>
</tbody>
</table>

### 簽到表單


**功能區域：**&#x200B;簽入表單</br>
**角色：**&#x200B;客戶</br>
**測試型別：**&#x200B;全部為正數

<table style="table-layout:auto">
<tr>
<th>函式</th>
<th>情境</th>
<th>預期結果</th>
</tr>
<tr>
<td><strong>簽入動作 — 提交請求</strong>
</td>
<td>在簽到表單上，客戶完成所有必填欄位，並提交請求。</td>
<td>客戶收到成功回應。</td>
</tr>
<tr>
<td><strong>簽入動作 — 檢視請求詳細資訊</strong></td>
<td>客戶已成功提交簽到請求。</td>
<td>訂單狀態會在FaaS系統中更新，而「商店關聯」可在FaaS中檢視簽入請求詳細資訊。
</td>
</tr>
<tr>
<td><strong>簽入動作 — 僅提交請求一次</strong></td>
<td>在提交訂單的簽到請求後，客戶會選取要第二次簽到的連結。</td>
<td>在「簽入」表單中，客戶看不到編輯或重新提交表單的選項。</td>
</tr>
<tr>
<td><strong>簽入動作 — 確認抵達</strong></td>
<td>店內取貨訂單已標示為可在FaaS中取貨。 客戶收到「準備好取貨」電子郵件，並選取[!UICONTROL Confirm Arrival]。</td>
<td>客戶看到訂單的「簽到」表單。</td>
</tr>
</tbody>
</table>

## 商店協助應用程式

測試計畫的這個區段涵蓋Store Assist應用程式中測試順序、挑選和移交工作流程的情況。

**功能區域：**&#x200B;商店協助應用程式</br>
**角色：**&#x200B;存放區關聯</br>
**測試型別：**&#x200B;全部為正數

<table style="table-layout:auto">
<tr>
<th>函式</th>
<th>情境</th>
<th>預期結果</th>
</tr>
<tr>
<td>
<strong>單一訂單撿料 — 快樂路徑，路邊撿料</strong></td>
<td>挑選單一和多數量料號。 沒有零撿料，且路邊撿料（含預備）。
</td>
<td>
</td>
</tr>
<tr>
<td><strong>多訂單撿料 — 快樂路徑、路邊撿料</strong></td>
<td>單一和多數量料號。 無零點選，路邊取貨（含預備）</td>
<td></td>
</tr>
<tr>
<td><strong>單一訂單取貨 — 店內取貨的快樂路徑</strong></td>
<td>單一和多數量料號。 無nil pick，和店內取貨（含分段）</td>
<td>
</td>
</tr>
<tr>
<td><strong>多訂單撿料 — 快樂路徑、店內撿料</strong></td>
<td>挑選單一和多數量料號。 沒有零撿料，且路邊撿料（含預備）。</td>
<td></td>
</tr>
<tr>
<td><strong>單一訂單取貨 — 路徑不愉快，店內取貨</strong></td>
<td>撿料單一與多數量料號，具有部份與零撿料與店內撿料（含暫存）</td>
</td>
<td></td>
</tr>
<td><strong>多訂單撿料 — 路邊撿料不愉快</strong></td>
<td>撿料單一與多數量料號，具有部份與零撿料與店內撿料（含暫存）</td>
<td></td>
</tr>
<td><strong>單一訂單撿料 — 路徑不愉快，路邊撿料</strong></td>
<td>撿料單一與多數量料號，具有部份與撿料與路邊撿料（含暫存）</strong></td>
</td>
<td></td>
</tr>
<tr><td><strong>已下訂單 — 撿料前已取消</strong></td>
<td></td>
<td></td>
</tr>
<tr>
<td><strong>下訂單 — 移交前已取消</strong></td>
<td></td>
<td></td>
</tr>
<tr>
<td><strong>已下訂單 — 依訂單模組搜尋</strong></td>
<td></td>
<td></td>
</tr>
<tr><td><strong>已下訂單 — 搜尋和手動簽入以進行移交</strong></td>
<td></td>
<td></td>
</tr>
<tr><td><strong>已下訂單 — 所有料號未撿料或撿料器未標示為可用</strong></td>
<td></td>
<td></td></tr>
<tr><td><strong>以組合料號下訂單 — 撿料與移交</strong></td>
<td></td>
<td></td></tr>
<tr><td><strong>已下訂單 — 已拒絕的交貨</strong></td>
<td></td>
<td></td></tr>
<tr><td><strong>已下訂單 — 交出，但拒絕所有料號</strong></td>
<td></td>
<td></td></tr>
</tbody>
</table>

## 部署

在您確認解決方案已設定完畢，並依照您的規格進行測試後，您就可以開始從測試環境部署至生產環境。

部署和測試會依您的基礎結構和功能而異。

>[!TIP]
>
>如需雲端基礎結構專案中Adobe Commerce的部署准則、檢查清單和最佳實務，請參閱Adobe Commerce開發人員檔案中的[部署您的存放區](https://experienceleague.adobe.com/zh-hant/docs/commerce-cloud-service/user-guide/develop/deploy/staging-production)。
