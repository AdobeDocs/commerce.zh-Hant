---
title: 銷售電子郵件範本
description: 設定異動電子郵件範本，以便在店舖取貨訂單的履行程式期間與客戶和店舖管理員通訊。
role: Admin
level: Intermediate
feature: Shipping/Delivery, Communications, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 1%

---


# 銷售電子郵件範本

「商店履行」提供一組擴充的交易式電子郵件範本，以支援訂單和履行工作流程。 它們提供跨頻道的一致自動化通訊和訊息 — 通知客戶和商店管理員訂單狀態變更、店內取貨訂單指示等。

「商店履行」電子郵件範本已設定預設訊息和設定。 Adobe Commerce中的商家管理員可以管理和修改設定，並選取電子郵件範本以在不同案例中與客戶溝通。 管理員也可以設定和自訂範本。

從管理員設定銷售電子郵件範本： **[!UICONTROL Stores > Configuration > Sales > Sales Emails]**。

## 電子郵件 — 一般設定

<table>
<thead>
<tr>
<th><strong>欄位</strong></th>
<th><strong>說明</strong></th>
<th><strong>範圍</strong></th>
<th><strong>必填</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>非同步傳送</strong></td>
<td>判斷是否以非同步方式傳送銷售電子郵件。 選項： <br/>**'停用'** （預設）事件觸發時會傳送銷售電子郵件。 若要以最快的速度進行「商店見面交收」的通訊和回應，請使用預設設定。 <br/>**'啟用'** — 啟用此選項會將處理結帳與訂單處理電子郵件通知的程式移至背景，以預先決定的定期間隔傳送。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
</tbody></table>

## 準備到店取貨的訂單

<table>
<thead>
<tr>
<th><strong>欄位</strong></th>
<th><strong>說明</strong></th>
<th><strong>範圍</strong></th>
<th><strong>必填</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>已啟用</strong></td>
<td>當市集關聯完成挑選客戶的訂單時，系統就會傳送此電子郵件給客戶。 設為「否」可停用電子郵件通知。 如果電子郵件範本已停用，並不會阻止商店關聯人員挑選訂單。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<tr>
<td><strong>訂單已準備好接收電子郵件寄件者</strong></td>
<td>傳送電子郵件通知時使用的寄件者身分。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<tr>
<td><strong>準備取貨的訂單電子郵件範本</strong></td>
<td>用來通知註冊客戶的電子郵件訊息範本。 預設範本會與整合一併提供。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<td><strong>賓客的訂單準備取貨電子郵件範本</strong></td>
<td>用來通知來賓客戶的電子郵件訊息範本。 預設範本會與整合一併提供。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<tr>
<td><strong>替代取貨連絡人的訂單準備取貨電子郵件範本</strong></td>
<td>用來通知順序中指定之其他連絡人的電子郵件訊息範本。 預設範本會與整合一併提供。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<tr>
<td><strong>將訂單準備取貨電子郵件副本傳送至</strong></td>
<td>以逗號分隔的電子郵件地址清單，用於傳送每個通知的副本。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<tr>
<td><strong>傳送訂單準備取貨電子郵件複製方法</strong></td>
<td>要使用的電子郵件複製方法（副本）。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
</tbody></table>


## 已在市集內取得訂單

<table>
<thead>
<tr>
<th><strong>欄位</strong></th>
<th><strong>說明</strong></th>
<th><strong>範圍</strong></th>
<th><strong>必填</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>已啟用</strong></td>
<td>此電子郵件會在客戶確認他們已從商店取貨時傳送給他們。 設為「否」可停用電子郵件通知。 如果電子郵件範本已停用，並不會阻止客戶提取訂單。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<tr>
<td><strong>訂單已接聽電子郵件寄件者</strong></td>
<td>傳送電子郵件通知時使用的寄件者身分。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<tr>
<td><strong>已擷取訂單的電子郵件範本</strong></td>
<td>用來通知註冊客戶的電子郵件訊息範本。 預設範本會與整合一併提供</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<td><strong>已接聽來賓的訂單電子郵件範本</strong></td>
<td>用來通知來賓客戶的電子郵件訊息範本。 預設範本會與整合一併提供。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<tr>
<td><strong>傳送已擷取的電子郵件副本至</strong></td>
<td>以逗號分隔的電子郵件地址清單，用於傳送每個通知的副本。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<tr>
<td><strong>傳送已選取電子郵件複製方法</strong></td>
<td>要使用的電子郵件複製方法（副本）。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
</tbody></table>

## 訂單已延遲

<table>
<thead>
<tr>
<th><strong>欄位</strong></th>
<th><strong>說明</strong></th>
<th><strong>範圍</strong></th>
<th><strong>必填</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>已啟用</strong></td>
<td>此電子郵件會傳送給客戶，通知他們商戶商店處理或取貨的延遲。 設為「否」可停用電子郵件通知。 如果電子郵件範本已停用，功能不會防止訂單延遲。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<tr>
<td><strong>訂購延遲的電子郵件寄件者
</strong></td>
<td>傳送電子郵件通知時使用的寄件者身分。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<tr>
<td><strong>訂購延遲的電子郵件範本</strong></td>
<td>用來通知註冊客戶的電子郵件訊息範本。 預設範本會與整合一併提供。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<td><strong>訪客的訂單延遲電子郵件範本</strong></td>
<td>用來通知來賓客戶的電子郵件訊息範本。 預設範本會與整合一併提供。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<tr>
<td><strong>傳送訂單延遲電子郵件副本至</strong></td>
<td>以逗號分隔的電子郵件地址清單，用於傳送每個通知的副本。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<tr>
<td><strong>傳送訂單延遲複製方法</strong></td>
<td>要使用的電子郵件複製方法（副本）。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
</tbody></table>



## 訂單已取消

<table>
<thead>
<tr>
<th><strong>欄位</strong></th>
<th><strong>說明</strong></th>
<th><strong>範圍</strong></th>
<th><strong>必填</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>已啟用</strong></td>
<td>此電子郵件會傳送給客戶，通知他們已在商戶商店取消訂單。 設定為<code>No</code>以停用電子郵件通知。 如果電子郵件範本已停用，此功能不會阻止訂單被取消。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<tr>
<td><strong>訂單已取消的電子郵件寄件者
</strong></td>
<td>傳送電子郵件通知時使用的寄件者身分。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<tr>
<td><strong>已取消訂單的電子郵件範本</strong></td>
<td>用來通知註冊客戶的電子郵件訊息範本。 預設範本會與整合一併提供。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<td><strong>已取消訪客的訂單</strong></td>
<td>用來通知來賓客戶的電子郵件訊息範本。 預設範本會與整合一併提供。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<tr>
<td><strong>傳送訂單取消的電子郵件副本至</strong></td>
<td>以逗號分隔的電子郵件地址清單，用於傳送每個通知的副本。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<tr>
<td><strong>傳送訂單取消的複製方法</strong></td>
<td>要使用的電子郵件複製方法（副本）。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
</tbody></table>


## 訂單已部份取消

<table>
<thead>
<tr>
<th><strong>欄位</strong></th>
<th><strong>說明</strong></th>
<th><strong>範圍</strong></th>
<th><strong>必填</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>已啟用</strong></td>
<td>此電子郵件會傳送給客戶，通知他們商戶商店已取消部分訂單。 設定為<code>No</code>以停用電子郵件通知。 如果電子郵件範本已停用，並不會阻止部分取消訂單。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<tr>
<td><strong>部分取消的訂單電子郵件寄件者
</strong></td>
<td>傳送電子郵件通知時使用的寄件者身分。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<tr>
<td><strong>部分取消的訂單電子郵件範本</strong></td>
<td>用來通知註冊客戶的電子郵件訊息範本。 預設範本會與整合一併提供。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<td><strong>替代取貨聯絡人的訂單部分取消電子郵件範本</strong></td>
<td>用來通知順序中指定之其他連絡人的電子郵件訊息範本。 預設範本會與整合一併提供。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<tr>
<td><strong>已部分取消客人的訂單</strong></td>
<td>用來通知來賓客戶的電子郵件訊息範本。 預設範本會與整合一併提供。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<tr>
<td><strong>將部分取消的訂單電子郵件副本傳送至</strong></td>
<td>以逗號分隔的電子郵件地址清單，用於傳送每個通知的副本。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<tr>
<td><strong>傳送部分取消的訂單複製方式</strong></td>
<td>要使用的電子郵件複製方法（副本）。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
</tbody></table>

## 收貨商店

<table>
<thead>
<tr>
<th><strong>欄位</strong></th>
<th><strong>說明</strong></th>
<th><strong>範圍</strong></th>
<th><strong>必填</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>訂單具有收貨商店產品電子郵件寄件者</strong></td>
<td>以彙總報表的形式傳送給指定的商戶人員的電子郵件，此彙總報表會包含所有在商戶商店中無法撿料的未結訂單，直到其存貨可用為止。 </br></br>商家可以使用此報表來啟動和管理商店到商店存貨移轉或補充。 </br></br>此通知僅適用於啟用[!DNL Ship-to-Store]功能時。
</br></br>此標籤不會影響選取的送貨業者或其可用的送貨方法標籤。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<tr>
<td><strong>收貨方儲存電子郵件收件者</strong></td>
<td>以逗號分隔的電子郵件地址清單，用於傳送每個通知的副本。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
<tr>
<td><strong>電子郵件範本</strong></td>
<td>用於通知收件者的電子郵件訊息範本。 預設範本會與整合一併提供。</td>
<td>存放區檢視</td>
<td>否</td>
</tr>
</tbody></table>

>[!NOTE]
>
>如果您允許延期交貨，則必須提供管理員電子郵件地址，以接收有關這些訂單的通知。 將位址新增至下列組態設定： [訂單延遲](#order-delayed)範本中的&#x200B;**[!UICONTROL Send Order Delayed Email Copy To]**，以及[送貨至商店](#ship-to-store)範本中的[!UICONTROL Ship To Store Email Recipients]。



