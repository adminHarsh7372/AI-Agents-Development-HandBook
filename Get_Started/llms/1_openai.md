# 🧠 Using OpenAI (GPT) in AI Agents

OpenAI’s GPT models (like GPT-4, GPT-4o) are some of the most powerful and widely used LLMs for building AI agents. They support reasoning, planning, text generation, tool calling, and more — all through a simple API.

---

## ⚡ Why Use OpenAI Models?

- 🔍 High-quality responses
- 🧠 Great reasoning + instruction following
- ⚒️ Native tool calling (function calling)
- 🧩 Easy integration with LangChain, CrewAI, Composio

If you're building AI agents with deep logic or task chaining — OpenAI models are a great choice.

---

## 🧰 Popular OpenAI Models (As of 2025)

| Model     | Description                            | Use Case Examples            |
|-----------|----------------------------------------|------------------------------|
| `gpt-3.5-turbo` | Fast & cheap for simple tasks        | Smart replies, parsing       |
| `gpt-4`         | More accurate, handles complexity    | Planning agents, summaries   |
| `gpt-4o`        | Multimodal (text, image, audio input)| Vision tasks, smarter agents |

> 💡 Use GPT-3.5 for testing, GPT-4 for production, GPT-4o for advanced multi-modal workflows.

---

## 🔑 How to Set Up OpenAI for Agents

1. **Create an account at** [https://platform.openai.com](https://platform.openai.com)
2. Go to your [API keys](https://platform.openai.com/account/api-keys)
3. Copy your secret key and save it in a `.env` file:

>**OPENAI_API_KEY=sk-xxxxxxxxxxxxxxxxxxxx**

---

## ⚙️ Basic Python Setup (Without Langchain)

```python
import openai

openai.api_key = "your-api-key"

response = openai.ChatCompletion.create(
 model="gpt-4",
 messages=[
     {"role": "system", "content": "You are a helpful assistant."},
     {"role": "user", "content": "Summarize this email..."}
 ]
)

print(response['choices'][0]['message']['content'])
```
---

### 🔄 How Agents Use OpenAI in LangChain / CrewAI
**In LangChain:**
```python
from langchain.chat_models import ChatOpenAI

llm = ChatOpenAI(model="gpt-4", temperature=0.2)
response = llm.invoke("What's a good email reply to this message?")
```

**In CrewAI:**
You just pass the LLM when creating your agent or crew:

```python

llm = ChatOpenAI(model="gpt-4")
agent = Agent(role="email_handler", goal="Reply to important emails", llm=llm)
```

### 📉 Rate Limits & Pricing
## 📉 Rate Limits & Pricing

| Model     | Rate Limit (est.) | Cost (approx)           |
|-----------|-------------------|--------------------------|
| GPT-3.5   | High              | ~$0.0015 per 1K tokens   |
| GPT-4     | Moderate          | ~$0.03 per 1K tokens     |
| GPT-4o    | Moderate-High     | ~$0.005–0.01 per 1K tokens |

> *Always use gpt-3.5 in dev mode and upgrade when needed.*

### ✅ Best Practices:
- Use temperature=0 for predictable responses.
- Keep prompts short and focused.
- Cache responses during testing.
- Use function calling for tools and structured output.

### 📌 Summary
OpenAI models are the gold standard for AI agents — flexible, powerful, and easy to plug into any workflow.

**If you're just getting started, go with gpt-3.5. When you need smart decisions and better planning — upgrade to gpt-4 or gpt-4o.**
