# 會議記錄與教程整理：Large Language Models and Agentic AI for Biomedical Informatics (Session 03)

本文件整理自會議記錄檔案 [session03.txt](file:///d:/antigravity/course-materials/ISMB2026/2026-07-12_Sunday/Tutorial%20IP2%20-%20Large%20Language%20Models%20and%20Agentic%20AI%20for%20Biomedical%20Informatics/Notes/session03.txt) 與 [session03_praticle.txt](file:///d:/antigravity/course-materials/ISMB2026/2026-07-12_Sunday/Tutorial%20IP2%20-%20Large%20Language%20Models%20and%20Agentic%20AI%20for%20Biomedical%20Informatics/Notes/session03_praticle.txt)，並結合動手操作教程 [ISMB_of_LLM_for_Bioinformatics_Demo.ipynb](file:///d:/antigravity/course-materials/ISMB2026/2026-07-12_Sunday/Tutorial%20IP2%20-%20Large%20Language%20Models%20and%20Agentic%20AI%20for%20Biomedical%20Informatics/Guided%20Hands-On/ISMB_of_LLM_for_Bioinformatics_Demo.ipynb) 內容進行深度整理。

---

## 📅 教程基本資訊 (Session 03 - 應用案例、智能體訓練與代碼生成基準)
*   **核心主題**：
    1.  生醫通用智能體生態與多智能體規模化（Biomni & Agentic Intelligence）
    2.  空間多體學分析智能體平台實踐（spatialOmicsLab）
    3.  生物資訊代碼生成基準測試（BioCoder）
*   **演講人**：Mark Gerstein (Yale, 虛擬)、Wenqi Shi (UT Southwestern)、Xuan Wang (Virginia Tech)、Robert Tang (Yale) 等

---

## 🧠 核心技術討論與實務應用

### 1. 通用生醫 AI 智能體：Biomni
*   **平台背景**：由史丹佛大學、Genentech、Arc 研究所、UCSF、普林斯頓與華盛頓大學等多家機構聯合開發。
*   **系統組成**：一個專門為生物醫學研究設計的通用智能體，集成了：
    *   **150 個專業工具**：涵蓋 DNA/RNA 序列分析、蛋白質結構預測、CRISPR 導向 RNA 設計、單細胞類型註釋、藥物-靶點相互作用（DTI）、藥代動力學（ADMET）預測、分子對接與克隆實驗方案設計等。
    *   **59 個生醫資料庫**：整合基因變異、蛋白質結構、生物通路、疾病關聯、藥物交互及科學文獻數據。
    *   **105 個套裝軟體**：包含常用的生物資訊分析管線、統計框架、機器學習工具與視覺化庫。
*   **人機協同工作空間**：提供整合式的可執行沙箱環境，生物學家提出研究目標與臨床問題，智能體在可重現的環境中搜尋文獻、編排並執行分析代碼、對接資料庫並產出結構化報告。

### 2. 生醫智能體訓練與規模化 (Scaling Agentic Intelligence)
演講者 Wenqi Shi 深入探討了如何提升科學智能體的能力：
*   **多智能體規模化陷阱**：在一些可以並行化的任務中，增加 Agent 數量能提升效能。但在複雜的科學研究任務中，如果單個 Agent 的基礎能力較弱，增加 Agent 數量（多智能體團隊）反而會因為協調混亂和錯誤傳播而**損害整體效能**。因此，首要任務是提升單一 Agent 的推理與執行能力。
*   **基於交互軌跡（Trajectory）的 Agent 訓練**：
    *   傳統 LLM 訓練僅需「問題 ➡️ 答案」對。而訓練一個合格的生醫 Agent 必須收集或合成完整的**執行軌跡數據**。
    *   一個軌跡包括：`原始任務 ➡️ 中間推理（Chain of Thought） ➡️ 寫代碼 ➡️ 執行代碼 ➡️ 獲取環境反饋（如執行出錯） ➡️ 錯誤排查與 Debug ➡️ 最終視覺化與驗證`。
    *   這種「在嘗試中學習（Trial and Error）」的動態軌跡在自然界中並不存在，需要通過專門的模擬環境（如 Biomni 或相關科學代碼沙箱）來大量合成。

### 3. 空間多體學智能體平台：spatialOmicsLab (omicsLab)
*   **背景痛點**：空間多體學（Spatial Omics）分析軟體生態極度碎片化，工具繁多且難以統一管線，生物學家難以實現跨工具的快速分析與結果重現。
*   **平台設計**：
    *   **集成規模**：集成了超過 **100 個空間多體學分析工具**、提供 **4000 多個可執行子任務**，並預置了 **16 個標準資料集**。
    *   **雙層架構**：
        1.  **環境層 (Environment Level)**：準備數據、容器化工具包、並提供輸出結果的驗證機制，以確保結果的固化與 100% 可重現性。
        2.  **智能體層 (Agent Level)**：接收用戶的自然語言意圖，自動將用戶目標翻譯為具體的工具參數、挑選演算法並串聯工作流。
    *   **專家級基準測試**：研究團隊在跨領域的 **28 個空間多體學資料集**上，將該智能體與人類專家手動分析進行了對比。測試涵蓋：空間結構聚類（Spatial Clustering）、細胞類型反褶積（Cell Type Deconvolution）和空間變異基因（SVG）識別。結果顯示，智能體自動化流程獲得了與人類專家手動優化高度 comparable 的分析效能。

---

## 💻 實作分享：BioCoder 生物資訊代碼生成基準

在動手操作部分，Robert Tang 與 Tom Qiu 展示了專門評估/輔助生物資訊代碼生成的基準平台 **BioCoder**（源自耶魯大學 Gerstein 實驗室）：

### 1. 什麼是 BioCoder？
*   **核心功能**：一個專門用於評估程式碼大模型（Code LLMs）在生物資訊學領域生成能力的 Benchmark。
*   **相較於通用代碼基準的特色**：一般的代碼生成任務（如 HumanEval）只要求生成獨立的簡單算法。但在實際的生物資訊項目中，代碼高度依賴於**整個倉庫的上下文（Whole-Repository Context）**——需要調用其他文件中的自定義類、輔助函數或第三方生物資訊包。

### 2. 實驗演示細節
教程基於 Google Colab，使用開源的 **DeepSeek-Coder-6.7B** 展示了三種代碼生成模式：
1.  **自然語言提示詞生成**：例如要求模型寫一個過濾 K-mers 的函數。在沒有上下文時，生成結果往往過於模糊或不符合特定庫的規律。
2.  **填補空白任務 (Fill in the Middle, FIM)**：展示了如何使用特定的 FIM 標記（如 `<|fim_hole|>`）告訴模型在已有代碼的中間插入多行缺失代碼。這是 GitHub Copilot 等工具的底層原理。
3.  **基於全倉庫上下文的檢索生成 (RAG-infused Generation)**：
    *   將整個 GitHub 倉庫代碼進行靜態分析與解析。
    *   在 Prompts 中注入相關文件的類定義與變數上下文（`contextCode`）、任務說明與預期解決方案。
    *   在有全倉庫上下文的支持下，模型可以成功調用自定義的生物資訊函數，生成正確的、與項目高度集成的代碼。
