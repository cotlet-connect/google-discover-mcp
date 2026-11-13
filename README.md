# How to connect Google Discover to Claude Code, ChatGPT and any AI agent

**Yes, Claude, ChatGPT and other AI agents can work with Google Discover.** Google has no official API for the Discover feed. Cotlet.dev reads country feeds and checks whether your domain appears, so your AI agent can monitor Discover in plain words.

## What you can ask

> Read the Google Discover feed for the US and list the first 10 cards.

> Is example.com in the Discover feed in Germany right now?

> Compare the Discover feeds for the US and UK and show stories that differ.

> Watch mysite.com every hour and report when a new card appears.

> List the videos Google Discover is showing in Poland today.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its Google Discover tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"google-discover":{"command":"uvx","args":["google-discover-cotlet-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t google-discover-mcp .
docker run -i --rm -e COTLET_API_KEY google-discover-mcp
```

Tools: `google_discover_guide`, `google_discover_status`, `google_discover_open`, `google_discover_read`, `google_discover_click`, `google_discover_type`, `google_discover_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install google-discover-cotlet-mcp        # or run it once: uvx google-discover-cotlet-mcp connect
google-discover-cotlet-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 google_discover_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 google_discover_agent.py status    # is Google Discover ready in your Cotlet.dev account
python3 google_discover_agent.py guide     # Google Discover screens and sign-in link
python3 google_discover_agent.py read      # open Google Discover, read the page, close the browser
python3 google_discover_agent.py tools     # list Cotlet.dev tools
python3 google_discover_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Google Discover users

**Does Google Discover have an API?**

Google has no official API for the Discover feed. Cotlet.dev provides hosted Google Discover tools that read country feeds and check domains through MCP and REST.

**How do I connect Google Discover to ChatGPT?**

Add Cotlet.dev as an app in ChatGPT (Settings → Apps, connector URL `https://cotlet.dev/mcp/v1`), then ask ChatGPT to read a country feed or check your domain. No Google account is needed.

**Is there a way to use Claude with Google Discover?**

Yes. In Claude Code run the one-line `claude mcp add` command above; in the Claude app add `https://cotlet.dev/mcp/v1` as a custom connector. Claude can then read the feed and check domains.

**Is there a Google Discover MCP server?**

Google has no official Discover MCP server. Cotlet.dev is a hosted MCP server with tools for reading country feeds and checking domain appearances.

## Find it on

- [Google Discover on Cotlet.dev](https://cotlet.dev/integrations/google-discover-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=google-discover&utm_content=find)
- [PyPI package google-discover-cotlet-mcp](https://pypi.org/project/google-discover-cotlet-mcp/)
- [Odel](https://odel.app/modules/cotlet/google-discover)
- [mcpbeat](https://mcpbeat.com/mcp-servers/cotlet/google-discover/)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-google-discover-to-ai-agents-guide)

## Also works with


- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/google-discover-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=google-discover

Start free: https://cotlet.dev/signup?app=google-discover&utm_source=github&utm_medium=readme&utm_campaign=google-discover
