# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A Python package implementing document-related tools exposed through an MCP (Model Context Protocol) server interface for AI assistant integration.

## Essential Commands

### Setup
```bash
# Create virtual environment
uv venv
source .venv/bin/activate  # On Windows: .venv/Scripts/activate

# Install in development mode
uv pip install -e .
```

### Running
```bash
# Start the MCP server
uv run main.py
```

### Testing
```bash
# Run all tests
uv run pytest

# Run specific test file
uv run pytest tests/test_document.py

# Run specific test method
uv run pytest tests/test_document.py::TestBinaryDocumentToMarkdown::test_binary_document_to_markdown_with_docx
```

## Architecture

### MCP Server Pattern

The project uses FastMCP to expose Python functions as MCP tools:

1. `main.py` creates a FastMCP instance and registers tools via decorator
2. Tool functions are imported from `tools/` modules
3. Registration: `mcp.tool()(function_name)`
4. Server starts with `mcp.run()`

### Tool Definition Standards

**Critical**: All tools must follow this exact pattern:

```python
from pydantic import Field

def tool_name(
    param1: type = Field(description="Detailed description of this parameter"),
    param2: type = Field(description="Explain what this parameter does")
) -> ReturnType:
    """One-line summary of what the tool does.
    
    Detailed explanation of functionality spanning multiple lines
    if needed to fully explain the tool's purpose.
    
    When to use:
    - Specific scenario 1
    - Specific scenario 2
    
    When NOT to use:
    - Anti-pattern or limitation
    
    Examples:
    >>> tool_name(value1, value2)
    expected_output
    >>> tool_name(different_value)
    different_output
    """
    # Implementation
```

**Required elements:**
- Explicit type annotations for ALL function parameters and return type
- `Field(description="...")` from Pydantic for ALL parameters
- Docstring with one-line summary (first line)
- Detailed explanation of functionality
- "When to use:" section (and optionally "When NOT to use:")
- "Examples:" section with doctest-style input/output

### Adding New Tools

1. Create tool function in `tools/<module>.py` following the standards above
2. Import in `main.py`: `from tools.<module> import tool_function`
3. Register: `mcp.tool()(tool_function)`
4. Create test file: `tests/test_<module>.py`
5. Add test fixtures to `tests/fixtures/` if needed

### Module Organization

- **`main.py`**: MCP server entry point - imports and registers all tools
- **`tools/`**: Tool implementations (one or more functions per module)
- **`tests/`**: Test suite with `fixtures/` subdirectory for test data
- Tool registration is explicit in `main.py`, not automatic discovery
