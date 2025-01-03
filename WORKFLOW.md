# GraphRAG System Workflow Guide

## System Overview
The GraphRAG system combines vector embeddings with a knowledge graph for enhanced document querying. It processes documents, creates embeddings, builds a knowledge graph, and provides two query methods: local and global.

## Prerequisites
1. Python 3.10 or higher
2. Ollama installed
3. Required Python packages (from requirements.txt)

## Directory Structure 

graphrag/
├── graphrag.py
├── indexer.py
├── querier.py
├── __init__.py
├── settings.yaml
├── input/
├── output/

## Setup Instructions

### 1. Initial Setup

# Create and activate virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate

# Install required packages
pip install -r requirements.txt


### 2. Install and Start Ollama

# Linux/Mac
curl https://ollama.ai/install.sh | sh
ollama serve

# Windows
# Download and install from https://ollama.ai/download


### 3. Pull Required Models

ollama pull mistral        # For text generation
ollama pull nomic-embed-text  # For embeddings


## Usage Workflow

### 1. Prepare Documents
- Place your documents in the `input/` directory
- Supported formats: .txt, .pdf

### 2. Create Database


python create_db.py

This will:
- Process all documents in input/
- Create embeddings
- Build knowledge graph
- Save everything to output/

### 3. Query Documents

python query.py

Two query methods available:
- `local`: Uses direct document similarity
- `global`: Uses graph relationships for broader context

### 4. Clean Database

To delete the existing database and start fresh:

python clean.py

## Configuration

### settings.yaml


llm:
type: ollama
model: mistral
temperature: 0.1
max_tokens: 1000
embeddings:
type: ollama
model: nomic-embed-text
index:
chunk_size: 500
chunk_overlap: 50


## Troubleshooting

### Common Issues

1. **Ollama Server Not Running**
   - Error: "Could not connect to Ollama server"
   - Solution: Run `ollama serve`

2. **No Documents Found**
   - Error: "No documents found in input"
   - Solution: Add documents to input/ directory

3. **Database Not Found**
   - Error: "Database not found"
   - Solution: Run create_db.py first

4. **Memory Issues**
   - Error: Out of memory
   - Solution: Reduce chunk_size in settings.yaml

### Best Practices

1. **Document Preparation**
   - Use clear, well-formatted documents
   - Break large documents into smaller files
   - Ensure documents are readable text (not scanned images)

2. **Database Management**
   - Run clean.py before recreating database
   - Keep input documents organized
   - Back up output/ directory if needed

3. **Querying**
   - Start with specific questions
   - Try both local and global methods
   - Use clear, well-formed questions

## Performance Tips

1. **Optimize Document Processing**
   - Keep documents under 100MB total
   - Use appropriate chunk sizes
   - Remove unnecessary formatting

2. **Query Optimization**
   - Use local method for specific questions
   - Use global method for broader context
   - Be specific in your questions

3. **System Resources**
   - Close unnecessary applications
   - Monitor memory usage
   - Consider GPU acceleration if available

## Maintenance

1. **Regular Updates**



# Update dependencies
pip install -r requirements.txt


# Update Ollama models
ollama pull mistral
ollama pull nomic-embed-text

2. **Database Maintenance**
- Regularly clean and rebuild database
- Monitor output directory size
- Back up important queries and results

## Support

If you encounter issues:
1. Check the troubleshooting section
2. Verify Ollama server status
3. Check system requirements
4. Review error messages carefully

## Security Notes

1. Only process trusted documents
2. Be cautious with allow_dangerous_deserialization
3. Keep Ollama and dependencies updated
4. Monitor system resource usage
