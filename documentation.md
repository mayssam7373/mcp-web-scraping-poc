# MCP Web Scraping POC Documentation (INCOMPLETE)

## Environment Setup (reference to README!)
- 
-
- Claude Sonnet/Opus 4 have MCP agent capabilities.
- Use OpenRouter for tokens (API key required).

## Provider Selection
- Cost and purchasing tokens for testing were initial challenges - different models have different capabilities.
-> (overall cost breakdown here)

## Installation Commands

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
uvx --from mcp-server-browser-use@latest python -m playwright install
uv tool install 'browser-use[cli]'
uv sync
uvx mcp-server-browser-use@latest
```

## Initial CLI Attempt
- Attempted to open Chromium via CLI, but it was not linked to the project - 
- Reference: [Browser Use CLI Docs](https://docs.browser-use.com/cli) (FAILED)

## Configuration (include example Claude file?)
- Update `claude_desktop_config.json` to enable internet access for Claude.
-> (include path on where to locate, both mac and windows)
    - Claude can search/read web content and orchestrate sub-agents.
    - Cannot yet interact with web forms (no tools yet)... where inspector comes in

## Example Config File - with Claude Sonnet 4 and Openrouter
```json
{ 
    "mcpServers": {
        "browser-use": {
            "command": "/Users/Your.Name/.local/bin/uvx",
            "args": ["mcp-server-browser-use@latest"],
            "env": {
                "MCP_LLM_OPENROUTER_API_KEY": "your-secret-key-here",
                "MCP_LLM_PROVIDER": "openrouter",
                "MCP_LLM_MODEL_NAME": "anthropic/claude-sonnet-4",
                "MCP_LLM_TEMPERATURE": "0.2",
                "MCP_BROWSER_HEADLESS": "false",
                "MCP_BROWSER_WINDOW_WIDTH": "1440",
                "MCP_BROWSER_WINDOW_HEIGHT": "1080",
                "MCP_AGENT_TOOL_USE_VISION": "true"
            }
        }
    }
}
```

## Inspector Setup
# make sure to select the inspector with the pre-filled token

```bash
npx @modelcontextprotocol/inspector \
  -e MCP_LLM_OPENROUTER_API_KEY=<your_key_here> \
  -e MCP_LLM_PROVIDER=openrouter \
  -e MCP_LLM_MODEL_NAME=anthropic/claude-sonnet-4 \
  -e MCP_LLM_TEMPERATURE=0.2 \
  -- /Users/Ella.Gonzalez/.local/bin/uvx mcp-server-browser-use@latest
```

## Troubleshooting

- Issues with OpenAI API keys -> make sure the key is the OPENROUTER KEY
- Ensure API keys are consistent across `.env` and config files.
- If Claude says it can't do something, REMIND Claude that it has the tools now

## Usage Tips

- Deploy the inspector, click connect, and check available tools.
- Remind Claude of its new abilities.
- Ask for browser agent or deep research tool usage.
- Provide form URLs or research topics.
    - note for deep research: you can request multiple sub-agents to work on seperate tasks!

## Example Form Filling Site

- [Test Form](https://testpages.herokuapp.com/styled/basic-html-form-test.html)
