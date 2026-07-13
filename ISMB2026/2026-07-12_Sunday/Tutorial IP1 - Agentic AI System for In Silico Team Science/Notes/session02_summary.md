# 會議記錄與教程整理：Agentic AI System for In Silico Team Science (Session 02)

本文件整理自會議記錄檔案 [session02.txt](file:///d:/Dropbox/2026_ismb26/會議記錄/Tutorial%20IP1%20Agentic%20AI%20System%20for%20In%20Silico%20Team%20Science%20From%20LLM%20Basics%20to%20Lab%20Assistant%20Agents%201/session02.txt)，並結合與會討論中提及的兩個核心 GitHub 專案內容進行補充。

---

## 📅 教程基本資訊 (Session 02 - Q&A 與實作探討)
*   **主題**：Q&A 與進階智能體工程探討 (LLM Benchmarking, State Management, and Future of Science)
*   **核心焦點**：
    *   開源與閉源 LLM 的基準測試對比（特別在基因集分析任務）。
    *   如何建構無幻覺的文獻檢索與知識驗證系統。
    *   智能體工作流的狀態管理、故障恢復與安全沙箱。
    *   AI 時代下生物資訊人才的教育轉型與學術論文發表的未來模式。

---

## 🧠 核心技術討論與問答精華

### 1. 開源/閉源模型在生物醫學任務的表現 (Open vs. Closed Models)
*   **基準測試**：針對基因集分析（Gene Set Analysis）等生物學任務，開源權重模型（Open-weight Models）與閉源模型（如 OpenAI/Anthropic 商業模型）的表現差距並不大。例如：閉源模型準確度約為 65%，而優秀的開源模型可達 63%。
*   **工具調用（Tool Call）與可靠度**：
    *   模型參數量與遵循工具指令的能力呈正相關。
    *   **27B (270億參數量)** 以上的模型（如 gemma-2-27b）在工具調用與 ReAct 循環中的表現相當穩定可靠。
    *   **7B (70億參數量)** 或更低參數的模型在工具調用的準確度上顯著下降，較不適用於複雜的智能體任務。

### 2. 智能體系統防幻覺機制 (Checks & Balances)
*   **多智能體制衡**：單一智能體容易產生幻覺，解決之道是建立多智能體團隊。包含「審查智能體 (Critic Agent)」、「品質控制智能體 (Quality Control Agent)」與「評估智能體 (Evaluation Agent)」。所有智能體在相同方向上同時幻覺的機率極低。
*   **邊緣門控/中間件 (Middleware & Gates)**：在智能體的工作流節點之間設置硬性規則門控（例如使用 Python 腳本檢驗輸出是否為標準 CSV，否則觸發重試）。此機制能有效截斷錯誤的累積與傳播。

### 3. 工作流狀態保存與恢復 (State Management)
*   **狀態記憶**：在執行複雜且耗時（例如數小時或花費數十美元）的工作流時，開發者可以鎖定前續節點的狀態並存檔。在對後續智能體進行除錯時，只需重新執行最後面的步驟，而不必從頭運行，大幅節省 Token 成本與時間。

### 4. 開源模型的安全性與沙箱隔離 (Security & Sandboxing)
*   **隱私與安全**：在本地運行開源模型是確保數據隱私的有效手段。針對下載開源權重可能包含惡意代碼的疑慮，講者指出在權重中藏入功能性惡意代碼在數學上極為困難。
*   **沙箱環境**：目前主流的 Agent 框架均內建安全沙箱環境（Sandbox），所有代碼生成與執行都在臨時容器中進行，不會危及宿主機安全。

### 5. AI 時代的生物資訊教育與學術發表變革
*   **教育轉型**：研究生不再需要死記硬背程式碼語法或公式推導。教育重點應轉向「**智能體團隊的管理能力 (Management Skills)**」以及「**批判性思考 (Critical Thinking)**」。學生需要學會如何拆解問題、指導多個專業 AI 智能體、審查 AI 的分析報告，並識辨隱藏的偏見。
*   **學術評級與發表**：傳統的論文發表與同行評審模式在 AI 寫作/AI 評審的普及下將面臨崩潰。未來的學術信用（Credit）應轉向**開源代碼庫的實質貢獻（GitHub Fork/PR）、工具的可重複性（Reproducibility）與數據共享**，而非單純的論文篇數。

---

## 🔗 核心 GitHub 專案補充整理

為配合 Session 02 的討論，以下詳細閱讀並整理了講者團隊與相關研究的兩個核心 Git 倉庫：

### 🧪 專案一：GeneAgent (Self-verification Language Agent)
*   **GitHub 連結**：[BinglanLi/GeneAgent](https://github.com/BinglanLi/GeneAgent)
*   **核心功能**：為**基因集分析 (Gene Set Analysis)** 專門設計的自我驗證語言智能體系統。
*   **解決痛點**：傳統 LLM 在解釋基因集功能時極易產生幻覺，編造不存在的生物學途徑或文獻。
*   **工作原理**：
    1.  基於 GPT-4 接收用戶的基因集，初步生成候選的生物學功能描述。
    2.  啟動**自我驗證機制 (Self-verification)**：自動調用 Web APIs 對接權威的領域資料庫（如 Gene Ontology, NCBI, Pathway Commons 等）。
    3.  根據獲取的客觀事實證據，對 LLM 的預測進行事實檢驗（Fact Verification），修正錯誤並給出具備客觀證據支持的分析報告。
*   **技術棧**：使用 `baseagent`（底層智能體框架）、`langgraph`（工作流調度）、`pydantic`（數據校驗）與 `requests`（資料庫 API 交互）。

### 🏫 專案二：ISMB 2026 Biomedical Agent Engineering Tutorial
*   **GitHub 連結**：[EpistasisLab/ismb-2026-biomedical-agent-engineering](https://github.com/EpistasisLab/ismb-2026-biomedical-agent-engineering)
*   **核心功能**：為計算生物學家設計的動手實作教程，涵蓋從無程式碼平台到生產級多智能體管線。
*   **教程章節 (Jupyter Notebooks)**：
    1.  **[01] GUI Agent Builders**：對比三大無程式碼智能體平台（n8n 可視化流、Flowise RAG 管道、AutoGen Studio 多智能體），並引導動手搭建第一個免程式碼 Agent。
    2.  **[02] Python Client SDKs**：深入分析 Anthropic、OpenAI 與 LangChain SDK，手把手演練模型分級、系統提示詞、工具調用、狀態記憶（Checkpointer）與 Pydantic 結構化輸出。
    3.  **[03] MCP Agents**：介紹**模型上下文協議 (MCP)** 的 stdio 與 HTTP 架構，演示如何利用 FastMCP 撰寫自定義的 **PubMed 文獻檢索與全文提取 MCP 伺服器** (`server_pubmed.py`)。
    4.  **[04] ReAct Agents**：手寫與利用 LangGraph 實現 ReAct（推理-行動-觀察）閉環，使智能體能執行多步生物醫學工具調用。
    5.  **[05] Reflection — PGx Use Case**：以藥物基因體學 (PGx) 為場景，展示反思設計模式。智能體自動起草用藥建議，對照 CPIC 指南進行反思檢索，並利用 `redlines` 展示推薦修改的 diff。
    6.  **[06] Multi-Agent Orchestration**：搭建由「文獻總結智能體」、「審查智能體」與「監督智能體」組成的三智能體管線，展示學術論文自動審查系統的協同工作。

---
*整理時間：2026-07-13 (Based on ISMB 2026 Tutorial)*
