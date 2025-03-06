# 🚀 Introduction to LangChain with Ollama  

This notebook demonstrates the integration of **LangChain** with **Ollama**, utilizing a **Large Language Model (LLM)** to generate responses based on user queries.  

## 📜 Overview  

The notebook covers:  
✅ Installation and setup of **LangChain** and **Ollama**.  
✅ The usage of **LangChain's core components** to structure a text generation pipeline.  
✅ A breakdown of the **ChatOllama** class, the **ChatPromptTemplate**, and how they work together.  
✅ Why the **Qwen2-7B-Instruct** model is used and its relevance in structured prompting.  
✅ **Multilingual capabilities** for global usability.  

## 🛠️ Requirements  

Before running the notebook, install the required dependencies:  

```bash
pip install langchain langchain-ollama langchain-community
pip install --upgrade pip
```

Additionally, ensure that **Ollama** is installed and running on your system. For installation and setup instructions, refer to the [Ollama documentation](https://ollama.com/).  

## 📌 Code Breakdown  

### 1️⃣ **Importing Dependencies**  
```python
from langchain_ollama import ChatOllama
from langchain_core.prompts import ChatPromptTemplate
```
- **ChatOllama**: A LangChain wrapper for **Ollama-based LLMs**, enabling seamless text generation.  
- **ChatPromptTemplate**: A LangChain class designed to structure conversations, defining system instructions and user input templates.  

### 2️⃣ **LLM Initialization**  
```python
llm = ChatOllama(
    model="qwen2:7b-instruct",
    temperature=0,
)
```
- **[Qwen2-7B-Instruct](https://ollama.com/library/qwen2:7b-instruct)**: A **7-billion parameter model** optimized for instruction-following tasks, making it highly effective for structured Q&A.  
- **Why "Instruct"?** Fine-tuned for **instruction-following**, enhancing reliability in assistant-like behavior.  
- **Temperature = 0**: Ensures **deterministic responses**, eliminating randomness.  

### 3️⃣ **Defining the Prompt Template**  
```python
prompt = ChatPromptTemplate.from_messages(
    [
        ("system", "You are a helpful assistant that answers questions."),
        ("human", "{input}"),
    ]
)
```
- **System Message**: Defines the model’s personality and behavior.  
- **Human Message**: A dynamic placeholder `{input}` for user queries.  

### 4️⃣ **Executing the LLM Chain**  
```python
chain = prompt | llm
response = chain.invoke(
    {
        "input": "Qual atriz brasileira ganhou o Globo de Ouro em 2025?",
    }
)
```
- **Pipeline Composition** (`prompt | llm`): Links the prompt with the model using LangChain’s composition operators.  
- **Invoke Method**: Executes the chain dynamically.  

## 🌍 Language Support  

The **Qwen2-7B-Instruct** model supports multiple languages beyond **English and Chinese**, including **Portuguese**, **Spanish**, **French**, **German**, and many others. This makes it suitable for **multilingual AI applications** without additional fine-tuning.  

## 🔍 Why LangChain?  

LangChain provides a modular framework for building **LLM-powered applications**, including:  
🔹 **Prompt Management**: Standardized structures for effective model interactions.  
🔹 **Model Agnosticism**: Easy switching between different LLMs (OpenAI, Ollama, Hugging Face, etc.).  