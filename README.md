# LocalPDF-Chat

An interactive conversational chatbot application that allows you to upload and chat with PDF documents. Built entirely on open-source technologies with no external API dependencies required.

## 📋 Features

- **PDF Upload & Processing**: Upload and process PDF documents locally
- **Intelligent Q&A**: Ask questions about your PDF content and get accurate answers
- **Open Source Stack**: Built with LangChain, Streamlit, and HuggingFace Transformers
- **No API Keys Required**: Runs completely locally without OpenAI or similar API dependencies
- **Vector Database**: Uses ChromaDB for efficient document retrieval
- **Fine-tuned Models**: Leverages LaMini-T5 model for high-quality responses
- **User-Friendly Interface**: Clean web interface powered by Streamlit

## 🛠️ Prerequisites

Before you begin, ensure you have the following installed on your system:

- **Python 3.8 or higher** - [Download Python](https://www.python.org/downloads/)
- **Git** - [Download Git](https://git-scm.com/downloads)
- **pip** - Usually comes with Python
- **At least 8GB RAM** - For model loading and processing
- **Python virtual environment support** (venv)

## 📦 Installation Guide

### Step 1: Clone the Repository

```bash
git clone <repository_url>
cd Chat-with-PDF-Chatbot
```

### Step 2: Create a Virtual Environment

It's recommended to use a virtual environment to avoid dependency conflicts:

**On Windows:**

```bash
python -m venv venv
venv\Scripts\activate
```

**On macOS/Linux:**

```bash
python3 -m venv venv
source venv/bin/activate
```

### Step 3: Install Dependencies

Upgrade pip first to ensure smooth installation:

```bash
pip install --upgrade pip
pip install -r requirements.txt
```

This will install all required packages including:

- `langchain` - LLM orchestration framework
- `streamlit` - Web application framework
- `transformers` - Hugging Face model library
- `torch` - PyTorch deep learning framework
- `chromadb` - Vector database
- `sentence-transformers` - Embedding models

### Step 4: Create Required Directories

The application needs specific directories to function:

```bash
mkdir db
mkdir models
mkdir docs
```

**Directory Explanation:**

- `db/` - Stores the ChromaDB vector database
- `models/` - Reserved for model files (if needed)
- `docs/` - Place your PDF files here

### Step 5: Add Your PDF Files

Place your PDF documents in the `docs` folder:

```
Chat-with-PDF-Chatbot/
├── docs/
│   ├── document1.pdf
│   ├── document2.pdf
│   └── ...
```

## 🚀 Usage

### Step 1: Prepare Your Documents (First Time Only)

Run the ingestion script to process all PDFs in the `docs` folder:

```bash
python ingest.py
```

**What this does:**

- Reads all PDF files from the `docs` folder
- Splits documents into chunks for better processing
- Creates embeddings using SentenceTransformer
- Stores embeddings in ChromaDB for fast retrieval
- Creates the vector database in the `db` folder

**Note:** This step may take a few minutes depending on the size and number of documents.

### Step 2: Launch the Chatbot Application

Start the Streamlit web application:

```bash
streamlit run chatbot_app.py
```

The application will open in your default web browser at `http://localhost:8501`

**What you can do:**

- Ask questions about your PDF documents
- Get instant answers based on document content
- View sources and references
- Chat in a conversational manner

## 📁 Project Structure

```
Chat-with-PDF-Chatbot/
│
├── chatbot_app.py          # Main Streamlit application
├── ingest.py               # PDF ingestion and embedding script
├── constants.py            # Configuration constants
├── requirements.txt        # Python dependencies
├── Dockerfile              # Docker containerization
├── README.md               # This file
│
├── docs/                   # PDF documents folder (create manually)
├── db/                     # Vector database folder (created automatically)
└── models/                 # Models folder (reserved for future use)
```

### File Descriptions

- **chatbot_app.py** - Main application file containing the Streamlit UI and chat logic
- **ingest.py** - Processes PDFs and creates vector embeddings for retrieval
- **constants.py** - Database configuration and settings
- **requirements.txt** - All Python package dependencies with versions

## 🔧 Troubleshooting

### Issue: Port 8501 already in use

**Solution:**

```bash
streamlit run chatbot_app.py --server.port 8502
```

### Issue: CUDA/GPU errors

**Solution:** The app is configured to run on CPU. If you have CUDA installed but experience issues:

```bash
pip install torch --index-url https://download.pytorch.org/whl/cpu
```

### Issue: "No module named 'streamlit'"

**Solution:** Make sure your virtual environment is activated and reinstall requirements:

```bash
pip install -r requirements.txt
```

### Issue: Slow document ingestion

**Solution:** This is normal for large PDFs. Reduce PDF file sizes or split them into smaller documents before ingestion.

### Issue: Running out of memory

**Solution:**

- Close other applications to free up RAM
- The application requires at least 8GB RAM minimum
- Process smaller batches of PDFs

## 🐳 Docker Support

To run this application using Docker:

```bash
docker build -t chat-with-pdf .
docker run -p 8501:8501 chat-with-pdf
```

## 📚 Dependencies

- **langchain** - Framework for building LLM applications
- **streamlit** - Web app framework
- **transformers** - Hugging Face transformer models
- **torch** - PyTorch framework
- **sentence-transformers** - Embedding generation
- **chromadb** - Vector database
- **pdfminer.six** - PDF text extraction
- **beautifulsoup4** - HTML parsing

## 🎯 Performance Tips

1. **First Run**: The first run will download models (~2-5 GB). This only happens once.
2. **Large PDFs**: Split very large PDFs (>100 pages) into smaller files
3. **Multiple Documents**: Process similar documents together for better context
4. **Memory**: Monitor your system's RAM usage during ingestion

## 📝 Notes

- All processing happens locally on your machine
- No data is sent to external APIs
- Suitable for confidential documents
- Works best with text-based PDFs
- Scanned PDFs may have lower accuracy

## 🤝 Contributing

Feel free to fork this repository and submit pull requests for any improvements.

## 📄 License

This project uses open-source libraries. Please refer to individual library licenses.

## ❓ Support

For issues and questions, please check the troubleshooting section above or create an issue in the repository.
