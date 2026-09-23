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
```
