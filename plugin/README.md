# DDX Plugin for Claude Code

MCP plugin that connects Claude Code and Claude Desktop to MedScout's DDX platform — Voice of Customer (VOC) and Go-to-Market (GTM) account research.

## Setup

### 1. Get Your API Token

1. Log into DDX at `https://ddx.medscout.io`
2. Visit **[/settings/mcp/](https://ddx.medscout.io/settings/mcp/)** — your token is auto-created
3. Copy the token

### 2. Set the Token

Add to your shell profile (`~/.zshrc` or `~/.bashrc`):

```bash
export DDX_API_TOKEN="<your-token>"
```

Then reload your shell (`source ~/.zshrc`) or open a new terminal.

### 3. Connect

**Claude Code:**
```
/plugin marketplace add medscout-dev/ddx-claude-plugin
/plugin install ddx@medscout
```

**Claude Desktop:**
Copy the JSON config from the [setup page](https://ddx.medscout.io/settings/mcp/) into your `claude_desktop_config.json`.

## What You Get

| Feature | Claude Code | Claude Desktop |
|---------|:-----------:|:--------------:|
| 21 MCP tools | Yes | Yes |
| 7 resources | Yes | Yes |
| 5 prompts | Yes | Yes |
| 7 skills (`/submit-voc`, etc.) | Yes | No |
| VOC Analyst agent | Yes | No |
| GTM Research Analyst agent | Yes | No |

## Available Skills

Skills are guided workflows you trigger with slash commands in Claude Code.

### VOC Skills
| Skill | What it Does |
|-------|-------------|
| `/submit-voc` | Gathers details, searches for duplicates, then creates or matches to an existing VOC item |
| `/analyze-feedback` | Paste meeting notes, transcripts, or emails — extracts structured VOC items with duplicate matching |
| `/voc-search` | Search items, browse themes, analyze trends, query transcripts, view company feedback history |
| `/merge-voc` | Merge two VOC items — AI-suggested content, target recommendation, full relationship transfer |

### Platform Skills
| Skill | What it Does |
|-------|-------------|
| `/feedback` | Submit feedback or a bug report about DDX directly to the #feedback-ddx Slack channel |

### GTM Skills
| Skill | What it Does |
|-------|-------------|
| `/research-search` | Search research packs, read report content, check request status |
| `/generate-research` | End-to-end research generation: transcripts → reports → published pack → completed request |

## Available Tools

### VOC Management
- `search_voc_items` — Keyword search across title, description, and problem statement
- `find_similar_voc_items` — Semantic similarity search via AI embeddings
- `get_voc_item` — Full item details with companies, themes, tags, and comments
- `create_voc_item` — Create a new VOC item (auto-generates embeddings)
- `add_company_to_voc_item` — Associate a company with priority and context
- `add_attachment_to_voc_item` — Upload a file (image, PDF, etc.) to a VOC item from a URL
- `search_companies` — Find companies by name, filter by health status

### Analytics
- `list_themes` — Browse themes with business metrics (ARR, company count, health)
- `get_theme_details` — Deep dive into a theme with items, companies, sub-themes
- `get_voc_analytics` — Flexible analytics: group by theme/company/status/tag, compare periods, semantic filter

### Transcripts
- `query_transcripts` — Filter transcripts by company, team, date; keyword search across full text
- `search_transcripts_semantic` — Find transcripts by meaning using AI embeddings

### Bulk Processing
- `parse_feedback` — Parse unstructured text into structured VOC proposals with automatic deduplication

### Platform Feedback
- `submit_platform_feedback` — Post feedback or bug reports about DDX to #feedback-ddx Slack channel

### VOC Merge
- `suggest_merge` — AI-suggested merge content with target recommendation and relationship preview
- `execute_merge` — Execute the merge with full relationship transfer (companies, themes, tags, features, attachments, comments, mentions)

### GTM Research
- `list_research_packs` — List research packs with company and report summaries
- `get_research_report` — Get full report content (fingerprint, AE briefing, CS briefing, full pack)
- `publish_research_pack` — Create or update a research pack with reports
- `list_research_requests` — List pending/submitted research requests
- `complete_research_request` — Mark a request as completed and link to a pack

## Agents

### VOC Analyst
Autonomous agent that answers product strategy questions using real customer data. Automatically selects the right tools, gathers data across multiple dimensions, and synthesizes findings into actionable insights with specific numbers (ARR, company count, health status).

Triggered automatically when you ask broad product questions like:
- "What are customers most frustrated about?"
- "Which themes have the highest at-risk ARR?"
- "Compare CS vs Sales feedback themes"

### GTM Research Analyst
Autonomous agent that generates account intelligence from call transcripts and company data. Processes research requests end-to-end: gathers transcript intelligence, generates reports, publishes packs, and completes requests with Slack notifications.

Triggered automatically when you ask about account research:
- "Generate research for Acme Corp"
- "What research requests are pending?"
- "Show me the latest research packs"
- "Process the next pending research request"

## Example Queries

You can ask questions in natural language — no slash commands required:

```
"What are the top VOC themes by ARR?"
"Search for items about profile usability"
"What has Acme Corp requested?"
"Show me the fingerprint for acme-corp"
"What research requests are pending?"
"Generate research for company XYZ"
"What calls mentioned data exports this month?"
"Parse this meeting notes into VOC items: ..."
"Merge VOC items 123 and 456"
```

## How It Works

The plugin connects to DDX's MCP server at `https://ddx.medscout.io/mcp` using Streamable HTTP transport. Your `DDX_API_TOKEN` is sent as a Bearer token in the Authorization header. The MCP server runs inside Django, accessing the same database as the DDX web app — so data is always live and consistent.

## Troubleshooting

**"Missing or malformed Authorization header" (401)**
- Check that `DDX_API_TOKEN` is set: `echo $DDX_API_TOKEN`
- Reload your shell after adding it to `.zshrc`/`.bashrc`

**"Invalid or inactive API token" (401)**
- Your token may have been regenerated. Visit [/settings/mcp/](https://ddx.medscout.io/settings/mcp/) to get your current token.

**Plugin not finding tools**
- Verify the plugin is installed: `claude plugin list`
- Reinstall if needed: `claude plugin remove ddx` then `/plugin install ddx@medscout`

**CI/scripting environments (no browser)**
- For headless environments, use a static API token instead:
  ```bash
  claude mcp add --transport http ddx https://ddx.medscout.io/mcp \
    --header "Authorization: Bearer <your-token>"
  ```
- Get your token from [/settings/mcp/](https://ddx.medscout.io/settings/mcp/)

## Architecture

```
plugin/
├── .claude-plugin/
│   └── plugin.json         # Plugin metadata (name, version, author)
├── .mcp.json               # MCP server connection config (HTTP URL + auth)
├── skills/
│   ├── submit-voc/         # /submit-voc skill
│   ├── analyze-feedback/   # /analyze-feedback skill
│   ├── voc-search/         # /voc-search skill
│   ├── merge-voc/          # /merge-voc skill
│   ├── feedback/           # /feedback skill
│   ├── research-search/    # /research-search skill
│   └── generate-research/  # /generate-research skill
├── agents/
│   ├── voc-analyst.md      # VOC Analyst autonomous agent
│   └── gtm-research-analyst.md  # GTM Research Analyst autonomous agent
└── README.md               # This file
```

The `.mcp.json` points to the production MCP server. The `${DDX_API_TOKEN}` variable is expanded by Claude Code at runtime from your environment.
