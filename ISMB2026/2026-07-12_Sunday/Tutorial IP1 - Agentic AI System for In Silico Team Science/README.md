# Tutorial IP1 - Agentic AI System for In Silico Team Science: From LLM Basics to Lab Assistant Agents

**日期**: 2026年7月12日 (星期日) Pre-Conference
**時間**: 
- **Part 1**: 09:00 AM – 10:45 AM (ET)
- **Part 2**: 11:00 AM – 01:00 PM (ET)
**地點**: Georgetown (In Person)
**組織與主講人**: 
- **Dr. Jason Moore** (美國賓州大學 Epistasis 實驗室主持人、生醫人工智慧中心主任)
- **Dr. Feng** (馮博士)
- **Bill** (比爾) 及團隊成員

---

## 📅 課程概述与目標

大型語言模型（LLM）目前廣泛應用於生物醫學研究中的代碼生成與決策支持。然而，從單純的聊天機器人（Chatbots）演進到能夠與生物醫學數據和工具緊密協作的可靠「實驗室助理 AI 智能體（Lab Assistant AI Agents）」仍具挑戰性。本教程旨在彌合概念與生產實踐之間的差距。

本教程平衡了生醫 AI 智能體的概念介紹與動手實踐。前半部分專注於基礎概念，包括智能體的定義、生醫研究中的應用機會，以及智能體系統的構建塊（如技能、工具、知識庫、推理和角色）。後半部分引導參與者構建自己的智能體系統，學會拆解自然語言任務、選擇合適的工具、運行數據分析並產出研究報告。最後探討了多智能體系統、人機協同工作流（Human-in-the-loop）、輕量級日誌與成本追蹤等進階議題。

### 🎯 核心學習目標
1. **智能體配置**：為首選 LLM 提供商配置自主智能體。
2. **工具與 MCP 註冊**：註冊生物資訊相關工具（如用於序列分析或變異注釋的本地 Python 腳本）以及通用的生醫 Model Context Protocol (MCP) 伺服器。
3. **系統協同編排**：編排單智能體、多智能體和人機協同（Human-in-the-loop）系統。
4. **工作流自動化**：構建簡單的端到端「生物資訊學助理」或「生物資訊團隊」，自動提出、解釋並執行計算生物學工作流。

---

## 📂 學習資源與目錄結構

本目錄下包含該 Tutorial 的完整會議記錄與主題整理：

### 📁 [Notes (會議記錄與整理摘要)](file:///d:/antigravity/course-materials/ISMB2026/2026-07-12_Sunday/Tutorial%20IP1%20-%20Agentic%20AI%20System%20for%20In%20Silico%20Team%20Science/Notes)

*   **Session 01：智能體架構與工程基礎**
    *   📂 [session01.txt (原始會議記錄)](file:///d:/antigravity/course-materials/ISMB2026/2026-07-12_Sunday/Tutorial%20IP1%20-%20Agentic%20AI%20System%20for%20In%20Silico%20Team%20Science/Notes/session01.txt)
    *   📝 [session01_summary.md (整理版摘要)](file:///d:/antigravity/course-materials/ISMB2026/2026-07-12_Sunday/Tutorial%20IP1%20-%20Agentic%20AI%20System%20for%20In%20Silico%20Team%20Science/Notes/session01_summary.md)
        *   *包含：自主計算智能體（Computational Agent）定義、智能體的六大解剖結構、智能體工程（Agent Engineering）與制衡監督機制、出院患者隨訪與實驗室自動化案例研究。*

*   **Demo 01：n8n 可視化工作流平台實踐**
    *   📂 [session01_demo01.txt (原始會議記錄)](file:///d:/antigravity/course-materials/ISMB2026/2026-07-12_Sunday/Tutorial%20IP1%20-%20Agentic%20AI%20System%20for%20In%20Silico%20Team%20Science/Notes/session01_demo01.txt)
    *   📝 [session01_demo01_summary.md (整理版摘要)](file:///d:/antigravity/course-materials/ISMB2026/2026-07-12_Sunday/Tutorial%20IP1%20-%20Agentic%20AI%20System%20for%20In%20Silico%20Team%20Science/Notes/session01_demo01_summary.md)
        *   *包含：基於 n8n 平台的無程式碼/低程式碼智能體工作流配置，包含 PDF 論文自動化生成短影音工作流的技術細節。*

*   **Demo 02：AutoGen Studio 多智能體編排實踐**
    *   📂 [session01_demo02.txt (原始會議記錄)](file:///d:/antigravity/course-materials/ISMB2026/2026-07-12_Sunday/Tutorial%20IP1%20-%20Agentic%20AI%20System%20for%20In%20Silico%20Team%20Science/Notes/session01_demo02.txt)
    *   📝 [session01_demo02_summary.md (整理版摘要)](file:///d:/antigravity/course-materials/ISMB2026/2026-07-12_Sunday/Tutorial%20IP1%20-%20Agentic%20AI%20System%20for%20In%20Silico%20Team%20Science/Notes/session01_demo02_summary.md)
        *   *包含：使用 AutoGen Studio UI 定義 Agents、Skills 與 Workflows，展示如何進行多智能體協作與本地代碼沙箱執行。*

*   **Session 02：進階討論與開源項目實務**
    *   📂 [session02.txt (原始會議記錄)](file:///d:/antigravity/course-materials/ISMB2026/2026-07-12_Sunday/Tutorial%20IP1%20-%20Agentic%20AI%20System%20for%20In%20Silico%20Team%20Science/Notes/session02.txt)
    *   📝 [session02_summary.md (整理版摘要)](file:///d:/antigravity/course-materials/ISMB2026/2026-07-12_Sunday/Tutorial%20IP1%20-%20Agentic%20AI%20System%20for%20In%20Silico%20Team%20Science/Notes/session02_summary.md)
        *   *包含：開源與閉源模型基準測試對比、防幻覺的中間件門控設計、工作流狀態保存與恢復、AI 時代的生信教育轉型、以及兩個核心 GitHub 開源庫（GeneAgent 自我驗證智能體、ismb-2026-biomedical-agent-engineering 實作教程代碼）的技術細節。*

---

## 🔗 相關開源倉庫

*   **EcoXAI** ([EpistasisLab/EcoXAI](https://github.com/EpistasisLab/EcoXAI))：自動化生醫研究的多智能體框架。
*   **KRAGEN** ([EpistasisLab/KRAGEN](https://github.com/EpistasisLab/KRAGEN))：基於知識圖譜與 Graph-of-Thoughts 的問答與推理引擎。
*   **AlzKB** ([EpistasisLab/AlzKB](https://github.com/EpistasisLab/AlzKB))：用於阿茲海默症研究的生醫知識圖譜。
*   **GeneAgent** ([BinglanLi/GeneAgent](https://github.com/BinglanLi/GeneAgent))：基因集分析的自我驗證語言智能體。
*   **ismb-2026-biomedical-agent-engineering** ([EpistasisLab/ismb-2026-biomedical-agent-engineering](https://github.com/EpistasisLab/ismb-2026-biomedical-agent-engineering))：本教程的官方實動手實驗庫（包含 Colab/Jupyter Notebooks）。
