# 🚀 RAG COURSE

A basic introduction to **Retrieval-Augmented Generation (RAG)** with **LangChain** and **Ollama**, featuring a companion PDF and two hands-on notebooks.

**Course Material:** [![Download PDF](https://img.shields.io/badge/Download-PDF-red?style=flat-square)](rag_course.pdf)


## 📜 Table of Contents (from the PDF)

| **Section** | **Description** |
| --- | --- |
| **1. 🔎 Retrieval-Augmented Generation (RAG)** | - Definition and overview <br> - Why it goes beyond a stand-alone LLM |
| **2. 💡 Concept** | - Core meaning of RAG <br> - Key benefits and features |
| **3. ⚙️ How to Build?** | - Guardrails <br> - Caching <br> - Monitoring <br> - Evaluation <br> - LLM Security |
| **4. 🏗 RAG System Design (Overview)** | - Input/Output orchestrator <br> - Retriever <br> - Data load & splitting <br> - Data conversion <br> - Storage component <br> - LLM setup <br> - Data indexing <br> - Prompt management |
| **5. 👀 Retriever: Indexing Pipeline** | - Data load & splitting <br> - Data conversion <br> - Storage (e.g., FAISS) |
| **6. 🧩 Generation Pipeline** | **Retriever** <br> &nbsp;&nbsp;• Query analysis (rewriting, decomposition, etc.) <br> &nbsp;&nbsp;• Information retrieval (lexical, vector-based, SQL, graph, etc.) <br><br> **Prompt Management** <br> &nbsp;&nbsp;• Contextual prompting, few-shot, controlled, chain of thought <br><br> **LLM** <br> &nbsp;&nbsp;• Model configuration and generation flow |
| **7. 🔧 Hands-On** | - Practical notebooks demonstrating **LangChain**, **Ollama**, and **FAISS** for RAG <br><br> **1. Introduction to LangChain and Ollama** <br> &nbsp;&nbsp;• [0_Intro_LangChain_Ollama.ipynb](./0_Intro_LangChain_Ollama/0_Intro_LangChain_Ollama.ipynb) <br> &nbsp;&nbsp;&nbsp;&nbsp;— Overview of LangChain & Ollama integration <br> &nbsp;&nbsp;&nbsp;&nbsp;— Explanation of ChatOllama and ChatPromptTemplate <br><br> **2. Fundamentals of RAG with Ollama** <br> &nbsp;&nbsp;• [1_RAG_LLM_Basics.ipynb](./1_RAG_Basics_Ollama/1_RAG_LLM_Basics.ipynb) <br> &nbsp;&nbsp;&nbsp;&nbsp;— Introduction to RAG <br> &nbsp;&nbsp;&nbsp;&nbsp;— How LangChain, FAISS, and LangGraph combine for document retrieval <br><br> *Note: These two notebooks serve as the primary hands-on exercises for a basic RAG workflow.* |


## 🔗 References  
[1] LangChain: Retrieval. *n.d.* Available at [https://python.langchain.com/docs/concepts/retrieval/](https://python.langchain.com/docs/concepts/retrieval/)  
[2] Ollama: Library. *n.d.* Available at [https://ollama.com/library](https://ollama.com/library)  
[3] Wolfe, Cameron R. The Basics of AI-Powered Vector Search. *n.d.* Available at [https://cameronrwolfe.substack.com/p/the-basics-of-ai-powered-vector-search](https://cameronrwolfe.substack.com/p/the-basics-of-ai-powered-vector-search)

## ⚖ License
This project is licensed under the [MIT License](./LICENSE).
