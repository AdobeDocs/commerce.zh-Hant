---
title: 為購物者和AI代理程式設計Commerce平台
description: 瞭解如何建置商業平台，從目錄設計和MCP到遙測，透過單一信任來源為人類購物者和AI代理程式提供服務。
role: Developer, Leader
recommendations: noCatalog
autotag-review: '2026-10-20T20:32:40.424Z'
TQID: 'https://experienceleague.adobe.com/ub4oTxr4IfLGgqqz0S1npY-sn0FZb3mKq-GdjD9eDjI'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4239b8a6-e74f-567d-a7a5-b98b9ead0ea4
    internal-label: Observability
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
    internal-label: Compliance
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: c4f010fa-1478-4300-a88d-706fbc036a7a
    internal-label: APIs and SDKs
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
topic_v2:
  - id: b4dd41a7-ccf8-4e9d-918e-acaab534a307
    internal-label: Data quality
  - id: bbbea26f-9621-49eb-9ab8-e06fb3bbce8c
    internal-label: Artificial intelligence
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
    internal-label: Governance
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
    internal-label: Privacy
source-git-commit: f54c816fd23786ec519d5c890bc2664c3dcf8c6f
workflow-type: tm+mt
source-wordcount: '1339'
ht-degree: 0%
---

# 為購物者和AI代理程式設計商務平台

<table style="table-layout:auto">
<tr style="border: 0;">
   <td valign="middle" style="vertical-align: middle;"><img alt="蘇利亞·拉梅赫肖像" src="../../assets/guidance-and-insights/agentic-commerce-author-avatar-slamech.png" width="96"><br><strong>Surya Lamech</strong><br><em>主要產品行銷經理</em></td>
</tr>
</table>

![代理商務平台的主圖插圖，其中人類和AI代理與單一真實來源互動](../../assets/guidance-and-insights/agentic-commerce-hero.png "代理商務平台的架構基礎")

*設計商業平台，讓人類和AI代理程式與單一真實來源互動。*

Commerce正在經歷結構性轉變。 客戶不再單純仰賴搜尋引擎或瀏覽店面來探索選項。 相反，他們改用LLM支援的介面、聊天式助理和代理商購物工具來提問、比較不同零售商的產品，並加速早期決策。

這些介面是探索、教育和比較的強大引擎。 相較於傳統的瀏覽方式，這些功能可協助客戶釐清需求、評估利弊和縮小選擇範圍。

然而，在購買完成時，絕大多數客戶仍然偏好受信任的店面和品牌擁有的網站，這些網站對於付款安全性、履行透明度和購買後服務都瞭如指掌。 轉換仍錨定在已建立信任的環境中。

重要的是，AI在此階段不會消失。 當客戶抵達品牌擁有的店面時，agentic AI可以透過指導產品選擇、即時個人化推薦、回應異議、捆綁補充專案和簡化結帳來增強體驗。 在這些信任的環境中，AI成為轉換加速器，提高完成率並增加平均訂單值。

為了在這種新的環境中競爭，企業需要一個&#x200B;**結構化、控管且針對人力和代理程式消耗最佳化的商務基礎**。 Adobe Commerce是針對此轉換而建置，而下列原則概述真正具備代理程式可用性所需的條件。

## 為兩個對象建立的商務架構

![圖表在左側顯示供人使用的店面和應用程式，在右側顯示聊天助理和自主代理程式，兩者皆從透過API和MCP公開的產品、定價、詳細目錄、促銷活動、購物車和結帳等中央Commerce核心中繪圖](../../assets/guidance-and-insights/agentic-commerce-foundational-model.png){width="800" zoomable="yes"}

*客戶看到的內容與代理程式使用的內容會保持一致、準確且符合品牌。*

現代商務棧疊現在必須為兩個同樣重要的受眾服務：人員和AI代理。 面對人的體驗，例如店面和應用程式，對於參與度、品牌表現和建立客戶忠誠度仍然至關重要。 但與此同時，還有快速擴展的代理程式對向表面：機器可讀端點，為LLM和自主代理程式提供結構化事實、控管內容和異動功能。

代理程式運用透過可預測API提供的簡潔結構化資料時，其效能最佳，而非嘗試解讀JavaScript或透過展示層推斷商業規則。 這表示產品規格、價格、可用性和促銷邏輯必須存在於API和標準化介面（例如MCP伺服器）所公開的可定址資源中。 當面向人類和代理程式的介面取自相同的基本信任來源時，品牌會確保客戶看到的內容以及代理程式使用的內容保持一致、準確且符合品牌。

這種雙面架構是代理商務的基礎。

## 為機器推理設計的目錄

![圖表顯示由目錄層和原則塑造的結構化產品實體（SKU、屬性、變體、組合、定價和可用性），然後透過目錄檢視傳送至品牌店面、市集、合作夥伴摘要、行動應用程式以及AI或代理程式介面](../../assets/guidance-and-insights/agentic-commerce-agent-interaction.png){width="800" zoomable="yes"}

*單一控管的信任來源，每個管道都經過調整，而且絕對不會取用產品資料。*

目錄是代理商的核心。 它必須為機器而建構，必須依法規進行管理，並且有足夠的彈性來支援所有的人力和代理程式互動。 Adobe Commerce的目錄模型是根據目錄檢視、原則、圖層和結構化產品實體所建立，是為未來所設計。

目錄檢視會定義產品資料在哪裡以及如何公開，無論是店面、市場、合作夥伴資訊源還是AI表面。 每個檢視都有各自的產品可用性、定價和屬性可見性規則，確保正確的資訊能傳達給正確的消費者或代理商。 目錄層可讓您擴充特定通道的產品資料，而不需修改來源產品資料。 原則可控管客戶資格、存貨邏輯、定價及法規遵循限制。 加在一起，企業就能精確控制代理程式可存取或操作的目錄資料。

## MCP作為代理程式的共同語言

![圖表顯示透過模型內容通訊協定（包括Commerce MCP和開發人員MCP）將請求傳送至Adobe Commerce功能（例如購物車建立、結帳、付款、清查、促銷和退貨）的購物助理、支援代理和開發人員工具](../../assets/guidance-and-insights/agentic-commerce-reference-stack.png){width="800" zoomable="yes"}

*MCP會標準化代理程式以自然意圖要求動作，而Adobe Commerce會以受管理的決定式動作來執行這些動作。*

為了讓Agentic Commerce能夠端對端運作，電子商務平台必須支援標準化通訊協定，讓代理程式可安全地執行動作，例如購物車建立、結帳啟動、付款協調、詳細目錄驗證、促銷和退貨。

透過對模型上下文通訊協定(MCP)的原生支援，Adobe以LLM可一致詮釋的方式建構和公開商業功能。 MCP將產品資料、商業規則和交易內容呈現給LLM的方式標準化，確保代理商能夠可靠地對其做出解釋，同時企業維持治理和控制。 透過Commerce MCP，企業可以建立自訂代理體驗，例如購物助理、代理購物車建立、支援代理等等。

開發人員MCP提供了AI支援的開發功能，使團隊能夠快速擴展平台功能並部署可組合的店面元件。 透過將Adobe的知識來源、檔案和平台最佳實務直接內嵌到開發工作流程中，開發人員MCP可協助新開發人員更快上線，並快速提高生產力。 它產生的程式碼遵循備受肯定的架構模式，易於維護，並符合企業商務要求的品質標準。 其結果是從創意到生產的加速路徑，讓企業以快於競爭者的速度在實驗、迭代和出貨商業功能方面領先。

Adobe也致力於支援代理商業通訊協定，例如Agentic Commerce Protocol (ACP)和Universal Commerce Protocol (UCP)，以實現產品探索和代理與您的店面之間安全且基於標準的交易互動。

透過採用開放通訊協定而不是點數整合，Adobe可確保商業互動受到控管、決定性和安全，同時啟用代理商對商家互動的新模式，即受信任的代理商可以根據明確界定的原則直接交易。

## 遙測和持續最佳化

在AI介導的生態系統中，遙測技術成為一項戰略優勢。 企業需要瞭解其品牌在LLM中的呈現方式、代理程式如何準確地呈現其內容、代理程式參考的流量如何轉換，以及出現治理或法規遵循問題的位置。 此外也需使用作業遙測來追蹤代理程式執行，以及跨代理程式互動的異常偵測。

Adobe可讓您檢視產品在LLM中的顯示情形，透過AI增強產品資料，並提高LLMS對資料的可讀性。 藉由為您的目錄新增有意義的內容，LLM不僅可準確探索您的產品，還可瞭解產品是什麼、其用途以及它們對客戶重要的原因。

此外，已針對人類消費最佳化的產品詳細資料頁面通常會有代理程式無法看到的資料。 這些資料可能會隱藏在模型、設定器和連結頁面後面。 代理程式可能無法完全瞭解產品類別、套件組合和變體。 Adobe可以識別這項重要的遺失資訊，並將其部署為JSON-LD至邊緣，讓代理程式取得所有相關產品資料。

透過這種持續的遙測與最佳化品牌，可確保最高可見度，並維持各個LLM的競爭力。

## 這很重要的原因

電子商務不再侷限於店面和搜尋結果。 LLM和自主代理程式日益協助探索、評估和交易。 這種轉變改變了可視性的機制、控制的動態性以及信任的基礎。 獲勝的品牌將為AI原生基礎進行架構。

## 相關指引

* [目錄檢視](/help/optimizer/setup/catalog-view.md)
* [目錄圖層](/help/optimizer/setup/catalog-layer.md)
* [原則](/help/optimizer/setup/policies.md)
* [Adobe Commerce App Builder的AI編碼開發人員工具](/help/cloud-service/migration/coding-tools.md)
* [COMMERCE API](../../apis/commerce-apis.md)
* [Commerce Developer Agent播放清單](https://experienceleague.adobe.com/zh-hant/playlists/commerce-developer-agent) — 觀看設定和使用Commerce Developer Agent的技術影片。
