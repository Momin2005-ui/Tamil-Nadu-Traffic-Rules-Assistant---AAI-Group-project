# Traffic Rules Assistant (Tamil Nadu RAG Chatbot)

An AI-powered assistant built using Retrieval-Augmented Generation (RAG) that provides context-aware answers about Tamil Nadu traffic rules, penalties, and driver rights. It combines semantic search with LLMs for accurate, explainable, and trustworthy responses.

## Group Members

| Name                           | Email                       |
|--------------------------------|-----------------------------|
| Mohana Krishnan                | 23bds035@iiitdwd.ac.in      |
| Momin M                        | 23bds036@iiitdwd.ac.in      |
| Prasann Kote                   | 23bds045@iiitdwd.ac.in      |
| Preetham P                     | 23bds046@iiitdwd.ac.in      |
| Prem Sagar                     | 23bds065@iiitdwd.ac.in      |


## Overview

This project extracts legal content from a government-issued traffic PDF and makes it queryable via natural language questions using a custom-built RAG pipeline. It uses:

* `sentence-transformers` for generating document embeddings
* `FAISS` for fast semantic retrieval
* `LangChain` with `Groq` LLM backend for fast and accurate response generation
* `FastAPI` to expose the system as an API

The assistant is designed to provide concise, legally grounded, and verifiable answers.

---

## Target Audience

* Citizens of Tamil Nadu
* Driving school instructors and trainees
* Traffic law educators
* AI/ML enthusiasts learning about RAG pipelines

---

---

### Project Demo Video 1
[![Watch the video](https://github.com/Momin2005-ui/Tamil-Nadu-Traffic-Rules-Assistant---AAI-Group-project/blob/main/Screenshot_15-11-2025_233625_docs.google.com.jpeg)](https://drive.google.com/file/d/1Vg5eeaam3KHCpOX7zrkDbkNp_MnZIkWN/view)

### Project Demo Video 2
[![Watch the video](https://github.com/Momin2005-ui/Tamil-Nadu-Traffic-Rules-Assistant---AAI-Group-project/blob/main/Screenshot%202025-11-16%20212531.png)](https://drive.google.com/file/d/1cZv2iexbnEI91Tb0dqirjipf5UtVv8P_/view)

## Rag Architecture
![Screenshot 2025-04-06 233208 1](https://github.com/Momin2005-ui/Tamil-Nadu-Traffic-Rules-Assistant---AAI-Group-project/blob/main/rag_architecture.png)

## Llama 3.1 Architecture
![Screenshot 2025-04-06 233208 1](https://github.com/Momin2005-ui/Tamil-Nadu-Traffic-Rules-Assistant---AAI-Group-project/blob/main/llama.png)

## Repo Structure
```plaintext
traffic_rules_assistant/
├── .venv/          
├── data/
|   ├── processed/
|   |    ├── faiss_index.idx
|   |    ├── TN_traffic_rules.json
|   |    └── TN_traffic_rules.txt
|   └──  TN Traffic rules.pdf
├── src/
│   ├── chunking.py 
│   ├── embedding.py 
│   ├── generator.py
│   ├── retriever.py
│   ├── main.py
│   └── text_extraction.py 
├── api/
│   └──  app.py
├── frontend/ 
│   └── index.html  
├── .gitignore
├── .python-version
├── README.md
├── requirements.txt
└── pyproject.toml
```

## Prerequisites

* Python 3.11+
* Basic terminal/CLI knowledge
* Internet access for LLM API (Groq)
* Groq API key (free tier available)

---

## Installation

```bash
# Clone the repository
https://github.com/madhans476/traffic_rules_assistant.git

cd traffic_rules_assistant

# Create environment
uv venv .venv
source .venv/bin/activate  # or .venv\Scripts\activate on Windows

# Install dependencies
uv pip install -r requirements.txt
```

---

## Environment Setup

### `.env` file (create at root):

```
GROQ_API_KEY=your-groq-api-key-here
```

### Required files:

* `data/TN Traffic rules.pdf`

---

## Usage

### 1. Text Extraction

```bash
python src/text_extraction.py
```

### 2. Chunking

```bash
python src/chunking.py
```

### 3. Embedding + FAISS Index Creation

```bash
python src/embedding.py
```

### 4. CLI Chatbot

```bash
python src/main.py
```

### 5. API (FastAPI)

```bash
uvicorn api.app:app --reload
# Visit http://localhost:8000/docs
```

---

## Data Requirements

* Input: A traffic rulebook in `.pdf`
* Output:

  * `.txt` file with full extracted text
  * `.json` with clean overlapping chunks
  * `.idx` FAISS index file

---

## Testing

Manual test cases:

* Ask questions from the CLI or Swagger UI
* Evaluate LLM responses vs. original PDF

(Automated tests can be added using `pytest`.)

---

## Configuration

### Chunking:

* `chunk_size = 300`
* `overlap = 50`

### FAISS:

* `IndexFlatIP` used for vector similarity search

### LLM (Groq):

* Model: `mixtral-8x7b-32768` (default)
* Temperature: `0.3`

---

## Methodology

1. Parse legal traffic PDF to text
2. Split text into semantic chunks
3. Embed chunks using `sentence-transformers`
4. Store in `FAISS` for fast vector search
5. On query:

   * Embed the question
   * Retrieve top-k relevant chunks
   * Pass to Groq LLM using LangChain
6. Return clean, structured answer

---

## Performance

* Fast local retrieval (\~50–100 ms)
* Groq LLM response: \~100 tokens/ms
* Accurate context-based answers
* No hallucinations (guardrails in prompt)

---

## License

MIT License. See `LICENSE` file.

---

## Contributing

Pull requests welcome!

* Fork the repo
* Create a new branch
* Submit a pull request with a meaningful message

---

## Changelog

### v1.0.0 (November 2025)

* Initial public release
* Added full pipeline: Extraction, Chunking, Embedding, Retrieval, Generation
* FastAPI API + CLI support
* Groq + LangChain integration

---
