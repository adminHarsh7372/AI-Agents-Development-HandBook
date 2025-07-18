# 🔗 Chains Node

The `Chains` node in Flowise allows you to build **multi-step logic** by linking prompts, tools, memory, and models together.

It’s built on top of Langchain’s “Chain” abstraction — which is basically a **pipeline of LLM-powered steps**, where the output of one node feeds into the next.

---

## 🤔 What is a Chain?

A chain is a **sequence of connected components** like:
- Prompt Templates
- LLMs
- Tools (like search, file loader, email)
- Output Parsers
- Memory

In Flowise, chains can be customized visually and saved as reusable flows.

---

## 🔗 Common Chain Types

| Chain Type         | Description                                               |
|--------------------|-----------------------------------------------------------|
| **Simple Chain**   | Prompt → LLM → Output                                     |
| **Sequential Chain** | Runs multiple chains one after another                   |
| **Conversational Chain** | Adds memory to handle multi-turn dialogue          |
| **Custom Chain**   | Combine any nodes you like manually in a visual flow      |

---

## 📦 Chain Components

You can build chains using:
- 🧠 LLM Nodes
- 📝 Prompt Templates
- 🧰 Tools (search, PDF, Gmail, etc.)
- 🧠 Memory Nodes
- 🔀 Conditional Logic (via Utility nodes)

---

## ⚙️ Example Chain

> **“Summarize a file and send via Gmail”**

```text
[File Loader]
   ↓
[Prompt Template]
   ↓
[LLM]
   ↓
[Output Parser]
   ↓
[Gmail Tool]
```

#### 🛠️ How to Use Chains in Flowise
- No separate "Chain node" is required — you create a chain visually by connecting multiple nodes.
- Every time you connect prompts → tools → LLM → memory → output, you are building a chain.
- You can export/import entire chains as .json files for reuse.

---

#### 🧠 Tips for Building Good Chains

✅ Keep steps modular: One function = one node

🔄 Avoid making chains too long in one go — break into sub-flows

🧪 Debug step-by-step using Text Output or Console nodes

💾 Save and reuse chains for similar problems

---

#### 💡 Advanced Tip: Use Conditional Logic in Chains
- Flowise allows branching logic using:
- Boolean check nodes
- Switch/Case type logic
- Value transformers
- This enables “if-else” type behavior in a chain.

