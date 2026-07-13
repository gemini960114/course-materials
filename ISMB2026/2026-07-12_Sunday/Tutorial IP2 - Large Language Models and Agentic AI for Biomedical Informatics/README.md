# Tutorial IP2 - Large Language Models and Agentic AI for Biomedical Informatics

**日期**: 2026年7月12日 (星期日) Pre-Conference
**時間**: 
- **Part 1**: 02:00 PM – 04:00 PM (ET) / 14:00 - 16:00
- **Part 2**: 04:15 PM – 06:00 PM (ET) / 16:15 - 18:00
**地點**: Jefferson West (In Person)
**主辦與演講者**:
- **Wenqi Shi** (德克薩斯大學西南醫學中心 UT Southwestern Medical Center)
- **Xuan Wang** (維吉尼亞理工大學 Virginia Tech)
- **Robert Tang** (耶魯大學 Yale University)
- **Mark Gerstein** (耶魯大學 Yale University, 遠端線上)
- 及協同研究員 Yuxuan Liao, Yi Fang, Yi Jiang 等

---

## 📅 課程概述與目標

大型語言模型（LLM）（如 ChatGPT 等）在理解、生成和推理自然語言方面展現了強大的能力。在生物資訊學與生物醫學資訊學中，這些模型正迅速崛起為一種新型的計算範式，並有望徹底變革文獻探勘、數據整合、工作流自動化以及生物醫學推理。本教程為生物醫學數據科學研究中理解和應用 LLM 及智能體 AI（Agentic AI）系統提供了一個實用的、入門級的動手實作指南。

本教程從 LLM 及其演進的簡要介紹開始，涵蓋科學應用中常用的商業與開源模型。參與者將學習核心技術，包括提示詞設計、針對生醫文獻與資料庫的檢索增強生成（RAG）、文字生成 SQL 查詢（Text-to-SQL）以及 Python 中的生物資訊程式碼生成。在此基礎上，本教程進一步引入了智能體 AI 系統，展示其如何執行複雜的多步推理、工具調用和工作流編排。此外，教程還特別強調了負責任且嚴謹地使用這些模型，探討了學術與臨床場景下的幻覺、偏見、魯棒性及可重複性限制。

### 🎯 核心學習目標
1. **理解大數據特徵**：理解大規模生物醫學數據的核心特徵。
2. **文獻與數據檢索**：將 LLM 應用於生物醫學文獻探勘與數據庫查詢。
3. **生信編程加速**：利用 LLMs 加速生物資訊學編程工作流。
4. **生醫問答 RAG**：實現針對生醫問答的檢索增強生成（RAG）管道。
5. **智能體系統實踐**：理解並構建用於解決複雜生醫任務的智能體 AI 系統。
6. **風險與限制評估**：批判性地評估基於 LLM 的方法所面臨的幻覺、偏見與可重複性風險。

---

## 📂 學習資源與目錄結構

本目錄下包含該 Tutorial 的完整動手實作 Notebook 與整理後的會議記錄：

### 📁 [Guided Hands-On (動手實作 Notebook)](file:///d:/antigravity/course-materials/ISMB2026/2026-07-12_Sunday/Tutorial%20IP2%20-%20Large%20Language%20Models%20and%20Agentic%20AI%20for%20Biomedical%20Informatics/Guided%20Hands-On)

*   📓 [ISMB_of_BioArc_Tutorial_GPU_DNA.ipynb](file:///d:/antigravity/course-materials/ISMB2026/2026-07-12_Sunday/Tutorial%20IP2%20-%20Large%20Language%20Models%20and%20Agentic%20AI%20for%20Biomedical%20Informatics/Guided%20Hands-On/ISMB_of_BioArc_Tutorial_GPU_DNA.ipynb)：**BioArc** (基礎序列模型的自動神經架構搜索) 教程。
    *   *引導使用 GPU 建立包含 CNN, RNN, Transformer, Mamba, Hyena 的超級網絡（Supernet），進行權重共享的一步預訓練（Masked Language Model），加載 8M 混合模型與 50M Transformer (Nucleotide Transformer) 在啟動子預測任務上進行微調和對比，並通過 Grad-CAM / Saliency 進行逐層可解釋性視覺化。*
*   📓 [ISMB_of_LLM_for_Bioinformatics_Demo.ipynb](file:///d:/antigravity/course-materials/ISMB2026/2026-07-12_Sunday/Tutorial%20IP2%20-%20Large%20Language%20Models%20and%20Agentic%20AI%20for%20Biomedical%20Informatics/Guided%20Hands-On/ISMB_of_LLM_for_Bioinformatics_Demo.ipynb)：**BioCoder** (生信代碼生成基準平台) 教程。
    *   *引導在 Colab 上使用 DeepSeek-Coder-6.7B 演示生信代碼生成，涵蓋自然語言函數生成、填補空白任務 (Fill in the Middle, FIM) 以及利用靜態解析提取全倉庫上下文進行代碼上下文感知生成的技術。*

### 📁 [Notes (會議記錄與整理摘要)](file:///d:/antigravity/course-materials/ISMB2026/2026-07-12_Sunday/Tutorial%20IP2%20-%20Large%20Language%20Models%20and%20Agentic%20AI%20for%20Biomedical%20Informatics/Notes)

*   **BioArc 核心技術與模型微調**
    *   📂 [session02.txt (原始會議記錄)](file:///d:/antigravity/course-materials/ISMB2026/2026-07-12_Sunday/Tutorial%20IP2%20-%20Large%20Language%20Models%20and%20Agentic%20AI%20for%20Biomedical%20Informatics/Notes/session02.txt)
    *   📝 [session02_summary.md (整理版摘要)](file:///d:/antigravity/course-materials/ISMB2026/2026-07-12_Sunday/Tutorial%20IP2%20-%20Large%20Language%20Models%20and%20Agentic%20AI%20for%20Biomedical%20Informatics/Notes/session02_summary.md)
        *   *詳細整理：BioArc 異構混合搜尋空間（CNN, Transformer, LSTM, Mamba/Hyena）、權重共享超級網絡（Supernet）訓練細節、DNA 任務微調（啟動子分類與編碼區辨識）以及利用 Grad-CAM 與 Saliency 進行模型內部運作機制的逐層解釋。*

*   **通用生醫智能體、軌跡訓練與空間多體學**
    *   📂 [session03.txt (原始會議記錄 - Biomni 及智能體訓練)](file:///d:/antigravity/course-materials/ISMB2026/2026-07-12_Sunday/Tutorial%20IP2%20-%20Large%20Language%20Models%20and%20Agentic%20AI%20for%20Biomedical%20Informatics/Notes/session03.txt)
    *   📂 [session03_praticle.txt (原始會議記錄 - spatialOmicsLab)](file:///d:/antigravity/course-materials/ISMB2026/2026-07-12_Sunday/Tutorial%20IP2%20-%20Large%20Language%20Models%20and%20Agentic%20AI%20for%20Biomedical%20Informatics/Notes/session03_praticle.txt)
    *   📝 [session03_summary.md (整理版摘要)](file:///d:/antigravity/course-materials/ISMB2026/2026-07-12_Sunday/Tutorial%20IP2%20-%20Large%20Language%20Models%20and%20Agentic%20AI%20for%20Biomedical%20Informatics/Notes/session03_summary.md)
        *   *詳細整理：通用生醫智能體 **Biomni** 的組成（150種專業工具、59個資料庫、105個套裝軟體及執行沙箱）、智能體規模化與交互軌跡（Trajectory）訓練原理、**spatialOmicsLab** 空間多體學整合分析環境的雙層設計與效能驗證、以及 **BioCoder** 倉庫上下文代碼生成基準。*

---

## 🔗 相關資源連結

*   **Biomni 官方網站**：[biomni.stanford.edu](https://biomni.stanford.edu/) (通用生醫 AI 智能體平台)
*   **BioCoder 開源倉庫**：[github.com/gersteinlab/BioCoder](https://github.com/gersteinlab/BioCoder) (耶魯大學生信代碼生成基準)
*   **BioArc 論文連結**：[ICML 2026 Poster 65801](https://icml.cc/virtual/2026/poster/65801) (發現最佳生物功能模型的自動架構搜索)
*   **本教程官方主頁**：[llm4biomed.github.io/2026/](https://llm4biomed.github.io/2026/)
