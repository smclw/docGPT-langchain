<p align="center">
    <img style="width: 50%; height: auto;" src="./static/img/repos_logo.png" alt="Chatbot Image">
</p>

[English](./README.md) | [中文版](./README.zh-TW.md)

免費的`docGPT`允許您與您的文件 (`.pdf`, `.docx`, `.csv`, `.txt`) 進行對話，無需任何金鑰或費用。

此外，您也可以根據該文件操作，將程序部屬在任何地方。

- 目錄
    - [Introduction](#introduction)
    - [Features](#🧨features)
    - [What's LangChain?](#whats-langchain)
    - [How to Use docGPT?](#how-to-use-docgpt)
    - [How to develope a docGPT with streamlit?](#how-to-develope-a-docgpt-with-streamlit)
    - [Advanced - How to build a better model in langchain](#advanced---how-to-build-a-better-model-in-langchain)

* 主要開發軟體與套件:
    * `Python 3.10.11`
    * `Langchain 0.0.218`
    * `Streamlit 1.22.0`
    * [more](./requirements.txt)

如果您喜歡這個專案，請給予⭐`Star`以支持開發者~

### 📚Introduction

* 上傳來自本地的 Document 連結 (`.pdf`, `.docx`, `.csv`, `.txt`)，並且向 `docGPT` 詢問有關 Document 內容。例如: 您可以請 GPT 幫忙總結文章
* 提供兩種模型選擇:
  * `gpt4free`
    * **完全免費，"允許使用者在無需輸入 API 金鑰或付款的情況下使用該應用程序"**
    * 需選擇 `Provider`。有關 `gpt4free` 的更多詳細信息，請參閱[源專案](https://github.com/xtekky/gpt4free)
  * `openai`
    * **須具備** `openai_api_key`，您可以從此[鏈接](https://platform.openai.com/)獲取金鑰
    * 若具備 `serpapi_key`，AI 的回應可以包括 Google 搜索結果

<p align="center">
<img src="static/img/2023-09-06-14-56-20.png" width="80%">
</p>

---

### 🧨Features

- **`gpt4free` 整合**：任何人都可以免費使用 GPT4，無需輸入 OpenAI API 金鑰。
- **支援 docx, pdf, csv, txt 檔案**: 可以上傳 PDF, Word, CSV, txt 檔
- **直接輸入 Document 網址**：使用者可以直接輸入 Document URL 進行解析，無需從本地上傳檔案(如下方demo所示)。
- **Langchain Agent**：AI 能夠回答當前問題，實現類似 Google 搜尋功能。
- **簡易操作環境**：友善的界面，操作簡便

---

### 🦜️What's LangChain?

* LangChain 是一個用於**開發由語言模型支持的應用程序的框架**。它支持以下應用程序
    1. 將 LLM 模型與外部數據源進行連接
    2. 允許與 LLM 模型進行交互

* 有關 langchain 的介紹，建議查看官方文件、[Github源專案](https://github.com/hwchase17/langchain)


**ChatGPT 無法回答的問題，交給 Langchain 實現!**

LangChain 填補了 ChatGPT 的不足之處。通過以下示例，您可以理解 LangChain 的威力：

> 在 ChatGPT 無法解答數學問題或回答 2020 年以後的問題（例如“2023 年的總統是誰？”）的情況下：
>
> * 數學問題: 有專門處理數學問題的 math-LLM 模型
> * 現今問題: 使用 Google 搜索
>
> 要創建一個全面的 AI 模型，我們需要結合 "ChatGPT"、"math-LLM" 和 "Google 搜索" 工具。
>
> 在非 AI 時代，我們將使用 `if...else...` 將用戶查詢進行分類，讓用戶選擇問題類型（通過 UI）。
>
> 在 AI 時代，用戶應能夠直接提問。通過 LangChain 的 agent：
>
>  * 我們向 agent 提供工具，例如 `tools = ['chatgpt', 'math-llm', 'google-search']`
>  * 工具可以包括使用 LangChain 設計的 chains，例如使用 `retrievalQA chain` 回答來自文檔的問題。
>  * agent 根據用戶查詢自動決定使用哪個工具（完全自動化）。

通過 LangChain，您可以創建通用的 AI 模型，也可以為**商業應用**量身定制。

---

### 🚩How to Use docGPT?

1. 🎬前往[應用程序](https://docgpt-app.streamlit.app/)

2. 🔑輸入您的 `API_KEY` (在版本 3 中為可選，您可以使用 `gpt4free` 免費模型):
    * `OpenAI API KEY`: 確保還有可用的使用次數。
    * `SERPAPI API KEY`: 如果您要查詢 Document 中不存在的內容，則需要使用此金鑰。

3. 📁上傳來自本地的 Document 檔案 (選擇一個方法)
    * 方法一: 從本地機瀏覽並上傳自己的 `.pdf`, `.docx`, `.csv` or `.txt` 檔
    * 方法二: 輸入 Document URL 連結

4. 🚀開始提問 ! 

![RGB_cleanup](https://github.com/Lin-jun-xiang/docGPT-streamlit/blob/main/static/img/docGPT.gif?raw=true)

> [!WARNING]
> 由於免費版 streamlit cloud 資源限制，該程序在多人同時使用時，容易引發崩潰([Oh no!](https://github.com/Lin-jun-xiang/docGPT-langchain/issues/2))，若遇上該問題歡迎到 Issue 提醒開發者，開發者會重啟程序。


---

### 🧠How to develope a docGPT with streamlit?

手把手教學，讓您快速建立一個屬於自己的 chatGPT !

首先請進行 `git clone https://github.com/Lin-jun-xiang/docGPT-streamlit.git`

方法有如下幾種方法:

* 於**本地開發方式(不使用docker)**:
    * 下載開發需求套件
        ```
        pip install -r requirements.txt
        ```

    * 於專案根目錄啟動服務
        ```
        streamlit run ./app.py
        ```

    * 開始體驗! 您的服務會運行在 `http://localhost:8501`.

* 於**本地開發方式(使用docker)**:
    * 使用 Docker Compose 啟動服務
        ```
        docker-compose up
        ```

        您的服務會運行在 `http://localhost:8501`. 您可以開始使用 `docGPT` 應用程序
    
    * 停止服務運行
        ```
        docker-compose down
        ```

* 使用 Streamlit Community **Cloud 免費部屬**、管理和共享應用程序
    * 將您的應用程序放在公共 GitHub 存儲庫中（確保有 `requirements.txt`！）
    * 登錄[share.streamlit.io](https://share.streamlit.io/)
    * 單擊“部署應用程序”，然後粘貼您的 GitHub URL
    * 完成部屬[應用程序](https://docgpt-app.streamlit.app//)

由於 `docGPT` 是使用 streamlit cloud 免費版部屬，受限於設備關係會有不少延遲，建議使用者可以使用本地部屬方式來體驗。

---

### 💬Advanced - How to build a better model in langchain

要在 LangChain 中構建功能強大的 docGPT 模型，請考慮以下技巧以改進性能

1. **Language Model**
   
   使用適當的 LLM Model，會讓您事半功倍，例如您可以選擇使用 OpenAI 的 `gpt-3.5-turbo` (預設是 `text-davinci-003`):

   ```python
   # ./docGPT/docGPT.py
   llm = ChatOpenAI(
    temperature=0.2,
    max_tokens=2000,
    model_name='gpt-3.5-turbo'
   ) 
   ```

   請注意，模型之間並沒有最好與最壞，您需要多試幾個模型，才會發現最適合自己案例的模型，更多 OpenAI model 請[參考](https://platform.openai.com/docs/models)
   
   (部分模型可以使用 16,000 tokens!)

2. **PDF Loader**

    在 Python 中有許多解析 PDF 文字的 Loader，每個 Loader 各有優缺點，以下整理三個作者用過的
    
    ([Langchain官方介紹](https://python.langchain.com/docs/modules/data_connection/document_loaders/how_to/pdf)):

    * `PyPDF`: 簡單易用
    * `PyMuPDF`: 讀取文件**速度非常快速**，除了能解析文字，還能取得頁數、文檔日期...等 MetaData。
    * `PDFPlumber`: 能夠解析出**表格內部文字**，使用方面與 `PyMuPDF` 相似，皆能取得 MetaData，但是解析時間較長。

    如果您的文件具有多個表格，且重要資訊存在表格中，建議您嘗試 `PDFPlumber`，它會給您意想不到的結果!
    請不要忽略這個細節，因為沒有正確解析出文件中的文字，即使 LLM 模型再強大也無用! 

3. **Tracking Token Usage**

    這個並不能讓模型強大，但是能讓您清楚知道 QA Chain 的過程中，您使用的 tokens、openai api key 的使用量。

    當您使用 `chain.run` 時，可以嘗試用 langchain 提供的 [方法](https://python.langchain.com/docs/modules/model_io/models/llms/how_to/token_usage_tracking):

    ```python
    from langchain.callbacks import get_openai_callback

    with get_openai_callback() as callback:
        response = self.qa_chain.run(query)

    print(callback)

    # Result of print
    """
    chain...
    ...
    > Finished chain.
    Total Tokens: 1506
    Prompt Tokens: 1350
    Completion Tokens: 156
    Total Cost (USD): $0.03012
    """
    ```

<a href="#top">Back to top</a>



啊伟哥运行后报错内容如下：

https://docgpt-app.streamlit.app/

ModuleNotFoundError: This app has encountered an error. The original error message is redacted to prevent data leaks. Full error details have been recorded in the logs (if you're on Streamlit Cloud, click on 'Manage app' in the lower right of your app).

Traceback: File "/home/adminuser/venv/lib/python3.10/site-packages/streamlit/runtime/scriptrunner/script_runner.py", line 552, in _run_script exec(code, module.dict) File "/mount/src/docgpt-streamlit/app.py", line 10, in from components import get_response, side_bar, theme, upload_and_process_document File "/mount/src/docgpt-streamlit/components/init.py", line 1, in from .sidebar import side_bar File "/mount/src/docgpt-streamlit/components/sidebar.py", line 6, in from docGPT import GPT4Free File "/mount/src/docgpt-streamlit/docGPT/init.py", line 10, in from .docGPT import DocGPT, GPT4Free File "/mount/src/docgpt-streamlit/docGPT/docGPT.py", line 6, in import g4f File "/home/adminuser/venv/lib/python3.10/site-packages/g4f/init.py", line 6, in from .models import Model, ModelUtils, _all_models File "/home/adminuser/venv/lib/python3.10/site-packages/g4f/models.py", line 4, in from .Provider import BaseProvider, RetryProvider File "/home/adminuser/venv/lib/python3.10/site-packages/g4f/Provider/init.py", line 42, in from .NoowAi import NoowAi

讨论微信+：yhfjmt

2023.12.19


