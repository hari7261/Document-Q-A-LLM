# Installation Guide

## Prerequisites

Before installing the Document Q&A Assistant, ensure you have the following prerequisites:

### System Requirements
- **Operating System**: Windows 10/11, macOS 10.14+, or Linux
- **Python**: Version 3.8 or higher
- **RAM**: Minimum 4GB (8GB recommended for better performance)
- **Storage**: At least 2GB free space for models and dependencies

### Required Software

#### 1. Python Installation
If you don't have Python installed:

**Windows:**
```bash
# Download from https://python.org
# Or use Windows Store
winget install Python.Python.3.11
```

**macOS:**
```bash
# Using Homebrew
brew install python@3.11
```

**Linux (Ubuntu/Debian):**
```bash
sudo apt update
sudo apt install python3.11 python3.11-pip python3.11-venv
```

#### 2. Ollama Installation

**Windows:**
1. Download the installer from [https://ollama.ai](https://ollama.ai)
2. Run the installer and follow the setup wizard
3. Restart your computer after installation

**macOS:**
```bash
# Using Homebrew
brew install ollama

# Or download from https://ollama.ai
```

**Linux:**
```bash
curl -fsSL https://ollama.ai/install.sh | sh
```

#### 3. Download Gemma3 Model
After installing Ollama:
```bash
ollama pull gemma3
```

## Application Installation

### Method 1: Clone from GitHub (Recommended)

```bash
# Clone the repository
git clone https://github.com/hari7261/Document-Q-A-LLM.git

# Navigate to project directory
cd Document-Q-A-LLM

# Create virtual environment
python -m venv venv

# Activate virtual environment
# Windows:
venv\Scripts\activate
# macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### Method 2: Download ZIP
1. Download the ZIP file from GitHub
2. Extract to your desired location
3. Follow the virtual environment steps above

### Method 3: Install as Package
```bash
# Install directly from GitHub
pip install git+https://github.com/hari7261/Document-Q-A-LLM.git

# Or install from local directory
pip install .
```

## Verification

Test your installation:

```bash
# Check Python version
python --version

# Check Ollama installation
ollama --version

# Check if Gemma3 model is available
ollama list

# Test the application
streamlit run app.py
```

## Troubleshooting

### Common Issues

#### Issue: "ollama: command not found"
**Solution:**
```bash
# Add Ollama to PATH (Linux/macOS)
export PATH=$PATH:/usr/local/bin

# Windows: Restart command prompt or add to System PATH
```

#### Issue: "Model 'gemma3' not found"
**Solution:**
```bash
ollama pull gemma3
```

#### Issue: Python package conflicts
**Solution:**
```bash
# Create a fresh virtual environment
python -m venv fresh_env
source fresh_env/bin/activate  # Linux/macOS
# or
fresh_env\Scripts\activate  # Windows

pip install -r requirements.txt
```

#### Issue: Port 8501 already in use
**Solution:**
```bash
# Use a different port
streamlit run app.py --server.port 8502
```

### Performance Optimization

#### For Better Performance:
1. **Increase system RAM**: 8GB+ recommended
2. **Use SSD storage**: Faster disk I/O for database operations
3. **Close unnecessary applications**: Free up system resources
4. **Update dependencies**: Keep packages up-to-date

#### Ollama Optimization:
```bash
# Set Ollama host (if using custom setup)
export OLLAMA_HOST=0.0.0.0:11434

# Increase context window (if needed)
export OLLAMA_NUM_CTX=4096
```

## Next Steps

After successful installation:
1. Read the [Usage Guide](usage.md)
2. Check out the [API Documentation](api.md)
3. Explore example documents in the `examples/` folder
4. Join our community discussions on GitHub

## Getting Help

If you encounter issues:
1. Check this installation guide
2. Review the [troubleshooting section](#troubleshooting)
3. Search existing GitHub issues
4. Create a new issue with detailed error information
