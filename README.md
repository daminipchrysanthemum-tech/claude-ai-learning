📖 Overview

This project was completed as part of the Claude 101 with Amazon Bedrock course on the Anthropic Learning Academy. The module covers the Model Context Protocol (MCP) — an open standard that allows AI models like Claude to securely connect to external tools, data sources, and services.


🧠 What I Learned

What MCP is and why it matters for building AI-powered applications
The difference between Tools, Resources, and Prompts in the MCP architecture
How to build a custom MCP Server that exposes document tools to an AI model
How to build an MCP Client that connects to the server and interacts with Claude
How to use the MCP Inspector (v0.21.2) to debug and test MCP servers interactively
How MCP enables Claude to read, edit, and reason over real documents


🏗️ Architecture

MCP Overview
The diagram below shows how MCP connects Claude to external tools and data sources:


<img width="1259" height="382" alt="MCP" src="https://github.com/user-attachments/assets/058eb6a3-c2a2-4953-9851-9b9f795b5e0e" />



🖥️ Building the MCP Server

Part 1 — Server Setup
Setting up the MCP server foundation, registering the server, and configuring transport:

<img width="1890" height="897" alt="MCP Server (Part 2)" src="https://github.com/user-attachments/assets/57adb26d-a7b8-40c2-87a7-5bb2cbfd8a79" />


<img width="1889" height="874" alt="MCP Server (Part 1)" src="https://github.com/user-attachments/assets/77320612-f04b-48c2-9de4-07f52f8a17c0" />



📁 Defining & Accessing Resources

Defining Resources
Exposing documents as MCP resources so Claude can discover and read them:

<img width="1785" height="933" alt="Defining Resources" src="https://github.com/user-attachments/assets/f4b688bc-07e1-4ee8-9011-48b59abc868e" />


Accessing Resources in the MCP Inspector
Testing the docs://documents resource and fetch_doc resource template via the MCP Inspector — the resource read returns the document content as text/plain:

<img width="1031" height="396" alt="Accessing Resources" src="https://github.com/user-attachments/assets/f9b2c671-20d8-46c3-b673-c712311a34b4" />



💬 Defining & Using Prompts

Defining Prompts (Code)
Implementing the format prompt that rewrites a document in Markdown syntax, accepting a doc_id parameter:


<img width="1041" height="552" alt="Defining Prompts" src="https://github.com/user-attachments/assets/1028acf3-2814-4f89-9622-2353a59a0c21" />


Defining Prompts (MCP Inspector)
Testing the format prompt in the MCP Inspector — selecting a doc_id and calling Get Prompt returns a structured message object ready for Claude:


<img width="1787" height="959" alt="Defining Prompts (MCP)" src="https://github.com/user-attachments/assets/0288a367-512a-4cee-b402-212d199e9165" />


Prompts in Clients

Using the /format slash command in the client to trigger the prompt — Claude reads the document and returns it fully reformatted in Markdown with headings, lists, and a table:


<img width="1056" height="920" alt="Prompts In Clients" src="https://github.com/user-attachments/assets/b45bf4d8-e577-4535-8432-2335b502dfa3" />



🤖 Implementing the MCP Client
Building the Python client that connects to the MCP server via STDIO, discovers available tools, and passes them to Claude through the Anthropic API:

<img width="1415" height="707" alt="Implementing a client" src="https://github.com/user-attachments/assets/4c48ddc3-906f-4c89-92af-bda97e2dc5f0" />



🧪 Live Demo — Client in Action

Querying a Document
Asking Claude what's in the report.pdf — Claude uses the read_doc_contents tool and returns a natural language answer:

> Whats in the @report.pdf document
Response:
The report.pdf document details the state of a 20m condenser tower.

Reformatting a Document with a Prompt
Using the format prompt via the client to reformat report.pdf in Markdown syntax:

> reformat the @report.pdf in markdown syntax
Response:
# Condenser Tower Report
## Overview
The report details the state of a 20m condenser tower.



🧠 Reasoning Test — Classic Riddle

To test Claude's reasoning ability through the MCP client, I submitted the classic "Missing Dollar" hotel riddle.
Initial Solution
Claude correctly identifies that there is no missing dollar and walks through the full accounting:

Initial Solution
Claude correctly identifies that there is no missing dollar and walks through the full accounting:


<img width="1413" height="800" alt="reasoning_test_solution" src="https://github.com/user-attachments/assets/2d84d72a-d439-4aba-b096-83a8c98061be" />


Follow-up — Why the Equation is Misleading
Pushing further by asking Claude to explain the grammatically correct way to phrase the equation so it's not misleading:


<img width="1408" height="537" alt="reasoning_test_followup" src="https://github.com/user-attachments/assets/fcce3fa3-74bf-4288-a22d-8f7d2e30468e" />


Claude explained that the word "plus" is the problem — the $2 the bellhop kept is already included in the $27 paid, so you should say "which includes" or "minus", not "plus". The puzzle tricks you by switching perspectives mid-calculation.



🛠️ Tools, Resources & Prompts Summary
TypeNameDescriptionToollist_documentsLists all available document IDsToolread_doc_contentsReads a document and returns it as a stringTooledit_documentReplaces a string in a document with new textResourcedocs://documentsStatic list of all documentsResource Templatefetch_docFetches a specific document by IDPromptformatRewrites a document in Markdown format


⚙️ Tech Stack
TechnologyPurposePython 3.14Server and client implementationuvPython package runnerMCP SDK (mcp)MCP server/client frameworkAnthropic APIClaude model integrationMCP Inspector v0.21.2Server debugging and testing UIWindows / VS CodeDevelopment environment


🚀 How to Run

1. Set up a virtual environment

bash
python -m venv .venv
.venv\Scripts\activate.bat       # Windows


2. Run the MCP Server (for Inspector testing)

bash
npx @modelcontextprotocol/inspector uv run mcp_server.py
Opens MCP Inspector at http://localhost:6274


3. Run the MCP Client (chat with Claude)
   
bash
uv run main.py



📂 Repo Structure

mcp/
├── mcp_server.py          # MCP server with tools, resources, and prompts
├── mcp_client.py          # MCP client (connection layer)
├── main.py                # Interactive CLI client powered by Claude
├── documents/             # Sample documents (report.pdf, deposition.md, plan.md, etc.)
├── screenshots/           # All module screenshots
│   ├── MCP.png
│   ├── MCP_Server__Part_1_.png
│   ├── MCP_Server__Part_2_.png
│   ├── Defining_Resources.png
│   ├── Accessing_Resources.png
│   ├── Defining_Prompts.png
│   ├── Defining_Prompts__MCP_.png
│   ├── Prompts_In_Clients.png
│   ├── Implementing_a_client.png
│   ├── reasoning_test_solution.png
│   └── reasoning_test_followup.png
└── README.md



📚 Course
Anthropic Learning Academy — Claude 101 with Amazon Bedrock
Module: Model Context Protocol (MCP)
Learn more: https://www.anthropic.com



🏅 Key Takeaways
MCP standardizes how AI models connect to external context — think of it as a "USB-C port for AI."
Tools let Claude take actions; Resources give Claude data; Prompts provide reusable interaction templates
A well-designed MCP server makes Claude dramatically more capable in specialized workflows
The MCP Inspector is invaluable for iterative development and debugging
Claude can reason through multi-step problems and follow-up questions with nuance
Built as part of structured AI learning — demonstrating hands-on experience with Claude, the Anthropic API, and the Model Context Protocol.









