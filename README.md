# Whyfi: RAG-based Financial Terminology Service
> Instant financial terminology insights delivered via RAG-powered browsing. -> 이거 더 내 플젝에 맞게

Whyfi provides simple, real-time explanations for complex financial terms through a Chrome Extension. By integrating RAG directly into the browser, it ensures high-fidelity information accessibility without interrupting the user’s workflow. ->근데 문제점 크롬 익스텐션만 한게 아님. 웹 프로토타입도 함.
<br><br>

*Note: This repository is a personal portfolio mirror of a team project. While the source code remains identical to the original, this **README** has been specifically curated to highlight my individual technical contributions. Original Repository: [[Original Repo Link]](https://github.com/Xeoyeon/whyfi)*
<br><br>

## Technical Specifications

### AI & Data
* **LLM**: Gemini 2.5 Flash (Upgraded to 1.5->2.5 for stability on HuggingFace Spaces)
* **Orchestration**: LangChain 
* **Embedding**: BGE-M3-ko (Multi-lingual & multi-granular support)
* **Vector DB**: ChromaDB 

### Interface & Deployment
* **Main Interface**: Chrome Extension (Developer Mode) 
* **Web Prototype**: Streamlit
* **External**: Naver News API, Google Trends API, KDI Economic Keyword Trend(Web crawling)

<br><br>

## System Architecture
Whyfi ensures high-fidelity responses by grounding the LLM in verified external knowledge bases, supplemented by real-time news integration.

### 1. Knowledge Base (Datasets)
- Bank of Korea: "700 Financial Terms" (Term definitions and relationships)
- National Tax Service: "2024 Stock and Tax" (Technical tax and stock guidelines)
<br>

### 2. Data Pipeline Flow
The system operates through a streamlined retrieval-generation loop:
1. **Preprocessing**: Raw PDFs are converted to Markdown using PyMuPDF and cleaned via custom regex scripts.
2. **Retrieval**: User queries are vectorized and compared against the Knowledge Base using Cosine Similarity to retrieve the most relevant context.
3. **Augmentation**: The Naver News API fetches the latest headlines to supplement the static knowledge with real-time events.
4. **Generation**: Gemini 2.5 Flash synthesizes the retrieved context and news into a jargon-free, intuitive explanation.

<br><br>

## Technical Highlights

### **1. Optimized ETL Pipeline**
* **Benchmarked Parsing**: Selected **PyMuPDF** after comparative testing with Tesseract and LlamaParse for superior accuracy in converting complex financial PDFs to LLM-ready Markdown.
* **Automated Data Cleaning**: Engineered custom **regex-based scripts** to remove redundant symbols and whitespace, significantly enhancing data quality for embedding.

### **2. Semantic Retrieval Strategy**
* **Multi-Source Retrieval**: Implemented a **parallel retrieval chain** with optimized weights (k=3 for dictionary terms, k=2 for book context) to provide comprehensive, multi-layered information.

### **3. Reliable Response Generation**
* **Verifiability & Benchmarking** : Integrated **search trends and news APIs with source citations**, ensuring high-fidelity outputs validated through **RAGAS**-based benchmarking.
* **Jargon-to-Analogy Mapping**: Developed prompt templates that translate technical financial terms into **intuitive analogies** and real-world examples for improved accessibility.


<br><br>


## 💻How to Use
### Streamlit Dashboard
* **Live Demo (HuggingFace Spaces)**: Access the interactive app directly on HuggingFace Spaces <br>
👉 [WhyFi: Financial Assistant](https://huggingface.co/spaces/xeoyeon/whyfi).
* **Local Execution**:
    1. Run the application: 
       ```bash
       $ streamlit run streamlit.py
       ```
    2. Access the dashboard at `http://localhost:8501`.

### Chrome Extension (Developer Mode)
1. **Start Backend Server**: Initialize the API by running:
   ```bash
   $ python3 app.py
   ```
2. **Install in Browser**:
    * Navigate to `chrome://extensions/` and enable **Developer Mode**.
    * Click **Load unpacked** and select the `chrome-extension` folder.


