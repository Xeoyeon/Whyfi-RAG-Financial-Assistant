# Whyfi: RAG-based Financial Terminology Service
> Bridging the financial literacy gap with real-time, context-aware AI.

**Whyfi** is a RAG assistant designed to simplify complex financial terminology and keep users updated with real-time economic trends. By leveraging a **Chrome Extension** as the primary delivery mechanism, the service maximizes information accessibility, providing instantaneous explanations within the user's browsing context.

<br><br>

## Tech Stack

### **AI & Data**
* **LLM**: Gemini 1.5 Flash 
* **Orchestration**: LangChain 
* **Embedding**: BGE-M3-ko 
* **Vector DB**: ChromaDB 

### **Interface & Infrastructure**
* **Main Interface**: Chrome Extension (Developer Mode) 
* **Prototype**: Streamlit
* **External APIs**: Naver News API, Google Trends API, KDI Economic Keyword Trend(Web crawling)

<br><br>

## System Architecture
Whyfi ensures high-fidelity responses by grounding the LLM in verified external knowledge bases, supplemented by real-time news integration.

### Data Flow & Pipeline
1.  **Ingestion**: Aggregates authoritative financial data, including the Bank of Korea's "700 Financial Terms" and the National Tax Service's "2024 Stock and Tax" guide.
2.  **Embedding Model**: **BGE-M3-ko** 
3.  **Storage**: **ChromaDB**
4.  **LLM**: **Gemini-2.5-Flash**(-> 1.5에서 바뀜을 명시)
5.  **Expansion**: Enhances reliability by integrating the **Naver News API** to provide the latest headlines related to the searched term.-> 정확히는 그냥 코사인 유사도 기반일걸

<br><br>

## Technical Highlights

### **1. Optimized ETL Pipeline**
* **Benchmarked Parsing**: Selected **PyMuPDF** after comparative testing with Tesseract and LlamaParse for superior accuracy in converting complex financial PDFs to LLM-ready Markdown.
* **Automated Data Cleaning**: Engineered custom **regex-based scripts** to remove redundant symbols and whitespace, significantly enhancing data quality for embedding.

### **2. Semantic Retrieval Strategy**
* **Context-Aware Embedding**: Utilized the **BGE-M3-ko** model to capture subtle financial nuances across diverse document formats[cite: 278].
* **Multi-Source Retrieval**: Implemented a **parallel retrieval chain** with optimized weights (k=3 for dictionary terms, k=2 for book context) to provide comprehensive, multi-layered information.

### **3. Reliable AI Generation**
* **Hallucination Mitigation**: Constrained LLM responses strictly to **retrieved vector context**, ensuring high-fidelity and grounded financial explanations[cite: 182, 314].
* **Jargon-to-Analogy Mapping**: Developed prompt templates that translate technical financial terms into **intuitive analogies** and real-world examples for improved accessibility.

<br><br>


## 💻How to Use
### Streamlit Dashboard
* **Live Demo (HuggingFace Spaces)**: Access the interactive app directly on HuggingFace Spaces 👉 [WhyFi: Financial Assistant](https://huggingface.co/spaces/xeoyeon/whyfi).
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


