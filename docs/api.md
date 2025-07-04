# API Documentation

## Overview

The Document Q&A Assistant provides several key functions and components that work together to process documents and answer questions. This documentation covers the main API functions and their usage.

## Core Functions

### Document Processing Functions

#### `chunk_text(text: str, chunk_size: int = 1000) -> List[str]`

Splits text into manageable chunks for processing.

**Parameters:**
- `text` (str): Input text to be chunked
- `chunk_size` (int, optional): Maximum size of each chunk in characters. Default: 1000

**Returns:**
- `List[str]`: List of text chunks

**Example:**
```python
text = "Your long document text here..."
chunks = chunk_text(text, chunk_size=500)
print(f"Created {len(chunks)} chunks")
```

**Features:**
- Attempts to split at sentence boundaries (`.`, `!`, `?`, `\n`)
- Falls back to hard split if no sentence boundary found
- Strips whitespace from chunks

---

#### `process_document(uploaded_file, progress_bar=None, status_text=None) -> int`

Processes an uploaded document and stores it in the vector database.

**Parameters:**
- `uploaded_file`: Streamlit uploaded file object
- `progress_bar` (optional): Streamlit progress bar widget
- `status_text` (optional): Streamlit text widget for status updates

**Returns:**
- `int`: Number of chunks created from the document

**Supported File Types:**
- PDF: `application/pdf`
- Word: `application/vnd.openxmlformats-officedocument.wordprocessingml.document`
- Text: `text/plain`

**Example:**
```python
# With progress tracking
chunks_count = process_document(
    uploaded_file, 
    progress_bar=st.progress(0),
    status_text=st.empty()
)

# Without progress tracking
chunks_count = process_document(uploaded_file)
```

**Processing Steps:**
1. Text extraction based on file type
2. Progress updates (50% for extraction)
3. Text chunking
4. Vector storage with metadata (50% for storage)

---

### Query and Response Functions

#### `retrieve_relevant_chunks(query: str, k: int = 5) -> Tuple[List[str], List[str]]`

Retrieves relevant document chunks based on semantic similarity.

**Parameters:**
- `query` (str): User question or search query
- `k` (int, optional): Number of chunks to retrieve. Default: 5

**Returns:**
- `Tuple[List[str], List[str]]`: (document_chunks, metadata_list)

**Features:**
- Uses semantic search with sentence transformers
- Cached for 5 minutes (300 seconds)
- Returns both content and source metadata

**Example:**
```python
chunks, metadata = retrieve_relevant_chunks(
    "What are the eligibility requirements?", 
    k=3
)
for chunk, meta in zip(chunks, metadata):
    print(f"From {meta['source']}: {chunk[:100]}...")
```

---

#### `generate_response(query: str, context: str, temp: float = 0.7, model: str = "gemma3") -> str`

Generates AI response using context from retrieved documents.

**Parameters:**
- `query` (str): User question
- `context` (str): Concatenated relevant document chunks
- `temp` (float, optional): Temperature for response generation. Default: 0.7
- `model` (str, optional): Model name. Default: "gemma3"

**Returns:**
- `str`: Generated response

**Features:**
- Cached for 1 minute (60 seconds)
- Optimized with token limits for faster responses
- Uses RAG (Retrieval-Augmented Generation) pattern

**Example:**
```python
context = "\n\n".join(relevant_chunks)
response = generate_response(
    query="How do I apply?",
    context=context,
    temp=0.5,
    model="gemma3"
)
```

**Generation Options:**
- `num_predict`: 512 (token limit for faster responses)
- `num_ctx`: 2048 (context window size)

## Data Structures

### Session State Variables

#### Messages
```python
st.session_state.messages = [
    {"role": "user", "content": "User question"},
    {"role": "assistant", "content": "AI response"}
]
```

#### Uploaded Files
```python
st.session_state.uploaded_files = [
    "document1.pdf",
    "document2.docx"
]
```

#### Performance Metrics
```python
st.session_state.performance_metrics = {
    "total_queries": int,
    "avg_response_time": float,
    "last_response_time": float
}
```

### Database Schema

#### ChromaDB Collection Structure
```python
collection.add(
    documents=["chunk1", "chunk2", ...],
    ids=["filename-0", "filename-1", ...],
    metadatas=[
        {"source": "filename.pdf"},
        {"source": "filename.pdf"}
    ]
)
```

## Configuration Options

### ChromaDB Settings
```python
# Database path
client = chromadb.PersistentClient(path="./chroma_db")

# Embedding function
sentence_transformer_ef = embedding_functions.SentenceTransformerEmbeddingFunction(
    model_name="all-MiniLM-L6-v2"
)
```

### Caching Configuration
```python
# Response caching
@st.cache_data(ttl=60, show_spinner=False)

# Search result caching  
@st.cache_data(ttl=300)
```

### Model Configuration
```python
ollama_options = {
    'temperature': 0.7,        # Randomness (0.0-1.0)
    'num_predict': 512,        # Max output tokens
    'num_ctx': 2048           # Context window
}
```

## Error Handling

### Common Exceptions

#### File Processing Errors
```python
try:
    chunks_count = process_document(uploaded_file)
except Exception as e:
    st.error(f"Error processing document: {str(e)}")
```

#### Database Connection Errors
```python
try:
    collection = client.get_collection(name="documents")
except:
    collection = client.create_collection(name="documents")
```

#### Model Generation Errors
```python
try:
    response = ollama.generate(model=model_name, prompt=prompt)
except Exception as e:
    st.error(f"Error generating response: {str(e)}")
```

## Performance Optimization

### Batch Processing
```python
# Process chunks in batches for better progress updates
batch_size = max(1, len(chunks) // 10)
for i in range(0, len(chunks), batch_size):
    end_idx = min(i + batch_size, len(chunks))
    collection.add(
        documents=chunks[i:end_idx],
        ids=ids[i:end_idx],
        metadatas=metadatas[i:end_idx]
    )
```

### Streaming Optimization
```python
# Efficient response streaming
words = response.split()
update_frequency = max(1, len(words) // 20)
for i in range(0, len(words), update_frequency):
    # Update UI in batches
```

## Integration Examples

### Custom Document Processor
```python
def custom_process_document(file_path: str) -> int:
    """Process document from file path"""
    with open(file_path, 'rb') as f:
        # Create mock uploaded file object
        uploaded_file = MockUploadedFile(f, file_path)
        return process_document(uploaded_file)
```

### Batch Question Processing
```python
def batch_query(questions: List[str]) -> List[str]:
    """Process multiple questions efficiently"""
    responses = []
    for question in questions:
        chunks, metadata = retrieve_relevant_chunks(question)
        context = "\n\n".join(chunks)
        response = generate_response(question, context)
        responses.append(response)
    return responses
```

### Custom Chunking Strategy
```python
def custom_chunk_text(text: str, strategy: str = "sentence") -> List[str]:
    """Custom chunking with different strategies"""
    if strategy == "sentence":
        return text.split('. ')
    elif strategy == "paragraph":
        return text.split('\n\n')
    else:
        return chunk_text(text)  # Default strategy
```

## API Limitations

### Rate Limits
- No explicit rate limiting implemented
- Performance depends on system resources
- Caching reduces redundant processing

### File Size Limits
- Streamlit default upload limit: 200MB
- Recommended: Keep individual files under 50MB for optimal performance
- Large files may cause memory issues

### Model Constraints
- Depends on Ollama model capabilities
- Context window limited by model (2048 tokens default)
- Response length limited to 512 tokens for performance

## Future API Enhancements

### Planned Features
1. **Multi-model Support**: Integration with additional LLM providers
2. **Advanced Chunking**: Semantic chunking based on content structure
3. **Real-time Collaboration**: Multi-user document sharing
4. **API Endpoints**: REST API for programmatic access
5. **Plugin System**: Custom processing plugins

### Extensibility Points
```python
# Custom embedding functions
def custom_embedding_function():
    # Implement custom embeddings
    pass

# Custom response generators
def custom_response_generator(query, context):
    # Implement custom generation logic
    pass
```

This API documentation provides a comprehensive guide for developers who want to understand, modify, or extend the Document Q&A Assistant functionality.
