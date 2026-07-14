---
source-git-commit: c99194b2eb7111a593cfe7c4ba1b4917e38589d2
workflow-type: tm+mt
source-wordcount: '1799'
ht-degree: 1%

---
# 新功能範本

## 新增功能

此頁面包含過去60天所做的變更。 我們將從此清單中排除所有微幅更新，例如複製編輯。

### 2026年7月7日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>說明</th>
      <th>型別</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>已新增Adobe Commerce as a Cloud Service的沙箱<a href="https://experienceleague.adobe.com/en/docs/commerce/cloud-service/release-notes">發行說明</a>。</p>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/976a43b367be87363307dc27c55f98df18271eb1">認可</a></td>
    </tr>
  </tbody>
</table>

### 2026年7月6日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>說明</th>
      <th>型別</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>移除LLM Optimizer和Commerce整合檔案。 此功能已重新設定範圍，並移至<a href="https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/catalog-enrichment">Commerce管理指南</a>。</p>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/edab7c8b3c7965425c5d3008a537f7e4a1fc374b">認可</a></td>
    </tr>
  </tbody>
</table>

### 2026年6月23日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>說明</th>
      <th>型別</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>已更新Commerce服務檔案的目錄資料同步驗證指引。 服務安裝和設定主題現在使用一致的兩步驟工作流程 — 在<a href="https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status">資料摘要同步狀態頁面</a>上確認匯出，然後在<a href="https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard">資料管理儀表板</a>上確認傳遞 — 其中包含<a href="https://experienceleague.adobe.com/en/docs/commerce/catalog-service/get-started#monitor-and-troubleshoot-data-export">目錄服務開始使用</a>、<a href="https://experienceleague.adobe.com/en/docs/commerce/live-search/install#monitor-sync-progress">即時搜尋安裝</a>、<a href="https://experienceleague.adobe.com/en/docs/commerce/product-recommendations/getting-started/install-configure#monitor-and-troubleshoot-data-synchronization">產品建議安裝</a>以及<a href="https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/data-synchronization/data-sync-manage#verify-that-the-data-sync-is-working">在<em>SaaS資料匯出指南</em>中管理同步</a>的更新指示。</p>
</td>
      <td>
        意見反應
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/82bdfd342d2d745721ed2b35f2dbfd8fa394ab5a">認可</a></td>
    </tr>
    <tr>
      <td><p>新增新的<a href="https://experienceleague.adobe.com/en/docs/commerce/aco-optimizer-connector/reference/feed-table-reference">Adobe Commerce Optimizer聯結器摘要資料表結構描述參考</a>並更新<a href="https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/data-synchronization/sync-overview">SaaS資料匯出同步</a>、<a href="https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/data-synchronization/data-sync-manage">手動同步管理</a>、<a href="https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/reference/data-export-cli-commands">Commerce CLI resync命令</a>以及<a href="https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/reference/feed-table-reference">摘要資料表結構描述</a>指南。</p>
</td>
      <td>
        重大更新，新主題
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/601d02435f388096d59ce7f8e2a9e3e7c8bec65b">認可</a></td>
    </tr>
  </tbody>
</table>

### 2026年6月17日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>說明</th>
      <th>型別</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>更新管理Adobe Commerce與連線的Commerce服務之間目錄資料同步的檔案。<br /> — 在<em>SaaS資料匯出指南</em>中新增<a href="https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/data-synchronization/data-sync-manage">檢視及管理同步化程式</a>主題，以監視匯出狀態、確認資料傳遞及手動重新同步Commerce服務與Adobe Commerce Optimizer整合的摘要。<br /> — 在<em>SaaS資料匯出指南</em>中新增<a href="https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/troubleshooting/troubleshooting-scenarios">疑難排解案例</a>、<a href="https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/reference/manage-extension">摘要資料表結構描述參考</a>以及其他疑難排解和參考資訊。<br /> — 更新<a href="https://experienceleague.adobe.com/en/docs/commerce/aco-optimizer-connector/get-started">開始使用Adobe Commerce Optimizer聯結器</a>並新增了<a href="https://experienceleague.adobe.com/en/docs/commerce/aco-optimizer-connector/data-sync-manage">管理與Commerce Optimizer的同步</a>、<a href="https://experienceleague.adobe.com/en/docs/commerce/aco-optimizer-connector/troubleshooting/troubleshooting">Adobe Commerce Optimizer聯結器疑難解答</a>、<a href="https://experienceleague.adobe.com/en/docs/commerce/aco-optimizer-connector/reference/connector-reference">聯結器模組和饋送端點</a>，以及有關估計資料量和與<em>Adobe Commerce Optimizer聯結器指南</em>同步時間的說明。</p>
</td>
      <td>
        重大更新，新主題
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/66d9db3ab63102a0fd639f274a4131bf69ac868a">認可</a></td>
    </tr>
  </tbody>
</table>

### 2026年6月16日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>說明</th>
      <th>型別</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>已新增Adobe Commerce as a Cloud Service的沙箱<a href="https://experienceleague.adobe.com/en/docs/commerce/cloud-service/release-notes">發行說明</a>。</p>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/0321b64a787b37a95af0568473bfcfc5e5d4189e">認可</a></td>
    </tr>
    <tr>
      <td><p>更新<a href="https://experienceleague.adobe.com/en/docs/commerce/payment-services/financial-reports/order-payment-status#asynchronous-monitoring-of-pending-capture-transactions">訂單付款狀態報告</a>，以澄清預設停用擱置擷取交易的非同步監視，並記錄啟用步驟。</p>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/7be26764bc3f3878c3c78a881ad8912038c7f07f">認可</a></td>
    </tr>
  </tbody>
</table>

### 2026年6月15日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>說明</th>
      <th>型別</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>已針對v2.15.0 （Google Pay和Apple Pay Express更新，略過檢閱）更新<a href="https://experienceleague.adobe.com/en/docs/commerce/payment-services/release-notes">Payment Services發行說明</a>；將<a href="https://experienceleague.adobe.com/en/docs/commerce/payment-services/payments-checkout/payments-options">付款選項</a>和<a href="https://experienceleague.adobe.com/en/docs/commerce/payment-services/configure/configure-admin">付款服務設定</a>與新行為一致。</p>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/b0eb472bfcb3fb568d4e8a70e63356d60873b641">認可</a></td>
    </tr>
  </tbody>
</table>

### 2026年6月12日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>說明</th>
      <th>型別</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>在<a href="https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/search-relevance-matching">搜尋比對和排名（即時搜尋）</a>和<a href="https://experienceleague.adobe.com/en/docs/commerce/optimizer/manage-results/search-relevance-matching">搜尋比對和排名(Adobe Commerce Optimizer)</a>中記錄搜尋比對優先順序（精確/接近片語、相同欄位、跨欄位）和排名權衡，以及來自概觀、索引、最佳實務和搜尋效能主題的連結。</p>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/6f9744e6a0b3390b9e29a1d973fa44456db1612c">認可</a></td>
    </tr>
    <tr>
      <td><p>已使用v1.3.8更新<a href="https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/release-notes">AEM Assets整合發行說明</a>。</p>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/8937c04dcb4da5f19bce017ef0da8a48bd61c3a6">認可</a></td>
    </tr>
  </tbody>
</table>

### 2026年6月10日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>說明</th>
      <th>型別</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>展開Adobe Commerce Optimizer Connector整合指南，包含新的技術和操作主題：<br />- <a href="https://experienceleague.adobe.com/en/docs/commerce/aco-optimizer-connector/connector-sync-pipeline">Connector同步管道</a> — cron工作、初始化、摘要提交和錯誤處理<br />- <a href="https://experienceleague.adobe.com/en/docs/commerce/aco-optimizer-connector/headless-storefront">Headless店面整合</a> — GraphQL <code>commerceOptimizer</code>查詢和套件組合產品編碼<br />- <a href="https://experienceleague.adobe.com/en/docs/commerce/aco-optimizer-connector/troubleshooting/troubleshooting">疑難排解</a> — 認證、同步和範圍設定問題<br />- <a href="https://experienceleague.adobe.com/en/docs/commerce/aco-optimizer-connector/reference/connector-reference">Connector參考</a> — 模組、摘要端點、批次限制和設定路徑<br />- <a href="https://experienceleague.adobe.com/en/docs/commerce/aco-optimizer-connector/reference/field-mapping">欄位對應</a> — Commerce到最佳化工具欄位對應</p>
</td>
      <td>
        重大更新，新主題
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/2973937a78f4ea425da7876ac006eb2023a35bb3">認可</a></td>
    </tr>
    <tr>
      <td><p>針對移轉至[!DNL Adobe Commerce as a Cloud Service]的使用者，在<a href="https://experienceleague.adobe.com/en/docs/commerce/cloud-service/overview">移轉評估</a>上新增頁面。</p>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/8f260d114983890872281115f74b1f98b32e524d">認可</a></td>
    </tr>
    <tr>
      <td><ul>
  <li>在<a href="https://experienceleague.adobe.com/en/docs/commerce/live-search/release-notes#hosted-service-updates">即時搜尋發行說明</a>中新增語意搜尋的2026年6月8日託管服務更新，包括Adobe Commerce as a Cloud Service的預設開啟行為、手動啟用PaaS以及英文目錄支援。<br /> — 在<a href="https://experienceleague.adobe.com/en/docs/commerce/optimizer/release-notes#june-2026">Adobe Commerce Optimizer發行說明</a>中新增語意搜尋和建議價格篩選器（測試版）的2026年6月區段。</li>
</ul>
</td>
      <td>
        重大更新，新主題
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/4c5b282a83b75c07d82dc34b5500916f22e08a44">認可</a></td>
    </tr>
  </tbody>
</table>

### 2026年6月9日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>說明</th>
      <th>型別</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>針對[!DNL Adobe Commerce Optimizer]個建議記錄動態和靜態的<a href="https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/recommendations/filters#price">價格篩選器</a>，包括PDP相對運運算元、位移語意，以及SKU相關建議型別的設定指南。</p>
</td>
      <td>
        意見反應，重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/bccb739bbbfcc7e3bfa645c2a0245933014b934f">認可</a></td>
    </tr>
  </tbody>
</table>

### 2026年6月8日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>說明</th>
      <th>型別</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>新增參考頁面，以提供更詳細的資訊，說明Adobe Commerce Optimizer <a href="https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/catalog-sources">目錄來源</a>及其建立方式。</p>
</td>
      <td>
        意見回饋，新主題，技術
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/8b4d08af43cbff9aaf9fc8f417ddab12185f5565">認可</a></td>
    </tr>
    <tr>
      <td><ul>
  <li>已針對[!DNL Live Search]新增<a href="https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/semantic-search">語意搜尋</a>，並包含啟用步驟、最佳作法和英文目錄限制。<br /> — 已針對[!DNL Adobe Commerce Optimizer]新增<a href="https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/semantic-search">語意搜尋</a>，並更新<a href="https://experienceleague.adobe.com/en/docs/commerce/optimizer/settings">設定 — 進階搜尋</a>，並包含簡化的啟用和選用的調整控制項。</li>
</ul>
</td>
      <td>
        重大更新，新主題
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/475c99e18380c961e400a75de1c06cd8cdb929d1">認可</a></td>
    </tr>
  </tbody>
</table>

### 2026年6月3日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>說明</th>
      <th>型別</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>已新增Adobe Commerce as a Cloud Service的生產<a href="https://experienceleague.adobe.com/en/docs/commerce/cloud-service/release-notes">發行說明</a>。</p>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/8ec59cfc8c9d4d1e804adefe7f88806843e3caa3">認可</a></td>
    </tr>
    <tr>
      <td><p>已針對SaaS資料匯出新增<a href="https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/data-synchronization/feed-lock-mechanism">摘要鎖定機制</a>，以說明摘要鎖定如何防止並行同步衝突，以及如何解譯Commerce資料匯出記錄檔(<code>commerce-data-export.log</code>)中包含的正常略過訊息。</p>
</td>
      <td>
        新主題
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/cb045b490482649a65bac9d763062700a90e9ecd">認可</a></td>
    </tr>
  </tbody>
</table>

### 2026年6月2日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>說明</th>
      <th>型別</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>Commerce管理員新增以資產為中心的<a href="https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/sync-status">同步狀態</a>清單，以依資產屬性搜尋、篩選和疑難排解已同步的AEM Assets。</p>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/a1cb3a063d9c4595220ca431356d34e6cbe8ea33">認可</a></td>
    </tr>
  </tbody>
</table>

### 2026年6月1日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>說明</th>
      <th>型別</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>已新增Adobe Commerce as a Cloud Service的沙箱<a href="https://experienceleague.adobe.com/en/docs/commerce/cloud-service/release-notes">發行說明</a>。</p>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/3e5f1a5366cb57cbdd1ed3f5721a82cd0c5c5271">認可</a></td>
    </tr>
  </tbody>
</table>

### 2026年5月28日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>說明</th>
      <th>型別</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><ul>
  <li>改善<a href="https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/configure-aco">為Commerce Optimizer設定AEM Assets</a>上線，因此AEM Assets設定會在租使用者註冊之前進行，提供專屬目錄層及圖層相關限制的更清楚指引。<br /> — 更新<a href="https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/configure-aem">為存放庫存取和管道部署設定AEM Assets專案</a>，其中包含重新排序的安裝步驟和Cloud Manager熒幕擷取畫面。<br /> — 說明<a href="https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization">設定整合</a>中的IMS型方案ID和環境ID選取專案。</li>
</ul>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/de94aaad29313b3e8254d11d8801ba0d7efff3dc">認可</a></td>
    </tr>
  </tbody>
</table>

### 2026年5月22日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>說明</th>
      <th>型別</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>已針對2026年5月20日發行版本新增<a href="https://experienceleague.adobe.com/en/docs/commerce/optimizer/release-notes">Adobe Commerce Optimizer</a>及Commerce <a href="https://experienceleague.adobe.com/en/docs/commerce/optimizer/release-notes">目錄服務</a>的API更新發行說明，該版本現在會在擷取產品資料時，強制記錄在案的每個請求100-SKU限制。</p>
</td>
      <td>
        技術
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/342a3015f743e12b7089e4d430a517804a7cd40c">認可</a></td>
    </tr>
    <tr>
      <td><p>在<a href="https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/rules/rules-add#intelligent-ranking-boost">新增規則</a>和<a href="https://experienceleague.adobe.com/en/docs/commerce/live-search/best-practice">最佳實務</a>中記錄[!DNL Live Search]的智慧型排名提升（每個規則可設定的行為權重，預設5.0），並包含來自<a href="https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/category-merch">類別銷售</a>的互動參照。 在「<a href="https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking-boost">建立和管理</a>」和「<a href="https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/best-practice">銷售規則最佳實務</a>」中，為「[!DNL Adobe Commerce Optimizer]」新增了相同的指引。</p>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/40b4528d417a4df09ac9ae9fb0d97b0f678b55ac">認可</a></td>
    </tr>
  </tbody>
</table>

### 2026年5月19日

<table style="table-layout:auto;">
  <thead>
    <tr>
      <th>說明</th>
      <th>型別</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p>AEM Assets整合指南說明編輯器如何在<a href="https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/release-notes">AEM Assets整合v1.3.6 </a>中設定<a href="https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/configure-aem#localized-alt-text-in-aem-assets-metadata">替代文字</a>。</p>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/6d3dfbc59e72c00c3552af5805b57c69e60b38b4">認可</a></td>
    </tr>
    <tr>
      <td><p>已新增Adobe Commerce as a Cloud Service的沙箱<a href="https://experienceleague.adobe.com/en/docs/commerce/cloud-service/release-notes">發行說明</a>。</p>
</td>
      <td>
        重大更新
      </td>
      <td><a href="https://github.com/AdobeDocs/commerce.en/commit/14aa082c1f0f8ce4c51328eb8ee9f4af25adf859">認可</a></td>
    </tr>
  </tbody>
</table>
