# Integrating Neural Networks for Genomic Data Analysis and Natural Language Querying of Antibiotic Resistance

This project integrates **neural networks**, **retrieval-augmented generation (RAG)**, and **high-throughput genomic pipelines** to enable natural language querying of antimicrobial resistance (AMR) datasets.  

It combines:  
- A **batch-processing genomic pipeline** (Bash, Python) for ingesting, cleaning, and assembling sequencing data from NCBI’s SRA.  
- **Neural embeddings (Nomic)** stored in **ChromaDB** for efficient similarity search.  
- A **retrieval-augmented chatbot** using **Llama 3.2 (1B)** via Ollama for natural language interaction with genomic resistance data.  

The system enables researchers to query resistance genes, plasmids, virulence factors, and mobile genetic elements (MGEs) using **free-text questions**, with results retrieved from multiple annotated datasets and contextualized by a language model.  

---

## Features

- 🧬 **Genome Assembly & Analysis**: Batch workflow for 631 resistance-related genome assemblies.  
- 📂 **Vector Database**: Store embeddings from resistance-related datasets (ResFinder, VFDB, PlasmidFinder, MGE).  
- 🔍 **Natural Language Querying**: Retrieve relevant resistance gene context using Nomic embeddings.  
- 🤖 **LLM Assistant**: Query contextualized by Llama 3.2 for concise, domain-specific answers.  
- ⚡ **Cluster-Optimized Workflow**: Scalable and reproducible pipeline for large genomic datasets.  

---

## Dependencies

Make sure the following dependencies are installed:

### Core
- **Python 3.9+**  
- **Bash** (for genomic pipeline scripting)  

### Python Libraries
- `chromadb`  
- `pandas`  
- `requests`  
- `gradio`  

Install via pip:  
```bash
pip install chromadb pandas requests gradio
pip install chromadb pandas requests gradio 
```

### External Requirements Ollama (for Llama 3.2 and Nomic embeddings) → https://ollama.ai 
- NCBI SRA Toolkit (for downloading raw sequencing data)
- Flye (or another assembler, depending on genomic pipeline setup)

### Setup Instructions 
- Install Ollama and pull required models:
  ```bash
  ollama pull nomic-embed-text:latest ollama pull llama3.2:1b
  ```
- Prepare ChromaDB storage: mkdir -p ~/chroma_storage_nomic
- Run embedding ingestion (example for ResFinder dataset): resfinder_col = recreate_collection("resistancefinder") load_csv_to_chroma("/path/to/resfinder_combined.csv", resfinder_col)
- Launch the chatbot: python chatbot.py This will open a Gradio web interface for querying resistance data.
- Usage Example Query the chatbot for antimicrobial resistance genes: User: Which resistance genes are common in E. coli from Europe? Assistant: Based on retrieved context, blaCTX-M and tetA genes are frequently reported in European E. coli isolates...
### Project Structure

      ├── embeddings.py       # Code for generating embeddings and loading into ChromaDB
      ├── chatbot.py          # Chatbot interface (Gradio + Llama + RAG)
      ├── data/               # Resistance datasets (CSV files)
      ├── scripts/            # Bash scripts for genomic assembly and preprocessing
      └── README.md           # Documentation


### Future Work
- Integration with additional AMR databases.
- Improved fine-tuning of Llama for bioinformatics-specific tasks.
- Expanded support for multimodal inputs (e.g., raw sequence fragments). 
