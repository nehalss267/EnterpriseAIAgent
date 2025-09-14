# EnterpriseAIAgent: A RAG-based PDF Q\&A System

EnterpriseAIAgent is a powerful Question-Answering (Q\&A) application built with Python. It leverages a **Retrieval-Augmented Generation (RAG)** architecture to answer questions based on the content of a specified PDF document.

This tool uses Google's **Gemini-1.5-Flash** model, **Milvus** for vector storage, and the **LangChain** framework to create a seamless interactive experience through a Gradio web interface.

## Key Features

  - **PDF Knowledge Base**: Ingests any PDF file as the source of truth for answering questions.
  - **State-of-the-Art LLM**: Powered by Google's `gemini-1.5-flash` for fast and contextually-aware responses.
  - **Efficient Vector Search**: Utilizes `Milvus`, a high-performance, open-source vector database for rapid semantic search.
  - **Advanced Text Processing**: Uses `Hugging Face Transformers` for cutting-edge text embedding and tokenization.
  - **Orchestration Framework**: Built entirely with `LangChain` to streamline and connect all components of the RAG pipeline.
  - **Interactive UI**: Features a simple and intuitive web interface created with `Gradio`.

-----

## How It Works

The application follows a standard RAG process:

### 1\. Indexing Phase

First, the application prepares the knowledge base.

  - **Load**: The specified PDF document (`EnterpriseAIAgent_knowledgeBase.pdf`) is loaded and its text is extracted.
  - **Split**: The extracted text is divided into smaller, manageable chunks.
  - **Embed**: Each chunk is converted into a numerical vector (an "embedding") that captures its semantic meaning.
  - **Store**: These embeddings are stored and indexed in a local Milvus vector database for efficient retrieval.

### 2\. Retrieval & Generation Phase

This is what happens when you ask a question.

  - **Embed Query**: Your question is also converted into an embedding using the same model.
  - **Retrieve**: The Milvus database is queried to find the most relevant text chunks from the PDF based on semantic similarity to your question's embedding.
  - **Generate**: These relevant chunks (the context) and your original question are sent to the Gemini LLM, which then generates a comprehensive, human-like answer.

-----

## Setup and Installation

Follow these steps to get the EnterpriseAIAgent running on your local machine.

### 1\. Prerequisites

  - Python 3.8 or higher.
  - `pip` package manager.

### 2\. Clone the Repository

If this project is in a Git repository, clone it:

```bash
git clone <your-repository-url>
cd <your-repository-name>
```

### 3\. Create a Virtual Environment (Recommended)

It's best practice to create a virtual environment to manage project dependencies.

```bash
# For Windows
python -m venv venv
.\venv\Scripts\activate

# For macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

### 4\. Install Dependencies

Install all the required Python libraries using `pip`:

```bash
pip install gradio langchain langchain_community langchain_milvus transformers pymilvus sentence-transformers google-generativeai langchain-google-genai pypdf pdfplumber torch
```

### 5\. Get Your Google API Key

  - Go to the [Google AI Studio](https://aistudio.google.com/app/apikey) to generate your free API key.
  - Open the Python script and replace `"<API_KEY>"` with your actual key:
    ```python
    os.environ["GOOGLE_API_KEY"] = "YOUR_ACTUAL_GEMINI_API_KEY"
    ```

### 6\. Add Your Knowledge Base PDF

  - Place the PDF file you want to query in the same directory as the script.
  - Ensure the PDF is named **`EnterpriseAIAgent_knowledgeBase.pdf`**. If you wish to use a different name, you must update the `filename` variable in the script:
    ```python
    filename = "your_document_name.pdf"
    ```

-----


## Running the Application

1.  **Execute the Script**
    With your virtual environment active, run the script from your terminal:

    ```bash
    python your_script_name.py
    ```

2.  **Access the Web Interface**
    The terminal will display a local URL (usually `http://127.0.0.1:7860`). Open this URL in your web browser to start interacting with the EnterpriseAIAgent.

Simply type your question about the PDF's content into the input box and press Enter. The AI will process your query and provide an answer based on its knowledge from the document.
