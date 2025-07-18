# CrewAI

*CrewAI is a framewoek use to build powerful agent and multi agent orchatration*

While there are many frameworks and tools for building AI agents, CrewAI offers simple syntax and several built-in features essential for creating powerful agents.

- **CrewAI supports both Python and YAML. However, it officially recommends YAML for those from non-technical or less experienced programming backgrounds.**

- **Python is also beginner-friendly and has a very simple syntax. Using python has its own benifits, its give more control over the agent, easy to add logics, conditons, we can easily integrate other frameworks and tools in agent.**

> ***I will also share examples and practical use cases of YAML-based agents and explain when to use them. But our focus will be more on Python-based agents.***

----
### *Let's start with installation*

- *Make sure Python version ≥3.10 and <3.14 is installed on your system before installing CrewAI.*

- *You can use `pip` but i recommend usimg `uv` to install CrewAI, because CrewAI uses the uv as its dependency management and package handling tool. It simplifies project setup and execution, offering a seamless experience.*

    - If you don't have `uv` installed, then run this command on you terminal or powershell.

    - On macOS/Linux:
        Use curl to download the script and execute it with sh:

    ```bash
    curl -LsSf https://astral.sh/uv/install.sh | sh
    ```
    If your system doesn’t have curl, you can use wget:

    ```bash
    wget -qO- https://astral.sh/uv/install.sh | sh
    ```
    - On Windows:
    ```bash
    powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
    ```
### Let's install CrewAI:

- Run the following CrewAI cli commands:

```bash
uv tool install crewai
```
- To verify that crewai is installed, run:
```bash
uv tool list
```
- You should see something like:
```text
crewai v0.102.0
- crewai
```
>**If you need to update the crewai, run:**
```bash
uv tool install crewai --upgrade
```   
        
---
### Creating a new project using crewai cli commands

Before starting I want to tell you that use cli command when you are going to use yaml to build the agent. because the cli command will give you the basic boilerplate of your project. You just need to upgrade or add new feature.
>As mentioned earlier, YAML is best suited for building simple agents. You can use it for complex projects too, but it's not recommended — and soon you'll understand why.?

*Let's start*

- To generate Project Scaffolding

    - Run the crewai CLI command
    ```bash
    crewai create crew <your_project_name>
    ```
    - This creates a new project with the following structure:

        ```text
        my_project/
        ├── .gitignore
        ├── knowledge/
        ├── pyproject.toml
        ├── README.md
        ├── .env
        └── src/
            └── my_project/
                ├── __init__.py
                ├── main.py
                ├── crew.py
                ├── tools/
                │   ├── custom_tool.py
                │   └── __init__.py
                └── config/
                    ├── agents.yaml
                    └── tasks.yaml
        ```

- Customize Your Project

    - Your project will contain these essential files:

        - agents.yaml:- Define your AI agents and their roles
        - tasks.yaml:-	Set up agent tasks and workflows
        - .env:-	Store API keys and environment variables
        - main.py:-	Project entry point and execution flow
        - crew.py:-	Crew orchestration and coordination
        - tools/:-	Directory for custom agent tools
        - knowledge/:-	Directory for knowledge base

    * Start by editing agents.yaml and tasks.yaml to define your crew’s behavior.

    * Keep sensitive information like API keys in .env.        

- Run your crew

    - Before you run your crew, make sure to run:
    ```bash
    crewai install
    ```
    - If you need to install additional packages, use:
    ```bash
    uv add <package-name>
    ```
    - To run your crew, execute the following command in the root of your project:
    ```bash
    crewai run
    ```

---
### For python user.
- You don't need to use any cli command.
- Create a diretory

```bash
mkdir 'your project name'
cd your project name
```
- Create new files. 
```bash
touch agent.py
```
- Your directory Scaffold looks if you copy the crewai directory scaffold:
```text
my_project/
        ├── .gitignore
        ├── knowledge/
        ├── pyproject.toml
        ├── README.md
        ├── .env
        └── src/
            └── my_project/
                ├── __init__.py
                ├── main.py
                ├── crew.py
                ├── tools/
                │   ├── custom_tool.py
                │   └── __init__.py
                └── config/
                    ├── agents.py
                    └── tasks.py
```
* But you can create your own:
```text
my_project/
        ├── .gitignore
        ├── knowledge/
        ├── pyproject.toml
        ├── README.md
        ├── .env
        └── src/
            └── my_project/
                ├── __init__.py
                ├── main.py
                ├── crew.py
                ├── tools/
                │   ├── custom_tool.py
                │   └── __init__.py
                └── agents/
                └── tasks/
```
---

***Let's now learn about agents, tasks, crews, processes, and flows.. After that we will start coding our agents***

*We focus more on building agent instead of reading theorys. The problems I face and you will also while building the agents*

*For More theortical knowledge you can check the crewai officail docs*

> 📌 **Note:** This handbook focuses primarily on building agents using **Python**, due to its flexibility and control.

> 💡 However, if you're interested in YAML-based agents — especially useful for low-code workflows or contributing templates — you can jump directly to the [`yaml/`](./yaml/) folder once you've understood the core concepts.

> 👉 It's recommended to read through the theoretical explanations in the `core/` section before jumping into implementation in either Python or YAML.
