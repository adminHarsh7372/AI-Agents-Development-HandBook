# 💾 Using Ollama (Local LLMs) in AI Agents

**Ollama** lets you run powerful open‑source LLMs entirely **locally**, without relying on cloud APIs. It's great for privacy, offline work, or cost-sensitive setups.

---

## 🧠 Why Use Ollama?

- 🔒 Full privacy—your data never leaves your machine
- 💰 No per‑token API costs
- ⚙️ Easy local server with a simple REST API
- 📚 Supports many open‑source models (LLaMA, LLaVA, Phi‑4, etc.).

---

## 🛠️ Setup & Installation

1. **Install Ollama CLI/app**  
   - macOS: `brew install ollama`  
   - Linux/WSL: `curl -fsSL https://ollama.com/install.sh` 

2. **Pull a model**, e.g.:  
   ```bash
   ollama pull llama3.2
    ```
3. **Run the model locally**
    ```bash
    ollama run llama3.2
    ```
4. **Serve REST API:**
    ```bash
    ollama serve
    ```
    → Available at http://127.0.0.1:11434

### 🔧 Example: REST API & Python
***Using cURL:**
```bash
   curl http://localhost:11434/api/generate \ 
   -d '{ "model": "llama3.2", "prompt": "What is Ollama?" }'
  ```

```python
import requests
resp = requests.post(
  "http://127.0.0.1:11434/api/generate",
  json={"model": "llama3.2", "prompt": "Explain Ollama LLM"}
)
print(resp.json()["completion"])
``` 
---

## ⚙️ Using Ollama with LangChain or LlamaIndex

With **LangChain**:
```python
from langchain_ollama.llms import OllamaLLM
model = OllamaLLM(model="llama3.1", request_timeout=120.0)
resp = model.complete("Hello Ollama!")
print(resp)
``` 

With **LlamaIndex**:
```python
from llama_index.llms.ollama import Ollama
llm = Ollama(model="llama3.1:latest", context_window=8000)
print(llm.complete("Who is Alan Turing?"))
``` 

---

## 🧩 Pros & Cons

| ✅ Pros                                          | ❌ Cons                                       |
|--------------------------------------------------|-----------------------------------------------|
| Privacy-first & offline                        | Needs local compute resources (RAM/CPU/GPU)  |
| No token/API costs                              | Performance varies by model/hardware         |
| Control over model choice & updates             | Lacks native tool-calling support            |
| Suitable for multimodal & RAG usage            | Requires local setup and maintenance         |

---

## ✅ Use Cases

Use Ollama when you need:
- Offline demos or workshops
- Cost-effective model hosting
- On-device assistants with full data control
- Integrations with LlamaIndex, local AI apps

---

## 📌 Summary

Ollama is a powerful local-first alternative to cloud LLMs. It empowers developers to:
- Pull and run open-source models like LLaMA and Phi‑4
- Serve them via API on localhost
- Integrate with LangChain or LlamaIndex for agent workflows

>***→ Next up: [Comparison »](5_comparison.md)*** 
