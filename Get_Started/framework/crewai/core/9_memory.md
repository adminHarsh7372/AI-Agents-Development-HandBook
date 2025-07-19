# CrewAI Memory System — Guide with Examples 🧠

In CrewAI, memory enables agents to retain relevant information across multiple tasks, executions, or even sessions. It mimics how humans use short-term and long-term memory to make better decisions and stay contextually aware.

---

## Why Memory Matters

Without memory, agents would treat every task as isolated—lacking the ability to:

* Recall previous user inputs
* Learn from past results
* Maintain coherent conversations
* Build long-term context across tasks

CrewAI supports various memory strategies depending on your use case.

---

## 1. **Short-Term Memory (STM)**

This type of memory only persists during a single run or execution cycle. Once the process completes, the memory resets.

**Use Cases**

* Multi-step reasoning in a flow
* Context passing between subtasks

**Example**:

```python
agent.run(task="Summarize this article")
# Memory stores only during the runtime of this execution.
```

---

## 2. **Long-Term Memory (LTM)**

Used for knowledge persistence between runs. This is ideal when your agent needs to recall past work, decisions, or conversations.

CrewAI lets you integrate with vector databases like:

* **ChromaDB**
* **Weaviate**
* **Pinecone**

**Example:**

```python
from crewai.memory import VectorStoreMemory

memory = VectorStoreMemory(
    index_name="project-insights",
    embedding_model="openai",
    vectorstore="chroma"
)

agent = Agent(
    role="Product Analyst",
    goal="Track product trends over time",
    memory=memory,
    backstory="You analyze product data daily and help make strategic decisions."
)
```

---

## 3. **Memory per Agent**

Each agent can be given its own memory configuration. This allows specialization:

* One agent may recall all prior queries
* Another may operate statelessly

This flexibility is key for designing crews with diverse capabilities.

---

## 4. **How Memory Interacts with Flows**

If you’re using **Flows**, memory can be accessed via shared state or by calling agent memory directly during task execution.

```python
# Inside a @start or @listen flow method
previous_answer = self.agent.memory.query("last_summary")
```

---

## Tips for Using Memory Wisely

* 🧠 Store only what's needed — don’t overload memory with junk
* 💬 Use memory with conversational agents to maintain context
* 📌 Leverage vector memory when your agent needs to search knowledge
* 🧪 Periodically test how memory affects task performance

---

## Final Note

Memory is one of the most powerful tools in CrewAI — it bridges the gap between isolated tasks and intelligent systems that learn and evolve over time.

In practice, combining short-term reasoning with long-term retention is how you’ll make agents that feel truly helpful and context-aware.

Let’s keep building smartly!

---

