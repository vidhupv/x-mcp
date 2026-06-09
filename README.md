# X(Twitter) MCP server

[![smithery badge](https://smithery.ai/badge/x-mcp)](https://smithery.ai/server/x-mcp)

An MCP server to create, manage and publish X/Twitter posts directly through Claude chat.

<a href="https://glama.ai/mcp/servers/jsxr09dktf">
  <img width="380" height="200" src="https://glama.ai/mcp/servers/jsxr09dktf/badge" alt="X(Twitter) Server MCP server" />
</a>

## Quick Setup

### Installing via Smithery

To install X(Twitter) MCP Server for Claude Desktop automatically via [Smithery](https://smithery.ai/server/x-mcp):

```bash
npx -y @smithery/cli install x-mcp --client claude
```

### Manual Installation
1. Clone the repository:
```bash
git clone https://github.com/vidhupv/x-mcp.git
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
        "run",
        "--project",
        "/path/to/x-mcp",
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
   - Go to [X API docs](https://docs.x.com/x-api)
   - Create a project
   - In User Authentication Settings: Set up with Read and Write permissions, Web App type
   - Set Callback URL to `http://localhost/` and Website URL to `http://example.com/`
   - Generate and copy all keys and tokens from Keys and Tokens section

6. Update the config file:
   - Replace `/path/to/x-mcp` with your actual repository path
   - Add your X/Twitter API credentials

7. Quit Claude completely and reopen it

If your client reports `unexpected argument '--directory'`, keep the `uv run`
command above. Older uv builds can reject `--directory` as a global argument,
while `uv run --project /path/to/x-mcp x-mcp` points uv at this project without
depending on that flag.

### OpenClaw MCP Setup

OpenClaw can save this server as a third-party MCP definition and keep the
working directory separate from uv arguments:

```bash
openclaw mcp add x-mcp \
  --command uv \
  --arg run \
  --arg x-mcp \
  --cwd /path/to/x-mcp \
  --env TWITTER_API_KEY=your_api_key \
  --env TWITTER_API_SECRET=your_api_secret \
  --env TWITTER_ACCESS_TOKEN=your_access_token \
  --env TWITTER_ACCESS_TOKEN_SECRET=your_access_token_secret

openclaw mcp status --verbose
openclaw mcp probe x-mcp --json
```

This MCP server stays focused on direct X/Twitter draft and publish workflows
with your own X API credentials. OpenClaw users who also need approval-gated
TweetClaw workflows for scraping tweets, searching tweet replies, follower
export, user lookup, direct messages, monitors, webhooks, giveaway draws, or
reviewed post/reply actions can install TweetClaw as a separate plugin:

```bash
openclaw plugins install npm:@xquik/tweetclaw@1.6.31
```

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
- If `uv --directory` fails, use the `uv run --project /path/to/x-mcp x-mcp`
  form shown above or update uv
- Verify all X/Twitter credentials are correct
- Check if the x-mcp path in config matches your actual repository location
