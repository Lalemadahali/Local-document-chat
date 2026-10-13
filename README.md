# Local-document-chat
Chat with PDF and text documents using LangChain, Ollama, and local embedding models.

# Local Document Chat with LangChain and Ollama

A Python notebook for asking questions about PDF, text, and Markdown documents using locally running AI models. This project demonstrates a **Retrieval-Augmented Generation (RAG)** workflow without paid API calls.

## Features

- Load PDF, TXT, and Markdown files.
- Split documents into overlapping text chunks.
- Generate embeddings locally with `embeddinggemma`.
- Search for relevant passages using LangChain’s `InMemoryVectorStore`.
- Generate answers with `gemma3:4b` through Ollama.
- Request numbered citations linking answers to retrieved excerpts.

## How It Works

1. **Load:** Read documents from the `documents` folder.
2. **Split:** Divide text into chunks of approximately 1,000 characters, with a target overlap of 150 characters.
3. **Embed:** Convert each chunk into a numerical vector representing its meaning.
4. **Retrieve:** Find up to four chunks most similar to the user’s question.
5. **Answer:** Provide those chunks and the question to the chat model.

The models are not trained or fine-tuned on the documents. Relevant passages are supplied as context when answering a question.

## Setup

### 1. Install Python packages

Run this command in your Python environment:

```bash
python -m pip install langchain-core langchain-community langchain-text-splitters langchain-ollama pypdf numpy jupyter
```

### 2. Install Ollama and download the models

Install [Ollama](https://ollama.com/download), then run:

```bash
ollama pull embeddinggemma
ollama pull gemma3:4b
```

Keep Ollama running while using the notebook.

### 3. Add your documents

Create a folder named `documents` in the notebook’s working directory. Add your PDF, TXT, or Markdown files there.

### 4. Run the notebook

Run the document-loading and indexing cell, followed by the cell that defines the chat model and `ask_documents()` function.

Then ask a question:

```python
ask_documents("What does the document say about machine learning?")
```

## Tools Used

- Python
- LangChain
- Ollama
- EmbeddingGemma
- Gemma 3
- InMemoryVectorStore
- Jupyter Notebook

## Current Limitations

- The vector index is stored in RAM and must be rebuilt after restarting the kernel.
- Scanned PDFs require OCR before their text can be searched.
- Each question is independent; conversation history is not retained.
- Answers depend on the retrieved excerpts and may miss information elsewhere in the documents.
- Generated answers and citations should be checked against the source text.
- Performance depends on available RAM and CPU/GPU resources.

## Privacy

The embedding and chat models run locally through Ollama. No OpenAI API key is required.

Keep private documents, API keys, and `.env` files out of this repository. Clear sensitive notebook outputs before committing changes.
