# MCP Server Prompt

A Model Context Protocol (MCP) server that provides tools to help developers bootstrap and build MCP server projects with best practices.

## Overview

This MCP server provides helpful tools for:
- **Initializing new MCP projects** with proper structure and configuration
- **Learning MCP best practices** for development
- **Setting up uv-based Python environments** for fast dependency management

## Features

### Tools

#### `initialize_mcp_project`
Generates complete setup instructions and project structure for a new MCP server.

**Parameters:**
- `project_name` (optional): Name of the MCP project to create (default: "new-mcp-server")

**Returns:**
- Detailed project structure
- Step-by-step setup instructions
- Template code for getting started
- Testing guidance with MCP Inspector

#### `mcp_project_best_practices`
Provides comprehensive best practices for developing MCP servers.

**Returns:**
- Project organization guidelines
- Type hints and docstring standards
- Dependency management with uv
- Testing strategies
- FastMCP decorator usage patterns

## Installation

### Prerequisites
- Python 3.14 or higher
- [uv](https://github.com/astral-sh/uv) - Fast Python package installer (install with `brew install uv`)

### Setup

1. Clone the repository:
```bash
git clone <repository-url>
cd mcp-server-prompt
```

2. Install dependencies with uv:
```bash
uv sync
```

## Usage

### Running the Server

Start the MCP server:
```bash
uv run python mcp-server-prompt.py
```

The server runs on streamable HTTP transport and waits for MCP client connections.

### Testing with MCP Inspector

Test the server interactively:
```bash
uv run mcp dev mcp-server-prompt.py
```

This opens the MCP Inspector in your browser where you can:
- Test tools with different parameters
- View server logs in real-time
- Debug before integrating with clients

### Configuring with Claude Desktop

This server uses **streamable-http transport** instead of stdio. Add to your Claude Desktop configuration (`~/Library/Application Support/Claude/claude_desktop_config.json` on macOS):

```json
{
  "mcpServers": {
    "mcp-server-prompt": {
      "url": "http://localhost:8000"
    }
  }
}
```

**Note:** You need to start the server manually before using it with Claude Desktop:
```bash
uv run python mcp-server-prompt.py
```

The server will run on `http://localhost:8000` by default (or the port configured in your FastMCP setup).

#### Alternative: Auto-start with Git URL

If you prefer Claude Desktop to manage the server lifecycle, you can configure it to fetch from a git repository:

```json
{
  "mcpServers": {
    "mcp-server-prompt": {
      "command": "uvx",
      "args": [
        "run",
        "--from",
        "git+https://github.com/see.d/mcp-server-prompt.git",
        "mcp-server-prompt"
      ]
    }
  }
}
```

Replace the git URL with your repository URL.

## Example Usage

Once configured with an MCP client like Claude Desktop, you can:

1. **Start a new MCP project:**
   - Ask: "Initialize a new MCP server project called 'weather-api'"
   - The tool will provide complete setup instructions

2. **Learn best practices:**
   - Ask: "What are the best practices for MCP server development?"
   - Get comprehensive guidelines for structure, testing, and deployment

## Development

### Project Structure

```
mcp-server-prompt/
├── mcp-server-prompt.py   # Main server implementation
├── main.py                 # Alternative entry point
├── pyproject.toml          # Project metadata and dependencies
├── uv.lock                 # Dependency lockfile
└── README.md               # This file
```

### Adding New Tools

To add new tools to the server:

1. Define a new function with the `@mcp.tool()` decorator
2. Add type hints for all parameters and return type
3. Write a clear docstring describing the tool's purpose
4. Test with MCP Inspector before deployment

Example:
```python
@mcp.tool()
def my_new_tool(param: str) -> str:
    """
    Clear description of what this tool does.
    
    Args:
        param: Description of the parameter
    """
    return f"Result: {param}"
```

## Dependencies

- **mcp[cli]** (>=1.25.0): Model Context Protocol SDK with CLI tools

## License

[Add your license here]

## Contributing

[Add contributing guidelines here]

## Support

For issues or questions:
- Open an issue in the repository
- Refer to [MCP documentation](https://modelcontextprotocol.io/)
