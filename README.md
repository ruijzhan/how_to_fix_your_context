# How to Fix Your Context

This repository contains practical implementations of the 6 key context management techniques outlined in Drew Breunig's post ["How to Fix Your Context"](https://www.dbreunig.com/2025/06/26/how-to-fix-your-context.html).

## 🚀 Quickstart 

### Prerequisites
- Python 3.9 or higher
- [uv](https://docs.astral.sh/uv/) package manager

### Installation
1. Clone the repository and activate a virtual environment:
```bash
git clone https://github.com/langchain-ai/how_to_fix_your_context
cd how_to_fix_your_context
uv venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
```

2. Install dependencies:
```bash
uv pip install -r requirements.txt
```

3. Set up environment variables for the model provider(s) you want to use:
```bash
export OPENAI_API_KEY="your-openai-api-key"
export ANTHROPIC_API_KEY="your-anthropic-api-key"
```

## Background

### The Context Problem

Chroma's report on [Context Rot](https://research.trychroma.com/context-rot) notes that LLMs do not treat every token in their context window equally. Across 18 models (including GPT‑4.1, Claude 4, Gemini 2.5, Qwen3, etc.), they show that performance on even very simple tasks degrades—often in non‑uniform and surprising ways—as the input length grows.

Drew Breunig has outlined four primary failure modes on [why long contexts fail](https://www.dbreunig.com/2025/06/22/how-contexts-fail-and-how-to-fix-them.html):

1. **Context Poisoning** - Hallucinations or errors that enter the context and get repeatedly referenced
2. **Context Distraction** - When context grows so large that models focus more on accumulated history than training
3. **Context Confusion** - Superfluous content that influences response quality, as models feel compelled to use all available context
4. **Context Clash** - Conflicting information within the accumulated context that degrades reasoning

### Why Context Management Matters

A key insight from Drew's post is that: **"Context is not free. Every token in the context influences the model's behavior."** Larger context windows don't automatically improve performance. As contexts grow, they introduce complex failure modes that can significantly degrade AI system effectiveness, especially for agents performing multi-step reasoning.

## The 6 Context Management Techniques

Drew has a follow up post that outlines [6 context management techniques](https://www.dbreunig.com/2025/06/26/how-to-fix-your-context.html).This repository demonstrates each technique through practical Jupyter notebooks:

### 1. RAG (Retrieval-Augmented Generation)
**Notebook**: [notebooks/01-rag.ipynb](notebooks/01-rag.ipynb)

Selectively adding relevant information to improve LLM responses while preventing information overload. RAG prevents context overload by carefully selecting relevant information from vector databases.

**Key implementation features:**
- Vector-based document retrieval using LangChain
- Agent-based RAG with LangGraph workflows
- Tool-based retrieval for dynamic context selection

### 2. Tool Loadout
**Notebook**: [notebooks/02-tool-loadout.ipynb](notebooks/02-tool-loadout.ipynb)

Selecting only the most relevant tool definitions when managing multiple tools. Drew's research shows **Llama 3.1 8b fails with 46 tools** but performs well with 19 tools.

**Key implementation features:**
- Semantic similarity search over tool descriptions
- LangGraph Bigtool for dynamic tool selection
- **44% performance improvement** with selective tool loading

### 3. Context Quarantine
**Notebook**: [notebooks/03-context-quarantine.ipynb](notebooks/03-context-quarantine.ipynb)

Isolating contexts in dedicated threads to allow parallel processing of subtasks. Anthropic's multi-agent system achieved **90.2% better performance** using this approach.

**Key implementation features:**
- Multi-agent supervisor architecture with LangGraph
- Parallel context processing with isolated agents
- Reduced path dependency through context isolation

### 4. Context Pruning
**Notebook**: [notebooks/04-context-pruning.ipynb](notebooks/04-context-pruning.ipynb)

Removing irrelevant information to dramatically reduce context size. The **Provence tool can reduce document size by 95%** while maintaining quality.

**Key implementation features:**
- LangChain's `trim_messages` function for message management
- Token-aware pruning with fallback mechanisms
- Heuristic compression for long-running conversations

### 5. Context Summarization
**Notebook**: [notebooks/05-context-summarization.ipynb](notebooks/05-context-summarization.ipynb)

Condensing accumulated context into shorter versions to prevent context distraction. **Gemini research found performance issues with contexts over 100,000 tokens**.

**Key implementation features:**
- Automatic summarization at conversation boundaries
- Tool output summarization to reduce token usage
- Running summary maintenance with LangGraph state

### 6. Context Offloading
**Notebook**: [notebooks/06-context-offloading.ipynb](notebooks/06-context-offloading.ipynb)

Storing information outside the primary context as a "scratchpad" for complex reasoning. Anthropic's research shows **performance improvements up to 54%**.

**Key implementation features:**
- State-based scratchpads with LangGraph
- Long-term memory across conversation threads
- Context selection strategies for optimal performance

## Getting Started

Each notebook contains:
- Theoretical background of the technique
- Practical implementation examples
- Code samples you can run and modify
- Real-world use cases and benchmarks

Start with any technique that matches your current context challenges, or work through them sequentially to build a comprehensive understanding of context management.

## References

- [How to Fix Your Context](https://www.dbreunig.com/2025/06/26/how-to-fix-your-context.html) by Drew Breunig
- [How Contexts Fail and How to Fix Them](https://www.dbreunig.com/2025/06/22/how-contexts-fail-and-how-to-fix-them.html) by Drew Breunig