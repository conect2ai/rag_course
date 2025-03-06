# 🚀 Introduction to Retrieval-Augmented Generation (RAG) with LangChain and Ollama

This notebook demonstrates the integration of **LangChain** with **Ollama**, using **Retrieval-Augmented Generation (RAG)** to generate responses based on a text source.

## 📜 Overview

The notebook covers:
- ✅ Installation and setup of **LangChain**, **Ollama**, **LangGraph**, and **FAISS**.
- ✅ Usage of **LangChain's core components** to structure a Retrieval-Augmented Generation (RAG) pipeline.
- ✅ Implementation of **ChatOllama** and **ChatPromptTemplate** for structured interactions.
- ✅ Indexing and document retrieval using **FAISS**.
- ✅ Building a graph-based workflow for question processing using **LangGraph**.
- ✅ **Multilingual capabilities** for global usability.

## 🛠️ Requirements

Before running the notebook, install the required dependencies:

```bash
pip install langchain langchain-ollama langchain-community langgraph faiss-cpu
pip install --upgrade pip
```

Additionally, ensure that **Ollama** is installed and running on your system. For installation instructions, refer to the [Ollama documentation](https://ollama.com/).

## 📌 Code Breakdown

### 1️⃣ **Importing Dependencies**
```python
from langchain_community.embeddings import OllamaEmbeddings
from langchain_community.vectorstores import FAISS
from langchain.schema import Document
from langchain_ollama import ChatOllama
from langchain_core.prompts import ChatPromptTemplate
from langgraph.graph import START, StateGraph
from langchain_text_splitters import RecursiveCharacterTextSplitter
```
- **OllamaEmbeddings**: Generates embeddings for vector representation of documents.
- **FAISS**: Library for efficient storage and retrieval of vectors.
- **ChatOllama**: LangChain wrapper for Ollama models.
- **ChatPromptTemplate**: Structures prompts for structured interactions.
- **StateGraph**: Enables structured workflows for step-by-step execution.

### 2️⃣ **Document Indexing**
```python
document = """
O Brasil amanheceu com uma conquista inédita: Fernanda Torres tornou-se a primeira atriz brasileira a vencer o Globo de Ouro em 2025.
Ela foi premiada por sua atuação em "Ainda Estou Aqui", primeiro filme original do Globoplay.
"""

text_splitter = RecursiveCharacterTextSplitter(chunk_size=200, separators=["\n\n"])
texts = text_splitter.create_documents([document])

embeddings = OllamaEmbeddings(model="nomic-embed-text")
vector_store = FAISS.from_documents(texts, embedding=embeddings)
```
- The document is split into smaller parts to optimize information retrieval.
- Embeddings are generated using **nomic-embed-text** and stored in **FAISS**.

### 3️⃣ **Defining the Prompt Template**
```python
template="""You are an assistant for question-answering tasks. Use the following pieces of retrieved context to answer the question. If you don't know the answer, just say that you don't know.

Question: {question}

Context: {context}

Answer (brazilian portuguese):"""

prompt = ChatPromptTemplate.from_template(template)

llm = ChatOllama(temperature=0, model="qwen2:7b-instruct")
```
- **System message**: Defines the model's behavior.
- **Placeholder `{question}`**: Represents the user query.

### 4️⃣ **Execution Flow via Graph**

#### 🔄 **Document Retrieval**
```python
def retrieve(state):
    retrieved_docs = vector_store.similarity_search(state["question"], k=2)
    return {"context": retrieved_docs}
```
- Retrieves the most relevant documents from the database.

#### 🌬️ **Response Generation**
```python
def generate(state):
    docs_content = "\n\n".join(doc.page_content for doc in state["context"])
    messages = prompt.invoke({"question": state["question"], "context": docs_content})
    response = llm.invoke(messages)
    return {"answer": response.content if hasattr(response, "content") else response}
```
- Generates a response based on the retrieved documents.

#### ⚖️ **Building the Graph**
```python
graph_builder = StateGraph(State).add_sequence([retrieve, generate])
graph_builder.add_edge(START, "retrieve")
graph = graph_builder.compile()
```
- The graph defines a sequential flow of **retrieval** and **generation**.

#### 🎨 **Graph Visualization**
```python
from IPython.display import Image, display
display(Image(graph.get_graph().draw_mermaid_png()))
```

### 5️⃣ **Executing the Chain**
```python
for step_result in graph.stream({"question": "Qual atriz brasileira ganhou o Globo de Ouro em 2025?"}, stream_mode="updates"):
    print(step_result)
```
- Runs the process and prints step-by-step results.
