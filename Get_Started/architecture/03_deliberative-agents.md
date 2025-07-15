# 🧭 Deliberative Agents

Deliberative agents are planners. Unlike reactive agents that just respond, these agents **think before they act**. They consider goals, internal state, and even future consequences.

---

## 🧠 How They Work

- **Have memory:** They store past data and internal state.
- **Do planning:** They evaluate multiple options before taking an action.
- **Goal-driven:** Their actions are chosen based on objectives, not just triggers.
- **Use models:** Some maintain a model of the world to make better decisions.

> "Given the current situation and my goals, what's the best action I can take?"

---

## 🔄 Real-Life Analogy

Imagine Google Maps:
> You enter your destination → It checks multiple routes → Picks the best path → Guides you step-by-step.

That’s a deliberative system. It doesn’t just “react” — it plans based on context, rules, and goals.

---

## ✅ Use Cases for Deliberative Agents

Deliberative agents are ideal when:
- Tasks require multi-step reasoning or planning
- Context or goals change over time
- Actions depend on previous steps or conditions

### Examples:
- AI project manager agent (plans, assigns tasks, checks progress)
- Resume analyzer that scores, ranks, and selects based on config
- Agents in games (strategy planning, simulations)

---

## 🔧 Pros and Cons

| Pros                          | Cons                              |
|-------------------------------|-----------------------------------|
| ✅ Smart & goal-oriented       | ❌ Slower than reactive agents     |
| ✅ Handles complex decisions   | ❌ Harder to build and maintain    |
| ✅ Can model complex workflows | ❌ Requires internal state & logic |

---

## 🛠️ Tools & Frameworks to Use

Deliberative agents work well with:
- **Langchain Agents** with multi-step tools
- **CrewAI** agents with memory + back-and-forth tasking
- **Traceloop / Langfuse** for tracking decisions and reasoning
- **LangGraph**

---

## 🧠 Basic Structure of a Deliberative Agent
- Input (Goal or Instruction)
- Context/State Lookup
- Planning Logic (LLM or rule-based)
- Action Decision
- Tool/Task Execution


---

## 📌 Summary

Deliberative agents are the **thinkers** in the agent world. They’re useful when:
- The task requires logic, memory, or decision-making
- You want the agent to adapt or choose from multiple paths
- You're building systems that involve reasoning, workflows, or decision trees

> → Next: [Learn About Learning Agents »](04_learning-agents.md)
