# RAG on Legal Documents 📚⚖️

A Retrieval-Augmented Generation (RAG) system built over a corpus of legal documents, applying semantic search to retrieve and synthesise information from contracts, NDAs, merger agreements, and privacy policies.

## 🎯 Objective

Legal firms and departments handle large volumes of complex documents, making it difficult to efficiently find specific information. This project implements a RAG-based solution that provides quicker and more precise responses to legal queries by dynamically retrieving and contextualising relevant excerpts from a legal corpus — helping legal professionals save time on document review, improve research accuracy, and make more informed decisions.

The pipeline covers the fundamental stages of a RAG system:

- Document loading and preprocessing
- Exploratory data analysis on the legal corpus
- Text chunking for embedding preparation
- Embedding generation and vector database storage
- Retrieval integrated with a language generation model
- Evaluation of retrieval and generation quality against benchmark Q&A files

## 🗂️ Dataset

The dataset consists of legal documents as text files (`.txt`) organised in a `corpus` folder with four subfolders:

| Folder | Contents |
|---|---|
| `contractnli` | Non-disclosure and confidentiality agreements |
| `cuad` | Contracts with annotated legal clauses |
| `maud` | Merger/acquisition contracts and agreements |
| `privacy_qa` | Privacy policies (question-answering dataset) |

A `benchmark` folder contains evaluation files in JSON format (`contractnli.json`, `cuad.json`, `maud.json`, `privacy_qa.json`). Each file contains test queries with ground-truth answers, source file paths, and answer spans, structured as:

```json
{
  "tests": [
    {
      "query": "<question>",
      "snippets": [
        {
          "file_path": "<source_file>",
          "span": [begin_position, end_position],
          "answer": "<relevant answer>"
        }
      ]
    }
  ]
}
```

## 🏗️ Solution Approach

### 1. Data Loading, Preparation and Analysis
- Load all `.txt` files from the corpus subfolders
- Preprocess text to remove noise and prepare it for analysis
- **EDA**: document length statistics (average, max, min), word frequency analysis (most/least occurring words), and document similarity analysis using TF-IDF vectors
- Split documents into chunks using an appropriate chunking strategy for embedding

### 2. Vector Database and RAG Chain
- Initialise an embedding function to generate document vectors
- Load embeddings into a vector database with a persistent storage directory
- Build a RAG chain integrating the retriever with an LLM
- Implement a query-answering function combining retrieval and generation

### 3. RAG Evaluation
- Extract questions and ground-truth answers from the benchmark files
- Evaluate both retrieval quality and generation quality
- Draw inferences from answers to a sample of benchmark questions

### 4. Conclusions and Insights
- Summarise findings, observations, and learnings from the pipeline

## 🛠️ Tech Stack

- **Language**: Python
- **GenAI Framework**: LangChain
- **Vector Database**: ChromaDB
- **Embeddings & LLM**: (fill in your choices, e.g. OpenAI embeddings + Claude/GPT for generation)
- **Analysis**: pandas, scikit-learn (TF-IDF), matplotlib

## 📁 Repository Structure

```
├── corpus/                  # Legal document corpus (not committed)
│   ├── contractnli/
│   ├── cuad/
│   ├── maud/
│   └── privacy_qa/
├── benchmark/               # Evaluation JSON files
├── vectordb/                # Persisted vector database (not committed)
├── results/                 # Generated outputs (not committed)
├── RAG_Legal_Docs_<name>.ipynb   # Solution notebook
├── .gitignore
└── README.md
```

## 🚀 Getting Started

1. Clone the repository
   ```bash
   git clone https://github.com/<your-username>/<repo-name>.git
   cd <repo-name>
   ```
2. Create a virtual environment and install dependencies
   ```bash
   python -m venv venv
   source venv/Scripts/activate   # Git Bash on Windows
   pip install -r requirements.txt
   ```
3. Add your API keys to a `.env` file (see `.env.example`)
4.  The dataset is in the `corpus/` and `benchmark/` folders
5. Run the notebook `RAG_Legal_Docs.ipynb`
