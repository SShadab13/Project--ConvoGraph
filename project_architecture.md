---
marp: true
theme: uncover
backgroundColor: #fff
color: #333
class:
  - lead
---

# **Context-Aware Conversational Search Companion for Multi-format Document Retrieval**

**A Comprehensive Architectural Overview**

**Sheikh Shadab**
2023AB05191
M.Tech, Artificial Intelligence & Machine Learning

---

## **The Enterprise Knowledge Problem: Motivation**

Critical business knowledge is often fragmented and locked away, leading to significant challenges.

* **Information Silos**
    Knowledge is scattered across diverse and complex formats like PDFs, technical blogs, and internal web pages.

* **The Context Gap**
    Traditional search fails to understand conversational queries or synthesize answers from these disconnected sources.

* **The Synthesis & Reasoning Gap**
    Systems struggle to connect fragmented information (e.g., a procedure from a blog and data from a PDF) into a single, coherent answer.

---

## **Phase 1: Knowledge Graph Construction Pipeline**

The first step is to build a structured foundation from unstructured data. This pipeline automates the extraction of entities and relationships to create a unified knowledge base.

![width:1000px](https://i.imgur.com/eB4u5yW.png)

---

## **Phase 2: From Raw Data to a Coherent Schema**

Once raw triples are extracted, the next critical step is to induce a formal schema. This involves clustering entities and relationships to discover types and then using an LLM to label and organize them into a structured ontology.

![width:1100px](https://i.imgur.com/J32bZ0L.png)

---

## **Future Vision: An Advanced Agentic Architecture**

A linear pipeline has limitations. The future of this architecture is a dynamic, multi-agent system where specialized agents collaborate to build, refine, and verify the knowledge graph in a continuous loop.

![width:1000px](https://i.imgur.com/0V3Y2qY.png)

---

## **Phase 3: The Search & Retrieval Workflow**

This is the user-facing application that leverages the knowledge hub. A team of agents collaborates to understand user intent, search across both the vector store and the knowledge graph, and generate a comprehensive, context-aware response.

![width:1000px](https://i.imgur.com/y3yLg3M.png)

---

## **Core Technology Stack**

This project integrates several key technologies to create a robust and intelligent system.

| Category | Technology | Purpose |
| :--- | :--- | :--- |
| **Knowledge Representation** | **Neo4j** | Models explicit relationships for multi-hop reasoning. |
| **Natural Language AI** | **Ollama (Llama 3)** | Understands queries, extracts information, synthesizes answers. |
| **Orchestration & Retrieval** | **LangChain / LangGraph** | Builds the RAG pipeline and manages agentic workflows. |
| **Vector Storage** | **ChromaDB** | Enables efficient semantic search on text chunks. |
| **User Interface** | **Streamlit** | Provides a simple interface for demonstration and feedback. |

---

## **Expected Outcomes & Contributions**

This research aims to deliver both a functional prototype and valuable insights for the field.

* **A Functional Prototype**
    A working "Context-Aware Conversational Search Companion" with a web interface.

* **A Populated Knowledge Graph**
    A rich KG built from a diverse public corpus, demonstrating the extraction pipeline.

* **A Framework for Human Feedback**
    A practical demonstration of how a human-in-the-loop mechanism can enable adaptive, self-improving AI systems.

* **Novel KG Construction Methodologies**
    Insights into building KGs from complex, multi-format web sources, especially for technical and procedural knowledge.

---

## **Conclusion: A Model for Next-Generation Search**

This project provides a comprehensive framework for building intelligent, context-aware, and adaptive search solutions.

1.  **Bridging Data and Dialogue**
    It transforms siloed, unstructured documents into an interconnected Knowledge Graph, making previously 'locked' information accessible for deep reasoning.

2.  **A Pathway for Adaptive Systems**
    The integrated human feedback loop provides a practical model for creating systems that learn and improve from user interaction.

3.  **A Blueprint for Enterprise AI**
    By demonstrating this architecture on a complex public dataset, this work offers a robust and transferable model for the next generation of enterprise search.

