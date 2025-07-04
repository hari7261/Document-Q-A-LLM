# Contributing to Document Q&A Assistant

Thank you for your interest in contributing to the Document Q&A Assistant! This guide will help you get started with contributing to the project.

## 🤝 Ways to Contribute

- **Bug Reports**: Report issues and bugs
- **Feature Requests**: Suggest new features and improvements
- **Code Contributions**: Submit pull requests for bug fixes and new features
- **Documentation**: Improve documentation and examples
- **Testing**: Help test the application and report issues
- **Community Support**: Help other users in discussions

## 🚀 Getting Started

### Prerequisites

1. **Fork the repository** on GitHub
2. **Clone your fork** locally:
   ```bash
   git clone https://github.com/hari7261/Document-Q-A-LLM.git
   cd Document-Q-A-LLM
   ```
3. **Set up development environment**:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   pip install -r requirements.txt
   pip install -e .  # Install in development mode
   ```

### Development Setup

```bash
# Install development dependencies
pip install pytest black flake8 isort

# Run tests
pytest

# Format code
black app.py
isort app.py

# Check code style
flake8 app.py
```

## 📝 Contribution Process

### 1. Create an Issue

Before starting work:
- Check existing issues to avoid duplicates
- Create a new issue describing the bug or feature
- Wait for maintainer feedback before starting major changes

### 2. Create a Branch

```bash
git checkout -b feature/your-feature-name
# or
git checkout -b bugfix/your-bug-fix
```

### 3. Make Changes

- Follow the coding standards (see below)
- Add tests for new functionality
- Update documentation if needed
- Commit your changes with clear messages

### 4. Submit a Pull Request

```bash
git push origin your-branch-name
```

Then create a pull request on GitHub with:
- Clear title and description
- Reference to related issues
- Screenshots if applicable
- Description of testing performed

## 🎯 Coding Standards

### Python Code Style

We follow PEP 8 with some modifications:

```python
# Use black formatter
black app.py

# Import organization with isort
isort app.py

# Line length: 88 characters (black default)
# Use double quotes for strings
# Use type hints where possible
```

### Code Structure

```python
# Function documentation
def process_document(uploaded_file, progress_bar=None):
    """
    Process an uploaded document and store in ChromaDB.
    
    Args:
        uploaded_file: Streamlit uploaded file object
        progress_bar: Optional progress bar widget
        
    Returns:
        int: Number of chunks created
    """
    # Implementation here
```

### Streamlit Best Practices

```python
# Use session state for persistence
if "key" not in st.session_state:
    st.session_state.key = default_value

# Cache expensive operations
@st.cache_data(ttl=300)
def expensive_function():
    pass

# Use containers for layout
with st.container():
    col1, col2 = st.columns(2)
```

## 🧪 Testing Guidelines

### Running Tests

```bash
# Run all tests
pytest

# Run with coverage
pytest --cov=app

# Run specific test
pytest tests/test_chunking.py
```

### Writing Tests

```python
import pytest
from app import chunk_text

def test_chunk_text_basic():
    """Test basic text chunking functionality."""
    text = "This is a test. This is another sentence."
    chunks = chunk_text(text, chunk_size=20)
    assert len(chunks) > 0
    assert all(len(chunk) <= 25 for chunk in chunks)  # Allow some buffer

def test_chunk_text_empty():
    """Test chunking empty text."""
    chunks = chunk_text("")
    assert chunks == []
```

## 📚 Documentation Standards

### README Updates

- Keep the main README concise and focused
- Update installation instructions if dependencies change
- Add new features to the features list

### Code Comments

```python
# Use docstrings for functions and classes
def retrieve_relevant_chunks(query: str, k: int = 5):
    """
    Retrieve relevant document chunks using semantic search.
    
    This function uses ChromaDB to find the most relevant chunks
    based on the input query using sentence transformer embeddings.
    
    Args:
        query: The search query string
        k: Number of chunks to retrieve (default: 5)
        
    Returns:
        Tuple containing (chunks, metadata) lists
        
    Raises:
        ChromaDBError: If database query fails
    """
```

### API Documentation

- Update `docs/api.md` for new functions
- Include examples and parameters
- Document return types and exceptions

## 🐛 Bug Report Guidelines

### Good Bug Reports Include:

1. **Clear Title**: Descriptive summary of the issue
2. **Environment**: OS, Python version, dependency versions
3. **Steps to Reproduce**: Exact steps to recreate the bug
4. **Expected Behavior**: What should happen
5. **Actual Behavior**: What actually happens
6. **Screenshots**: If applicable
7. **Logs**: Error messages or console output

### Bug Report Template

```markdown
## Bug Description
Brief description of the bug

## Environment
- OS: [Windows 10/macOS/Linux]
- Python Version: [3.9.0]
- App Version: [1.0.0]
- Browser: [Chrome 96.0]

## Steps to Reproduce
1. Go to '...'
2. Click on '...'
3. See error

## Expected Behavior
A clear description of what you expected to happen.

## Actual Behavior
A clear description of what actually happened.

## Additional Context
Add any other context about the problem here.
```

## ✨ Feature Request Guidelines

### Good Feature Requests Include:

1. **Problem Statement**: What problem does this solve?
2. **Proposed Solution**: How should it work?
3. **Alternatives**: Other solutions considered
4. **Use Cases**: When would this be useful?
5. **Implementation Ideas**: Technical suggestions (optional)

## 🔧 Development Tips

### Local Development

```bash
# Run with auto-reload
streamlit run app.py --server.runOnSave true

# Run on different port
streamlit run app.py --server.port 8502

# Debug mode
export STREAMLIT_DEBUG=true
streamlit run app.py
```

### Debugging

```python
# Use Streamlit debugging
st.write("Debug info:", variable)
st.json(data_structure)

# Python debugging
import pdb; pdb.set_trace()

# Logging
import logging
logging.basicConfig(level=logging.DEBUG)
```

### Performance Testing

```python
import time
import streamlit as st

# Time operations
start_time = time.time()
result = expensive_operation()
execution_time = time.time() - start_time
st.metric("Execution Time", f"{execution_time:.2f}s")
```

## 📋 Pull Request Checklist

Before submitting a PR, ensure:

- [ ] Code follows project style guidelines
- [ ] Tests pass locally
- [ ] New functionality includes tests
- [ ] Documentation is updated
- [ ] Commit messages are clear and descriptive
- [ ] PR description explains the changes
- [ ] Screenshots included for UI changes
- [ ] No sensitive information in code
- [ ] Dependencies are justified and documented

## 🏷️ Release Process

### Version Numbering

We follow Semantic Versioning (SemVer):
- **MAJOR**: Incompatible API changes
- **MINOR**: Backward-compatible functionality additions
- **PATCH**: Backward-compatible bug fixes

### Release Checklist

1. Update version in `setup.py`
2. Update `CHANGELOG.md`
3. Create release notes
4. Tag the release
5. Update documentation

## 🆘 Getting Help

### Community Resources

- **GitHub Discussions**: For questions and community support
- **GitHub Issues**: For bug reports and feature requests
- **Documentation**: Check `docs/` folder for detailed guides

### Contact Maintainers

- Create an issue for technical questions
- Use discussions for general questions
- Email for security-related issues

## 📜 Code of Conduct

### Our Standards

- **Be Respectful**: Treat everyone with respect and kindness
- **Be Inclusive**: Welcome developers of all backgrounds and experience levels
- **Be Constructive**: Provide helpful feedback and suggestions
- **Be Patient**: Help others learn and grow

### Unacceptable Behavior

- Harassment or discrimination of any kind
- Offensive or inappropriate comments
- Spam or promotional content
- Sharing private information without permission

## 🙏 Recognition

Contributors will be recognized in:
- `CONTRIBUTORS.md` file
- Release notes for significant contributions
- GitHub contributors page

Thank you for contributing to making this project better! 🎉
