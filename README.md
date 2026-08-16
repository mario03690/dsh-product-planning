# dsh-product-planning

Interrogate a product idea instead of praising it: YC-style six forcing questions, a multi-persona panel allowed to disagree, and the narrowest two-week wedge with a pass/fail test.

## What & why

`validate_idea` forces answers to six questions (who is in acute pain, today's workaround, narrowest wedge, why now, how you'd observe demand in two weeks, whether it holds in three years) — and calls out weak answers instead of cheerleading. `panel_review` simulates a pessimistic investor, the target user, and a competitor CTO giving mutually-conflicting takes, then the real disagreements (where the risk lives). `narrowest_wedge` cuts a big plan to the smallest two-week-testable slice with a numeric pass/fail. Plus make_user_story / make_okr / make_test_cases. Pass `model` for a flagship.

Start with `what_can_you_do` — describe your task in any language, get the exact tool and a ready-to-run call.

## Install

```sh
dsh plugin --profile <your-profile> add github:mario03690/dsh-product-planning
```

Thin config layer only (one `@deepseek-ai/dsh-mcp-client` row, shipped as `cordis.patch.yml`) — no tool code on your machine. Built against the dsh v0.1 developer preview's MCP client config shape (2026-08-13); if a later preview changes it, open an issue for a same-day fix.

## Cost, quota, privacy

First heavy call is free (anonymous, no signup); afterwards billed at real upstream cost, reported in every response; failed calls are not charged. Bring an [AllRouter](https://allrouter.ai) key to run any tool on a flagship model at direct rates. The config URL carries `?s=dsh-dsh-product-planning` — a channel tag identifying the install path, not you.

**Disclosure:** built and run by the team behind [ainetcafe.com](https://ainetcafe.com). Full bundle: [dsh-netcafe](https://github.com/mario03690/dsh-netcafe). MIT.
