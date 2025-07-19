# CrewAI: Agent Knowledge Management 🧠

In CrewAI, knowledge isn't just about what an agent knows — it's about how you give that knowledge to the agent *at the right time and in the right format.* This file explains how knowledge is structured, loaded, and used to make agents more intelligent and efficient.

---

## Why Knowledge Matters

LLMs are smart — but forgetful. If you want your agents to:

* Answer questions about your product or docs
* Follow company-specific workflows
* Use proprietary data to make decisions

Then you need to load that information into the system as "knowledge." Without it, agents will just hallucinate.

---

## How to Add Knowledge in CrewAI

CrewAI lets you inject custom knowledge into agents using:

* **Files** (PDF, TXT, etc.)
* **Webpages** (URLs)
* **Text chunks** (raw string content)

Behind the scenes, CrewAI splits the content, embeds it, and adds it to a vectorstore like ChromaDB.

---

## The `CrewKnowledge` Object

This is the main object to provide knowledge. Here's how to use it:

### Basic Example:

```python
from crewai.knowledge import CrewKnowledge

knowledge = CrewKnowledge()

knowledge.add(name="Docs", urls=["https://docs.crewai.com"])
knowledge.add(name="Whitepaper", files=["whitepaper.pdf"])
knowledge.add(name="HelpText", text_chunks=["Always respond politely"])
```

Then pass it into your `Crew`:

```python
crew = Crew(agents=[...], tasks=[...], knowledge=knowledge)
crew.kickoff()
```

That’s it! Now your agents will have access to these sources during task execution.

---

## You Can Add Multiple Knowledge Sources

You can combine as many types as needed:

```python
knowledge.add(
  name="MyKnowledge",
  urls=[...],
  files=[...],
  text_chunks=[...]
)
```

Each `add()` call registers a new source, and they all become available during the task phase.

---

## How Agents Use Knowledge

When a task runs, CrewAI augments the prompt with relevant chunks from the knowledge base.
It’s just like Retrieval-Augmented Generation (RAG).

> Note: If you want more control over vectorstore, embeddings, or retrieval logic, you'll need to dig into advanced usage or contribute to the CrewAI backend.

---

## Some Best Practices

* Keep knowledge focused (don’t overload irrelevant data)
* Preprocess large PDFs (split into focused sections)
* Use consistent formatting in your documents
* Always give examples when possible

---

## When to Use Knowledge

Use CrewKnowledge when:

* Tasks require custom domain knowledge
* Agents need to answer or write based on specific info
* You want to avoid LLM hallucination in critical systems

Avoid using it for:

* Temporary memory (use memory module instead)
* Simple workflows with no domain-specific data

---

## YAML Support

Yes, CrewAI also supports YAML-based knowledge configuration, but it’s easier to debug and reason with Python if you're doing custom builds.

If you're using YAML:

```yaml
knowledge:
  - name: Docs
    urls:
      - "https://docs.crewai.com"
  - name: Local
    files:
      - "guide.pdf"
```

Then load it in your CLI or programmatically.

---

## Summary

Knowledge = power. And CrewKnowledge makes it easy to inject that power into your agents.

* Use `CrewKnowledge` to add docs, URLs, or raw text
* Attach it when initializing your `Crew`
* Your agents will then access this info when running tasks

It’s simple, flexible, and makes your agents 10x smarter.

---

