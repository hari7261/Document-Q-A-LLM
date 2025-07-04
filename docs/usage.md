# Usage Guide

## Getting Started

This guide will help you effectively use the Document Q&A Assistant to get the most out of your document analysis and question-answering capabilities.

## Basic Workflow

### 1. Starting the Application

```bash
# Navigate to project directory
cd document-qa-assistant

# Activate virtual environment (if using one)
source venv/bin/activate  # Linux/macOS
venv\Scripts\activate     # Windows

# Start the application
streamlit run app.py
```

The application will open in your default browser at `http://localhost:8501`.

### 2. Interface Overview

The application consists of:
- **Main Chat Area**: Where conversations happen
- **Sidebar**: Document upload and settings
- **Progress Tracking**: Real-time processing feedback
- **Performance Metrics**: Response time tracking

## Document Management

### Supported File Types
- **PDF**: `.pdf` files (text-based PDFs work best)
- **Word Documents**: `.docx` files
- **Text Files**: `.txt` files with UTF-8 encoding

### Uploading Documents

1. **Access the Upload Area**:
   - Look for "Document Management" in the sidebar
   - Click on "Browse files" or drag and drop

2. **Select Multiple Files**:
   - Hold Ctrl (Windows/Linux) or Cmd (macOS) to select multiple files
   - Maximum recommended: 10 files per batch for optimal performance

3. **Process Documents**:
   - Click "Process Documents" button
   - Watch real-time progress tracking
   - Wait for completion notification

### Progress Tracking Features

During document processing, you'll see:
- **Progress Bar**: Visual progress indicator
- **Status Updates**: Current processing stage
- **Metrics Display**:
  - Chunks Created: Number of searchable segments
  - Time Remaining: Estimated completion time
- **Completion Notification**: Success message with balloons

## Asking Questions

### Best Practices for Questions

#### Effective Question Types:
```
✅ "What are the main benefits mentioned in the policy document?"
✅ "How does the application process work according to the guidelines?"
✅ "What eligibility criteria are specified for this scheme?"
✅ "Can you summarize the key points from the research paper?"
```

#### Less Effective Questions:
```
❌ "Tell me everything" (too broad)
❌ "Is this good?" (requires opinion, not facts)
❌ "What's the weather?" (unrelated to documents)
```

### Question Strategies

#### 1. Specific Queries
- Ask about specific topics, procedures, or requirements
- Reference particular sections or aspects you're interested in

#### 2. Comparative Questions
- "What's the difference between X and Y in these documents?"
- "How do the requirements compare across different schemes?"

#### 3. Summarization Requests
- "Summarize the main points of..."
- "What are the key takeaways from..."

#### 4. Procedural Questions
- "What steps are required to..."
- "How do I apply for..."

## Settings Configuration

### Temperature Control (0.0 - 1.0)
- **0.0**: More focused, deterministic responses
- **0.3-0.5**: Balanced creativity and accuracy (recommended)
- **0.7**: More creative but less predictable
- **1.0**: Highly creative but potentially inconsistent

### Model Selection
- Currently supports **Gemma3**
- Future versions may include additional models

## Understanding Responses

### Response Components

1. **Main Answer**: Direct response to your question
2. **Source Citations**: Documents used to generate the answer
3. **Confidence Indicators**: Based on available information

### Source Attribution
- Every response includes source documents
- Multiple sources indicate comprehensive analysis
- Single source may indicate specialized content

### Interpreting "I don't know" Responses
The system will honestly indicate when:
- Information isn't available in uploaded documents
- Question is outside the scope of provided content
- Confidence level is too low for a reliable answer

## Performance Monitoring

### Metrics Available
- **Average Response Time**: Overall system performance
- **Last Response Time**: Most recent query performance
- **Total Queries**: Usage statistics

### Optimization Tips
1. **Document Size**: Smaller, focused documents process faster
2. **Question Specificity**: Specific questions get faster, better responses
3. **System Resources**: Close unnecessary applications
4. **Network**: Ensure stable internet for model downloads

## Advanced Features

### Caching System
- Responses are cached for 1 minute
- Search results cached for 5 minutes
- Repeated questions get instant responses

### Batch Processing
- Upload multiple documents simultaneously
- Efficient processing with progress tracking
- Optimized storage in vector database

## Common Use Cases

### 1. Government Schemes Analysis
```
Examples:
- "What are the eligibility requirements for this scheme?"
- "How do I apply for benefits mentioned in these documents?"
- "What documents are required for application?"
```

### 2. Research Paper Review
```
Examples:
- "What methodology was used in this study?"
- "What were the main findings and conclusions?"
- "How does this research compare to other studies?"
```

### 3. Policy Document Analysis
```
Examples:
- "What are the new policy changes?"
- "How will this affect current procedures?"
- "What are the implementation timelines?"
```

### 4. Legal Document Review
```
Examples:
- "What are the key terms and conditions?"
- "What are my rights and obligations?"
- "Are there any important deadlines mentioned?"
```

## Troubleshooting

### Common Issues and Solutions

#### Slow Processing
- **Cause**: Large documents or limited system resources
- **Solution**: Break large documents into smaller files, close other applications

#### Incomplete Responses
- **Cause**: Information may not be in uploaded documents
- **Solution**: Upload additional relevant documents, rephrase questions

#### No Source Citations
- **Cause**: No relevant information found in documents
- **Solution**: Check if documents contain the requested information, upload more comprehensive materials

#### Application Freezing
- **Cause**: Memory issues or model problems
- **Solution**: Restart application, check system resources, verify Ollama is running

## Tips for Best Results

### Document Preparation
1. **Use text-based PDFs**: Scanned images won't work without OCR
2. **Organize content**: Well-structured documents yield better results
3. **Remove irrelevant content**: Focus on relevant information

### Question Formulation
1. **Be specific**: Target particular aspects or sections
2. **Use keywords**: Include important terms from your documents
3. **Ask follow-up questions**: Build on previous responses for deeper understanding

### System Optimization
1. **Regular updates**: Keep dependencies updated
2. **Clear cache**: Restart application periodically
3. **Monitor performance**: Use built-in metrics to track efficiency

## Getting Help

For additional support:
- Check the [Installation Guide](installation.md)
- Review [API Documentation](api.md)
- Submit issues on GitHub
- Join community discussions
