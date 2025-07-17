# 📄 Document Loaders

Document Loaders in Flowise let your agents **ingest and process data from external sources** like PDFs, websites, Notion pages, and more.

These nodes are the first step for building retrieval-augmented generation (RAG), summarizers, Q&A bots, and any agent that needs real data to work with.

---

## 🗃️ What Do Document Loaders Do?

They take **unstructured content** from a file, web page, or service, and return it as **clean text** chunks your LLM can understand.

Example formats supported:
- PDF
- DOCX / Word files
- Markdown
- Notion pages
- Web articles

---

## 📂 Common Loader Nodes in Flowise

| Node Name             | Description                                 |
|------------------------|---------------------------------------------|
| **PDF Loader**         | Reads PDF files and returns text            |
| **Web Page Loader**    | Loads full HTML page and extracts content   |
| **Notion Loader**      | Accesses Notion docs via API *(token needed)*|
| **Directory Loader**   | Reads all files from a folder               |
| **YouTube Transcript** | Loads and parses video transcripts          |

> 📌 Note: Each loader may require API keys or file upload based on source

---

## 🛠️ PDF Loader Example

Use Case: Summarize a PDF or extract structured answers

### Flow:
```text
[PDF Loader] → [Text Splitter] → [LLM / Retriever]
```

>*Tips:*
>- Always connect a Text Splitter to break down long documents.
>- Can be combined with embeddings for RAG-style Q&A

___

#### 🔗 Web Page Loader Example
*Use Case: Summarize live articles or blog posts*

Flow:
```text
[Web Page Loader (URL)] → [Prompt] → [LLM]
```
>*Tips:*
>- Make sure target page has plain text or basic HTML (avoid login walls)
>- You can dynamically change URLs using Variable or Input nodes

---
### 🧠 Best Practices

| Tip                              | Why It Helps                       |
| -------------------------------- | ---------------------------------- |
| Use `Text Splitter` after loader | Prevents hitting LLM token limits  |
| Clean HTML manually if needed    | Some sites may contain junk data   |
| Limit file size for local runs   | Large PDFs can slow down execution |
| Use loaders with VectorStores    | For building context-aware memory  |

---

### ❌ Common Mistakes
| Mistake                    | Fix                                  |
| -------------------------- | ------------------------------------ |
| Feeding full PDF to LLM    | Use `Text Splitter` node             |
| Web loader returns garbage | Check if page is behind a login      |
| Notion loader fails        | Make sure integration token is valid |

---

### 🧠 Real-World Agent Use Cases
*PDF Chatbot: "Ask me anything about this research paper"*

- Smart Resume Screener
- Blog Article Summarizer
- Legal Contract Analyzer
- Daily Web Article Digest