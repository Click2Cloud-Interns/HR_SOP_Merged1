# 🏢 PT Bio Farma AI Assistant - Unified Dual-Agent System

<div align="center">

![Python Version](https://img.shields.io/badge/python-3.9%2B-blue)
![FastAPI](https://img.shields.io/badge/FastAPI-0.111.0-green)
![Streamlit](https://img.shields.io/badge/Streamlit-1.36.0-red)
![Azure OpenAI](https://img.shields.io/badge/Azure-OpenAI-purple)
![License](https://img.shields.io/badge/license-MIT-yellow)

**A production-ready RAG system with dual specialized AI agents for SOP compliance and Human Capital management**

[Features](#-features) • [Demo](#-demo) • [Quick Start](#-quick-start) • [Documentation](#-documentation) • [API](#-api-documentation)

</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Architecture](#-architecture)
- [Agents](#-agents)
- [Tech Stack](#-tech-stack)
- [Installation](#-installation)
- [Usage](#-usage)
- [Project Structure](#-project-structure)
- [Development](#-development)


---

## 🎯 Overview

PT Bio Farma AI Assistant is a unified dual-agent system powered by Azure OpenAI that provides intelligent assistance for two critical business functions:

1. **SOP & Work Procedure Assistant** - Helps employees quickly find and understand Standard Operating Procedures
2. **Human Capital Assistant** - Provides instant answers to HR policy questions and employee benefits

Built with LangChain, FastAPI, and Streamlit, this system uses Retrieval-Augmented Generation (RAG) to deliver accurate, source-cited answers from your organization's documents.

---

## ✨ Features

### 🤖 Dual-Agent System
- **Two Specialized Agents** with different personas and expertise areas
- **Separate Vector Stores** for optimal retrieval performance
- **Independent Chat Histories** for each agent
- **Unified Interface** with seamless agent switching

### 🎨 Modern UI
- **Intuitive Streamlit Interface** with gradient designs
- **Real-time Chat Experience** with source citations
- **Example Questions** for quick onboarding
- **Document Upload** for HR documents
- **Responsive Design** for desktop and mobile

### 🔧 Production-Ready API
- **RESTful FastAPI Backend** with automatic documentation
- **Separate Endpoints** for each agent
- **CORS Support** for frontend integration
- **Health Check** and status monitoring
- **Error Handling** and validation

### 📚 Advanced RAG
- **FAISS Vector Store** for fast similarity search
- **Azure OpenAI Embeddings** (text-embedding-ada-002)
- **GPT-4.1 Mini** for intelligent responses
- **Chunk Optimization** (800 tokens, 120 overlap)
- **Top-K Retrieval** (4 most relevant chunks)

### 🔒 Enterprise Security
- **Environment Variables** for credential management
- **.env File Support** with python-dotenv
- **No Hardcoded Secrets** in codebase
- **API Key Validation** on startup

---

## 🏗 Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     Streamlit Frontend                       │
│                    (app_final.py)                            │
└────────────────────────┬────────────────────────────────────┘
                         │ HTTP/REST
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                   FastAPI Backend (api.py)                   │
├─────────────────────────────────────────────────────────────┤
│  ┌──────────────────────┐    ┌──────────────────────┐       │
│  │   SOP Agent          │    │   HC Agent           │       │
│  │   /sop/ask           │    │   /hc/upload         │       │
│  │                      │    │   /hc/ask            │       │
│  └──────────┬───────────┘    └──────────┬───────────┘       │
└─────────────┼──────────────────────────┼─────────────────────┘
              │                          │
              ▼                          ▼
   ┌──────────────────┐      ┌──────────────────┐
   │  SOP FAISS Index │      │  HC FAISS Index  │
   │  (Markdown SOPs) │      │  (PDF/DOCX HRs)  │
   └──────────────────┘      └──────────────────┘
              │                          │
              └──────────┬───────────────┘
                         ▼
              ┌─────────────────────┐
              │   Azure OpenAI      │
              │  - Embeddings       │
              │  - GPT-4.1 Mini     │
              └─────────────────────┘
```

---

## 👥 Agents

### Agent 1: SOP Assistant 📋
**Persona:** Filman Galuh Purnawidjaya (AVP Kepatuhan)

**Specialized In:**
- Standard Operating Procedures (SOPs)
- Work Instructions (WIs)
- Quality Assurance Documents
- Compliance Procedures
- Manufacturing Protocols

**Response Style:**
- Numbered procedural steps
- Direct and concise
- SOP-style formatting
- Real-world pharma tone

**Example Questions:**
- "What is the temperature for aseptic filling?"
- "How do I perform LAL endotoxin testing?"
- "What are the gowning requirements for Grade A?"

### Agent 2: Human Capital Assistant 👥
**Persona:** Ditya Handayani (VP Layanan Human Capital)

**Specialized In:**
- HR Policies & Regulations
- Leave Policies (sick, annual, maternity)
- Employee Benefits
- Notice Periods & Exit Formalities
- Reimbursement Policies
- Working Hours & Attendance

**Response Style:**
- Professional HR tone
- Empathetic and helpful
- Policy citations
- Clear explanations

**Example Questions:**
- "What is the notice period?"
- "How many sick leaves do I get?"
- "What is the reimbursement policy?"

---

## 🛠 Tech Stack

| Component | Technology | Version |
|-----------|-----------|---------|
| **LLM** | Azure OpenAI GPT-4.1 Mini | Latest |
| **Embeddings** | Azure OpenAI text-embedding-ada-002 | Latest |
| **Vector DB** | FAISS (CPU) | 1.8.0 |
| **Framework** | LangChain | 0.2.6 |
| **Backend** | FastAPI | 0.111.0 |
| **Frontend** | Streamlit | 1.36.0 |
| **Language** | Python | 3.9+ |
| **Doc Processing** | PyPDF, python-docx | Latest |

---

## 📥 Installation

### Prerequisites
- Python 3.9 or higher
- Azure OpenAI account with:
  - text-embedding-ada-002 deployment
  - gpt-4.1-mini deployment
- Git (for cloning)

### Step 1: Clone Repository
```bash
git clone https://github.com/yourusername/biofarma-ai-assistant.git
cd biofarma-ai-assistant
```

### Step 2: Create Virtual Environment
```bash
# Windows
python -m venv venv
venv\Scripts\activate

# Mac/Linux
python3 -m venv venv
source venv/bin/activate
```

### Step 3: Install Dependencies
```bash
pip install -r requirements.txt
```

### Step 4: Create .env File
Create a `.env` file in the root directory:

```env
# Azure OpenAI Configuration
AZURE_OPENAI_ENDPOINT=https://your-resource.openai.azure.com/
AZURE_OPENAI_KEY=your-api-key-here
AZURE_OPENAI_API_VERSION=2024-02-01

# Deployment Names
AZURE_EMBEDDING_DEPLOYMENT=text-embedding-ada-002
AZURE_CHAT_DEPLOYMENT=gpt-4.1-mini
```

**Important:** Replace `your-resource` and `your-api-key-here` with your actual Azure OpenAI credentials.

### Step 5: Create Directory Structure
```bash
mkdir -p data/sop_documents
mkdir -p data/hc_documents
mkdir -p data/vectorstore
mkdir -p uploads/hc
```

---


## 🚀 Usage

### Option 1: Run Everything with Scripts

#### 1. Ingest Documents
```bash
# Process SOP documents
python ingest_unified.py sop

# Process HC documents (optional - can upload via UI)
python ingest_unified.py hc
```

#### 2. Start Backend API
```bash
python api.py
```
API will be available at: `http://localhost:8000`

#### 3. Start Frontend (New Terminal)
```bash
streamlit run app_final.py
```
Web UI will open at: `http://localhost:8501`

### Option 2: Use API Directly

#### Ask SOP Question
```bash
curl -X POST "http://localhost:8000/sop/ask" \
  -H "Content-Type: application/json" \
  -d '{"question": "What is the temperature for aseptic filling?"}'
```

#### Upload HC Document
```bash
curl -X POST "http://localhost:8000/hc/upload" \
  -F "file=@employee_manual.pdf"
```

#### Ask HC Question
```bash
curl -X POST "http://localhost:8000/hc/ask" \
  -H "Content-Type: application/json" \
  -d '{"question": "What is the notice period?"}'
```

#### Check System Status
```bash
curl http://localhost:8000/status
```

---

## 📁 Project Structure

```
biofarma-ai-assistant/
├── .env                      # Environment variables (not in repo)
├── README.md                # This file
├── requirements.txt         # Python dependencies
├── config.py                # Configuration settings
├── prompts.py               # System prompts for agents
├── agents.py                # Agent class implementations
├── ingest.py                # Document ingestion script
├── api.py                   # FastAPI backend
├── streamlit.py             # Streamlit frontend
├── data/
│   ├── sop_documents/       # SOP markdown files
│   │   ├── SOP-MFG-2024-018.md
│   │   ├── WI-QC-2024-042.md
│   │   └── QA-PROC-2024-025.md
│   ├── hc_documents/        # HR PDF/DOCX files
│   │   └── employee_manual.pdf
│   └── vectorstore/
│       ├── sop_faiss_index/ # SOP vector store
│       └── hc_faiss_index/  # HC vector store
└── uploads/
    └── hc/                  # Temporary HC uploads
```

---

### Adding New Agents

1. **Create Agent Class** in `agents.py`:
```python
class NewAgent(BaseAgent):
    def __init__(self):
        super().__init__("NEW")
        # Your initialization
```

2. **Add Prompts** in `prompts.py`:
```python
NEW_SYSTEM_PROMPT = """Your prompt here"""
NEW_RESPONSE_TEMPLATE = """Your template here"""
```

3. **Add Endpoints** in `api.py`:
```python
@app.post("/new/ask")
async def ask_new_question(question: Question):
    # Your endpoint logic
```

4. **Update UI** in `app_final.py`:
```python
AGENT_CONFIGS["New Agent"] = {
    "key": "new",
    # Your config
}
```

---



</div>
