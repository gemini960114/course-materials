# 會議記錄與教程整理：Agentic AI 系統實務 Demo 演示

本文件整理自 Demo 演示會議記錄檔案 [session01_demo01.txt](file:///d:/Dropbox/2026_ismb26/%E6%9C%83%E8%AD%B0%E8%A8%98%E9%8C%84/Tutorial%20IP1%20Agentic%20AI%20System%20for%20In%20Silico%20Team%20Science%20From%20LLM%20Basics%20to%20Lab%20Assistant%20Agents%201/session01_demo01.txt)。

---

## 📅 演示基本資訊
*   **主題**：自主特徵工程與預測建模流程演示 (Autonomous Feature Engineering and Predictive Modeling Pipeline)
*   **使用技術**：
    *   **核心 LLM**：Claude 3.5 Sonnet（因其性價比高、工具調用能力強）
    *   **管道框架**：LangGraph（被講者稱為「智能體管道工程的 scikit-learn」）
    *   **工具接口**：本地託管的 MCP (Model Context Protocol) 伺服器與自定義工具
    *   **知識庫**：成癮知識庫 (Addiction KB, NLM 提供，包含數十萬節點、百萬連接)
*   **核心比喻**：設計智能體系統就像在組建一個 RPG（角色扮演遊戲）冒險隊伍，隊伍的角色（職業）越多元，能解決的複雜問題就越多。

---

## 🏕️ 六大智能體管線與角色分工 (RPG Campfire)

本演示採用**線性拓撲結構**（從智能體 1 順序流轉至智能體 6，無內部循環），各智能體圍繞「篝火」協作：

```mermaid
graph LR
    A[Architect 建築師] --> B[Scout 偵察兵]
    B --> C[OKF Parser 文獻解析器]
    C --> D[Declarer 臨床醫生]
    D --> E[Inquisitor 審判官]
    E --> F[Wizard 嚮導]
    F --> A2[Architect 終審]
```

1.  **建築師 (Architect)**：負責啟動整個智能體管線。
2.  **偵察兵 (Scout)**：
    *   負責在本地訪問龐大的知識圖譜（Addiction KB）。
    *   尋找關鍵節點（如 HIV 感染），提取一跳、兩跳、三跳的關聯特徵。
    *   利用網絡科學工具（如 Python 庫 `NetworkX`）進行鏈接預測，將候選特徵與合理的推薦依據（Rationale）存入列表。
3.  **文獻解析器 (Stage/OKF Parser)**：
    *   解析以 **OKF (Open Knowledge Format)**——Google 推出的層次化 Markdown 格式壓縮的醫學論文，並從中提取與 HIV 療效相關的特徵。
4.  **聲明者/臨床醫生 (Declarer/Clinician)**：
    *   不使用外部工具，純粹依靠推理。角色預設為「具備多年 HIV 治療經驗的臨床醫生」。
    *   評估偵察兵與文獻解析器提供的特徵，並根據臨床經驗加入新的候選特徵（例如糖尿病與 HIV 預後的關聯）。
5.  **質詢者/審判官 (Quizzer/Inquisitor)**：
    *   審查所有候選特徵，從臨床、社會經濟學及數據完整性的角度，對每個特徵給予「贊成 (Thumbs up)」或「反對 (Thumbs down)」並附上原因。
6.  **嚮導/巫師 (Wizard)**：
    *   執行無監督統計分析。利用變異數閾值和皮爾森相關係數分析特徵間的相關性。
    *   檢查特徵的普及率（Prevalence check，若某特徵在數據集中僅出現在單一患者身上，則予以排除）。
    *   從數據統計的角度給予「贊成」或「反對」（例如：8.6% 的患者具有 HCV 合併感染，給予贊成）。
7.  **建築師 (Architect - 終審)**：
    *   匯總所有特徵的推薦依據、審判官的質詢評語及嚮導的統計指標，做最終篩選決策（Demo中將特徵從 37 個刪減至 29 個）。

---

## 📈 建模結果與可重複性驗證

### 1. 建模結果
*   **方法**：在最終確定的 29 個特徵上運行 **XGBoost** 模型。
*   **評估指標**：輸出 ROC 曲線、PR 曲線與平衡準確率 (Balanced Accuracy)。
*   **關鍵預測因子 (Feature Importance)**：
    *   CD4 細胞計數 (CD4 count)
    *   血紅蛋白 (Hemoglobin)
    *   尼古丁/煙草依賴 (Nicotine dependence)
    *   慢性肝臟疾病 (Chronic liver disease)
    *   *(這些指標在臨床醫學上皆具備高度合理性)*

### 2. 可重複性 (Replicability)
*   **驗證方法**：將智能體管線運行 10 次，並與 10 組隨機挑選的同等大小特徵集進行統計對照。
*   **結論**：
    *   智能體生成的特徵集在預測力上**顯著優於隨機特徵集**。
    *   **核心特徵的高度一致性**：在 10 次獨立運行中，CD4 細胞計數/CD8 比率、貧血/紅血球狀態在 10 次運行中皆被成功提取。年齡、腎功能、白血球計數、血小板、尼古丁依賴等也具備極高的再現率。

---

## 💬 現場 Q&A 互動精華

*   **Q1：如何確保智能體是使用數據集的特徵，而不是憑空捏造 ML 訓練知識？**
    *   **A**：系統內設有中間件（Middleware）與規則限制。智能體生成的特徵必須實際存在於數據集中。智能體本身從不直接接觸數據（Data），它們只負責生成與調用特徵提取的腳本（Scripts），數據處理在安全沙箱內運行。
*   **Q2：深度學習（黑盒子）與本系統的 explainable feature engineering 有何不同？**
    *   **A**：傳統深度學習架構難以解釋特徵提取的內在邏輯。此智能體系統強調**可解釋性 (Explainable AI)**，每一個特徵的挑選與保留都有智能體的 Rationale（依據）和 Audit trail（審計線索），並能讓臨床醫生標記和追蹤預測背後的關鍵驅動因子。
*   **Q3：如此複雜的智能體管線，花費的 Token 成本如何？**
    *   **A**：本演示由於採用**線性管線（Linear Pipeline）**，且將多個審查步驟集中在單次 API 調用（One-shot call）中以減少往返，**單次運行的總成本僅為 2.30 美元**。
*   **Q4：智能體如何處理長期與短期記憶？**
    *   **A**：此 Demo 為線性無循環管道，沒有引入複雜的記憶機制或多輪對話循環，所有審查均在單次調用中完成，出錯時管線會直接中止。

---

## 🔮 未來展望與優化方向
1.  **人機協同 (Human-in-the-loop)**：測試在管線中加入人工中斷與反饋機制，允許臨床醫生隨時調整或重跑部分步驟。
2.  **動態拓撲與進化算法**：捨棄線性架構，引入動態的循環拓撲，並利用進化算法（Evolutionary Algorithms）自動尋找最佳的智能體協作結構。
3.  **引入更多專業智能體**：
    *   **調色板 (Palette)**：負責藥物動力學 (PK) 優化。
    *   **公平性智能體 (Fairness Agent)**：評估偏見與再現性。
    *   **特徵工程智能體 (Feature Engineer)**：進行高級特徵組合，自動生成元特徵 (Meta-features)。

---
*整理時間：2026-07-12*
