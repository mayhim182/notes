
*LangChain is a framework to build applications powered by LLMs, it helps you combine LLMs + tools + memory + logic in a modular way*

For example : 
### A Basic Math Assistant Agent
You want an agent that:
- Accepts a user query like: _“What is 15 times 4?”_
- Uses an LLM to **decide** it needs a calculator tool
- Invokes the tool
- Returns the final result

**LangChain Implementation**

```bash
from langchain.agents import initialize_agent, Tool
from langchain.llms import OpenAI
from langchain.agents.agent_types import AgentType
import math

# step 1 define tool
def calculator_tool(input: str) -> str:
	return str(eval(input))

tools = [
	Tool(
		name="calculator",
		func=calculator_tool,
		description="Useful for math operations like multiplication or addition"
	)
]

#step 2 use LLM (e.g. gpt4)
llm = OpenAI(temperature=0)

#step 3 Create the agent
agent = initialize_agent(
	tools = tools, 
	llm = llm,
	agent = AgentType.ZERO_SHOT_REACT_DESCRIPTION, 
	verbose = True,
)

#step 4 Run the agent
response = agent.run("What is 15 times 4?")
print(response)
```

# LangGraph
*LangGraph is a framework to build stateful, multi-step, cyclic workflows for LLM applications - like DAGs with memory*

### Planning and Executing a Task Using Two Agents
You want a system that:
- Has a **Planner Agent** to decide next step
- Has an **Executor Agent** to perform it
- Repeats until goal is achieved

```bash
from langgraph.graph import StateGraph, END
from langchain.chat_models import ChatOpenAI
from langgraph.prebuilt import chat_agent_executor

# Define shared state
class GraphState(dict): pass

# Step 1: Define planner node
def planner_node(state: GraphState) -> dict:
    user_input = state['input']
    return {
        "next_action": "calculator" if "times" in user_input else "none",
        "input": user_input
    }

# Step 2: Define executor node
def calculator_executor(state: GraphState) -> dict:
    expression = state['input'].replace("times", "*")
    result = eval(expression)
    return {"output": f"Answer is {result}"}

# Step 3: Build the graph
graph_builder = StateGraph(GraphState)
graph_builder.add_node("planner", planner_node)
graph_builder.add_node("calculator", calculator_executor)

# Edges
graph_builder.set_entry_point("planner")
graph_builder.add_edge("planner", "calculator")
graph_builder.add_edge("calculator", END)

# Compile graph
graph = graph_builder.compile()

# Run
result = graph.invoke({"input": "15 times 4"})
print(result['output'])

```

| Feature      | LangChain                                   | LangGraph                                  |
| ------------ | ------------------------------------------- | ------------------------------------------ |
| You build    | **Single agent logic**                      | **Multi-step graphs** (agents + tools)     |
| Example      | One-shot agent decides and calls calculator | Planner + Executor nodes with control flow |
| Control flow | LLM decides internally                      | You define it via graph                    |
| Reusability  | Great for atomic tools and agents           | Great for complex workflows                |