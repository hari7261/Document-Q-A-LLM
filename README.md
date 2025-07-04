# Document Q&A Assistant with RAG

A powerful Streamlit application that allows you to upload documents and ask questions about them using Retrieval-Augmented Generation (RAG) with local LLM processing.

![Document Q&A Assistant with RAG](/image.png)

## 🚀 Features

- **Document Upload Support**: PDF, DOCX, and TXT files
- **Real-time Progress Tracking**: Visual progress indicators during document processing
- **Local Processing**: All data processing happens locally using Ollama
- **Smart Chunking**: Intelligent text splitting with sentence boundary detection
- **Vector Search**: ChromaDB for efficient similarity search
- **Caching**: Optimized performance with smart caching mechanisms
- **Performance Metrics**: Track response times and query statistics
- **Interactive Chat Interface**: User-friendly chat experience with streaming responses

## 📋 Prerequisites

Before running this application, make sure you have:

1. **Python 3.8+** installed
2. **Ollama** installed and running locally
3. **Gemma3 model** downloaded in Ollama

### Installing Ollama

1. Download and install Ollama from [https://ollama.ai](https://ollama.ai)
2. Pull the Gemma3 model:
   ```bash
   ollama pull gemma3
   ```

## 🛠️ Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/hari7261/Document-Q-A-LLM.git
   cd Document-Q-A-LLM
   ```

2. **Create a virtual environment** (recommended):
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

## 🚀 Usage

1. **Start the application**:
   ```bash
   streamlit run app.py
   ```

2. **Open your browser** and navigate to `http://localhost:8501`

3. **Upload documents**:
   - Use the sidebar to upload PDF, DOCX, or TXT files
   - Click "Process Documents" to index your files
   - Watch the real-time progress tracking

4. **Ask questions**:
   - Type your questions in the chat input
   - Get AI-powered answers based on your documents
   - View source citations for transparency

## 📁 Project Structure

```
Document-Q-A-LLM/
├── app.py                 # Main Streamlit application
├── requirements.txt       # Python dependencies
├── README.md             # Project documentation
├── .gitignore            # Git ignore rules
├── LICENSE               # License file
├── setup.py              # Package setup file
├── chroma_db/            # ChromaDB storage (created automatically)
│   └── chroma.sqlite3    # Vector database
├── .github/              # GitHub templates and workflows
│   └── ISSUE_TEMPLATE/   # Issue templates
└── docs/                 # Additional documentation
    ├── installation.md
    ├── usage.md
    └── api.md
```

## ⚙️ Configuration

### Model Settings
- **Temperature**: Control randomness in responses (0.0 - 1.0)
- **Model**: Currently supports Gemma3 (more models can be added)

### Performance Optimization
- **Caching**: Responses are cached for 1 minute, search results for 5 minutes
- **Chunking**: Documents are split into 1000-character chunks with sentence boundary detection
- **Batch Processing**: Documents are processed in optimized batches

## 🔧 Advanced Configuration

You can customize the application by modifying these parameters in `app.py`:

```python
# Chunk size for document splitting
chunk_size = 1000

# Number of relevant chunks to retrieve
k = 5

# Cache TTL settings
cache_ttl_responses = 60    # 1 minute
cache_ttl_search = 300      # 5 minutes
```

## 📊 Performance Metrics

The application tracks:
- Average response time
- Last response time
- Total queries processed

Access these metrics through the expandable "Performance Metrics" section in the sidebar.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🐛 Known Issues

- Large PDF files may take longer to process
- Ensure Ollama is running before starting the application
- ChromaDB requires write permissions in the project directory

## 🆘 Troubleshooting

### Common Issues

1. **"Model not found" error**:
   ```bash
   ollama pull gemma3
   ```

2. **ChromaDB permission errors**:
   - Ensure the application has write permissions in the project directory

3. **Slow processing**:
   - Check if Ollama is running locally
   - Verify system resources (RAM, CPU)

## 📞 Support

If you encounter any issues or have questions:
- Open an issue on GitHub
- Check the [documentation](docs/)
- Review the troubleshooting section

## 🙏 Acknowledgments

- [Streamlit](https://streamlit.io/) for the amazing web framework
- [Ollama](https://ollama.ai/) for local LLM capabilities
- [ChromaDB](https://www.trychroma.com/) for vector database functionality
- [SentenceTransformers](https://www.sbert.net/) for embeddings

---

**Made with ❤️ by [Hariom Kumar](https://github.com/hari7261) for the open-source community**

Repository: [https://github.com/hari7261/Document-Q-A-LLM](https://github.com/hari7261/Document-Q-A-LLM)
