# Tasks

**Before you jump into writing your agent, focus on what your agent will do — the task.**

In CrewAI, a task isn't just a random instruction — it's the *core objective* your agent will act upon. If your task is unclear, even the best-designed agent won’t be able to perform well. That's why we always say: before building agents, **learn how to define tasks properly.**

---

## 🧠 The 80/20 Rule: Focus on Tasks Over Agents

> When building effective AI systems, remember this crucial principle:
>
> **80% of your effort should go into designing tasks, and only 20% into defining agents.**

Why?

Because even the most perfectly defined agent will fail with poorly designed tasks, but well-designed tasks can elevate even a simple agent. This means:

* Spend most of your time writing clear task instructions
* Define detailed inputs and expected outputs
* Add examples and context to guide execution
* Dedicate the remaining time to agent role, goal, and backstory

**This doesn’t mean agent design isn’t important** — it absolutely is. But task design is where most execution failures occur, so prioritize accordingly.

---

## 🔍 What Makes a Good Task?

When you're designing tasks for your agent or crew, make sure you:

* **Clearly define the objective:** What is the agent supposed to achieve?
* **Include specific context or examples:** Guide the agent with relevant information.
* **Limit ambiguity:** The less vague your task, the better the outcome.
* **Specify the output format:** Especially important if other agents/tools need to use the result.

---

## 🛠️ Python Example

```python
from crewai import Task

research_task = Task(
    description="Find the latest research papers about large language models.",
    expected_output="A list of 5 recent papers with their titles, authors, and short summaries.",
    tools=[arxiv_tool],
    agent=researcher_agent
)
```

---

## 📄 YAML Example

```yaml
tasks:
  - description: "Find the latest research papers about large language models."
    expected_output: "A list of 5 recent papers with their titles, authors, and short summaries."
    tools: [arxiv_tool]
    agent: researcher_agent
```

---

## 💡 Tip:

If your agent is giving weird or incomplete answers, go back and re-check your task first. Most of the time, **the issue is in the task design, not the agent logic**.

---

## 🔧Task Attributes

1. `description` - A clear, concise statement of what the task entails.
2. `expected_output` - A detailed description of what the task’s completion looks like.
3. `agent` - The agent responsible for executing the task.
4. `tools` - The tools/resources the agent is limited to use for this task.
5. `async_execution` - Whether the task should be executed asynchronously. Defaults to False.
6 `human_input` - Whether the task should have a human review the final answer of the agent. Defaults to False.
7. `markdown` - Whether the task should instruct the agent to return the final answer formatted in Markdown. Defaults to False.
8. `output_file	` - File path for storing the task output

*These are the most used attirbutes of the task.*
> For more task attributes, check out official [docs](https://docs.crewai.com/en/concepts/tasks)