# Medical Chatbot

An AI-powered Medical Chatbot built using **Flask, LangChain, Groq, Hugging Face Embeddings, and Pinecone**.

The chatbot uses a **Retrieval-Augmented Generation (RAG)** architecture to retrieve relevant information from medical documents and generate context-based responses using a Large Language Model.

---

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
- Separate script for storing document embeddings

---

## Tech Stack

| Technology | Purpose |
|---|---|
| Python 3.13 | Programming language |
| Flask | Web application backend |
| LangChain | RAG and LLM integration |
| Groq | Large Language Model |
| Hugging Face | Text embeddings |
| Pinecone | Vector database |
| PyPDF | PDF document processing |
| HTML/CSS/JavaScript | Frontend |
| Jupyter Notebook | Research and experimentation |

---

## Project Architecture

```text
Medical Documents
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
Pinecone Vector Database
       |
       v
Retriever
       |
       v
Relevant Medical Context
       |
       v
Groq LLM
       |
       v
Generated Answer
       |
       v
Chatbot UI
```

---

## Project Structure

```text
Medical-Chatbot/
│
├── data/
│   └── Medical documents / PDF files
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
├── .env
├── .gitignore
├── app.py
├── LICENSE
├── README.md
├── requirements.txt
├── setup.py
├── store_index.py
└── template.sh
```

---

# Installation

## STEP 01 - Clone the Repository

```bash
git clone <your-github-repository-url>
cd Medical-Chatbot
```

---

## STEP 02 - Create a Conda Environment

Create a Conda environment using Python 3.13:

```bash
conda create -n medibot python=3.13 -y
```

Activate the environment:

```bash
conda activate medibot
```

Check the Python version:

```bash
python --version
```

---

## STEP 03 - Install Requirements

Install the required packages:

```bash
pip install -r requirements.txt
```

---

## STEP 04 - Configure Environment Variables

Create a `.env` file in the root directory of the project.

Add your API keys:

```env
PINECONE_API_KEY=your_pinecone_api_key
GROQ_API_KEY=your_groq_api_key
FLASK_SECRET_KEY=your_flask_secret_key
```

**Do not upload your `.env` file to GitHub.**

Make sure `.env` is included in `.gitignore`.

---

## STEP 05 - Add Medical Documents

Place your medical PDF documents inside the:

```text
data/
```

directory.

Example:

```text
data/
├── medical_book.pdf
├── medical_notes.pdf
└── other_medical_documents.pdf
```

---

## STEP 06 - Store Embeddings in Pinecone

After adding the medical documents, run:

```bash
python store_index.py
```

This script processes the documents, creates embeddings using the Hugging Face embedding model, and stores them in the Pinecone vector database.

---

## STEP 07 - Run the Application

Start the Flask application:

```bash
python app.py
```

The chatbot will run locally.

Open:

```text
http://localhost:8080
```

in your browser.

---

# How It Works

### 1. Medical Documents

Medical PDF files are stored inside the `data/` directory.

The application loads the documents and extracts their text.

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

The embedding model generates vector representations that can be used for semantic search.

### 4. Pinecone

The generated embeddings are stored in a Pinecone vector index.

When a user asks a question, the chatbot searches Pinecone for the most relevant medical information.

### 5. Groq LLM

The retrieved medical context is passed to the Groq LLM along with the user's question.

The model generates the final response.

---

# Main Files

## `app.py`

The main Flask application.

It:

- Creates the Flask server
- Loads environment variables
- Connects to Pinecone
- Initializes the Groq LLM
- Creates the retrieval chain
- Handles chatbot requests
- Returns responses to the frontend

---

## `store_index.py`

Used to process the medical documents and store their embeddings in Pinecone.

Run:

```bash
python store_index.py
```

whenever the document collection needs to be indexed.

---

## `src/helper.py`

Contains helper functions used for:

- Loading PDF documents
- Splitting documents into chunks
- Creating Hugging Face embeddings

---

## `src/prompt.py`

Contains the prompt used by the LLM to generate responses based on the retrieved medical context.

---

## `templates/chatbot.html`

Contains the HTML structure of the chatbot interface.

---

## `static/style.css`

Contains the styling and UI design for the chatbot.

---

## `research/trials.ipynb`

Used for experimentation, testing, and development during the project.

---

# RAG Pipeline

```text
User Question
      |
      v
Flask Application
      |
      v
Retriever
      |
      v
Pinecone
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

---

# Embedding Model

The project uses:

```text
sentence-transformers/all-MiniLM-L6-v2
```

This model converts text into vector embeddings that are stored and searched in Pinecone.

---

# LLM

The chatbot uses **Groq** as the LLM provider through LangChain.

The model is configured in `app.py` using:

```python
from langchain_groq import ChatGroq
```

---

# Vector Database

**Pinecone** is used as the vector database.

It stores the embeddings generated from the medical documents and retrieves relevant documents when the user asks a question.

---

# Environment Variables

| Variable | Purpose |
|---|---|
| `PINECONE_API_KEY` | Pinecone vector database access |
| `GROQ_API_KEY` | Groq API access |
| `FLASK_SECRET_KEY` | Flask application secret key |

---

# Important Notes

- Add medical PDF files inside the `data/` directory.
- Run `store_index.py` after adding or changing documents.
- Make sure the Pinecone index is available before running the chatbot.
- Keep API keys private.
- Do not commit `.env` to GitHub.
- Run the commands from the project root directory.

---

# Medical Disclaimer

This chatbot is intended for educational and informational purposes only.

It should not be considered a replacement for professional medical advice, diagnosis, or treatment.

For medical concerns, consult a qualified healthcare professional.

---

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

---

# License

This project is intended for educational and development purposes.