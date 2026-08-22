# dsh-product-planning

Interrogate a product idea instead of praising it: YC-style six forcing questions, a multi-persona panel allowed to disagree, and the narrowest two-week wedge with a pass/fail test.

## What & why

`validate_idea` forces answers to six questions (who is in acute pain, today's workaround, narrowest wedge, why now, how you'd observe demand in two weeks, whether it holds in three years) — and calls out weak answers instead of cheerleading. `panel_review` simulates a pessimistic investor, the target user, and a competitor CTO giving mutually-conflicting takes, then the real disagreements (where the risk lives). `narrowest_wedge` cuts a big plan to the smallest two-week-testable slice with a numeric pass/fail. Plus make_user_story / make_okr / make_test_cases. Pass `model` for a flagship.

Start with `what_can_you_do` — describe your task in any language, get the exact tool and a ready-to-run call.

<!-- TOOLS:BEGIN -->
## What's in this pack

7 tools, read from the live endpoint on 2026-08-22 — **this table is generated, not hand-written**, so it cannot drift away from what `tools/list` actually returns. The **Arguments** column is what the tool genuinely reads; it comes from the tool's own declared input schema.

| Tool | What it does | Arguments | Price / call |
|---|---|---|---|
| `what_can_you_do` | Describe a task in plain language (any language) and get back exactly which tools on this server do it, with ready- | `task` | — |
| `make_test_cases` | A function or spec → a table of test cases (input, expected, edge cases) as a Markdown file. | `code`, `spec` | $0.025 |
| `validate_idea` | YC-style idea validation: answers six forcing questions about your idea (who is in pain, current workaround, narrow | `idea`, `text`, `description`, `model` | $0.03 |
| `panel_review` | Multi-persona review: a pessimistic investor, a target user, and a competitor CTO each give their OWN (mutually con | `plan`, `idea`, `text`, `model` | $0.04 |
| `narrowest_wedge` | Cut a big plan into the smallest slice that can be validated in two weeks, with a concrete pass/fail test. plan = t | `plan`, `idea`, `text`, `model` | $0.02 |
| `make_user_story` | A feature idea → agile user stories with acceptance criteria (Markdown file). | `feature`, `count` | $0.015 |
| `make_okr` | A goal → structured OKRs (objective + measurable key results) as a Markdown file. | `goal`, `timeframe` | $0.015 |

`—` in the price column means the tool is not metered per call (session/trial-gated instead). Failed calls are never charged. Check it yourself:

```sh
curl -s -X POST https://ainetcafe.com/mcp/plan -H 'content-type: application/json' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list"}'
```
<!-- TOOLS:END -->

## Install

```sh
dsh plugin --profile <your-profile> add github:mario03690/dsh-product-planning
```

Thin config layer only (one `@deepseek-ai/dsh-mcp-client` row, shipped as `cordis.patch.yml`) — no tool code on your machine. Built against the dsh v0.1 developer preview's MCP client config shape (2026-08-13); if a later preview changes it, open an issue for a same-day fix.

## Cost, quota, privacy

First heavy call is free (anonymous, no signup); afterwards billed at real upstream cost, reported in every response; failed calls are not charged. Bring an [AllRouter](https://allrouter.ai) key to run any tool on a flagship model at direct rates. The config URL carries `?s=dsh-dsh-product-planning` — a channel tag identifying the install path, not you.

**Disclosure:** built and run by the team behind [ainetcafe.com](https://ainetcafe.com). Full bundle: [dsh-netcafe](https://github.com/mario03690/dsh-netcafe). MIT.

## Compatibility & permissions (at a glance)

| Signal | This plugin |
| --- | --- |
| **Runtime** | dsh v0.1 developer preview (2026-08-13, Cordis v4). Touches only the MCP client config shape — the narrowest surface available. Verified against a live endpoint on 2026-08-17. |
| **What runs locally** | Nothing. Ships one `cordis.patch.yml` row; there is no tool code, no build step and no lifecycle script in this package. |
| **Filesystem access** | None. |
| **Shell / process access** | None. |
| **Network access** | Outbound HTTPS to `ainetcafe.com` only, from the MCP client that dsh already ships. |
| **Credentials** | None required. No signup, no API key for the free tier. An optional AllRouter key, if you supply one, is sent by dsh as a request header and is never stored by us. |
| **Data retention** | Documents and prompts are processed in memory and not retained. |
| **Dependencies** | One peer dependency: `@deepseek-ai/dsh-mcp-client` (ships with dsh). |
| **License** | MIT (see `LICENSE`). |
| **Publisher** | The team that runs [ainetcafe.com](https://ainetcafe.com) — our own hosted service, free tier plus paid usage. Issues get a same-day reply. |

> A directory listing is not a security review. Read `cordis.patch.yml` — it is short enough to read in full in under a minute.
