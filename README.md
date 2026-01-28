# ai-text-detector
A full-stack project for detecting AI-generated text. Includes data collection, preprocessing, model selection and training, backend deployment, and frontend interface.

## 簡介
- **資料收集**

    我將 2010 年作為可信非 AI 生成資料的時間界線。

    **非 AI 文本**：在 Google 搜尋引擎中使用「關鍵詞＋before:2010」的格式進行查找，找到符合的文章後近一步做處理，以句號做切分且確保每句皆無空格並以句號做結尾。每句標記為 0（表示非 AI 生成）存入 CSV 檔案中。

    **AI 文本**：將上述找到的非 AI 文章丟入至各類 GPT 生成相似內容，以產出 AI 生成的對應文本，Prompt 大致格式為 :「整理以下並生成相似文章，不要有標題和列點，x 字左右：」每句標記為 1（表示 AI 生成）存入 CSV 檔案中。

    **CSV 檔案格式**：

    <img src="fig1.png" alt="示意圖" width="450">

    【註】實際範例請見 [sample1.csv](/data/sample/sample1.csv)

    **最終資料量**：

    <img src="fig2.png" alt="示意圖" width="450">

    ---

- **資料處理**

    資料單位為筆，以句號做切分，所以一個句子為一筆，另外在訓練集和測試集上我們以 8:2 做分割，為了讓各類別的比例和整體資料集中是一致的，有加入額外參數。實際資料量如下：

    <img src="fig3.png" alt="示意圖" width="450">

    我在訓練集中加入了詞性標註 (POS tagging)、依存句法分 (Dependency Parsing) 以及 TF-IDF 關鍵詞萃取。

    ---

- **模型選擇**

    
