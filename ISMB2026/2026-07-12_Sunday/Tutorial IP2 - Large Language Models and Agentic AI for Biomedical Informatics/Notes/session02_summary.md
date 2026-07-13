# 會議記錄與教程整理：Large Language Models and Agentic AI for Biomedical Informatics (Session 02)

本文件整理自會議記錄檔案 [session02.txt](file:///d:/antigravity/course-materials/ISMB2026/2026-07-12_Sunday/Tutorial%20IP2%20-%20Large%20Language%20Models%20and%20Agentic%20AI%20for%20Biomedical%20Informatics/Notes/session02.txt)，並結合動手操作教程 [ISMB_of_BioArc_Tutorial_GPU_DNA.ipynb](file:///d:/antigravity/course-materials/ISMB2026/2026-07-12_Sunday/Tutorial%20IP2%20-%20Large%20Language%20Models%20and%20Agentic%20AI%20for%20Biomedical%20Informatics/Guided%20Hands-On/ISMB_of_BioArc_Tutorial_GPU_DNA.ipynb) 內容進行深度整理。

---

## 📅 教程基本資訊 (Session 02 - BioArc 生物序列基礎模型架構搜尋)
*   **主題**：BioArc: Discovering Optimal Architectural Biological Foundation Models
*   **主講人**：Xuan Wang (Virginia Tech)、Yi Fang 等人
*   **核心痛點**：目前的生物序列（如 DNA、蛋白質）基礎模型大多直接借用處理文本的 Transformer 架構。然而，生物數據具有自身的特徵（如局部 Motif、超長距離依賴性、週期性等），單一的 Transformer 並不一定是最佳選擇。此外，超大型 Transformer 模型參數極大、訓練與推理成本高昂。
*   **核心目標**：利用自動化神經架構搜索（Neural Architecture Search, NAS），自動尋找體積小但效能極高的異構混合架構（Heterogeneous Hybrid Architectures）作為生物基礎模型的核心骨幹。

---

## 🧠 核心技術解析：BioArc 異構架構與權重共享

### 1. 異構混合搜尋空間 (Heterogeneous Search Space)
BioArc 不限制只用單一種模組，而是構建了一個包含多種主流序列建模模組的搜尋空間：
*   **CNN (卷積神經網路)**：擷取局部特徵與 Motif。
*   **Transformer (自注意力機制)**：建立全域關聯與上下文交互。
*   **LSTM (長短期記憶網路)**：捕捉序列的嚴格順序關係。
*   **Mamba / Hyena (狀態空間模型/長卷積)**：進行高效率的超長距離依賴建模。

同時，BioArc 還對以下維度進行聯合優化：
*   **寬度 (Width)**：如每層 hidden dimension 可在 64, 128, 256 等之間變化。
*   **深度 (Depth)**：層數通常設計在 3 到 6 層。
*   **Tokenization (標記化方式)**：不同的網路架構可能偏好不同的 k-mer 標記化，BioArc 採用 Tokenizer 與架構設計的**聯合優化**。
*   **組合可能性**：這使得搜尋空間包含數百萬種可能的架構路徑。

### 2. 權重共享超級網絡 (Weight-Sharing Supernet)
由於無法對百萬種架構都進行從頭訓練，BioArc 採用 **One-shot NAS（一次性架構搜索）**：
*   將所有候選模組（如不同維度的 CNN、Transformer 等）放入一個模組池（ModuleDict）中，相同類型與維度的模組在不同路徑間**共享權重**。
*   **One-shot 預訓練**：使用 Masked Language Model (MLM) 任務在 GRCh38 人類基因組序列上預訓練。在每個 Step，隨機選擇一條架構路徑進行前向和反向傳播，更新該路徑上所有共享模組的權重。

---

## 📊 實作任務與模型表現評估 (Fine-tuning & Evaluation)

本實作在 GPU 環境下，將搜尋出的 **BioArc 8M 混合模型** 與基於 Transformer 的大模型 **Nucleotide Transformer 50M (NT-50M)** 在三個 DNA 分類資料集上進行了微調對比：

### 1. 任務資料集
1.  **Core Promoter Prediction**：辨識 DNA 序列中是否包含核心啟動子（對齊到轉錄起始位點 TSS 左右）。
2.  **Human Non-TATA Promoters**：辨識不包含典型 TATA-box 的人類啟動子。
3.  **Coding vs. Intergenomic Seqs**：區分蛋白質編碼區段與基因間非編碼區段。

### 2. 模型效能對比
*   **體積差距**：BioArc-8M 比 NT-50M 在參數體積上**小了 6 倍以上**（BioArc 為 8M 參數，NT-50M 為 50M 參數），且 BioArc 的搜尋過程產生的模型比常見大模型（如 DNABERT-2）小了數十到數百倍。
*   **準確率表現**：在小資料集微調任務上，參數僅 8M 的 BioArc 混合模型達到了與 50M Transformer 相當甚至更優的準確率。這證明了**異構架構組合在生物醫學任務上的特化優勢**，小模型透過架構優化亦可擊敗通用大模型。

---

## 🔍 逐層模型可解釋性 (Layer-wise Interpretability)

異構混合模型通常被認為是「黑盒子」。教程中展示了如何對 BioArc-8M 的不同層級進行視覺化解釋：

### 1. CNN 區塊解釋 (Grad-CAM)
*   使用 **Grad-CAM (梯度加權類激活映射)** 計算 DNA 各位置特徵對分類決策的梯度貢獻。
*   結果顯示，BioArc 中的 CNN 層會精確關注轉錄起始位點（TSS）附近的局部核心啟動子元件（如 Inr、MTE、DPE 等 Motif），符合卷積專注局部特徵的直覺。

### 2. Transformer 區塊解釋 (Attention & Saliency)
*   **Attention Map**：展示模型在資訊聚合時在哪些鹼基位置之間建立了交互關聯（關注「看哪裡」）。
*   **Saliency Map (顯著性映射)**：利用輸出對輸入 Embedding 的梯度，估計各鹼基位置對最終預測的因果重要性（關注「哪些位置起決定作用」）。
*   將 Attention 與 Saliency 結合分析，可精確追蹤模型是如何在全域範圍內整合長距離生物訊號的。
