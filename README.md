# Mifos X Copilot

A panel inside the Mifos web app that fills in a banking form from a typed sentence,
and then waits for you.

**Page:** https://shubhamkumar9199.github.io/mifos-copilot-showcase/

The five operations that move money all pause and hand the officer a card to read.
Nothing reaches the banking system until they press Confirm, and the action then runs
under their own login, so their permissions decide what is possible and the audit trail
names them.

This repository holds the project page: what was built, what it refuses to do, the
screenshots from a run against the public Mifos sandbox on 22 August 2026, and four
things that were wrong until running it found them.

## The code

| Change | Repository | State |
| --- | --- | --- |
| [#3819](https://github.com/openMF/web-app/pull/3819) the panel and the SSE transport | openMF/web-app | merged |
| [#433](https://github.com/openMF/mcp-mifosx/pull/433) dating commands from the banking calendar | openMF/mcp-mifosx | merged |
| [#434](https://github.com/openMF/mcp-mifosx/pull/434) cards that read like banking | openMF/mcp-mifosx | merged |
| [#437](https://github.com/openMF/mcp-mifosx/pull/437) the receipt names the account | openMF/mcp-mifosx | open |
| [#3889](https://github.com/openMF/web-app/pull/3889) rendering those cards, and one product name | openMF/web-app | open |

The gateway lives in `gateway/` in the mcp-mifosx repository.
`DEPLOY-SANDBOX.txt` here carries the instructions for connecting a Mifos environment
to it, including the Groq, OpenAI and Ollama variants.

## The screenshots

`shots/` holds the images the page uses. Every one is a browser screenshot of the
shipped user interface, taken against `sandbox.mifos.community`. The gateway was running
with its keyword stand-in rather than a language model for that session, which the page
says where it shows them.

Built by Shubham Kumar for Google Summer of Code 2026, mentored by Victor Romero.
