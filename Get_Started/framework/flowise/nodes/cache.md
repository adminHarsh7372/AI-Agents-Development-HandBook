# 🗂️ Cache Node

The `Cache` node in Flowise helps you **store and reuse previous LLM outputs** to reduce cost, improve speed, and avoid repeated computation.

Flowise uses Langchain's caching system under the hood — especially useful when dealing with repeated inputs or heavy prompts.

---

## ⚡ Why Use Cache?

| Benefit            | What It Means                                                  |
|--------------------|----------------------------------------------------------------|
| 🧠 Smarter Performance | Avoid re-querying the LLM for the same input                  |
| 💸 Cost Efficient   | Saves tokens on repeated calls (especially with OpenAI/Groq)   |
| ⚡ Faster Responses | Zero waiting when inputs are already seen                      |
| 📊 Useful in Loops  | Reduces latency in iterative or agent-style workflows          |

---

## 🛠️ How the Cache Works

1. User input is received
2. Flowise checks if **that exact input** exists in the cache
3. If yes → returns cached response
4. If no → sends input to LLM → saves result in cache

---

## 🧱 Cache Node Inputs & Outputs

| Input           | Description                          |
|------------------|--------------------------------------|
| Input Text       | The original prompt or query         |
| LLM              | Optional, used to trigger fallback   |

| Output           | Description                          |
|------------------|--------------------------------------|
| Cached Response  | Text returned from memory or LLM     |

---

## 🔧 Configuration Options

| Field              | Description                                     |
|--------------------|-------------------------------------------------|
| Cache Backend      | `InMemory` or `Redis` *(if supported)*          |
| Namespace          | (Optional) Custom label to organize cache       |
| Auto Save          | Whether to store every result automatically     |
| Manual Control     | You can also trigger saving using logic nodes   |

---

## ⚙️ Example Use Case

> **Prompt Caching for Smart Reply Bot**

```text
[Chat Input] → [Cache Node] → [LLM (fallback)] → [Text Output]
``` 
If the same user query is sent twice, Flowise will return the cached result instantly.

#### 🧪 Tips for Using Cache Effectively
- Use caching in loops, debug mode, or when testing prompts
- Combine with Prompt Template to make sure formatting is consistent
- If using Redis (advanced), cache becomes persistent across sessions

---
#### ✅ Summary
- The Cache node improves performance & saves tokens
- Especially useful in production agents with repeated prompts
- Works silently in the background, but can be customized

```text
Use cache when:
✅ Testing LLM flows
✅ Reducing cost
✅ Improving agent response time
```