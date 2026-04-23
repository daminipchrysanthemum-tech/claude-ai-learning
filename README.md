🤖 Claude Code in Action

Used Claude Code directly inside VS Code as an agentic coding assistant — not just for autocomplete, but for reading the codebase, planning tests, writing implementations, and running verifications end to end.


Part 1 — Initializing the Project Context
Running /init with a custom instruction to include notes on MCP tool definitions from the README. Claude Code read the repository and auto-generated a CLAUDE.md file in 102 lines — capturing the FastMCP server pattern, Pydantic Field annotation standards, tool registration flow, and module organization without any manual input.

## Running

```bash
# Start the MCP server
uv run main.py
```

## Testing

```bash
# Run all tests
uv run pytest
```

## Development

### Tool Definitions

Tools are defined as Python functions and registered with the MCP server:

```python
mcp.tool()(my_function)
```

Tool descriptions should:

- Begin with a one-line summary
- Provide detailed explanation of functionality
- Explain when to use (and not use) the tool
- Include usage examples with expected input/output

Use `Field` from pydantic for parameter descriptions:

```python
from pydantic import Field

def my_tool(
    param1: str = Field(description="Detailed description of this parameter"),
    param2: int = Field(description="Explain what this parameter does")
) -> ReturnType:
    """Comprehensive docstring here"""
    # Implementation
```
