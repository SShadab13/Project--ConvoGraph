# 🧠 ConvoGraph: A Context-Aware Conversational Search Companion

[![GitHub Repo](https://img.shields.io/badge/GitHub-ConvoGraph-blue?logo=github)](https://github.com/SShadab13/Project--ConvoGraph)

ConvoGraph is a **context-aware conversational search companion** that ingests **multi-format documents** (PDFs, blogs, tables, web pages), builds a **Knowledge Graph + Vector Index hybrid**, and powers a **retrieval-augmented conversational interface** with **human feedback loops** for continuous improvement.  
It is designed to be **cost-efficient, provenance-first, and modular**, serving as both a **research prototype** and a **publish-ready open-source project**.

---

## 🚀 Features
- 📄 **Multi-format ingestion** → PDFs, blogs, tables, and web pages.
- 🔗 **Knowledge Graph + Vector Index hybrid** → powered by Neo4j + Chroma/FAISS.
- 💬 **Conversational interface** → context-aware retrieval with citations.
- 👍👎 **Human-in-the-loop feedback** → refine relevance, correct triples, improve retrieval.
- ⚡ **Cost-efficient** → built with open-source LLMs (Llama3, Mistral, Gemma) or free-tier APIs (Gemini Flash, Groq).
- 🔒 **Provenance-first** → every fact is cited with its source.

---

## 🏗️ System Architecture

```mermaid
flowchart TD
    A[Multi-format Docs: PDFs, Blogs, Tables, Webpages] --> B[Preprocessing & Cleaning\n(trafilatura, PyMuPDF, Docling)]
    B --> C[LLM-powered Triple Extraction\nFew-shot + CoT + Schema Validation]
    C --> D1[Knowledge Graph DB\nNeo4j]
    C --> D2[Vector DB\nChroma/FAISS]
    D1 --> E[Hybrid Retrieval]
    D2 --> E
    E --> F[LangGraph Orchestration\n+ LangChain Components]
    F --> G[Conversational Interface\n(Streamlit/Next.js Chat UI)]
    G --> H[Human Feedback Loop\n👍 👎 Corrections]
    H --> D1
    H --> D2
````

---

## 📦 Tech Stack

* **Backend:** Python (FastAPI, LangChain, LangGraph)
* **Knowledge Graph:** Neo4j / NetworkX (prototype)
* **Vector Store:** Chroma / FAISS / Weaviate
* **Models:** Gemma, Llama3, Mistral (via Ollama/LM Studio) or Gemini Flash API
* **Frontend:** Streamlit (prototype) / Next.js (planned)
* **Infra:** Docker, GitHub Actions CI/CD

---

## ⚡ Quick Start

### 1. Clone the Repo

```bash
git clone https://github.com/SShadab13/Project--ConvoGraph.git
cd Project--ConvoGraph
```

### 2. Install Requirements

```bash
python -m venv venv
source venv/bin/activate   # or venv\Scripts\activate on Windows
pip install -r requirements.txt
```

### 3. Run Backend

```bash
uvicorn backend.app:app --reload
```

### 4. (Optional) Run UI

```bash
streamlit run ui/app_streamlit.py
```

---

## 📅 Roadmap

**Phase 1: KG + Vector Foundation (Month 1)**

* [x] Repo created & GitHub setup
* [ ] Data acquisition & preprocessing (Week 1)
* [ ] LLM-powered triple extraction (Week 2)
* [ ] KG + Vector integration (Week 3)
* [ ] Conversational retrieval prototype (Week 4)

**Phase 2: Conversational RAG (Month 2)**

* [ ] LangGraph orchestration
* [ ] Hybrid retrieval (KG + Vector)
* [ ] Answer composer with citations

**Phase 3: Human Feedback Integration (Month 3)**

* [ ] Feedback API + schema
* [ ] Update loop for KG & Vector
* [ ] Feedback dashboard

**Phase 4: Evaluation & Scaling (Month 4)**

* [ ] Benchmarks (Recall\@k, faithfulness, latency)
* [ ] Guardrails (PII, injection filtering)
* [ ] Scaling ingestion with Crawl4AI

---

## 📚 Blog Series: *The ConvoGraph Journey*

* Part 1: *Scraping Smarter – Hybrid Ingestion Pipeline*
* Part 2: *From Messy Text to Triples – LLM-Powered KG Construction*
* Part 3: *Bridging Graphs & Vectors – Designing a Hybrid Retrieval Backbone*
* Part 4: *Ask Your Docs – Conversational Search Prototype*
* Quarterly: *ConvoGraph: Blueprint for Hybrid KG + RAG Systems with Feedback*

---

## 🙌 Contributions

This project is part of my **M.Tech Dissertation** at BITS Pilani.
Feedback, suggestions, and PRs are welcome!

---

## 📜 License

MIT License – feel free to fork, use, and extend with attribution.

---

🔗 **Project URL:** [https://github.com/SShadab13/Project--ConvoGraph](https://github.com/SShadab13/Project--ConvoGraph)

