# 🧰 Frameworks for AI Agent Development

Welcome to the framework zone!  
Here you'll explore the core **platforms and libraries** used to build and run AI agents — visually, programmatically, or with fine-tuned control.

Each of these frameworks has its own style and use case. This section will help you choose the right one based on your goals and tech stack.

---

## 🚀 Frameworks Covered

### 🔷 Flowise
> Visual low-code builder for LLM agents  
Perfect for beginners or fast prototyping. Drag-drop interface powered by LangChain under the hood.

- Visual canvas
- Modular nodes (tools, LLMs, memory)
- Great for demos, agents, and tutorials

👉 [flowise/](./flowise/)

---

### 🟣 Langflow
> Python-based visual LangChain alternative  
Open-source, React/Node frontend with powerful LLM integrations and agent design.

- Clean visual interface
- Highly customizable
- Works great with LangChain agents

👉 [langflow/](./langflow/)

---

### 🧠 CrewAI
> Multi-agent framework where agents collaborate like a team  
Ideal for goal-oriented task execution where multiple agents (roles) coordinate together.

- Define roles (Researcher, Coder, Reviewer, etc.)
- Agents can talk to each other
- Chain of thought & planning logic

👉 [crewai/](./crewai/)

---

### 🐍 LangChain
> The most mature Python library for building LLM apps  
Everything Flowise/Langflow uses is basically built on LangChain.

- Programmatic control
- AgentExecutor, Chains, Tools, Memory
- Advanced workflows & integrations

👉 [langchain/](./langchain/)

---

### 🤗 Hugging Face
> Community platform for models, datasets & inference  
Not a framework by itself, but a **key infrastructure** for loading, deploying, or fine-tuning open models.

- Access to open-source LLMs (Mistral, LLaMA, Phi, etc.)
- Use via Transformers or Inference APIs
- Good for hosting custom endpoints

👉 [huggingface/](./huggingface/)

---

## ⚖️ When to Use What?

| Goal                              | Best Framework         |
|-----------------------------------|------------------------|
| Just build agents fast            | **Flowise**            |
| Want visuals + more flexibility   | **Langflow**           |
| Need agents to collaborate        | **CrewAI**             |
| Going full-code & custom logic    | **LangChain**          |
| Hosting or fine-tuning models     | **Hugging Face**       |

---

## ✅ Summary

Each framework has its strength — some are plug-and-play, some are for devs, and some are for teams of agents.  
Pick based on your comfort level and the type of app you're building.

> “Frameworks are the toolbox. Your agent is what you build with them.”

