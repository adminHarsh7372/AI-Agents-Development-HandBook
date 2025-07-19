# Event Listeners 🎧
CrewAI’s event listener system is your go-to tool for hooking into the internal lifecycle of your agents and tasks—without messing with the core code. In short, listeners let you watch what happens and react in real time.

---

### 🧠 The Basics
- You extend BaseEventListener and override setup_listeners()
- Inside, you register handler functions for events using the event bus, e.g.:

```python
@crewai_event_bus.on(SomeEventType)
def handle_event(source, event):
    ...
```
- Handlers take two parameters:

    - `source` – the emitter, like a Crew or an agent
    - `event` – subclass of `BaseEvent`, includes a common `timestamp` and `type` with event‑specific fields

---

### 🪄 Real‑World Example: AgentOps Integration
*CrewAI ships an example listener with built‑in integration to AgentOps:*

- Listens to Crew kickoff & completion events.
- Starts a session in AgentOps on kickoff, registers agents, tracks tool usage, and closes the session on completion.
- Also captures tool errors and logs them via AgentOps

It’s a terrific starting point if you're building your own observability system.

---

### 🔍 Listening to Knowledge & Memory Events
CrewAI emits many useful internal events:

**Knowledge Retrieval Events** \
Track the agent’s readings of knowledge sources:

- `KnowledgeRetrievalStartedEvent`

- `KnowledgeRetrievalCompletedEvent` (including query & results count)

Monitor and log who started retrieval, what query was issued, and how much content was fetched.

---

### Memory Events
**Hook into memory operations with:**

1. Query start/completion/failure

2. Save start/completion/failure

3. Retrieval start/completion

You can build listeners for performance metrics, detailed logs, failure alerts, analytics forwarding—a ton of useful stuff.

---

### 🛠️ Capturing Tool Usage & Errors
Want to see every tool call, their responses, or errors?

**Example listener captures:**

- ToolUsageStartedEvent
- ToolUsageFinishedEvent
- ToolUsageErrorEvent

Other related tool‑error types

You can pretty-print the entire event object to debug and intercept actual request/response payloads.

---

### 🚀 When to Use Event Listeners vs. Subclassing
Instead of overriding Task behavior, listeners let you respond to task lifecycle events—much lighter and less invasive. For example, listening to `TaskStartedEvent`, `TaskCompletedEvent`, `TaskFailedEvent` works smoothly alongside other listeners like AgentOps or custom ones
CrewAI
.

---
### ✅ Best Practices
- **Keep it light**: your handlers should be fast and non-blocking
- **Choose log levels wisely**: INFO for normal operations, DEBUG for data dumps, ERROR for failures
- **Aggregate metrics when possible** (batching before forwarding)

- **Graceful error handling so a faulty handler won’t crash your Crew execution**
- **Be memory-conscious, especially if you store or buffer event data**

---

### 📋 Quick Reference Table
| Event Type Area          | Events                                             | Use Case Summary                                                                                                                                   |
| ------------------------ | -------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| Crew Lifecycle           | `CrewKickoffStarted`, `CrewKickoffCompleted`, etc. | Trigger integration sessions or summary logic                                                                                                      |
| Knowledge Retrieval      | `KnowledgeRetrievalStarted/Completed`              | Monitor queries made and results fetched                                                                                                           |
| Memory Operations        | `MemoryQuery*`, `MemorySave*`, `MemoryRetrieval*`  | Track memory performance and debugging                                                                                                             |
| Tool Usage               | `ToolUsageStarted/Finished/Error`, etc.            | Inspect tool invocation lifecycle, record payloads, catch errors                                                                                   |
| LLM Streaming (optional) | `LLMStreamChunkEvent`                              | To capture individual streaming tokens if using `stream=True`([docs.crewai.com][1], [docs.crewai.com][2], [DeepWiki][3], [CrewAI][4], [CrewAI][5]) |

[1]: https://docs.crewai.com/concepts/event-listener?utm_source=chatgpt.com "Event Listeners - CrewAI"
[2]: https://docs.crewai.com/concepts/memory?utm_source=chatgpt.com "Memory - CrewAI"
[3]: https://deepwiki.com/crewAIInc/crewAI/8.2-integration-with-observability-platforms?utm_source=chatgpt.com "Integration with Observability Platforms | crewAIInc/crewAI | DeepWiki"
[4]: https://community.crewai.com/t/how-do-i-see-actual-request-and-response-for-tools-used-during-tracing/4484/4?utm_source=chatgpt.com "How do I see actual request and response for Tools used during Tracing - #4 by Max_Moura - General - CrewAI"
[5]: https://community.crewai.com/t/openai-streaming/3556?utm_source=chatgpt.com "OpenAI streaming? - General - CrewAI"

---

### 🧑‍💻 Example Snippet: Custom Listener
```python
from crewai.utilities.events.base_event_listener import BaseEventListener
from crewai.utilities.events.tool_usage_events import (
    ToolUsageStartedEvent,
    ToolUsageFinishedEvent,
    ToolUsageErrorEvent
)

class MyToolListener(BaseEventListener):
    def setup_listeners(self, crewai_event_bus):
        @crewai_event_bus.on(ToolUsageStartedEvent)
        def on_start(src, event):
            print("Tool started:", event.tool_name)

        @crewai_event_bus.on(ToolUsageFinishedEvent)
        def on_finish(src, event):
            print("Tool finished:", event.tool_name, "output:", event.output)

        @crewai_event_bus.on(ToolUsageErrorEvent)
        def on_error(src, event):
            print("Tool error:", event.error)
```

>***CrewAI’s event listener system is a flexible way to integrate observability, analytics, debugging, or external tooling—without ever touching the core task logic. Use it to get visibility into your agents, tools, or memory in a clean, modular way.***