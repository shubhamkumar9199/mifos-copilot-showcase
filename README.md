# Mifos Copilot

An AI assistant for Mifos X where the officer still decides.

**Live page:** https://shubhamkumar9199.github.io/mifos-copilot-showcase/

A loan officer types one sentence instead of working through twenty clicks.
Nothing that touches money executes without a human pressing Confirm, and every
action runs under the officer's own Fineract login so existing permissions and
the audit trail still apply.

This repository hosts the project page: what was built, the engineering
decisions behind it, and screenshots from a live run against a real core
banking system.

## The code

| Component | Repository |
| --- | --- |
| Copilot panel and transport | [openMF/web-app](https://github.com/openMF/web-app) PR #3819, merged |
| Copilot Gateway | [openMF/mcp-mifosx](https://github.com/openMF/mcp-mifosx) PR #421, merged, module `gateway/` |

`DEPLOY-SANDBOX.txt` carries the instructions for connecting a Mifos
environment to the gateway.

Built by Shubham Kumar for Google Summer of Code 2026, mentored by Victor Romero.
