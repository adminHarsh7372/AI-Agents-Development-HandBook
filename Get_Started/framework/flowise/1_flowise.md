# 🧩 Flowise Overview

Flowise is a low-code/no-code framework to build AI workflows visually. It allows you to create agents, connect them to tools, models, and external APIs — all through a drag-and-drop interface.

If you're not a fan of wiring up Python code or you're building agents for non-developers, Flowise is your best friend.

---

## 🎯 Why Use Flowise?

- ✅ **No coding needed** – Build complete agent systems using a visual editor
- 🔌 **Tool integration** – Connect to APIs, LLMs, vector DBs, Google services, and more
- ⚙️ **Modular** – Design and debug each node independently
- 🧱 **Composable agents** – Easily create multi-step logic without managing backends

---

## 🧠 Use Cases for Flowise Agents

- AI Assistants 
- Multi-Agent System
- RAG 
- Local LLM Workflows using Ollama
- ChatBot for you web pages 

---

## ⚙️ Agent Architecture in Flowise

While Flowise isn’t a framework like Langchain or CrewAI, it **lets you build workflows that look and behave like agentic systems**:

| Agent Component | Flowise Equivalent |
|-----------------|--------------------|
| Agent           | Flow start node    |
| Tools           | Function/API nodes |
| Task/Action     | Chain logic        |
| Memory          | Vector store / conversation history |
| Model           | OpenAI / Ollama / Gemini node |
| Orchestrator    | Entire Flow        |

---

## 📌 When to Use Flowise (vs. Langchain/CrewAI)

| Scenario                         | Use Flowise? |
|----------------------------------|--------------|
| No coding skills required        | ✅ Yes        |
| Need frontend quickly            | ✅ Yes        |
| Want to build open-source LLM apps visually | ✅ Yes |
| Need extreme customization / advanced agents | ❌ Use Langchain or CrewAI |
| Need multi-agent planning        | ❌ Better with CrewAI |

---

## 🔗 Examples

You can find ready-to-use examples built using Flowise in this repo:
👉 [Flowise Agents Examples](https://github.com/KNIHAL/flowise-agents-examples)

---


> “Flowise makes building agents feel like building with LEGO — intuitive, modular, and actually fun.”

