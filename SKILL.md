---
name: project-news-monitor
description: Set up and run personalized daily news monitoring for user-defined domains, then match and notify about items that impact the users current projects or work content. Trigger on requests for project-aware news alerts, industry monitoring tied to work, daily domain digests with impact analysis, competitive intelligence for specific products, or uploading project context for relevance filtering.
---

# Project News Monitor

## Overview

Enable users to define topic domains for daily automated news/info gathering, upload project or work descriptions, and receive matched notifications focused on items that can impact those projects (tech changes, regulations, competitors, supply chain, market shifts, etc.).

## Core Workflow

### 1. Onboarding / Setup

When a user first activates this skill or asks to set up monitoring:

1. Collect **monitoring domains** (topics). Examples: "4G/5G IoT modules", "Rockchip RV1106", "Quectel EG800Q", "smart glasses assistive tech", "China smartphone R&D subsidies", "Type-C fast charging standards".
2. Collect **project/work context**. Ask the user to paste or describe:
   - Current products under development
   - Key technical challenges or risks
   - Competitors, suppliers, target markets
   - Keywords that signal high relevance
3. Store both permanently using the memory system (or a dedicated project file if the conversation is long-running). Prefer structured entries:
   - Domains: list of topic strings + preferred sources if any
   - Projects: short title + 3-8 sentence description + impact keywords
4. Confirm the schedule. Default is daily. Offer weekly or on-demand. Note that true recurring push requires the Automations connector.

### 2. Daily / Scheduled Gathering

When running a monitoring pass (user-triggered or via Automation):

1. For each domain, perform targeted searches:
   - Use `web_search` with recent operators where useful (e.g. after:YYYY-MM-DD).
   - Prefer primary sources: official blogs, standards bodies, regulatory sites, major tech news, company press releases, arXiv/scholar for research.
   - Also check X (Twitter) via `x_keyword_search` or `x_semantic_search` for fast-breaking signals from engineers and companies.
2. Fetch full content of promising links with `open_page` or `open_page_with_find`.
3. Deduplicate against previously reported items (keep a short rolling list of already-notified titles/URLs in memory or a local file).

### 3. Relevance Matching (Impact Analysis)

For every candidate news item:

1. Score relevance against each stored project using these criteria (in priority order):
   - Direct technical impact (new chip, protocol change, SDK update, known bug/fix)
   - Regulatory / compliance change affecting the product
   - Competitor product launch or strategy shift
   - Supply-chain or component availability news
   - Market / customer demand signal that changes priority
   - Funding, partnership, or standard adoption news
2. Only keep items that clearly map to at least one project. Discard pure general-interest news.
3. For kept items, write a concise impact note: "Affects [Project X] because … Possible action: …"

### 4. Notification Format

Present results as a clean digest:

```
## Project Impact Digest — YYYY-MM-DD

### High Impact
- **[Title](url)**  
  Domain: …  
  Project: …  
  Impact: …  
  Suggested next step: …

### Medium / Watch
- …

### Sources scanned
- list of domains + number of items reviewed
```

If no high-impact items, say so explicitly and optionally surface 1-2 medium items.

### 5. Updating Context

- Users can add/edit domains or projects at any time.
- When a project changes significantly, re-evaluate the last 7 days of news against the new description.
- Keep the stored context lean. Prefer short, keyword-rich descriptions over long documents.

## Implementation Notes

- Prefer `web_search` + `open_page` for depth. Use X tools for real-time signals.
- Never invent news. Every item must come from a tool result and be citable.
- When the user wants true daily push without manual triggering, guide them to create an Automation that runs a prompt such as "Run project-news-monitor digest for my domains and projects".
- For multi-project users, group the digest by project first, then by impact level.
- Chinese-language sources are first-class when the domains are China-centric (use Chinese search terms when appropriate).

## Example Trigger Phrases

- "帮我设置每天监控 IoT 模组相关新闻，并匹配我的项目"
- "Upload my current RV1106 dashcam project and start monitoring relevant news"
- "Run today’s project impact digest"
- "Add a new domain: smart glasses for the visually impaired"
- "Update project description for OpenClaw"

See `references/example-prompts.md` for complete setup and update prompt templates.

## Limitations

- True unattended daily push depends on the Automations connector being connected and a schedule being created by the user.
- Source coverage is limited to what web_search and X tools can reach.
- Matching quality depends on the quality of the project descriptions the user provides. Encourage concrete technical details.
