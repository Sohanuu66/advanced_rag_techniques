# Advanced RAG Techniques 🦜🔗

[![Python Version](https://img.shields.io/badge/Python-3.11+-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![LangChain](https://img.shields.io/badge/LangChain-0.4.0+-1C3C3C?style=flat-square&logo=chain)](https://github.com/langchain-ai/langchain)

A dedicated laboratory and reference implementation library for studying, engineering, and comparing **Advanced Retrieval-Augmented Generation (RAG)** paradigms.

---

## 📌 Repository Overview

This repository is a curated collection of hands-on implementations exploring the boundaries of modern search and retrieval. RAG systems in production require much more than basic vector search; they demand structured query construction, semantic routing, advanced chunking strategies, multi-vector representations, and late interaction search.

Here, theory meets execution. Each notebook is designed as an isolated, step-by-step experiment using the **LangChain** ecosystem, Google's Gemini models, Hugging Face local pipelines, and specialized retrieval libraries.

---

## 🎯 Repository Objectives

- **Deconstruct Complex Frameworks**: Break down papers and design patterns into minimal, self-contained Python implementations.
- **Benchmark Retrieval Strategies**: Compare and contrast how different query transformation, indexing, and routing techniques affect context retrieval precision.
- **Build Production-Grade Reference Code**: Provide clean, modular, and reusable LCEL (LangChain Expression Language) code structures for downstream architectures.
- **Bridge Foundations to State-of-the-Art**: Maintain a clear progression from basic model orchestration up to hierarchical cluster-based indexing.

---

## 🗺️ Roadmap & Implemented Techniques

Below is the structured roadmap of retrieval paradigms covered in this repository.

### 🟢 Implemented Paradigms

| Category | Technique / Pattern | Notebook / Module | Core Library / Concept |
| :--- | :--- | :--- | :--- |
| **Query Transformation** | **Multi-Query** | [`MultiQueryRetriever.ipynb`](./Query_transformation/MultiQueryRetriever.ipynb) | Generates alternative queries to bypass distance-based search gaps |
| | **RAG Fusion** | [`RAGFusion.ipynb`](./Query_transformation/RAGFusion.ipynb) | Multi-query search ranked via Reciprocal Rank Fusion (RRF) |
| | **Decomposition** | [`Decomposition_Individually.ipynb`](./Query_transformation/Decomposition_Individually.ipynb)<br>[`Decomposition_Recursive.ipynb`](./Query_transformation/Decomposition_Recursive.ipynb) | Breaks complex prompts into sub-problems solved step-by-step |
| | **Step-Back Prompting** | [`StepBackPrompting.ipynb`](./Query_transformation/StepBackPrompting.ipynb) | Abstracts queries to retrieve high-level principles/general context |
| | **HyDE** | [`HyDE.ipynb`](./Query_transformation/HyDE.ipynb) | Hypothetical Document Embeddings (aligning query with answers) |
| **Routing** | **Logical Routing** | [`LogicalRouting.ipynb`](./Routing/LogicalRouting.ipynb) | Directs query to distinct data sources based on LLM decisions |
| | **Semantic Routing** | [`SemanticRouting.ipynb`](./Routing/SemanticRouting.ipynb) | Directs query based on embedding distance to predefined query classes |
| **Indexing** | **Parent Document (PDR)** | [`PDR.ipynb`](./Indexing/PDR.ipynb) | Retain tiny chunks for vector match, retrieve parent chunk for context |
| | **Multi-Representation (MRI)** | [`MRI.ipynb`](./Indexing/MRI.ipynb) | Index document summaries via `MultiVectorRetriever`, fetch raw texts |
| | **RAPTOR** | [`RAPTOR.ipynb`](./Indexing/RAPTOR.ipynb) | Hierarchical tree indexing via recursive document clustering |
| | **ColBERT / PyLate** | [`colBERT.ipynb`](./Indexing/colBERT.ipynb) | Multi-vector contextualized token-level late-interaction search |
| **Query Construction** | **Metadata Filtering** | [`MetaDataFiltering.ipynb`](./Query_Construction/MetaDataFiltering.ipynb) | Translating query intents into structured metadata filters |
| | **Text-to-SQL** | [`TextToSQL.ipynb`](./Query_Construction/TextToSQL.ipynb) | Translating natural language to SQLite relational queries |
| **Retrieval** | **Hybrid / Ensemble Search** | [`Hybrid_Retrieval.ipynb`](./Retrieval/Hybrid_Retrieval.ipynb) | Combining dense semantic search with sparse keywords (e.g., BM25) |

### 🟡 Planned Paradigms (Under Development)

* [ ] **Reranking Layers** (Integrating Cohere / Cross-Encoder post-retrieval filters)
* [ ] **Self-RAG / Corrective RAG (CRAG)** (Implementing agentic self-evaluations and corrective loops)
* [ ] **Graph RAG** (Structuring semantic chunk relationships using Neo4j and Knowledge Graphs)
* [ ] **Long-Context RAG Optimizations** (Lost-in-the-Middle mitigation techniques)

---

## 🛠️ Tech Stack & Architecture

- **Core Orchestration**: `langchain` + `langchain-core` + `langchain-community`
- **LangChain Expression Language (LCEL)**: Serving as the execution engine for composable pipelines.
- **LLM Integrations**:
  - Cloud API: Google Gemini (`gemini-3.1-flash-lite`, `gemini-1.0-pro` via `langchain-google-genai`)
  - Local Models: Hugging Face pipelines (`TinyLlama/TinyLlama-1.1B-Chat-v1.0` via `langchain-huggingface`)
- **Embeddings**: Local sentence-transformers (`all-MiniLM-L6-v2`), Google Generative AI Embeddings.
- **Vector & Document Storage**: Chroma DB (embedded metadata-filtered retrieval), FAISS (local index execution).
- **Interactive Playground**: Streamlit (web interface for YouTube Q&A bot).

---

## 📁 Repository Structure

```directory
advanced_rag_techniques/
├── Indexing/                          # Advanced document representation structures
│   ├── colBERT.ipynb                  # Late-interaction token matching (PyLate)
│   ├── MRI.ipynb                      # Multi-Representation Indexing via MultiVectorRetriever
│   ├── PDR.ipynb                      # Parent Document Retriever (two-tier chunking)
│   └── RAPTOR.ipynb                   # Recursive clustering for hierarchical tree indexing
├── Query_transformation/              # Techniques to expand/rewrite incoming queries
│   ├── Decomposition_Individually.ipynb
│   ├── Decomposition_Recursive.ipynb
│   ├── HyDE.ipynb                     # Hypothetical Document Embeddings
│   ├── MultiQueryRetriever.ipynb      # LLM query expansion
│   ├── RAGFusion.ipynb                # Query expansion + Reciprocal Rank Fusion
│   └── StepBackPrompting.ipynb        # Abstract principle retrieval
├── Routing/                           # Decision layers for query direction
│   ├── LogicalRouting.ipynb           # LLM-guided function routing
│   └── SemanticRouting.ipynb          # Similarity-guided embedding routing
├── Query_Construction/                # Relational and structured query builders
│   ├── MetaDataFiltering.ipynb        # Auto-query filters
│   └── TextToSQL.ipynb                # SQL generation from prompts
├── Retrieval/                         # Retrieval ensemble strategies
│   └── Hybrid_Retrieval.ipynb         # BM25 + Dense vector integration
├── 01_Langchain_Models/ to 12_Langchain_Agents/ # Core foundational LangChain building blocks
├── GenerativeAICourse/                # Accompanying course notes and learning materials
├── app.py                             # Interactive Streamlit application (YouTube Q&A Bot)
└── requirements.txt                   # Dependency locks
```

---

## 🎯 Current Scope

This repository focuses **strictly on Advanced Retrieval-Augmented Generation (RAG) patterns and LangChain configurations**. All implementations use notebook setups to ensure that code changes, prompt configurations, and retrieval histories are easily inspectable.

## 🚀 Future Scope (Out of Scope)

The following topics are intentionally excluded from the current roadmap to keep the codebase highly specialized, though they may be explored in independent projects:
* **Custom Autonomous Agents**: Building complex, persistent web agents or task execution loops.
* **Model Context Protocol (MCP)**: Custom context servers or protocol implementations.
* **LangGraph Pipelines**: Advanced stateful multi-agent execution graphs.
* **LLM Evaluation**: Production-level evaluation suites (e.g., Ragas, TruLens, LangSmith).

---

## 📥 Setup & Installation

Follow these steps to run the notebooks or play with the Streamlit app:

1. **Clone the repository**:
   ```bash
   git clone https://github.com/Sohanuu66/langchain_learning.git
   cd langchain_learning
   ```

2. **Configure your environment**:
   Create a `.env` file in the root directory:
   ```env
   GEMINI_API_KEY=your_google_gemini_api_key_here
   OPENAI_API_KEY=your_openai_api_key_here
   ```

3. **Install dependencies**:
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   pip install -r requirements.txt
   ```

4. **Run the Streamlit Playground**:
   ```bash
   streamlit run app.py
   ```

---

## 📄 License

This repository is licensed under the MIT License.