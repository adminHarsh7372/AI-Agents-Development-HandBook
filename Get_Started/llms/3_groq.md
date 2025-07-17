# ⚡ Using Groq in AI Agents

**Groq** isn’t just another LLM — it’s an ultra-fast LLM **execution engine** built to run models like LLaMA and Mixtral at crazy speeds (100+ tokens/sec). It’s perfect when **latency matters** — like in real-time agents, chat apps, or rapid pipelines.

If you want blazing speed with decent quality — Groq is worth exploring.

---

## 🚀 Why Use Groq?

- ⚡ Insanely fast output (up to 500+ tokens/sec)
- 💵 Free to use (as of now)
- 🧠 Runs top open-source models like Mixtral and LLaMA 3
- 🌐 Easy API access, no GPU needed on your end

---

## 🧠 What Models Run on Groq?

| Model Name       | Type        | Strengths                         |
|------------------|-------------|-----------------------------------|
| `Mixtral-8x7B`   | Mixture of Experts | Great speed + accuracy balance     |
| `LLaMA3-8B`      | Meta's model | Lightweight, solid reasoning       |
| `Gemma-7B`       | Google       | Clean code output, multilingual    |

> Groq doesn’t build its own LLM — it **executes existing open-source models faster.**

---

## 🛠️ Getting Started with Groq

1. Go to [https://console.groq.com/](https://console.groq.com/)
2. Sign in with GitHub or Google
3. Create an API key
4. Add it to your `.env` file: 
**GROQ_API_KEY=your-key-here**
---

## ⚙️ Example (Python + Requests)

```python
import requests

response = requests.post(
 "https://api.groq.com/openai/v1/chat/completions",
 headers={
     "Authorization": "Bearer YOUR_GROQ_API_KEY",
     "Content-Type": "application/json"
 },
 json={
     "model": "mixtral-8x7b-32768",
     "messages": [
         {"role": "user", "content": "Summarize this email..."}
     ]
 }
)

print(response.json()["choices"][0]["message"]["content"])
```

### 🧩 Groq in LangChain
```python 
from langchain.chat_models import ChatGroq

llm = ChatGroq(
    model_name="mixtral-8x7b-32768",
    temperature=0.2
)

response = llm.invoke("Write a one-line smart reply.")
print(response)
```
### 📌 When to Use Groq in Agents
✅ Use Groq when:

- You want ultra-fast response agents
- You're okay with slightly less reasoning power than GPT-4
- You’re building real-time bots, chat tools, or embedded agents

### ❌ Avoid if:

- You need tool-calling, code execution, or fine-tuned reliability
- You want tight integration with Gmail, Drive, or paid LLM tools

### ✅ Summary
Groq brings speed to the LLM game — ideal for fast, lightweight AI agents. Pair it with open-source models for instant, responsive assistants that won’t burn your budget.

**For fast chatbots, inbox agents, or front-end helpers — Groq is 🔥.**

