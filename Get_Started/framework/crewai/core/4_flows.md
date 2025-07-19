# Flows in CrewAI 

Alright, let’s talk **Flows**.

## 🧠 What Exactly Are Flows?

Think of Flows as your AI system’s **brain wiring**. They’re not just scripts — they’re structured blueprints that:

* 🔗 Connect tasks
* 🧠 Share memory/state
* 🌀 Handle multi-step logic
* 💥 React to real-time events

They’re perfect when your AI agents need to **collaborate**, pass results to each other, or work in stages.

---

## ⚙️ Flow Components — The Building Blocks

### 1. `@start()`

* Marks the entry point.
* You can have multiple — they’ll all run **in parallel**.

### 2. `@listen(task_name)`

* Waits for a previous task before triggering.
* Like saying: “Do this *after* that finishes.”

### 3. State Management

* **Unstructured**: Use `self.state["anything"] = value` — good for fast prototyping.
* **Structured**: Use a `Pydantic` model for typed, clean, scalable state (better for teams).

### 4. `kickoff()`

* This triggers the whole thing.
* It returns the final output based on the last method.

---

## 🔥 Example: Generate City → Then Fun Fact

```python
from crewai.flow.flow import Flow, start, listen
from litellm import completion

class CityFactFlow(Flow):
    model = "gpt-4o-mini"

    @start()
    def generate_city(self):
        resp = completion(model=self.model, messages=[{"role": "user", "content": "Name a random city."}])
        city = resp["choices"][0]["message"]["content"]
        self.state["city"] = city
        return city

    @listen(generate_city)
    def generate_fun_fact(self, city):
        resp = completion(model=self.model, messages=[{"role": "user", "content": f"Fun fact about {city}?"}])
        fact = resp["choices"][0]["message"]["content"]
        self.state["fun_fact"] = fact
        return fact

flow = CityFactFlow()
flow.plot()
print("Result:", flow.kickoff())
```

Yep, that’s it. First the city, then a fun fact. Each step builds on the last.

---

## 🧳 Structured vs Unstructured State

### 🗃 Unstructured

```python
@start()
def init(self):
    self.state["name"] = "Alex"
    self.state["visits"] = 0
```

* Fast to write
* No type checks

### 🧠 Structured

```python
from pydantic import BaseModel

class MyState(BaseModel):
    name: str = ""
    visits: int = 0

class MyFlow(Flow[MyState]):
    @start()
    def init(self):
        self.state.name = "Alex"
        self.state.visits += 1
```

* Cleaner
* Safer
* Better for collab projects

---

## ⚙️ Some Advanced Stuff (Quick Hits)

* **`@persist()`** → Save flow state across runs.
* **Conditional Flows** → Use `or_()`, `and_()`, or `@router()` for dynamic decisions.
* **Crews inside Flows** → You can plug full agent crews into steps. Wild.

---

## 📂 Suggested Folder Structure

```
my_flow/
├── main.py         # Flow logic lives here
├── crews/          # Define your agents
│   └── my_crew/
├── tools/          # Any tools/helpers
├── .env            # API keys
└── pyproject.toml
```

In `main.py`, you wire everything together with `@start()` and `@listen()`, and trigger it with `kickoff()`.

---

## 🧠 Why Should You Use Flows?

| Feature    | What It Gives You                        |
| ---------- | ---------------------------------------- |
| Modular    | Clean step-by-step logic                 |
| Robust     | Type-safe states, branching, reusability |
| Observable | `.plot()` gives visual of flow execution |
| Scalable   | Add agents, persistence, tools, whatever |

From weekend projects to serious AI pipelines — **Flows give you control without complexity.**
>You will learn more about Flows in the crewai_example, but for now, focus more on building Crews.