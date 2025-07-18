# 🧠 Agents Node

The `Agents` node in Flowise allows you to create **autonomous decision-making AI agents** powered by LLMs and tools. It wraps Langchain’s agent system in a drag-and-drop UI.

Agents are useful when you don’t want to hardcode logic, and instead want your LLM to decide *which tool to use and when*.

---

## 🚦 When to Use Agents

✅ When you want:
- Multi-tool reasoning (e.g., decide whether to search the web, load a PDF, or email)
- Dynamic tool calling based on user query
- Chat-like interfaces with flexible backends

❌ Don’t use agents if:
- You have fixed logic (e.g., summarization → email → done)
- You want maximum speed (agents are slower due to planning)

---

## 🧱 Agent Types in Flowise

| Agent Type               | Description                                                  |
|--------------------------|--------------------------------------------------------------|
| **Conversational Agent** | Most commonly used; supports memory and tools                |
| **OpenAI Function Agent**| Uses OpenAI's function calling mode (structured output)       |
| **Zero-Shot Agent**      | Basic reasoning, selects tools without past conversation      |
| **React Agent**          | Uses reasoning steps ("Thought > Action > Observation") loop  |

> Tip: Most use cases work best with **Conversational Agent**

---

## 🛠️ Required Inputs

| Input           | Description                                  |
|------------------|----------------------------------------------|
| LLM              | The brain of the agent (OpenAI, Ollama, etc.)|
| Tools            | Tools the agent can use (search, file, email)|
| Prompt Template  | Optional. Customize system prompt            |
| Memory           | Optional. Enables context/history            |

---

## ⚙️ Config Options

- **Agent Type**: Choose from available Langchain agent types
- **Verbose Mode**: Show step-by-step decision logs
- **Max Iterations**: How many times agent can plan/act in one query
- **Early Stop**: Whether to quit early if loop exceeds limits

---

## 🔗 Example Use Case

> **“Smart Email Assistant”**
```text
User: "Summarize my PDF and draft a reply to that client"
→ Agent decides:
   - Use file loader
   - Summarize with LLM
   - Use GmailTool to send draft
   - Agent Flow
    [Chat Input] → [Conversational Agent Node]
                     ↓
          [PDFTool, GmailTool, LLM]
```

#### 🧠 Tips & Best Practices
- Combine with Memory for multi-turn reasoning
- Use Output Parser to structure agent’s response
- Add Tool Description carefully — it helps agent choose tools better
- Start with 2–3 tools max to keep behavior predictable
---
