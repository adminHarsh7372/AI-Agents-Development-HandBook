# 🧠 LLMs Node

The `LLMs` node in Flowise lets you use **large language models** for general-purpose text generation — like summarizing, answering questions, generating titles, and more.

This node focuses on **completion-style models**, unlike the `Chat Models` node which is optimized for dialogue.

---

## 🤖 What is an LLM?

A Large Language Model (LLM) is a deep learning model trained to understand and generate human-like text. It takes in a prompt (text input) and returns a response based on probability.

---

## 📌 When to Use LLM (vs. Chat Models)

| Use Case                     | Use This Node?    |
|------------------------------|-------------------|
| Summarization                | ✅ Yes             |
| Headline / Content Generation| ✅ Yes             |
| Classification or extraction| ✅ Yes             |
| Conversation or chat agents | ❌ Use Chat Models |

---

## 🌐 Supported Providers

Flowise supports many LLM providers through this node:

| Provider       | Notes                                      |
|----------------|--------------------------------------------|
| **OpenAI**     | `text-davinci-003` and other base models   |
| **Cohere**     | Language generation & classification       |
| **Replicate**  | Custom LLMs hosted on Replicate            |
| **Ollama**     | Local models like Mistral, LLaMA           |
| **HuggingFace**| Use via API or locally with Ollama         |

---

## ⚙️ Key Configuration Options

| Field           | Description                                       |
|------------------|---------------------------------------------------|
| Model Name       | Choose provider model (e.g. `text-davinci-003`)  |
| Temperature      | Controls randomness (0 = focused, 1 = creative)  |
| Max Tokens       | Limits response length                           |
| Top P            | Controls diversity of output                     |
| Stop Sequences   | Define where the model should stop               |

---

## 🧱 Input/Output

| Input             | What to Send                                     |
|-------------------|--------------------------------------------------|
| Prompt Text       | The raw or templated input                       |

| Output            | What You Receive                                 |
|-------------------|--------------------------------------------------|
| Generated Text    | The LLM’s raw output (no memory, no roles)       |

---

## 🔗 Example Use Case

> **"Summarize this blog post in one sentence"**

```text
[Web Page Loader]
   ↓
[Prompt Template: "Summarize this: {{input}}"]
   ↓
[LLM (text-davinci-003)]
   ↓
[Text Output]
```
---

#### 🧠 Best Practices
| Tip                                   | Why It Helps                          |
| ------------------------------------- | ------------------------------------- |
| Use a Prompt Template                 | Ensures structured and reusable input |
| Lower `temperature` for factual tasks | Prevents hallucinations               |
| Add stop sequences for clean output   | Prevents overly long or messy replies |
| Combine with Output Parser            | Makes responses usable in automation  |

---

#### ⚠️ Common Pitfalls
| Issue                            | Fix                                  |
| -------------------------------- | ------------------------------------ |
| Output is too long or irrelevant | Lower temperature or revise prompt   |
| LLM ignores instruction          | Add examples or clearer format       |
| Too expensive (OpenAI)           | Use Ollama or smaller models locally |

---

#### 🧠 LLM Prompting Tips
- ✅ Use few-shot examples to guide model
- ✅ Be specific: “Return exactly 3 bullet points.”
- ✅ Avoid ambiguous prompts like “explain this” — add context
- ✅ Test output with different models (results vary)

---

#### ✅ Summary
The LLMs node is perfect for standalone generation tasks — not multi-turn conversations.

```text
Use LLM node when:
✅ You want simple text generation
✅ You don’t need chat history or memory
✅ You want fast, low-cost completions
```