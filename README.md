# Secure RAG: Prompt Injection Detection

## Project Overview

This project implements a Secure Retrieval-Augmented Generation (RAG) pipeline with prompt-injection detection.

The system analyses a user query before it enters the RAG pipeline. Queries identified as prompt-injection attacks are blocked, while safe queries proceed through semantic retrieval and context-grounded answer generation.

The project demonstrates how a security layer can be integrated into a RAG application to help protect against instruction overrides, role manipulation, prompt leakage attempts, and context manipulation.

## Key Features

- Prompt-injection detection before RAG processing.
- Query classification using a Hugging Face prompt-injection detection model.
- Configurable confidence threshold for blocking suspicious queries.
- Semantic document retrieval using embeddings and FAISS.
- Context-grounded answer generation using FLAN-T5.
- Blocking of detected prompt-injection attacks.
- Testing with normal and manipulated prompts.
- Demonstration of different prompt manipulation techniques.

## How the System Works

The Secure RAG pipeline follows this process:

```text
User Query
    ↓
Prompt Injection Detection
    ↓
Is the Query Safe?
   ↙           ↘
Blocked        Semantic Retrieval
                    ↓
                 FAISS
                    ↓
             Retrieved Context
                    ↓
                FLAN-T5
                    ↓
             Generated Answer
```

## Prompt Injection Detection

The project uses the following Hugging Face model:

`protectai/deberta-v3-base-prompt-injection-v2`

The model classifies user queries and returns a label and confidence score.

The detection function uses a configurable confidence threshold. If a query is classified as an injection attack and meets the threshold, the query is blocked before retrieval and answer generation.

## RAG Pipeline

The RAG system uses:

### Embedding Model

`sentence-transformers/all-MiniLM-L6-v2`

Used to convert knowledge-base documents and user queries into vector embeddings.

### Vector Database

**FAISS**

Used for similarity search and retrieval of relevant context.

### Language Model

`google/flan-t5-base`

Used to generate answers based only on the retrieved context.

## Prompt Manipulation Examples

The project tests several types of suspicious prompts:

- **Instruction Override** — attempts to ignore previous instructions.
- **Role Manipulation** — attempts to change the assistant's intended role.
- **Prompt Leakage** — attempts to reveal hidden or system prompts.
- **Context Manipulation** — attempts to bypass retrieved context.

The notebook compares normal queries with manipulated versions to demonstrate how the detection layer responds.

## Technologies Used

- Python
- Hugging Face Transformers
- Sentence Transformers
- FAISS
- PyTorch
- Pandas
- NumPy
- Google Colab

## Installation

Install the required libraries:

```bash
pip install transformers sentence-transformers accelerate faiss-cpu pandas numpy torch tqdm
```

## Running the Project

1. Upload a CSV dataset containing `query` and `answer` columns.
2. Load and clean the dataset.
3. Generate document embeddings.
4. Create the FAISS vector index.
5. Load the prompt-injection detection model.
6. Load the FLAN-T5 language model.
7. Run the `secure_rag()` function with a user query.
8. The system blocks detected injection attacks or retrieves relevant context and generates an answer for safe queries.

## Project Structure

```text
Secure-RAG-Prompt-Injection-Detection/
│
├── Prompt Injection.ipynb
├── README.md
└── dataset.csv
```

> The dataset should only be uploaded if you have permission to share it publicly.

## Author

**Harshita Sharma**

AI/ML Engineer

GitHub: github.com/harshitasharma891  
LinkedIn: linkedin.com/in/harshita-sharma-b843031b5
