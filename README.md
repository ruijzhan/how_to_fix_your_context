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

Context problems occur when information in an LLM's context window negatively impacts response quality. As Drew Breunig notes in his foundational post on [How Contexts Fail](https://www.dbreunig.com/2025/06/22/how-contexts-fail-and-how-to-fix-them.html), there are four primary failure modes:

1. **Context Poisoning** - Hallucinations or errors that enter the context and get repeatedly referenced
2. **Context Distraction** - When context grows so large that models focus more on accumulated history than training
3. **Context Confusion** - Superfluous content that influences response quality, as models feel compelled to use all available context
4. **Context Clash** - Conflicting information within the accumulated context that degrades reasoning

### Why Context Management Matters

A key insight from Breunig's research: **"Context is not free. Every token in the context influences the model's behavior."** Larger context windows don't automatically improve performance. As contexts grow, they introduce complex failure modes that can significantly degrade AI system effectiveness, especially for agents performing multi-step reasoning.

## The 6 Context Management Techniques

This repository demonstrates each technique through practical Jupyter notebooks:

### 1. RAG (Retrieval-Augmented Generation)
**Notebook**: [01-rag.ipynb](01-rag.ipynb)

Selectively adding relevant information to improve LLM responses while preventing information overload. Critical even with large context windows.

### 2. Tool Loadout
**Notebook**: [02-tool-loadout.ipynb](02-tool-loadout.ipynb)

Selecting only the most relevant tool definitions when managing multiple tools. Can improve performance and reduce power consumption.

### 3. Context Quarantine
**Notebook**: [03-context-quarantine.ipynb](03-context-quarantine.ipynb)

Isolating contexts in dedicated threads to allow parallel processing of subtasks and reduce path dependency.

### 4. Context Pruning
**Notebook**: [04-context-pruning.ipynb](04-context-pruning.ipynb)

Removing irrelevant or unnecessary information to dramatically reduce context size while maintaining response quality.

### 5. Context Summarization
**Notebook**: [05-context-summarization.ipynb](05-context-summarization.ipynb)

Condensing accumulated context into shorter versions to prevent context distraction, particularly useful for long-running conversations.

### 6. Context Offloading
**Notebook**: [06-context-offloading.ipynb](06-context-offloading.ipynb)

Storing information outside the primary context to create a "scratchpad" for notes and intermediate thinking in complex multi-step processes.

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