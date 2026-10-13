# Medical Chatbot

An AI-powered Medical Chatbot built using **Flask, LangChain, Groq, Hugging Face Embeddings, and Pinecone**.

The chatbot uses a Retrieval-Augmented Generation (RAG) architecture to provide answers based on medical documents stored in a vector database.

## Features

- AI-powered medical question answering
- Retrieval-Augmented Generation (RAG)
- Medical PDF document processing
- Semantic search using Hugging Face embeddings
- Pinecone vector database for document retrieval
- Groq LLM for generating responses
- Flask-based web application
- Modern chatbot interface
- Environment variable support for API keys
- Designed for future conversational memory integration

## Tech Stack

| Technology | Purpose |
|---|---|
| Python | Programming language |
| Flask | Web application backend |
| LangChain | RAG and LLM integration |
| Groq | Large Language Model |
| Hugging Face | Text embeddings |
| Pinecone | Vector database |
| PyPDF | PDF document processing |
| HTML/CSS/JavaScript | Frontend |
| Jupyter Notebook | Development and experimentation |

## Project Architecture

```text
User
  |
  v
Chatbot UI
  |
  v
Flask Backend
  |
  v
User Question
  |
  v
Retriever
  |
  v
Pinecone Vector Database
  |
  v
Relevant Medical Documents
  |
  v
Groq LLM
  |
  v
Generated Answer
  |
  v
User
```

## Project Structure

```text
Medical-Chatbot/
│
├── data/
│   └── medical PDFs
│
├── research/
│   └── trials.ipynb
│
├── src/
│   ├── __init__.py
│   ├── helper.py
│   └── prompt.py
│
├── static/
│   └── style.css
│
├── templates/
│   └── chatbot.html
│
├── app.py
├── requirements.txt
├── setup.py
├── .env
├── .gitignore
└── README.md
```

## How It Works

### 1. Medical Documents

Medical PDF documents are placed inside the `data/` directory.

The PDFs are loaded and converted into documents using `PyPDFLoader`.

### 2. Text Splitting

The extracted text is divided into smaller chunks using a text splitter.

Example configuration:

```python
RecursiveCharacterTextSplitter(
    chunk_size=500,
    chunk_overlap=50
)
```

### 3. Embeddings

Each text chunk is converted into a numerical vector using:

```text
sentence-transformers/all-MiniLM-L6-v2
```

The embedding model produces 384-dimensional vectors.

### 4. Pinecone

The generated embeddings are stored in a Pinecone vector index.

When a user asks a question, the chatbot searches Pinecone for the most relevant medical information.

### 5. Groq LLM

The retrieved information is provided to the Groq LLM along with the user's question.

The model generates the final response.

# Installation

## 1. Clone the Repository

```bash
git clone <your-repository-url>
cd Medical-Chatbot
```

## 2. Create Conda Environment

```bash
conda create -n medibot python=3.13 -y
```

Activate it:

```bash
conda activate medibot
```

## 3. Install Dependencies

```bash
pip install -r requirements.txt
```

# Environment Variables

Create a `.env` file in the project root:

```env
PINECONE_API_KEY=your_pinecone_api_key
GROQ_API_KEY=your_groq_api_key
FLASK_SECRET_KEY=your_secret_key
```

Never upload your `.env` file to GitHub.

Add it to `.gitignore`:

```text
.env
__pycache__/
*.pyc
.venv/
venv/
```

# Running the Application

Start the Flask application:

```bash
python app.py
```

The application will run locally at:

```text
http://localhost:8080
```

# RAG Pipeline

```text
Medical PDFs
     |
     v
PDF Loader
     |
     v
Text Extraction
     |
     v
Text Splitting
     |
     v
Hugging Face Embeddings
     |
     v
Pinecone
     |
     v
Retriever
     |
     v
Groq LLM
     |
     v
Medical Chatbot
```

# Medical Disclaimer

This chatbot is intended for educational and informational purposes only.

It should not be considered a replacement for professional medical advice, diagnosis, or treatment.

Users should consult a qualified healthcare professional for medical concerns.

# Author

**Ravi Bhamniya**

B.Tech — Artificial Intelligence & Data Science

Interested in:

- Artificial Intelligence
- Machine Learning
- Generative AI
- Data Science
- Natural Language Processing
- AI-powered applications

# License

This project is intended for educational and development purposes.