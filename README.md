# langgraph
# LangGraph Learning

This repository contains my practice notebooks and experiments while learning **LangGraph**.

## What is LangGraph?

LangGraph is a framework for building **stateful AI applications and agent workflows** using a graph-based architecture.

Instead of writing an AI application as one long sequence of operations, LangGraph allows us to represent the workflow as a graph.

The main concepts are:

- **State** — Data shared between different parts of the workflow.
- **Nodes** — Functions or operations that process the state.
- **Edges** — Connections that define how execution moves between nodes.
- **Conditional Edges** — Route execution based on conditions.
- **START / END** — Define where the graph begins and finishes.

A simple LangGraph workflow looks like:

```text
START
  |
  v
Node A
  |
  v
Node B
  |
  v
 END
```

LangGraph becomes especially useful for building more complex AI systems such as:

- AI Agents
- Tool-calling agents
- RAG workflows
- Multi-step LLM applications
- Stateful conversational systems
- Multi-agent systems

---

## Installation

### 1. Create a virtual environment

```bash
python -m venv myvenv
```

### 2. Activate the virtual environment

Windows PowerShell:

```powershell
.\myvenv\Scripts\Activate.ps1
```

### 3. Install LangGraph

```bash
pip install langgraph
```

For LLM-based workflows, additional packages can be installed depending on the provider.

For example:

```bash
pip install langchain
pip install langchain-google-genai
python-dotenv
```

Or install them together:

```bash
pip install langgraph langchain langchain-google-genai python-dotenv
```

---

## Environment Configuration

Create a `.env` file in the project root:

```env
GOOGLE_API_KEY=your_api_key_here
```

Load environment variables in Python:

```python
from dotenv import load_dotenv

load_dotenv()
```

> **Important:** Never push `.env` files or API keys to GitHub.

Add the following to `.gitignore`:

```gitignore
.env
myvenv/
.venv/
venv/
__pycache__/
.ipynb_checkpoints/
```

---

## Basic LangGraph Example

```python
from typing import TypedDict
from langgraph.graph import StateGraph, START, END


class State(TypedDict):
    message: str


def process_message(state: State):
    return {
        "message": state["message"].upper()
    }


graph = StateGraph(State)

graph.add_node("process", process_message)

graph.add_edge(START, "process")
graph.add_edge("process", END)

app = graph.compile()

result = app.invoke({
    "message": "hello langgraph"
})

print(result)
```

Output:

```text
{'message': 'HELLO LANGGRAPH'}
```

---

## Repository Progress

This repository will be updated continuously as I learn more LangGraph concepts.
