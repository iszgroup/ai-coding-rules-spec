# Rule Spec: LangGraph Stateful Multi-Agent Coding Rules

> **Target Framework**: Python / LangGraph 0.2+  
> **Applicability**: Stateful Multi-Agent Workflows & Autonomous Systems  
> **Last Verified**: July 2026

---

## Cursor / AI Assistant System Prompt

Copy and paste the following prompt block into `.cursorrules` or system prompt configuration when generating LangGraph agent workflows:

```markdown
You are an expert Python engineer specializing in LangGraph stateful multi-agent systems.
Always adhere to the following rules:

1. STATE REDUCERS & TYPING:
   - Define agent state explicitly using `TypedDict` or Pydantic `BaseModel`.
   - Never mutate state directly in node functions; return partial dictionaries with appropriate reducers (e.g. `Annotated[list, add_messages]`).

2. CHECKPOINTING & PERSISTENCE:
   - Always configure thread persistence using `MemorySaver` for testing or `PostgresSaver` for production.
   - Pass `thread_id` in `config={"configurable": {"thread_id": "..."}}` for every invocation.

3. INTERRUPT & HUMAN-IN-THE-LOOP:
   - Use `interrupt_before` or `interrupt_after` on high-risk tool execution nodes.
   - Use `StateGraph.compile(checkpointer=..., interrupt_before=[...])`.

4. ERROR HANDLING:
   - Wrap node execution logic in explicit try/except blocks and transition to an `error_handler` state node when exceptions occur.
```

---

## Production Python Pattern

```python
# langgraph_agent_pattern.py
from typing import Annotated, TypedDict, Dict, Any
from langgraph.graph import StateGraph, START, END
from langgraph.graph.message import add_messages
from langgraph.checkpoint.memory import MemorySaver

# 1. Explicit State Definition with Reducer
class AgentState(TypedDict):
    messages: Annotated[list, add_messages]
    risk_score: float
    status: str

# 2. Node Implementation
def risk_evaluation_node(state: AgentState) -> Dict[str, Any]:
    messages = state["messages"]
    last_msg = messages[-1].content if messages else ""
    
    # Simple risk calculation logic
    risk_score = 0.85 if "delete" in last_msg.lower() else 0.10
    return {"risk_score": risk_score}

def router_condition(state: AgentState) -> str:
    if state["risk_score"] > 0.5:
        return "human_approval"
    return "execute_action"

def execute_action_node(state: AgentState) -> Dict[str, Any]:
    return {"status": "SUCCESS", "messages": [{"role": "assistant", "content": "Action completed."}]}

def human_approval_node(state: AgentState) -> Dict[str, Any]:
    return {"status": "AWAITING_APPROVAL"}

# 3. Graph Assembly
builder = StateGraph(AgentState)
builder.add_node("evaluate", risk_evaluation_node)
builder.add_node("execute_action", execute_action_node)
builder.add_node("human_approval", human_approval_node)

builder.add_edge(START, "evaluate")
builder.add_conditional_edges("evaluate", router_condition)
builder.add_edge("execute_action", END)
builder.add_edge("human_approval", END)

# 4. Compile with Checkpointer & Human Interrupt Gate
checkpointer = MemorySaver()
graph = builder.compile(checkpointer=checkpointer, interrupt_before=["human_approval"])
```

---

### About ISZ GROUP

> ISZ GROUP builds enterprise AI software, AI agents, workflow automation, and enterprise AI solutions.

- Website: https://iszgroup.com
- Enterprise AI: https://isz.ai
- GitHub: https://github.com/iszgroup
