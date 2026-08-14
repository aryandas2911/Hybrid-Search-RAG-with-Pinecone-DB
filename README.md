# Hybrid Search RAG with Pinecone DB

A comprehensive miniproject demonstrating Retrieval-Augmented Generation (RAG) using hybrid search capabilities with Pinecone, LangChain, and modern NLP embeddings.

## 📋 Overview

This project implements a **Hybrid Search RAG system** that combines two powerful search methodologies:

- **Semantic Search**: Uses dense vector embeddings from HuggingFace to find conceptually similar documents
- **Keyword Search**: Uses BM25 sparse encoding for exact term matching

By combining both approaches, the system retrieves documents that are not only conceptually similar but also contain important exact keywords, providing more accurate and relevant search results.

## 🎯 Key Features

- **Hybrid Search Integration**: Combines dense and sparse vector search for improved retrieval accuracy
- **Pinecone Vector Database**: Serverless vector database for efficient similarity search
- **LangChain Integration**: Uses LangChain's PineconeHybridSearchRetriever for seamless integration
- **HuggingFace Embeddings**: Leverages the `all-MiniLM-L6-v2` model for generating document embeddings
- **BM25 Encoding**: Sparse vector encoding for keyword-based search
- **Environment Configuration**: Secure API key management using `.env` files

## 🛠️ Tech Stack

| Technology | Purpose |
|-----------|---------|
| **Pinecone** | Vector database for storing and retrieving embeddings |
| **LangChain** | Framework for building RAG applications |
| **HuggingFace** | Pre-trained embedding models |
| **Python** | Programming language |
| **Jupyter Notebook** | Interactive development environment |

## 📦 Installation

### Prerequisites
- Python 3.8 or higher
- Pinecone API key ([Get one here](https://www.pinecone.io/))
- pip (Python package manager)

### Setup

1. **Clone or download the project**
   ```bash
   cd "Hybrid Search RAG with Pinecone DB"
   ```

2. **Create a virtual environment** (recommended)
   ```bash
   python -m venv .venv
   # On Windows
   .venv\Scripts\activate
   # On macOS/Linux
   source .venv/bin/activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure environment variables**
   - Create a `.env` file in the project root directory
   - Add your Pinecone API key:
     ```
     PINECONE_API_KEY=your_api_key_here
     ```

## 🚀 Usage

### Running the Jupyter Notebook

```bash
jupyter notebook "Hybrid Search RAG Project.ipynb"
```

### Main Workflow

The notebook follows this workflow:

1. **Initialize Pinecone Index**
   - Creates a serverless index with 384-dimensional vectors
   - Uses AWS US-East-1 region with dot product metric

2. **Load Embeddings**
   - Initializes HuggingFace embeddings using `all-MiniLM-L6-v2` model
   - Sets up BM25 encoder for sparse vectors

3. **Add Documents**
   - Sample documents on RAG, PostgreSQL, and Prompt Injection are added to the index
   - Documents are indexed with both dense and sparse representations

4. **Perform Hybrid Search**
   - Query the retriever with natural language questions
   - Returns relevant documents ranked by hybrid search score

### Example Query

```python
# Query the retriever
results = retriever.invoke("What is Prompt Injection?")

# Access retrieved documents with scores
for doc in results:
    print(f"Content: {doc.page_content}")
    print(f"Score: {doc.metadata['score']}")
```

## 📚 Project Structure

```
Hybrid Search RAG with Pinecone DB/
├── Hybrid Search RAG Project.ipynb  # Main Jupyter notebook
├── requirements.txt                  # Python dependencies
├── bm25_values.json                 # BM25 encoder values (auto-generated)
├── .env                             # Environment variables (create this)
└── README.md                        # This file
```

## 🔑 Key Concepts

### Hybrid Search
Combines two complementary search techniques:
- **Dense vectors** capture semantic meaning and conceptual similarity
- **Sparse vectors** (BM25) capture exact keyword matches

This hybrid approach reduces false negatives by ensuring exact keywords aren't overlooked, while also finding conceptually similar documents.

### Retrieval-Augmented Generation (RAG)
RAG systems enhance LLM responses by:
1. Retrieving relevant documents from a knowledge base
2. Providing these documents as context to the language model
3. Generating responses based on both the retriever documents and the model's training

### Pinecone Index
- **Dimension**: 384 (matches the embedding model output)
- **Metric**: Dot product for similarity calculation
- **Spec**: Serverless architecture for automatic scaling
- **Cloud**: AWS US-East-1

## 🧪 Sample Data

The project includes sample documents covering:

1. **Retrieval-Augmented Generation (RAG)**
   - Explanation of RAG systems
   - Hybrid search advantages
   - How RAG improves LLM responses

2. **PostgreSQL**
   - Relational database features
   - Indexing strategies
   - Query optimization

3. **Prompt Injection**
   - Definition and attack vectors
   - Direct vs. indirect prompt injection
   - Security implications for RAG systems

## 🔐 Security Considerations

- **API Key Management**: Store Pinecone API keys in `.env` files, never commit them to version control
- **Indirect Prompt Injection**: Be aware that retrieved documents in RAG systems can potentially contain malicious instructions
- **Document Validation**: Consider validating and sanitizing documents before adding them to the knowledge base

## 📝 Notes

- The BM25 encoder is trained on the sample documents and saved to `bm25_values.json`
- For production use, train the BM25 encoder on your actual document corpus
- Experiment with different embedding models from HuggingFace for better domain-specific results

## 🤝 Contributing

Feel free to enhance this project by:
- Adding more sophisticated document preprocessing
- Implementing different embedding models
- Building a web interface for the RAG system
- Extending with multi-document retrieval pipelines
