# Crew

*A Crew is the brain of your multi-agent system. It manages agents, tasks, and how they interact to complete the job efficiently.*

When you’re building a system using CrewAI, think of the `Crew` as your main controller – it handles the flow, process, and strategy of how your agents execute their assigned tasks.

---

## 🧠 Core Crew Attributes

Here are some of the most important attributes when defining a Crew:

* `agents`: A list of agents that will work together. These agents can have different roles and goals.
* `tasks`: A list of tasks that must be completed. These are distributed and executed by the agents.
* `process`: The execution style. Can be **sequential**, **hierarchical**.
* `verbose` *(optional)*: Set this to **True** if you want detailed logs while running the crew.
* `step\_callback` *(optional)*: If you want to run some custom logic (like logging, database storage, or UI updates) after each step.
* `memory` *(optional)*: Pass a memory backend if you want the agents to remember and reference previous interactions.
* `max\_rpm` *(optional)*: Requests per minute limit. Helps avoid rate-limiting with APIs.
* `max\_iter` *(optional)*: Total number of iterations allowed. Useful to control token usage.

> 💡 **Pro tip:** Always set `max_iter` thoughtfully. Too high and you’ll burn tokens. Too low and the task might fail early.

---

## 👨‍💼 When There’s a Manager Agent Involved

If your system includes a **manager** or **supervisor** agent (like in complex agent hierarchies), you need to structure your crew differently:

### 🧩 Example Strategy:

1. **Manager Agent** doesn’t perform the task directly, instead it delegates work to worker agents.
2. Create two crews:

   * A **Main Crew** that only has the manager agent and a task like: *"Supervise and delegate tasks to appropriate agents"*.
   * **Sub-crews** created inside the tool or via custom logic which the manager triggers.

This pattern allows for:

* Nested crew orchestration
* Delegation logic handled by manager
* Cleaner code and better modularity

---

### 🛠 Creating the Crew

Here’s a basic Python example:

```python
from crewai import Crew
from agents import researcher, writer
from tasks import research_task, write_task

crew = Crew(
    agents=[researcher, writer],
    tasks=[research_task, write_task],
    process="sequential",
    verbose=True,
    max_iter=5
)
```

If you have a **manager agent**:

```python
crew = Crew(
    agents=[manager],
    tasks=[manage_task],
    process="sequential",
    verbose=True,
    max_iter=3
)
```

Then within `manager`, you can spawn sub-crews or logic to dynamically create agents and tasks.
>You can learn more about the manager agent, task and crew in [crewai_example/]()
---
### Kicking Off a Crew
Once your crew is assembled, initiate the workflow with the kickoff() method. This starts the execution process according to the defined process flow.
```python
result = my_crew.kickoff()
print(result)
```
---

### Thought

Think of your `Crew` as the **game master** — it decides the rules, the order of play, and how the agents communicate. Set it up smartly and the rest of your system becomes way easier to manage and scale.
