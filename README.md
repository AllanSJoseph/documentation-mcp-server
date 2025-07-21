# Documentation MCP Server

A simple Python based **MCP (Model Context Protocol) Server** that provides documentation of some frameworks to an LLM Chatbot so that it will generate up to date results.

This is a MCP server project built with the guidance of Alejandro AO - Software & Ai 's Youtube Video Tutorial. 

Refer the video here [Learn MCP Servers with Python (EASY)](https://youtu.be/Ek8JHgZtmcI?si=JJOn3OnnUOjFEWu3)

## What this MCP Server does

- Provides a tool named **documentation**
- Uses [Serper](https://serper.dev/) a google search API to search for specific sections of documentations.
- Returns the documentation results from the below documentation sites.
    - Django Docs [Visit](https://docs.djangoproject.com/en/5.2/)
    - PostgreSQL Docs [Visit](https://www.postgresql.org/docs/)
    - Langchain Docs [Visit](https://python.langchain.com/docs)
    - llama-index [Visit](https://docs.llamaindex.ai/en/stable)
    - OpenAI docs [Visit](https://platform.openai.com/docs)
- Uses Beautiful Soup to parse the results


## How to Setup this MCP Server

### Prerequisites
- Python 3.8 or higher
- uv (Python package manager for MCP servers)
- Serper API key (you can get a free trial API key for first login with 2000 credits -> [Open Serper Homepage](https://serper.dev/))
- An MCP client that supports MCP servers eg: Claude Desktop, Cursor, WindSurf, etc.
- [Optional] Node.js (for inspecting the MCP server)


#### Setup uv

For Windows users:

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

For Linux/Mac users (Note: This server is ran and tested on Windows):

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

#### Setup Serper API Key,

Create a `.env` file in the project directory and add your Serper API key like

Copy the api key from your Serper account and paste it in the `.env` file as shown below:
```plaintext
SERPER_API_KEY=your_serper_api_key_here
```

1. Open an MCP Client (here I am using Claude Desktop).
2. Go To Claude Settings ```Ctrl + ,```.
3. Go to the Developer tab.
4. Click on ```Edit Config``` under Local MCP Servers.
5. It highlights the ```claude_desktop_config.json``` file, Open it in your favourite text editor.
6. Add the below code to the ```mcp_servers``` list in the JSON file save and close.

```json
"mcpServers": {
        "documentation": {
            "command": "uv",
            "args": [
                "--directory",
                "your_project_directory_path",
                "run",
                "main.py"
            ]
        }
    }
```
7. Restart Claude Desktop
8. Open a new chat and click on tools button on the chat box and you will see the **documentation** tool available.
9. Try a prompt like below:
```plaintext
How do I add and connect a PostgreSQL Database in Django? Use the documentation tool to get the answer.
```
10. The LLM will use the **documentation** tool to search for the answer and return it in the chat. 

Please Note that free version of Claude has a limitation of number of tokens or characters, so it may not give results as desired and can sometimes give you an error of exceeding the token limit. You can try with a paid version of Claude or use other MCP clients like Cursor, WindSurf, etc.

Refer the official MCP Documentation from Antropic for more details on how to setup MCP servers in your client [For Server Developers - Model Context Protocol](https://modelcontextprotocol.io/quickstart/server#python)



## Inspect this MCP Server

To inspect the tools and check if tools are working properly, run the below command in terminal on the project directory.

```bash
npx @modelcontextprotocol/inspector or uv run main.py
```

Thank you Alejandro AO for the amazing tutorial and guidance on building this MCP server.
