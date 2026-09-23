# 🤖 HR RAG AI Assistant

A Retrieval-Augmented Generation (RAG) based AI assistant that answers HR-related questions using a collection of company policy and employee documents.

The system retrieves relevant information from HR PDF documents and uses a Large Language Model (LLM) to generate grounded answers based on the retrieved context.

---

## 🚀 Project Overview

This project demonstrates how **Retrieval-Augmented Generation (RAG)** can be used to build an AI assistant for querying company HR documents.

Instead of relying only on the knowledge stored inside an LLM, the system:

1. Loads HR documents from PDF files.
2. Splits documents into smaller chunks.
3. Converts document chunks into vector embeddings.
4. Stores the embeddings in a FAISS vector database.
5. Retrieves the most relevant documents for a user's question.
6. Sends the retrieved context to an LLM.
7. Generates an answer based only on the provided HR documents.

---

## 🧠 RAG Architecture

```text
                User Question
                      │
                      ▼
             ┌─────────────────┐
             │   Query Input   │
             └────────┬────────┘
                      │
                      ▼
             ┌─────────────────┐
             │ FAISS Retriever │
             └────────┬────────┘
                      │
              Relevant Chunks
                      │
                      ▼
             ┌─────────────────┐
             │  RAG Prompt     │
             │ Context + Query │
             └────────┬────────┘
                      │
                      ▼
             ┌─────────────────┐
             │    Groq LLM     │
             │ GPT-OSS-20B     │
             └────────┬────────┘
                      │
                      ▼
                Final Answer
```

---

## ✨ Features

* 📄 PDF document ingestion
* 🔎 Semantic document retrieval
* 🧠 Retrieval-Augmented Generation
* 🤗 Hugging Face embeddings
* ⚡ FAISS vector search
* 🤖 Groq-powered LLM
* 📝 Context-grounded answers
* 📚 HR policy question answering
* 🔗 Source document retrieval
* 📊 Evaluation/submission support
* 🔍 LangSmith tracing for RAG execution

---

## 📚 HR Document Corpus

The project uses HR-related PDF documents covering areas such as:

* Company Profile
* Employee Handbook
* Leave Policy
* Work From Home Policy
* Code of Conduct
* Performance Review
* Compensation and Benefits
* IT and Data Security
* Prevention of Sexual Harassment
* Onboarding
* Travel and Expense Policy

---

## 🛠️ Technologies Used

| Technology            | Purpose                           |
| --------------------- | --------------------------------- |
| Python                | Core programming language         |
| LangChain             | RAG pipeline                      |
| LangChain Community   | PDF loading and FAISS integration |
| Hugging Face          | Text embeddings                   |
| FAISS                 | Vector similarity search          |
| Groq                  | Large Language Model inference    |
| GPT-OSS-20B           | LLM used for answering questions  |
| Sentence Transformers | Embedding generation              |
| PyPDF                 | PDF processing                    |
| LangSmith             | RAG tracing and monitoring        |
| python-dotenv         | Environment variable management   |
| Jupyter Notebook      | Development environment           |

---

## 📂 Project Structure

```text
RAG_Based_Projects/
│
├── project-2-intelligent-rag/
│   │
│   ├── code.ipynb
│   ├── requirements.txt
│   ├── .gitignore
│   │
│   └── zyro-dynamics-hr-corpus/
│       ├── 00_Company_Profile.pdf
│       ├── 01_Employee_Handbook.pdf
│       ├── 02_Leave_Policy.pdf
│       ├── 03_Work_From_Home.pdf
│       ├── 04_Code_of_Conduct.pdf
│       ├── 05_Performance_Review.pdf
│       ├── 06_Compensation_and_Benefits.pdf
│       ├── 07_IT_and_Data_Security.pdf
│       ├── 08_Prevention_of_Sexual_Harassment.pdf
│       ├── 09_Onboarding_and_Joining.pdf
│       └── 10_Travel_and_Expense_Policy.pdf
│
└── README.md
```

> `.env` is intentionally excluded from the repository because it contains API credentials.

---

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone https://github.com/Sameer041475/RAG_Based_Projects.git
```

### 2. Navigate to the project

```bash
cd RAG_Based_Projects/project-2-intelligent-rag
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

---

## 🔐 Environment Variables

Create a `.env` file inside the project directory:

```env
GROQ_API_KEY=your_groq_api_key_here
```

The API key should **never be committed to GitHub**.

The application loads the key using:

```python
from dotenv import load_dotenv
import os

load_dotenv()

GROQ_API_KEY = os.getenv("GROQ_API_KEY")
```

---

## ▶️ Running the Project

Open:

```text
code.ipynb
```

Select your Python/Jupyter kernel and execute the cells in order.

The main pipeline performs:

```text
PDF Loading
    ↓
Text Chunking
    ↓
Embedding Generation
    ↓
FAISS Vector Store
    ↓
Retriever
    ↓
RAG Prompt
    ↓
Groq LLM
    ↓
Answer
```

---

## 💬 Example Questions

You can ask questions such as:

```text
What benefits are provided to employees?
```

```text
What is the employee assistance programme?
```

```text
What is the company's leave policy?
```

```text
What is the work from home policy?
```

```text
What are the rules regarding employee conduct?
```

```text
What is the travel reimbursement policy?
```

---

## 🔍 Example RAG Response

### Question

```text
What benefits are provided to employees?
```

### Retrieved information

The system retrieves relevant sections from the Compensation and Benefits Policy.

### Generated answer

The assistant summarizes the benefits available to employees based on the retrieved HR document context.

The system is instructed not to invent information when the requested information is unavailable in the provided documents.

---

## 🧩 Core RAG Components

### 1. Document Loading

```python
loader = PyPDFDirectoryLoader(CORPUS_PATH)
documents = loader.load()
```

### 2. Text Splitting

```python
splitter = RecursiveCharacterTextSplitter(
    chunk_size=800,
    chunk_overlap=100
)

chunks = splitter.split_documents(documents)
```

### 3. Embeddings

```python
embedding_model = HuggingFaceEmbeddings(
    model_name="sentence-transformers/all-MiniLM-L6-v2"
)
```

### 4. FAISS Vector Store

```python
vectorstore = FAISS.from_documents(
    chunks,
    embedding_model
)
```

### 5. Retriever

```python
retriever = vectorstore.as_retriever(
    search_kwargs={"k": 5}
)
```

### 6. LLM

```python
llm_model = ChatGroq(
    model="openai/gpt-oss-20b",
    temperature=0.2,
    max_tokens=500,
    api_key=GROQ_API_KEY
)
```

---

## 🛡️ Hallucination Control

The RAG prompt instructs the model to answer using only the retrieved HR context.

If the required information is not available, the assistant responds with:

```text
I don't have that information in the provided HR documents.
```

This helps reduce unsupported or hallucinated answers.

---

## 📈 Future Improvements

Potential improvements include:

* 🌐 Streamlit web interface
* 💬 Chat history
* 📌 Better source citations
* 🔄 Conversational memory
* 📊 RAG evaluation metrics
* ⚡ Retrieval optimization
* 🗂️ Metadata-based filtering
* 🔐 User authentication
* 📄 Support for DOCX and TXT files
* 🧪 Automated evaluation pipeline
* 🐳 Docker deployment
* ☁️ Cloud deployment

---

## 🎯 Learning Outcomes

Through this project, I worked with:

* Retrieval-Augmented Generation
* Vector databases
* Semantic search
* Embedding models
* LangChain
* Large Language Models
* Prompt engineering
* PDF document processing
* API integration
* Environment variable security
* LangSmith tracing
* Git and GitHub

---

## 👨‍💻 Author

**Sameer Kampa**

CSE – Artificial Intelligence Student

### Interests

* Artificial Intelligence
* Machine Learning
* Deep Learning
* Generative AI
* RAG Systems
* AI Agents
* Full-Stack Development

---

## ⭐ If you find this project useful

Consider giving the repository a ⭐ on GitHub.
