# Parsing Outputs: From Text to Structured Data 🧩

When your AI agent gives you a wall of text, it’s not very useful—especially if you want to extract details or plug responses into your app. That’s where smart output parsing comes in: getting the model to return JSON, YAML, or XML so your code can process it reliably.

---

## Why Structure Matters

Imagine your AI says:

> “The user mentioned MegaWidget 3000 and felt frustrated after two days.”

Great for humans—but not for your parser. Instead, clean, structured output looks like:

```yaml
product_name: MegaWidget 3000  
sentiment: Negative  
summary: Broke after 2 days, user frustrated  
```
Structured data is consistent, easy to parse, and less brittle for automation 🛠️.

---

**1. Use Model Features**

- Some LLMs support structured outputs natively:
- OpenAI function-calling / JSON Mode – define a JSON schema and the model does the rest.
- Gemini – specify a response schema in the API config and it outputs structured JSON.

**2. Prompt‑Based Formatting**

- This method works across all models:
- Clearly ask: “Return only JSON with keys X, Y, Z”
- Provide an example snippet or schema
- Be explicit: “Do not add prose or quotes around numbers”
- Use ast.literal_eval()-friendly formatting
- Show a JSON or YAML example in the prompt to guide structure

**3. Practical Prompt Templates**
Example – JSON output:
```json
Please answer ONLY in this JSON format:
{
  "name": string,
  "age": number,
  "languages": [string]
}
```
- User: “[user input here]”
- Example – YAML output (more human-friendly):Output in YAML:

```yaml
name: string  
age: number  
languages:  
  - string
```
YAML is often cheaper, cleaner, and easier for models to follow.

---

### 4. Tooling + Parsers
**LangChain Parsers**
LangChain includes built-in parsers:

`JsonOutputParser` – streams and validates JSON output

`PydanticOutputParser` – maps output to Python models with validation

These combine prompt instructions with code-level parsing. For example:

```python
from langchain.output_parsers import JsonOutputParser
from pydantic import BaseModel

class Movie(BaseModel):
    title: str
    year: int

parser = JsonOutputParser(pydantic_object=Movie)
prompt = PromptTemplate(
    input_variables=["plot"],
    template="Tell me about this movie plot:\n{plot}\n{format_instructions}"
)
formatted_prompt = prompt.format(
    plot="A space adventure involving robots.",
    format_instructions=parser.get_format_instructions()
)
response = llm(formatted_prompt)
movie = parser.parse(response)
```
### Handling Parsing Errors
Even with clear prompts, models can mess up. Here are strategies:

- Retry prompts – ask the model to fix its output
- Output-fixing – send back malformed output and say “format this properly”
- Structural validation – use JSON Schema or Pydantic to catch and reject invalid output

---
