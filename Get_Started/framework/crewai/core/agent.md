# agents.md

Agents are the heart of CrewAI - a specialized AI entity designed to perform specific roles within a collaborative framework. Without them, nothing would move forward. They're the brains that perform the thinking and execution in your multi-agent system.

In simple words: **Agent = Role + Goal + Backstory+ Tools + Memory (Optional)**

An agent is like a specific character with a defined role and skillset. You can assign them tasks, give them memory, provide them tools, and define how they should behave.

---

## 🧠 How to define an agent in Python:

You need to import `Agent` from `crewai`:

```python
from crewai import Agent

my_agent = Agent(
    role='Senior Software Engineer',
    goal='Develop a scalable API for an AI-based system',
    backstory='Experienced engineer at OpenAI with 8 years of backend expertise.',
    verbose=True,
    memory=True
)
```
## Yaml
```yaml
researcher:
  role: >
    {topic} Senior Data Researcher
  goal: >
    Uncover cutting-edge developments in {topic}
  backstory: >
    You're a seasoned researcher with a knack for uncovering the latest
    developments in {topic}. Known for your ability to find the most relevant
    information and present it in a clear and concise manner.
```

---

## 🧱 Key Components of an Agent:

* `role`: Who the agent is. Be specific. Not just "engineer" but "backend developer who optimizes APIs for LLM systems."
* `goal`: What do you want the agent to achieve? Keep it focused.
* `backstory`: The context behind the agent. It helps define how the agent behaves.
* `tools`: You can give agents specific tools like web search, file read/write, custom scripts.
* `memory`: This allows the agent to remember previous interactions or data.
* `verbose`: This helps in debugging. Shows what the agent is doing step-by-step.

---
### Role: Example
```text
Example >
role: You're a senior python engineer.
role: You're a Documentation writer.
```

*Goal: Example*
```text
Example >
goal: "Uncover actionable user insights by analyzing interview data and identifying recurring patterns, unmet needs, and improvement opportunities"
goal: "Design robust, scalable system architectures that balance performance, maintainability, and cost-effectiveness"
goal: "Craft clear, empathetic crisis communications that address stakeholder concerns while protecting organizational reputation"
```
*Backstory: Example*
```text
backstory: "You have spent 15 years conducting and analyzing user research for top tech companies. You have a talent for reading between the lines and identifying patterns that others miss. You believe that good UX is invisible and that the best insights come from listening to what users don't say as much as what they do say."

backstory: "With 20+ years of experience building distributed systems at scale, you've developed a pragmatic approach to software architecture. You've seen both successful and failed systems and have learned valuable lessons from each. You balance theoretical best practices with practical constraints and always consider the maintenance and operational aspects of your designs."

backstory: "As a seasoned communications professional who has guided multiple organizations through high-profile crises, you understand the importance of transparency, speed, and empathy in crisis response. You have a methodical approach to crafting messages that address concerns while maintaining organizational credibility."
```
---
## 🔧 Example: Agent with Tools and Memory

```python
from crewai import Agent
from tools.search_tool import SearchTool

research_agent = Agent(
    role='AI Researcher',
    goal='Find the latest breakthroughs in NLP models',
    backstory='Researcher focused on open-source LLMs.',
    tools=[SearchTool()],
    memory=True,
    verbose=True
)
```

---

### Agent Attribute 
*There are several agent attribute. But these are the most used attributes*
1. `role` -  Who the agent is.
2. `goal` - What do you want the agent to achieve?
3. `backstory` - The context behind the agent. It helps define how the agent behaves.
4. `verbose` - This helps in debugging. Shows what the agent is doing step-by-step.
4. `memory` - This allows the agent to remember previous interactions or data.
6. `llm` - Language model that powers the agent. 
7. `tools` - Capabilities or functions available to the agent.
8. `allow_delegation` - Allow the agent to delegate tasks to other agents. Default is False.
9. `max_retry_limit` - Maximum number of retries when an error occurs. Default is 2.
10. `max_iter` - Maximum iterations before the agent must provide its best answer. Default is 20.
>For more attributes check the official [docs](https://docs.crewai.com/en/concepts/agents)

- *Agent must have these attributes, not just to make the agent powerful, but also to save on API usage costs. As you can see, the default maximum number of iterations is 20, which consumes a lot of API tokens. That's why we need to assign them ourselves.*

- *If you don’t give memory or tools, the agent still works — but they’ll be limited. Give them powers if you want them to work like real assistants.*

