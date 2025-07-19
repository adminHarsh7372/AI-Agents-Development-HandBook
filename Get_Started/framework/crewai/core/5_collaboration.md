# Collaboration 🤝
One of the most powerful things about CrewAI is how it lets multiple agents collaborate with each other like a real-world team. This isn’t just about parallel execution—it’s about real teamwork.

---
#### What Does "Collaboration" Mean Here?
**In CrewAI, collaboration means agents:**

   - Can depend on each other’s outputs
   - Can have a shared goal and work on sub-tasks
   -  Can pass context across tasks
   -  Follow a defined task order that simulates coordinated workflow

It’s not just about automation. It’s about distributed intelligence.

----

### How Agent Collaboration Work
When allow_delegation=True, CrewAI automatically provides agents with two powerful tools:

1. Delegate Work Tool - 
  - Agent automatically gets this tool:
  - Delegate work to coworker(task: str, context: str, coworker: str)

2. Ask Question Tool - 
  - Agent automatically gets this tool:
  - Ask question to coworker(question: str, context: str, coworker: str)

---
### Example:
1. **Allow Delegation**
```python
from crewai import Agent, Crew, Task, Process

researcher = Agent(
    role="Research Specialist",
    goal="Find accurate, up-to-date information on any topic",
    backstory="""You're a meticulous researcher with expertise in finding 
    reliable sources and fact-checking information across various domains.""",
    allow_delegation=True,
    verbose=True
)

writer = Agent(
    role="Content Writer",
    goal="Create engaging, well-structured content",
    backstory="""You're a skilled content writer who excels at transforming 
    research into compelling, readable content for different audiences.""",
    allow_delegation=True,
    verbose=True
)

editor = Agent(
    role="Content Editor",
    goal="Ensure content quality and consistency",
    backstory="""You're an experienced editor with an eye for detail, 
    ensuring content meets high standards for clarity and accuracy.""",
    allow_delegation=True,
    verbose=True
)

# Create a task that encourages collaboration
article_task = Task(
    description="""Write a comprehensive 1000-word article about 'The Future of AI in Healthcare'.
    
    The article should include:
    - Current AI applications in healthcare
    - Emerging trends and technologies  
    - Potential challenges and ethical considerations
    - Expert predictions for the next 5 years
    
    Collaborate with your teammates to ensure accuracy and quality.""",
    expected_output="A well-researched, engaging 1000-word article with proper structure and citations",
    agent=writer  # Writer leads, but can delegate research to researcher
)

# Create collaborative crew
crew = Crew(
    agents=[researcher, writer, editor],
    tasks=[article_task],
    process=Process.sequential,
    verbose=True
)

result = crew.kickoff()
```

2. **Context** - 
To get the output of the first agent 

```python
research_task = Task(
    description="Research the latest developments in quantum computing",
    expected_output="Comprehensive research summary with key findings and sources",
    agent=researcher
)

writing_task = Task(
    description="Write an article based on the research findings",
    expected_output="Engaging 800-word article about quantum computing",
    agent=writer,
    context=[research_task]  # Gets research output as context
)

editing_task = Task(
    description="Edit and polish the article for publication",
    expected_output="Publication-ready article with improved clarity and flow",
    agent=editor,
    context=[writing_task]  # Gets article draft as context
)
```
3. **Hierarchical Collaboration** - 
For complex projects, use a hierarchical process with a manager agent:
```python
from crewai import Agent, Crew, Task, Process

# Manager agent coordinates the team
manager = Agent(
    role="Project Manager",
    goal="Coordinate team efforts and ensure project success",
    backstory="Experienced project manager skilled at delegation and quality control",
    allow_delegation=True,
    verbose=True
)

# Specialist agents
researcher = Agent(
    role="Researcher",
    goal="Provide accurate research and analysis",
    backstory="Expert researcher with deep analytical skills",
    allow_delegation=False,  # Specialists focus on their expertise
    verbose=True
)

writer = Agent(
    role="Writer", 
    goal="Create compelling content",
    backstory="Skilled writer who creates engaging content",
    allow_delegation=False,
    verbose=True
)

# Manager-led task
project_task = Task(
    description="Create a comprehensive market analysis report with recommendations",
    expected_output="Executive summary, detailed analysis, and strategic recommendations",
    agent=manager  # Manager will delegate to specialists
)

# Hierarchical crew
crew = Crew(
    agents=[manager, researcher, writer],
    tasks=[project_task],
    process=Process.hierarchical,  # Manager coordinates everything
    manager_llm="gpt-4o",  # Specify LLM for manager
    verbose=True
)
```

---
### Best Practice
1. Clear Role Definition
2. Strategic Delegation Enabling
3. Context Sharing
4. Clear Task Descriptions

>***We explore and build many more projects using Allow Delegation, Context, and Hierarchical features in [crewai_example]()***