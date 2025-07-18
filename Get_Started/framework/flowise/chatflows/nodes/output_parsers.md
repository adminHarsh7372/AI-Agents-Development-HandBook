# 🧾 Output Parsers

Output Parsers in Flowise help **clean, format, and structure** raw responses from LLMs. They’re essential when your agents need to return data in a specific format (like JSON, list, number, etc.) or use that output in another tool.

Without parsers, LLMs may return unpredictable or unstructured text — not ideal for automation or integration.

---

## 🧠 Why Use an Output Parser?

| Use Case                         | How It Helps                            |
|----------------------------------|------------------------------------------|
| Need JSON output for API         | Parses raw text to valid JSON            |
| Extracting values (name, email)  | Converts messy text into clean fields    |
| Looping or branching logic       | Makes output predictable and usable      |
| Tool chaining                    | Ensures next node gets expected format   |

---

## 🛠️ Common Parser Nodes in Flowise

| Parser Name          | Description                                       |
|----------------------|---------------------------------------------------|
| **Structured Output Parser** | Parses model output using Langchain's structured system |
| **Comma Separated List**     | Turns text into list of items              |
| **Output Fixing Parser**     | Tries to auto-correct malformed outputs    |
| **Regex Parser**             | Use custom regex to extract fields         |
| **Number Parser**            | Extracts numeric values only               |
| **Boolean Parser**           | Extracts and evaluates true/false answers  |

---

## 🔗 Example Flow

> **"Summarize and return JSON with title, key points, and action items"**

```text
[Prompt Template]
   ↓
[LLM]
   ↓
[Structured Output Parser]
   ↓
[Webhook / Display / Conditional Logic]
```
### 🔧 Structured Output Parser Details
This parser works best when your prompt includes a clear output schema.

**Example Prompt:**
```typescript
You are a task extractor.
Return a JSON like:
{
  "title": string,
  "key_points": [string],
  "action_items": [string]
}
```
**LLM Output:**
```json
{
  "title": "AI in Education",
  "key_points": ["Personalized learning", "Automation"],
  "action_items": ["Research impact", "Test pilot program"]
}
```
The parser ensures this gets passed cleanly to the next node.

---

#### 🧪 Tips for Effective Output Parsing
| Tip                                        | Why It Helps                            |
| ------------------------------------------ | --------------------------------------- |
| Define format clearly in prompt            | Increases model reliability             |
| Add “If you can’t return JSON...” fallback | Handles failure cases gracefully        |
| Use Output Fixing if structure fails       | Attempts auto-repair of output          |
| Combine with `Memory`                      | To track and store structured responses |


----

#### ⚠️ Common Mistakes
| Problem                     | How to Fix                            |
| --------------------------- | ------------------------------------- |
| LLM returns bad formatting  | Use Output Fixing Parser              |
| JSON is missing fields      | Be more explicit in prompt template   |
| Regex parser fails silently | Test regex pattern in a sandbox first |

----

### 🧠 Real Agent Use Cases
Task Extractor → Output Parser → Task Manager API

Resume Analyzer → Output Parser → Candidate Scorer

PDF Reader → Summarizer → Output Parser → Email Sender

Form Assistant → LLM → JSON → Zapier/Webhook

---
#### ✅ Summary
Output Parsers bring structure to chaos.
They’re essential for turning "language" into data.

```text
Use Output Parsers when:
✅ You need JSON or structured formats
✅ You want to chain tools reliably
✅ You’re building real integrations
```
>“LLMs speak in paragraphs. Parsers turn that into instructions.”