![MCP-for-beginners](../../translated_images/zh-HK/mcp-beginners.2ce2b317996369ff.webp) 

[![GitHub contributors](https://img.shields.io/github/contributors/microsoft/mcp-for-beginners.svg)](https://GitHub.com/microsoft/mcp-for-beginners/graphs/contributors)
[![GitHub issues](https://img.shields.io/github/issues/microsoft/mcp-for-beginners.svg)](https://GitHub.com/microsoft/mcp-for-beginners/issues)
[![GitHub pull-requests](https://img.shields.io/github/issues-pr/microsoft/mcp-for-beginners.svg)](https://GitHub.com/microsoft/mcp-for-beginners/pulls)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)

[![GitHub watchers](https://img.shields.io/github/watchers/microsoft/mcp-for-beginners.svg?style=social&label=Watch)](https://GitHub.com/microsoft/mcp-for-beginners/watchers)
[![GitHub forks](https://img.shields.io/github/forks/microsoft/mcp-for-beginners.svg?style=social&label=Fork)](https://GitHub.com/microsoft/mcp-for-beginners/fork)
[![GitHub stars](https://img.shields.io/github/stars/microsoft/mcp-for-beginners?style=social&label=Star)](https://GitHub.com/microsoft/mcp-for-beginners/stargazers)


[![Microsoft Foundry Discord](https://dcbadge.limes.pink/api/server/nTYy5BXMWG)](https://discord.gg/nTYy5BXMWG)

Follow these steps to get started using these resources:
1. **Fork the Repository**: Click [![GitHub forks](https://img.shields.io/github/forks/microsoft/mcp-for-beginners.svg?style=social&label=Fork)](https://GitHub.com/microsoft/mcp-for-beginners/fork)
2. **Clone the Repository**:   `git clone https://github.com/microsoft/mcp-for-beginners.git`
3. **Join The** [![Microsoft Foundry Discord](https://dcbadge.limes.pink/api/server/nTYy5BXMWG)](https://discord.gg/nTYy5BXMWG)


### 🌐 多語言支援

#### 透過 GitHub Action 支援（自動且常保最新）

<!-- CO-OP TRANSLATOR LANGUAGES TABLE START -->
[Arabic](../ar/README.md) | [Bengali](../bn/README.md) | [Bulgarian](../bg/README.md) | [Burmese (Myanmar)](../my/README.md) | [Chinese (Simplified)](../zh-CN/README.md) | [Chinese (Traditional, Hong Kong)](./README.md) | [Chinese (Traditional, Macau)](../zh-MO/README.md) | [Chinese (Traditional, Taiwan)](../zh-TW/README.md) | [Croatian](../hr/README.md) | [Czech](../cs/README.md) | [Danish](../da/README.md) | [Dutch](../nl/README.md) | [Estonian](../et/README.md) | [Finnish](../fi/README.md) | [French](../fr/README.md) | [German](../de/README.md) | [Greek](../el/README.md) | [Hebrew](../he/README.md) | [Hindi](../hi/README.md) | [Hungarian](../hu/README.md) | [Indonesian](../id/README.md) | [Italian](../it/README.md) | [Japanese](../ja/README.md) | [Kannada](../kn/README.md) | [Korean](../ko/README.md) | [Lithuanian](../lt/README.md) | [Malay](../ms/README.md) | [Malayalam](../ml/README.md) | [Marathi](../mr/README.md) | [Nepali](../ne/README.md) | [Nigerian Pidgin](../pcm/README.md) | [Norwegian](../no/README.md) | [Persian (Farsi)](../fa/README.md) | [Polish](../pl/README.md) | [Portuguese (Brazil)](../pt-BR/README.md) | [Portuguese (Portugal)](../pt-PT/README.md) | [Punjabi (Gurmukhi)](../pa/README.md) | [Romanian](../ro/README.md) | [Russian](../ru/README.md) | [Serbian (Cyrillic)](../sr/README.md) | [Slovak](../sk/README.md) | [Slovenian](../sl/README.md) | [Spanish](../es/README.md) | [Swahili](../sw/README.md) | [Swedish](../sv/README.md) | [Tagalog (Filipino)](../tl/README.md) | [Tamil](../ta/README.md) | [Telugu](../te/README.md) | [Thai](../th/README.md) | [Turkish](../tr/README.md) | [Ukrainian](../uk/README.md) | [Urdu](../ur/README.md) | [Vietnamese](../vi/README.md)

> **想要本地 Clone？**

> 這個倉庫包含 50 多種語言翻譯，因此下載大小會明顯增加。若想不下載翻譯內容，請使用 sparse checkout：
> ```bash
> git clone --filter=blob:none --sparse https://github.com/microsoft/mcp-for-beginners.git
> cd mcp-for-beginners
> git sparse-checkout set --no-cone '/*' '!translations' '!translated_images'
> ```
> 這樣您可以更快完成所需課程內容的下載。
<!-- CO-OP TRANSLATOR LANGUAGES TABLE END -->

# 🚀 Model Context Protocol（MCP）初學者課程

## **使用 C#, Java, JavaScript, Rust, Python 和 TypeScript 實作範例學習 MCP**

## 🧠 Model Context Protocol 課程概覽
歡迎踏上您的 Model Context Protocol 之旅！如果您曾經好奇 AI 應用程式如何與不同工具和服務溝通，現在您將發現這個優雅的解決方案，它正在改變開發者構建智能系統的方式。

將 MCP 想像成 AI 應用程式的萬用翻譯器——就像 USB 埠讓您能將任何裝置連接到電腦一樣，MCP 讓 AI 模型以標準化的方式連接任何工具或服務。無論您正在構建第一個聊天機器人還是正在開發複雜的 AI 工作流程，了解 MCP 都會讓您擁有創造更強大更靈活應用程式的能力。

這個課程以耐心與關懷設計您的學習歷程。我們會從您已了解的簡單概念開始，並透過您喜愛的程式語言循序漸進地建立專業知識。每一步都包含清晰的說明、實作範例及滿滿鼓勵。

當您完成這趟旅程時，您將有信心打造自己的 MCP 伺服器，將它們與流行 AI 平台整合，並理解這項技術如何重塑 AI 開發的未來。讓我們一起展開這場令人興奮的冒險吧！

### 官方文件與規範

本課程對應 **MCP 規範 2025-11-25**（最新穩定版本）。MCP 規範使用日期版本號（YYYY-MM-DD 格式）以確保協定版本清晰。

這些資源隨著您的理解加深而越來越有價值，但不必急於一次看完。請從最感興趣的主題開始！
- 📘 [MCP 文件](https://modelcontextprotocol.io/) – 這是您實作教程與使用指南的首選資源。文件為初學者量身打造，提供清楚易懂的範例，讓您可自行跟著一步步練習。
- 📜 [MCP 規範](https://modelcontextprotocol.io/specification/2025-11-25) – 此為完整參考手冊。隨著課程進展，您會經常回來查閱特定細節或探索進階功能。
- 📜 [MCP 規範版本](https://modelcontextprotocol.io/specification/versioning) – 在此可了解協定版本沿革及 MCP 使用基於日期的版本號（YYYY-MM-DD 格式）。
- 🧑‍💻 [MCP GitHub 倉庫](https://github.com/modelcontextprotocol) – 裡面有多種程式語言的 SDK、工具和程式碼範例。彷彿是眼前的寶藏，充滿實用範例及現成元件。
- 🌐 [MCP 社群](https://github.com/orgs/modelcontextprotocol/discussions) – 與其他學習者與經驗豐富的開發者一同討論 MCP。這裡是友善的社群，歡迎提問並自由分享知識。
  
## 學習目標

完成本課程後，您將信心滿滿且充滿熱忱。您將能達成以下目標：

• **了解 MCP 基礎**：您會理解 Model Context Protocol 是什麼，以及為什麼它正在革新 AI 應用合作方式，搭配生活類比與範例幫助理解。

• **構建第一個 MCP 伺服器**：您將用自己熟悉的程式語言打造一個可運作的 MCP 伺服器，從簡單範例開始，逐步提升技能。

• **連接 AI 模型與實際工具**：您會學會如何橋接 AI 模型與真實服務，為應用帶來強大新功能。

• **實作安全性最佳做法**：您將了解如何保持 MCP 實作安全，保護應用及用戶。

• **有信心部署**：您將知道如何將 MCP 專案從開發帶向正式環境，實用的部署策略助您在實際世界成功上線。

• **加入 MCP 社群**：您將成為快速茁壯的開發者社群一員，共同形塑 AI 應用開發的未來。

## 基本背景知識

在深入 MCP 細節前，我們先確保您了解一些基礎概念。別擔心，如果您不是這些領域的專家，我們會一路解說所需知識！

### 理解協定（基礎）

把協定想像成人與人溝通的規則。打電話給朋友時，雙方都知道接聽時說「哈囉」，輪流說話，結束時說「再見」。電腦程式之間也需要類似規則，才能順利溝通。

MCP 是一種協定——一組約定的規則，幫助 AI 模型和應用程式與工具及服務作有意義的「對話」。就像人際溝通有規則才能順暢，MCP 讓 AI 應用溝通更可靠、更強大。

### 客戶端－伺服器關係（程式如何共同工作）

您每天都在使用客戶端－伺服器模式！使用瀏覽器（客戶端）瀏覽網站時，您連到傳送網頁內容的網頁伺服器。瀏覽器知道怎麼提出要求，伺服器知道如何回應。

MCP 也是類似關係：AI 模型當作客戶端請求資料或動作，而 MCP 伺服器提供這些能力。就像 AI 有個貼心助手（伺服器），能幫忙執行特定任務。

### 標準化的重要（讓所有東西一起運作）

想像如果每家車廠的油槍形狀都不一樣——您每台車都得有不同接頭！標準化就是同意用共通設計，確保東西能無縫連接。

MCP 就是 AI 應用的標準化。取代每個 AI 模型都得為每個工具寫專屬程式碼，MCP 建立標準溝通方式。如此開發者可只寫一次工具，卻能與多種 AI 系統配合。

## 🧭 您的學習路徑總覽

您的 MCP 旅程經過精心規劃，逐步建立自信與技能。每個階段除了引入新概念，也強化既有學習。

### 🌱 基礎階段：理解基本（模組 0-2）

冒險從此開始！我們用熟悉的比喻與簡單範例介紹 MCP 概念。您會了解 MCP 是什麼、為何存在，以及它如何融入 AI 開發更廣大的世界。

• **模組 0 — MCP 介紹**：探索 MCP 是什麼，為什麼對現代 AI 應用如此重要。您將看到 MCP 在現實世界的應用範例，了解它如何解決開發者常見問題。

• **模組 1 — 核心概念說明**：這裡學習 MCP 的主要構成元素。我們用大量比喻和視覺範例，確保概念直覺且易於理解。

• **模組 2 — MCP 的安全性**：安全性或許聽起來很複雜，但我們會說明 MCP 內建的安全機制，並教您從一開始就落實的最佳實踐。

### 🔨 建構階段：打造您的第一個實作（模組 3）

現在真正的樂趣開始了！您將親手打造 MCP 伺服器與客戶端。別擔心，我們從簡單開始，並逐步帶您完成每一步。
此模組包含多個實作指南，讓您可使用偏好的程式語言進行練習。您將建立第一個伺服器、打造一個連接該伺服器的用戶端，甚至整合流行的開發工具，如 VS Code。

每個指南都包含完整的程式碼範例、疑難排解技巧，以及我們作出特定設計選擇的說明。完成本階段後，您將擁有可自豪的 MCP 實作！

### 🚀 成長階段：進階概念與實務應用（模組 4-5）

在掌握基礎後，您準備探索更複雜的 MCP 功能。我們將涵蓋實務實現策略、除錯技巧，以及多模態 AI 整合等進階主題。

您還將學習如何擴展 MCP 實作以用於生產環境，並與 Azure 等雲端平台整合。這些模組助您打造可應付現實世界需求的 MCP 解決方案。

### 🌟 精通階段：社群與專業領域（模組 6-11）

最後階段聚焦加入 MCP 社群並專注您最感興趣的領域。您會學習如何貢獻開源 MCP 專案、實作進階認證模式，建構完整的資料庫整合解決方案。

特別推薦模組 11 — 是完整的 13 實驗室動手學習路線，教您打造具 PostgreSQL 整合的生產就緒 MCP 伺服器。猶如一個總結專案，將您所學全部結合！

### 📚 完整課程結構

| Module | Topic | Description | Link |
|--------|-------|-------------|------|
| **Module 0-3: Fundamentals** | | | |
| 00 | MCP 簡介 | Model Context Protocol 概述及其在 AI 流程中的重要性 | [Read more](./00-Introduction/README.md) |
| 01 | 核心概念詳解 | 深入探討 MCP 核心概念 | [Read more](./01-CoreConcepts/README.md) |
| 02 | MCP 安全 | 安全威脅與最佳實務 | [Read more](./02-Security/README.md) |
| 03 | MCP 快速入門 | 環境設定、基本伺服器/用戶端、整合 | [Read more](./03-GettingStarted/README.md) |
| **Module 3: 建立第一個伺服器與用戶端** | | | |
| 3.1 | 第一個伺服器 | 建立第一個 MCP 伺服器 | [Guide](./03-GettingStarted/01-first-server/README.md) |
| 3.2 | 第一個用戶端 | 開發基本 MCP 用戶端 | [Guide](./03-GettingStarted/02-client/README.md) |
| 3.3 | 帶 LLM 的用戶端 | 整合大型語言模型 | [Guide](./03-GettingStarted/03-llm-client/README.md) |
| 3.4 | VS Code 整合 | 在 VS Code 使用 MCP 伺服器 | [Guide](./03-GettingStarted/04-vscode/README.md) |
| 3.5 | stdio 伺服器 | 使用 stdio 傳輸建立伺服器 | [Guide](./03-GettingStarted/05-stdio-server/README.md) |
| 3.6 | HTTP 串流 | 實作 MCP 的 HTTP 串流功能 | [Guide](./03-GettingStarted/06-http-streaming/README.md) |
| 3.7 | AI 工具包 | 與 MCP 一起使用 AI 工具包 | [Guide](./03-GettingStarted/07-aitk/README.md) |
| 3.8 | 測試 | 測試您的 MCP 伺服器實作 | [Guide](./03-GettingStarted/08-testing/README.md) |
| 3.9 | 部署 | 將 MCP 伺服器部署到生產環境 | [Guide](./03-GettingStarted/09-deployment/README.md) |
| 3.10 | 高階伺服器使用 | 使用高階伺服器享用進階功能與改良架構 | [Guide](./03-GettingStarted/10-advanced/README.md) |
| 3.11 | 簡易認證 | 從頭學習認證與角色基礎存取控制（RBAC） | [Guide](./03-GettingStarted/11-simple-auth/README.md) |
| 3.12 | MCP 主機 | 設定 Claude Desktop、Cursor、Cline 等 MCP 主機 | [Guide](./03-GettingStarted/12-mcp-hosts/README.md) |
| 3.13 | MCP 檢查器 | 使用 Inspector 工具進行 MCP 伺服器除錯與測試 | [Guide](./03-GettingStarted/13-mcp-inspector/README.md) |
| **Module 4-5: 實務與進階** | | | |
| 04 | 實務實作 | SDK、除錯、測試、可重用提示模板 | [Read more](./04-PracticalImplementation/README.md) |
| 4.1 | 分頁 | 使用游標分頁處理大量結果集 | [Guide](./04-PracticalImplementation/pagination/README.md) |
| 05 | MCP 進階主題 | 多模態 AI、擴展、企業應用 | [Read more](./05-AdvancedTopics/README.md) |
| 5.1 | Azure 整合 | MCP 與 Azure 整合 | [Guide](./05-AdvancedTopics/mcp-integration/README.md) |
| 5.2 | 多模態 | 多種模式處理 | [Guide](./05-AdvancedTopics/mcp-multi-modality/README.md) |
| 5.3 | OAuth2 示範 | 實作 OAuth2 認證 | [Guide](./05-AdvancedTopics/mcp-oauth2-demo/README.md) |
| 5.4 | 頂層上下文 | 理解並實作根上下文 | [Guide](./05-AdvancedTopics/mcp-root-contexts/README.md) |
| 5.5 | 路由 | MCP 路由策略 | [Guide](./05-AdvancedTopics/mcp-routing/README.md) |
| 5.6 | 取樣 | MCP 中的取樣技術 | [Guide](./05-AdvancedTopics/mcp-sampling/README.md) |
| 5.7 | 擴展 | 擴展 MCP 實作 | [Guide](./05-AdvancedTopics/mcp-scaling/README.md) |
| 5.8 | 安全 | 進階安全考量 | [Guide](./05-AdvancedTopics/mcp-security/README.md) |
| 5.9 | 網路搜尋 | 實作網路搜尋功能 | [Guide](./05-AdvancedTopics/web-search-mcp/README.md) |
| 5.10 | 即時串流 | 建立即時串流功能 | [Guide](./05-AdvancedTopics/mcp-realtimestreaming/README.md) |
| 5.11 | 即時搜尋 | 實作即時搜尋 | [Guide](./05-AdvancedTopics/mcp-realtimesearch/README.md) |
| 5.12 | Entra ID 認證 | 使用 Microsoft Entra ID 認證 | [Guide](./05-AdvancedTopics/mcp-security-entra/README.md) |
| 5.13 | Foundry 整合 | 與 Azure AI Foundry 整合 | [Guide](./05-AdvancedTopics/mcp-foundry-agent-integration/README.md) |
| 5.14 | 上下文工程 | 有效的上下文工程技巧 | [Guide](./05-AdvancedTopics/mcp-contextengineering/README.md) |
| 5.15 | MCP 自訂傳輸 | 自訂傳輸實作 | [Guide](./05-AdvancedTopics/mcp-transport/README.md) |
| 5.16 | 協定功能 | 進度通知、取消、資源模板 | [Guide](./05-AdvancedTopics/mcp-protocol-features/README.md) |
| **Module 6-10: 社群與最佳實務** | | | |
| 06 | 社群貢獻 | 如何參與 MCP 生態系 | [Guide](./06-CommunityContributions/README.md) |
| 07 | 早期採用洞見 | 現實世界實作故事 | [Guide](./07-LessonsfromEarlyAdoption/README.md) |
| 08 | MCP 最佳實務 | 性能、容錯、韌性 | [Guide](./08-BestPractices/README.md) |
| 09 | MCP 案例研究 | 實務實作範例 | [Guide](./09-CaseStudy/README.md) |
| 10 | 動手工作坊 | 使用 AI 工具包建 MCP 伺服器 | [Lab](./10-StreamliningAIWorkflowsBuildingAnMCPServerWithAIToolkit/README.md) |
| **Module 11: MCP 伺服器動手實驗室** | | | |
| 11 | MCP 伺服器資料庫整合 | PostgreSQL 整合的完整 13 實驗室動手學習路線 | [Labs](./11-MCPServerHandsOnLabs/README.md) |
| 11.1 | 簡介 | MCP 與資料庫整合及零售分析案例概述 | [Lab 00](./11-MCPServerHandsOnLabs/00-Introduction/README.md) |
| 11.2 | 核心架構 | 理解 MCP 伺服器架構、資料庫層級及安全模式 | [Lab 01](./11-MCPServerHandsOnLabs/01-Architecture/README.md) |
| 11.3 | 安全與多租戶 | 行級安全、認證與多租戶資料存取 | [Lab 02](./11-MCPServerHandsOnLabs/02-Security/README.md) |
| 11.4 | 環境設定 | 設定開發環境、Docker、Azure 資源 | [Lab 03](./11-MCPServerHandsOnLabs/03-Setup/README.md) |
| 11.5 | 資料庫設計 | PostgreSQL 設定、零售架構設計及範例資料 | [Lab 04](./11-MCPServerHandsOnLabs/04-Database/README.md) |
| 11.6 | MCP 伺服器實作 | 建置具資料庫整合的 FastMCP 伺服器 | [Lab 05](./11-MCPServerHandsOnLabs/05-MCP-Server/README.md) |
| 11.7 | 工具開發 | 建立資料庫查詢工具與架構檢視 | [Lab 06](./11-MCPServerHandsOnLabs/06-Tools/README.md) |
| 11.8 | 語意搜尋 | 使用 Azure OpenAI 與 pgvector 實作向量嵌入 | [Lab 07](./11-MCPServerHandsOnLabs/07-Semantic-Search/README.md) |
| 11.9 | 測試與除錯 | 測試策略、除錯工具及驗證方法 | [Lab 08](./11-MCPServerHandsOnLabs/08-Testing/README.md) |
| 11.10 | VS Code 整合 | 設定 VS Code MCP 整合及 AI 聊天使用 | [Lab 09](./11-MCPServerHandsOnLabs/09-VS-Code/README.md) |
| 11.11 | 部署策略 | Docker 部署、Azure Container Apps 及擴展考量 | [Lab 10](./11-MCPServerHandsOnLabs/10-Deployment/README.md) |
| 11.12 | 監控 | 應用洞察、日誌紀錄、性能監控 | [Lab 11](./11-MCPServerHandsOnLabs/11-Monitoring/README.md) |
| 11.13 | 最佳實務 | 性能優化、安全強化及生產環境建議 | [Lab 12](./11-MCPServerHandsOnLabs/12-Best-Practices/README.md) |

### 💻 範例程式專案

學習 MCP 最令人興奮的部分之一是看到您的程式能力逐步成長。我們設計的程式碼範例從簡單開始，隨著您理解深化而變得更複雜。以下介紹了我們如何引入概念 – 使用易懂且展示真實 MCP 原則的程式碼，您不僅會理解程式碼在做什麼，也會知道為何如此結構，以及它如何融入更大的 MCP 應用中。

#### 基本 MCP 計算機範例

| Language | Description | Link |
|----------|-------------|------|
| C# | MCP 伺服器範例 | [View Code](./03-GettingStarted/samples/csharp/README.md) |
| Java | MCP 計算機 | [View Code](./03-GettingStarted/samples/java/calculator/README.md) |
| JavaScript | MCP 展示 | [View Code](./03-GettingStarted/samples/javascript/README.md) |
| Python | MCP 伺服器 | [View Code](../../03-GettingStarted/samples/python/mcp_calculator_server.py) |
| TypeScript | MCP 範例 | [View Code](./03-GettingStarted/samples/typescript/README.md) |
| Rust | MCP 範例 | [View Code](./03-GettingStarted/samples/rust/README.md) |

#### 進階 MCP 實作

| Language | Description | Link |
|----------|-------------|------|
| C# | 進階範例 | [View Code](./04-PracticalImplementation/samples/csharp/README.md) |
| Java with Spring | Container App 範例 | [View Code](./04-PracticalImplementation/samples/java/containerapp/README.md) |
| JavaScript | 進階範例 | [View Code](./04-PracticalImplementation/samples/javascript/README.md) |
| Python | 複雜實作 | [View Code](./04-PracticalImplementation/samples/python/README.md) |
| TypeScript | 容器範例 | [View Code](./04-PracticalImplementation/samples/typescript/README.md) |


## 🎯 MCP 學習先決條件

為了充分利用此課程，您應具備：

- 基本程式設計能力，且熟悉以下至少一種語言：C#、Java、JavaScript、Python 或 TypeScript
- 了解客戶端-伺服器模型及 API
- 熟悉 REST 與 HTTP 概念
- （選項）具 AI/ML 概念基礎

- 加入我們的社群討論以取得支援

## 📚 學習指南與資源

本儲存庫包含多項資源，協助您有效導航與學習：

### 學習指南
一份全面的[學習指南](./study_guide.md)可幫助你有效瀏覽此儲存庫。這個視覺課程地圖展示了所有主題的連結，並提供如何有效使用範例專案的指引。對於喜歡從整體視角學習的視覺學習者尤其有用。

該指南包含：
- 顯示所有涵蓋主題的視覺課程地圖
- 各儲存庫部分的詳細拆解
- 如何使用範例專案的指導
- 針對不同技能層級的推薦學習路徑
- 補充你學習旅程的額外資源

### 變更日誌

我們維護詳細的[變更日誌](./changelog.md)，追蹤課程材料的所有重大更新，讓你隨時掌握最新的改進與新增內容。
- 新增內容
- 結構變更
- 功能改進
- 文件更新

## 🛠️ 如何有效使用本課程

本指南中的每堂課包括：

1. 清楚解釋 MCP 概念  
2. 多種語言的實時程式碼範例  
3. 建立實際 MCP 應用的練習  
4. 進階學習者的額外資源

### 一起用 C# 學習 MCP - 教學系列
讓我們一起了解 Model Context Protocol (MCP)，這是一個用以標準化 AI 模型與客戶端應用程式間互動的先進框架。透過這個初學者友善的課程，我們將介紹 MCP 並引導你建立第一個 MCP 伺服器。
#### C#: [https://aka.ms/letslearnmcp-csharp](https://aka.ms/letslearnmcp-csharp)
#### Java: [https://aka.ms/letslearnmcp-java](https://aka.ms/letslearnmcp-java)
#### JavaScript: [https://aka.ms/letslearnmcp-javascript](https://aka.ms/letslearnmcp-javascript)
#### Python: [https://aka.ms/letslearnmcp-python](https://aka.ms/letslearnmcp-python)

## 🎓 你的 MCP 旅程開始了

恭喜你！你剛踏出了充滿刺激的旅程第一步，這將擴展你的程式能力並將你接軌至人工智能開發的前沿。

### 你已完成的成就

藉由閱讀這份介紹，你已開始構建自己的 MCP 知識基礎。你理解 MCP 是什麼、它的重要性，以及這套課程如何支持你的學習旅程。這是一個重大成就，也是你在這項重要技術中獲得專業知識的開始。

### 未來的冒險

隨著你逐步完成各模組，請記得每位專家都曾是初學者。現在看似複雜的概念，隨著不斷練習和應用，將會變得自然而然。每個小步驟都匯聚成強大的能力，將伴隨你的整個開發生涯。

### 你的支援網絡

你將加入一群熱衷於 MCP 的學習者與專家社群，大家樂於幫助他人成功。無論你在程式碼挑戰中卡關，還是發現突破點想分享，社群都會支持你的旅程。

如果你遇到瓶頸或有關於建構 AI 應用的任何疑問，請加入與其他學習者和經驗豐富開發者的討論。這是一個支持性的社群，歡迎發問並自由分享知識。

[![Microsoft Foundry Discord](https://dcbadge.limes.pink/api/server/nTYy5BXMWG)](https://discord.gg/nTYy5BXMWG)

如果你在建構過程中有產品反饋或錯誤，請造訪：

[![Microsoft Foundry Developer Forum](https://img.shields.io/badge/GitHub-Microsoft_Foundry_Developer_Forum-blue?style=for-the-badge&logo=github&color=000000&logoColor=fff)](https://aka.ms/foundry/forum)

### 準備好開始了嗎？

你的 MCP 冒險現在開始！從 Module 0 開始，深入體驗你的第一個手把手 MCP 實作，或先探索範例專案看看你將會建置什麼。記住—每位專家都從你現在的位置開始，只要有耐心與練習，你會驚訝自己能達成的成就。

歡迎來到 Model Context Protocol 開發的世界。讓我們一起打造出驚人的作品！

## 🤝 為學習社群做出貢獻

這套課程隨著像你這樣的學習者貢獻而日益強大！不論是修正錯字、建議更清楚說明，或是新增範例，你的貢獻都能幫助其他初學者成功。

感謝 Microsoft 優秀專家 [Shivam Goyal](https://www.linkedin.com/in/shivam2003/) 貢獻程式碼範例。

貢獻流程設計為友善且支持性的。大部分貢獻需要簽署貢獻者授權協議 (CLA)，但自動化工具會引導你順利完成流程。

## 📜 開源學習

整個課程均採用 MIT [LICENSE](../../LICENSE) 授權，意味著你可以自由使用、修改與分享。這支持我們讓 MCP 知識觸及全球開發者的使命。

## 🤝 貢獻指引

本專案歡迎貢獻與建議。大多數貢獻需同意  
貢獻者授權協議 (CLA)，聲明你有權利且確實授權我們  
使用你的貢獻。詳情請見 <https://cla.opensource.microsoft.com>。

提交拉取請求時，CLA 機器人會自動判斷你是否需提供CLA，並在 PR 上標記（例如狀態檢查、留言）。請依照機器人指示操作。你只需在所有帶 CLA 的儲存庫中完成一次。

本專案已採用[Microsoft 開源行為守則](https://opensource.microsoft.com/codeofconduct/)。  
詳情請參閱[行為守則常見問題](https://opensource.microsoft.com/codeofconduct/faq/)，或將任何疑問發送至[opencode@microsoft.com](mailto:opencode@microsoft.com)。

---

*準備好開始你的 MCP 旅程了嗎？從[Module 00 - MCP 簡介](./00-Introduction/README.md)開始，踏出你進入 Model Context Protocol 執行開發世界的第一步！*



## 🎒 其他課程
我們團隊還製作了其他課程！請查看：

<!-- CO-OP TRANSLATOR OTHER COURSES START -->
### LangChain
[![LangChain4j for Beginners](https://img.shields.io/badge/LangChain4j%20for%20Beginners-22C55E?style=for-the-badge&&labelColor=E5E7EB&color=0553D6)](https://aka.ms/langchain4j-for-beginners)
[![LangChain.js for Beginners](https://img.shields.io/badge/LangChain.js%20for%20Beginners-22C55E?style=for-the-badge&labelColor=E5E7EB&color=0553D6)](https://aka.ms/langchainjs-for-beginners?WT.mc_id=m365-94501-dwahlin)
[![LangChain for Beginners](https://img.shields.io/badge/LangChain%20for%20Beginners-22C55E?style=for-the-badge&labelColor=E5E7EB&color=0553D6)](https://github.com/microsoft/langchain-for-beginners?WT.mc_id=m365-94501-dwahlin)
---

### Azure / Edge / MCP / Agents
[![AZD for Beginners](https://img.shields.io/badge/AZD%20for%20Beginners-0078D4?style=for-the-badge&labelColor=E5E7EB&color=0078D4)](https://github.com/microsoft/AZD-for-beginners?WT.mc_id=academic-105485-koreyst)
[![Edge AI for Beginners](https://img.shields.io/badge/Edge%20AI%20for%20Beginners-00B8E4?style=for-the-badge&labelColor=E5E7EB&color=00B8E4)](https://github.com/microsoft/edgeai-for-beginners?WT.mc_id=academic-105485-koreyst)
[![MCP for Beginners](https://img.shields.io/badge/MCP%20for%20Beginners-009688?style=for-the-badge&labelColor=E5E7EB&color=009688)](https://github.com/microsoft/mcp-for-beginners?WT.mc_id=academic-105485-koreyst)
[![AI Agents for Beginners](https://img.shields.io/badge/AI%20Agents%20for%20Beginners-00C49A?style=for-the-badge&labelColor=E5E7EB&color=00C49A)](https://github.com/microsoft/ai-agents-for-beginners?WT.mc_id=academic-105485-koreyst)

---
 
### 生成式 AI 系列
[![Generative AI for Beginners](https://img.shields.io/badge/Generative%20AI%20for%20Beginners-8B5CF6?style=for-the-badge&labelColor=E5E7EB&color=8B5CF6)](https://github.com/microsoft/generative-ai-for-beginners?WT.mc_id=academic-105485-koreyst)
[![Generative AI (.NET)](https://img.shields.io/badge/Generative%20AI%20(.NET)-9333EA?style=for-the-badge&labelColor=E5E7EB&color=9333EA)](https://github.com/microsoft/Generative-AI-for-beginners-dotnet?WT.mc_id=academic-105485-koreyst)
[![Generative AI (Java)](https://img.shields.io/badge/Generative%20AI%20(Java)-C084FC?style=for-the-badge&labelColor=E5E7EB&color=C084FC)](https://github.com/microsoft/generative-ai-for-beginners-java?WT.mc_id=academic-105485-koreyst)
[![Generative AI (JavaScript)](https://img.shields.io/badge/Generative%20AI%20(JavaScript)-E879F9?style=for-the-badge&labelColor=E5E7EB&color=E879F9)](https://github.com/microsoft/generative-ai-with-javascript?WT.mc_id=academic-105485-koreyst)

---
 
### 核心學習
[![ML for Beginners](https://img.shields.io/badge/ML%20for%20Beginners-22C55E?style=for-the-badge&labelColor=E5E7EB&color=22C55E)](https://aka.ms/ml-beginners?WT.mc_id=academic-105485-koreyst)
[![Data Science for Beginners](https://img.shields.io/badge/Data%20Science%20for%20Beginners-84CC16?style=for-the-badge&labelColor=E5E7EB&color=84CC16)](https://aka.ms/datascience-beginners?WT.mc_id=academic-105485-koreyst)
[![AI for Beginners](https://img.shields.io/badge/AI%20for%20Beginners-A3E635?style=for-the-badge&labelColor=E5E7EB&color=A3E635)](https://aka.ms/ai-beginners?WT.mc_id=academic-105485-koreyst)
[![Cybersecurity for Beginners](https://img.shields.io/badge/Cybersecurity%20for%20Beginners-F97316?style=for-the-badge&labelColor=E5E7EB&color=F97316)](https://github.com/microsoft/Security-101?WT.mc_id=academic-96948-sayoung)
[![Web Dev for Beginners](https://img.shields.io/badge/Web%20Dev%20for%20Beginners-EC4899?style=for-the-badge&labelColor=E5E7EB&color=EC4899)](https://aka.ms/webdev-beginners?WT.mc_id=academic-105485-koreyst)
[![IoT for Beginners](https://img.shields.io/badge/IoT%20for%20Beginners-14B8A6?style=for-the-badge&labelColor=E5E7EB&color=14B8A6)](https://aka.ms/iot-beginners?WT.mc_id=academic-105485-koreyst)
[![XR Development for Beginners](https://img.shields.io/badge/XR%20Development%20for%20Beginners-38BDF8?style=for-the-badge&labelColor=E5E7EB&color=38BDF8)](https://github.com/microsoft/xr-development-for-beginners?WT.mc_id=academic-105485-koreyst)

---
 
### Copilot 系列
[![Copilot for AI Paired Programming](https://img.shields.io/badge/Copilot%20for%20AI%20Paired%20Programming-FACC15?style=for-the-badge&labelColor=E5E7EB&color=FACC15)](https://aka.ms/GitHubCopilotAI?WT.mc_id=academic-105485-koreyst)
[![Copilot for C#/.NET](https://img.shields.io/badge/Copilot%20for%20C%23/.NET-FBBF24?style=for-the-badge&labelColor=E5E7EB&color=FBBF24)](https://github.com/microsoft/mastering-github-copilot-for-dotnet-csharp-developers?WT.mc_id=academic-105485-koreyst)
[![Copilot 冒險](https://img.shields.io/badge/Copilot%20Adventure-FDE68A?style=for-the-badge&labelColor=E5E7EB&color=FDE68A)](https://github.com/microsoft/CopilotAdventures?WT.mc_id=academic-105485-koreyst)
<!-- CO-OP TRANSLATOR OTHER COURSES END -->

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**免責聲明**：
本文件是使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 所翻譯。雖然我們致力於提供準確的翻譯，但請注意，自動翻譯可能包含錯誤或不準確之處。原始文件的母語版本應被視為權威來源。對於重要資訊，建議採用專業人工翻譯。我們不對因使用此翻譯而引起的任何誤解或誤讀承擔責任。
<!-- CO-OP TRANSLATOR DISCLAIMER END -->