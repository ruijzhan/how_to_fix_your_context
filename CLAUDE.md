# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This repository demonstrates six context engineering techniques using LangGraph to address LLM context window limitations. Based on Drew Breunig's blog post "How to Fix Your Context", it implements RAG, Tool Loadout, Context Quarantine, Context Pruning, Context Summarization, and Context Offloading in interactive Jupyter notebooks.

## Environment Setup

### Package Management
- Uses `uv` as the primary package manager
- Python 3.9+ required
- Virtual environment activation: `source .venv/bin/activate`
- Install dependencies: `uv pip install -r requirements.txt`

### Environment Variables
Required for model provider access:
- `OPENAI_API_KEY` - For OpenAI models and embeddings
- `ANTHROPIC_API_KEY` - For Anthropic models

## Architecture

### Core Dependencies
- **LangGraph** (>=0.5.4) - Low-level orchestration framework for building stateful AI workflows
- **LangChain** (>=0.3.0) - Core framework components and tool integration
- **langchain-openai** & **langchain-anthropic** - Model provider integrations
- **langgraph_supervisor** - Multi-agent supervisor architecture
- **langgraph_swarm** - Swarm-based multi-agent patterns
- **pydantic** (>=2.0.0) - Data validation and type checking

### Project Structure
```
├── notebooks/                    # All implementation notebooks
│   ├── 01-rag.ipynb             # Retrieval-Augmented Generation
│   ├── 02-tool-loadout.ipynb    # Semantic tool selection
│   ├── 03-context-quarantine.ipynb # Multi-agent isolation
│   ├── 04-context-pruning.ipynb  # Intelligent content removal
│   ├── 05-context-summarization.ipynb # Context compression
│   ├── 06-context-offloading.ipynb # External storage patterns
│   └── utils.py                 # Shared utility functions
├── requirements.txt              # Python dependencies
└── README.md                    # Comprehensive documentation
```

## Development Workflow

### Running Notebooks
- All examples are implemented as Jupyter notebooks
- Use `jupyter lab` or `jupyter notebook` to start the development environment
- Each notebook is self-contained with complete implementations

### Key Patterns
- **StateGraph**: Primary LangGraph abstraction using nodes, edges, and shared state
- **Tool Binding**: Dynamic tool selection and binding patterns
- **Multi-Agent**: Supervisor and swarm architectures for context isolation
- **Vector Stores**: In-memory vector storage for semantic search and retrieval

### Utility Functions
The `notebooks/utils.py` file provides:
- `format_messages()` - Rich formatting for conversation display
- `format_retriever_results()` - Formatted display of retrieval tool outputs
- Console-based visualizations with color coding for different message types

## Context Engineering Techniques

### 1. RAG (Retrieval-Augmented Generation)
- **File**: `notebooks/01-rag.ipynb`
- **Purpose**: Selectively add relevant information to improve LLM responses
- **Implementation**: Vector store with document chunking, conditional edges for tool calling

### 2. Tool Loadout
- **File**: `notebooks/02-tool-loadout.ipynb`
- **Purpose**: Dynamically select relevant tools to avoid context confusion
- **Implementation**: Vector store indexing of tool descriptions, semantic similarity-based selection

### 3. Context Quarantine
- **File**: `notebooks/03-context-quarantine.ipynb`
- **Purpose**: Isolate contexts in dedicated threads to prevent clash
- **Implementation**: Multi-agent supervisor architecture with specialized agents

### 4. Context Pruning
- **File**: `notebooks/04-context-pruning.ipynb`
- **Purpose**: Remove irrelevant information from context
- **Implementation**: Smaller LLM (GPT-4o-mini) for intelligent content extraction

### 5. Context Summarization
- **File**: `notebooks/05-context-summarization.ipynb`
- **Purpose**: Condense accrued context while preserving essential information
- **Implementation**: Comprehensive summarization with 50-70% reduction target

### 6. Context Offloading
- **File**: `notebooks/06-context-offloading.ipynb`
- **Purpose**: Store information outside LLM context via external tools
- **Implementation**: Session scratchpad and persistent cross-thread memory patterns

## Common Commands

```bash
# Environment setup
uv venv
source .venv/bin/activate
uv pip install -r requirements.txt

# Start Jupyter environment
jupyter lab

# Run specific notebook (from command line)
jupyter nbconvert --to notebook --execute notebooks/01-rag.ipynb --inplace
```

## Testing and Validation

- Each notebook includes test queries and expected outputs
- Performance metrics (token usage, response quality) are tracked throughout
- LangSmith tracing integration for debugging and optimization
- Compare token usage between basic and optimized implementations