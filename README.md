# X(Twitter) MCP server

[![smithery badge](https://smithery.ai/badge/x-mcp)](https://smithery.ai/server/x-mcp)

An MCP server to create, manage and publish X/Twitter posts directly through Claude chat.

## Quick Setup

### Installing via Smithery

To install X(Twitter) MCP Server for Claude Desktop automatically via [Smithery](https://smithery.ai/server/x-mcp):

```bash
npx -y @smithery/cli install x-mcp --client claude
```

### Manual Installation
1. Clone the repository:
```bash
git clone https://github.com/yourusername/x-mcp.git
```

2. Install UV globally using Homebrew in Terminal:
```bash
brew install uv
```

3. Create claude_desktop_config.json:
   - For MacOS: Open directory `~/Library/Application Support/Claude/` and create the file inside it
   - For Windows: Open directory `%APPDATA%/Claude/` and create the file inside it

4. Add this configuration to claude_desktop_config.json:
```json
{
  "mcpServers": {
    "x_mcp": {
      "command": "uv",
      "args": [
        "--directory",
        "/path/to/x-mcp",
        "run",
        "x-mcp"
      ],
      "env": {
        "TWITTER_API_KEY": "your_api_key",
        "TWITTER_API_SECRET": "your_api_secret",
        "TWITTER_ACCESS_TOKEN": "your_access_token",
        "TWITTER_ACCESS_TOKEN_SECRET": "your_access_token_secret"
      }
    }
  }
}
```

5. Get your X/Twitter API credentials:
   - Go to [X API Developer Portal](https://developer.x.com/en/products/x-api)
   - Create a project
   - In User Authentication Settings: Set up with Read and Write permissions, Web App type
   - Set Callback URL to `http://localhost/` and Website URL to `http://example.com/`
   - Generate and copy all keys and tokens from Keys and Tokens section

6. Update the config file:
   - Replace `/path/to/x-mcp` with your actual repository path
   - Add your X/Twitter API credentials

7. Quit Claude completely and reopen it

## Usage Examples

* "Tweet 'Just learned how to tweet through AI - mind blown! 🤖✨'"
* "Create a thread about the history of pizza"
* "Show me my draft tweets"
* "Publish this draft!"
* "Delete that draft"

## Troubleshooting

If not working:
- Make sure UV is installed globally (if not, uninstall with `pip uninstall uv` and reinstall with `brew install uv`)
- Or find UV path with `which uv` and replace `"command": "uv"` with the full path
- Verify all X/Twitter credentials are correct
- Check if the x-mcp path in config matches your actual repository location
