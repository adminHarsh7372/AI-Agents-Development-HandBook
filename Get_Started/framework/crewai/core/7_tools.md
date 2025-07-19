# CrewAI Tools

Tools in CrewAI are powerful components that extend the abilities of your agents by letting them take real-world actions—like calling APIs, querying databases, or interacting with external systems. Instead of only thinking and planning, agents can use tools to actually **do** things.


* Pull data from external sources (e.g., search engines, databases)
* Trigger actions (e.g., send emails, update records)
* Perform calculations, summaries, or other utilities

You define them manually or integrate with toolkits like **CrewAI Toolkit**, **Composio**, **LangChain tools**, or **custom Python functions**.

---
#### To use the tools, install the package
```python
pip install 'crewai[tools]'
```

---
## Creating Tools

CrewAI supports multiple ways to define tools:

### Creating your own Tools


```python
from crewai.tools import BaseTool
from pydantic import BaseModel, Field

class MyToolInput(BaseModel):
    """Input schema for MyCustomTool."""
    argument: str = Field(..., description="Description of the argument.")

class MyCustomTool(BaseTool):
    name: str = "Name of my tool"
    description: str = "What this tool does. It's vital for effective utilization."
    args_schema: Type[BaseModel] = MyToolInput

    def _run(self, argument: str) -> str:
        # Your tool's logic here
        return "Tool's result"
```

### 2. Using LangChain Tools

CrewAI can directly wrap LangChain tools if you're already using them. Example:

```python
from langchain.agents import load_tools
from crewai import Tool

lc_tools = load_tools(["serpapi"])
wrapped_tool = Tool.from_langchain(lc_tools[0])
```

### 3. Using Composio Tools

Composio provides plug-and-play tools for services like Notion, Slack, Google Sheets, etc. These are great for SaaS workflows.

We’ll cover this more deeply in the integrations section.

---

## Tool Attributes

Each tool in CrewAI typically has:

* `name`: Human-readable name
* `description`: Clear explanation of what the tool does and when to use it
* `func`: The Python function to execute
* `return_direct` (optional): If set to `True`, the tool output is returned directly by the agent (no reasoning or follow-up)

---
### Available CrewAI Tools

*CrewAI have alot of different tools for different use.*

*Here are the some of the tools name:*

1. `File & Documentation Tools` - These tools enable your agent to work with various file formats and  document types. From reading PDFs to processing JSON data.
   - File Read Tool - To Read the text file
   ```python
   from creawai_tools import FileReadTool
   file_read_tool=FileReadTool(file_path='/./you file path')
   ```
   - File Write Tool - Writing content to the file.
   ```python
   from creawai_tools import FileWriteTool
   file_write_tool=FileWriteTool('file_name.txt')
   ```
   - PDF Rag Search - To search pdf files and return the most relevant results.
   ```python 
   from creawai_tools import PDFSearchTool
   pdf_tool=PDFSearchTool(path=your file path)
   ```
2. `Web Scraping & Browsing Tools` -
Useful for extracting web content or interacting with websites:

    - ScrapeWebsiteTool -
    Scrape text from a given URL.

    ```python
    from crewai_tools import ScrapeWebsiteTool

    scraper = ScrapeWebsiteTool(website_url='https://example.com')
   ```

    - SeleniumScrapingTool -
    Target specific page elements via CSS selectors.

    ```python
    from crewai_tools import SeleniumScrapingTool

    selenium_scraper = SeleniumScrapingTool(
        website_url='https://example.com',
        css_element='.main-content'
    )
    ```
3. `Search & Research Tools` - Perfect when your agents need to fetch info from the web:

    - SerperDevTool (Google search API)
    ```python
    from crewai_tools import SerperDevTool

    google = SerperDevTool()
    ```
    *Seper Dev Tool need serper api key, To get the serper api key go to its official site*

    - WebsiteSearchTool - 
    Ideal for RAG-based search on specific sites.

    ```python
    from crewai_tools import WebsiteSearchTool

    site_search = WebsiteSearchTool(website='https://docs.crewai.com')
    summary = site_search.run(query="PDFSearchTool usage")
    print(summary)
    ```

4. `AI & Machine Learning Tools` - 
Make your agents smarter with AI-powered tools:

    - DallETool - 
    Generate images directly from prompts.

    ```python
    from crewai_tools import DallETool

    dalle_tool = DallETool(model="dall-e-3",
                       size="1024x1024",
                       quality="standard",
                       n=1)

    Agent(
    ...
        tools=[dalle_tool]
    )
    ```

    - CodeInterpreterTool -
    Run and test Python code within your agent.

    ```python
    from crewai_tools import CodeInterpreterTool

    code_interpreter = CodeInterpreterTool()

    programmer_agent = Agent(
        role="XYZ",
        goal="XYZ",
        backstory="XYZ",
        tools=[code_interpreter],
        verbose=True,
        )

    ```

5. `DataBase & Data` - These tools enable your agents to interact with various database systems, from traditional SQL databases to modern vector stores and data warehouses.
    - MySQL RAG Search - Searches within MySQL database tables.
    ```python
      from crewai_tools import MySQLSearchTool

        # Initialize the tool with the database URI and the target table name
        tool = MySQLSearchTool(
            db_uri='mysql://user:password@localhost:3306/mydatabase',
            table_name='employees'
        )
    ```

    - PG RAG Search - The PGSearchTool is designed to search PostgreSQL databases and return the most relevant results.
    ```python
      from crewai_tools import PGSearchTool

        # Initialize the tool with the database URI and the target table name
        tool = PGSearchTool(
            db_uri='postgresql://user:password@localhost:5432/mydatabase', 
            table_name='employees'
        )

    ```
---
### 🧩 Using Tools Together in an Agent
Combine tools to build a multi-functional agent:
```python 
from crewai_tools import FileReadTool, SerperDevTool, WebsiteSearchTool
from crewai import Agent, Task, Crew

agent = Agent(
    role="Research Assistant",
    goal="Find and summarize info on AI ethics",
    tools=[FileReadTool(), SerperDevTool(), WebsiteSearchTool()],
    verbose=True
)

task = Task(
    description="Search for recent AI ethics papers and summarize them.",
    expected_output="Bullet-point summary of 5 papers"
)

crew = Crew(agents=[agent], tasks=[task])
crew.kickoff()
```
---
### ✅ Most Used Tools
***These are the tools you’ll probably use the most while developing and practicing.***
| Tool                               | Use Case                       |
| ---------------------------------- | ------------------------------ |
| `FileReadTool`                     | Read local files               |
| `PDFSearchTool`                    | Search and extract from PDFs   |
| `ScrapeWebsiteTool`                | Scrape entire websites         |
| `SeleniumScrapingTool`             | Scrape specific page elements  |
| `SerperDevTool`                    | Web search (via Google API)    |
| `WebsiteSearchTool`                | RAG-based site search          |
| `DallETool`, `CodeInterpreterTool` | AI generation & code execution |
---

## Best Practices

* Keep tools **simple** and **modular**
* Use descriptive names and clear docstrings
* Return meaningful, formatted output
* Avoid mixing side effects (like writing to DB and printing) in the same tool

---

## When to Use Tools

Use tools for any task that requires **external interaction** or **specialized processing** outside LLM reasoning:

* API calls
* Data transformation
* File operations
* CRUD operations on external systems

Agents should **reason**, but tools should **act**.

---

You’ll see real examples of tool usage in the `crewai_examples/` folders.

