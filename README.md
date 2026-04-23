## 🤖 Claude Code in Action

Used Claude Code directly inside VS Code as an agentic coding assistant — not just for autocomplete, but for reading the codebase, planning tests, writing implementations, and running verifications end to end.


Part 1 — Initializing the Project Context
Running /init with a custom instruction to include notes on MCP tool definitions from the README. Claude Code read the repository and auto-generated a CLAUDE.md file in 102 lines — capturing the FastMCP server pattern, Pydantic Field annotation standards, tool registration flow, and module organization without any manual input.


<img width="1407" height="791" alt="Claude Code In Action (Part 1)" src="https://github.com/user-attachments/assets/ff9fe753-b572-460c-b88e-9d81cd663667" />


---


Part 2 — Reading and Auditing Source Files
Asked Claude Code to read tools/document.py and tools/math.py simultaneously. It analyzed both files and flagged that document.py was missing Pydantic Field descriptions and the complete docstring format specified in CLAUDE.md — catching a standards violation before any new code was written.


<img width="1391" height="624" alt="Claude Code In Action (Part 2)" src="https://github.com/user-attachments/assets/405bd378-747f-461e-8909-ead78092408d" />


---


Part 3 — Test Planning Before Writing Code
Before writing a single line, I asked Claude Code to think through tests for a new document_path_to_markdown tool. It returned 20 structured tests across four categories — Core Functionality, File Handling, File Type, Content Variation, and Integration — and asked for approval before proceeding.


<img width="1388" height="918" alt="Claude Code In Action (Part 3)" src="https://github.com/user-attachments/assets/54fb8a28-0f4e-4166-9667-677a30c7535d" />


---


Part 4 — Implementing the Tests
Claude Code implemented tests 1–5, reusing existing fixtures (mcp_docs.docx and mcp_docs.pdf) and following the existing test file patterns exactly. Tests were ready to run as soon as the function was implemented.


<img width="1323" height="276" alt="Claude Code In Action (Part 4)" src="https://github.com/user-attachments/assets/29f05984-8c0c-4e7d-a03b-b998c17ac68e" />


---


Part 5 — Full Implementation, All Tests Passing ✅
Claude Code implemented the document_path_to_markdown function in tools/document.py with proper Pydantic Field descriptions, complete docstrings, file validation, error handling (FileNotFoundError, IsADirectoryError, and ValueError), and registered it with the MCP server in main.py. All 8 tests pass (3 existing + 5 new).


<img width="1322" height="520" alt="Claude Code In Action (Part 5)" src="https://github.com/user-attachments/assets/fcdc8b2a-53f2-4547-ba4f-bad6f33b34c4" />


---


## 🔌 Enhancements with MCP Servers
Used the newly implemented document_path_to_markdown tool through Claude Code to convert a real DOCX file (tests/fixtures/mcp_docs.docx) to markdown. The conversion extracted live MCP documentation content, including the full MCP primitives table — Prompts, Resources, and Tools — confirming the tool works correctly end-to-end.


<img width="1049" height="490" alt="Enhancements with MCP Servers" src="https://github.com/user-attachments/assets/1595c65e-5285-4a97-a501-ffad0eeb59e8" />


---


## ⚡ Parallelizing Claude Code with Git Worktrees
Set up Git worktrees so Claude Code can work on multiple features simultaneously on separate branches without conflicts. Claude Code verified the worktree didn't exist, created .trees/feature_a on a new feature_a branch, symlinked the shared .venv, and launched a second VS Code window — all in one command sequence.



<img width="1260" height="587" alt="Parallelizing Claude Code" src="https://github.com/user-attachments/assets/0b151707-b1cd-498c-8a06-26e107541efe" />


---


## 🛠️ Claude Code Workflow Summary

| Type | Name | Description |
|------|------|-------------|
| **Initialization** | `/init` | Auto-generated a 102-line CLAUDE.md capturing FastMCP server pattern, Pydantic Field annotation standards, tool registration flow, and module organization |
| **File Audit** | `Read document.py + math.py` | Analyzed both source files simultaneously and flagged a standards violation in document.py before any new code was written |
| **Test Planning** | `document_path_to_markdown tests` | Planned 20 tests across Core Functionality, File Handling, File Type, Content Variation, and Integration categories before writing any code |
| **Test Implementation** | `Tests 1–5` | Implemented 5 tests reusing existing fixtures (mcp_docs.docx, mcp_docs.pdf) and following existing project patterns |
| **Full Implementation** | `document_path_to_markdown tool` | Built the function with Pydantic Field descriptions, complete docstrings, file validation, error handling, and MCP server registration — all 8 tests passing |
| **MCP Enhancement** | `DOCX to Markdown conversion` | Used the new tool to convert a real DOCX file to markdown, extracting live MCP documentation, including the full primitives table |
| **Parallelization** | `Git worktree setup` | Created .trees/feature_a on a new branch, symlinked shared .venv, and launched a second VS Code window for simultaneous development


---


## ⚙️ Tech Stack


| Layer | Technology |
|------------|---------|
| Agentic Coding Tool | Claude Code |
| Editor | VS Code |
| Language | Python 3.14 |
| Package Runner | uv |
| MCP Framework | FastMCP |
| Data Validation | Pydantic |
| Document Conversion | MarkItDown |
| Version Control | Git + Git Worktrees |
| Testing | pytest |


