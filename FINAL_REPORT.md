# GSoC 2026 Final Report - Mifos X Copilot

- **Contributor:** Shubham Kumar
- **Organization:** The Mifos Initiative
- **Mentor:** Victor Romero
- **Repositories:** [openMF/web-app](https://github.com/openMF/web-app) and [openMF/mcp-mifosx](https://github.com/openMF/mcp-mifosx)
- **Live demo with screenshots:** https://shubhamkumar9199.github.io/mifos-copilot-showcase/

## What the project is

Mifos X is the web app that loan officers at microfinance institutions use every day. Most tasks mean going through many forms. My project adds an AI assistant to the app, so an officer can just ask in normal language: find a client, show a repayment schedule, create a client, submit and approve a loan.

The most important rule: the assistant can never change a record by itself. When it wants to do a write, the reply stops and the officer gets a card showing exactly what will happen, with the client, the product and the amount in plain words. Nothing runs until a human clicks approve.

The gateway also has no Fineract account of its own. It sends the officer's own login with every call, so the permissions the institution already set up still decide what is allowed. There are 12 tools in total, 7 that read and 5 that write, all declared in one manifest file. Anything outside that list is refused.

## All my pull requests

### Frontend (openMF/web-app) - all merged

| PR | Date | What it did |
|----|------|-------------|
| [#3648](https://github.com/openMF/web-app/pull/3648) | Jun 19 | The Copilot panel: components, theming, feature flag, lazy loading |
| [#3671](https://github.com/openMF/web-app/pull/3671) | Jun 21 | Translations for all 13 locales |
| [#3675](https://github.com/openMF/web-app/pull/3675) | Jun 21 | Context detection, so the assistant knows which client or loan is on screen |
| [#3677](https://github.com/openMF/web-app/pull/3677) | Jun 21 | Made the feature configurable per deployment |
| [#3678](https://github.com/openMF/web-app/pull/3678) | Jun 21 | Input sanitizer between the officer and the model |
| [#3696](https://github.com/openMF/web-app/pull/3696) | Jun 30 | Core services and the confirmation dialog |
| [#3819](https://github.com/openMF/web-app/pull/3819) | Aug 10 | Connected the panel to the gateway over server-sent events |
| [#3889](https://github.com/openMF/web-app/pull/3889) | Aug 22 | Confirmation cards name the account and product properly |
| [#3903](https://github.com/openMF/web-app/pull/3903) | Aug 24 | Copy, ask again, rate, export to PDF and share on every reply, full screen mode, and a real Preferences tab |

### Gateway (openMF/mcp-mifosx) - all merged

| PR | Date | What it did |
|----|------|-------------|
| [#421](https://github.com/openMF/mcp-mifosx/pull/421) | Aug 10 | The Copilot Gateway: a new Java 21 Spring Boot service |
| [#433](https://github.com/openMF/mcp-mifosx/pull/433) | Aug 22 | Writes are dated from Fineract's business date, not the server clock |
| [#434](https://github.com/openMF/mcp-mifosx/pull/434) | Aug 22 | Confirmation cards read like banking, not like a database |
| [#437](https://github.com/openMF/mcp-mifosx/pull/437) | Aug 22 | The receipt after a write names the account instead of showing an id |
| [#438](https://github.com/openMF/mcp-mifosx/pull/438) | Aug 23 | Fixed seven places where values were hardcoded instead of read from the product or the officer's login |
| [#439](https://github.com/openMF/mcp-mifosx/pull/439) | Aug 24 | Every write is validated with the same rules the web app's own forms use |
| [#440](https://github.com/openMF/mcp-mifosx/pull/440) | Aug 24 | The Fineract API path is configurable, for deployments behind an API gateway |

### Open right now

| PR | What it does |
|----|--------------|
| [mcp #443](https://github.com/openMF/mcp-mifosx/pull/443) | Client search matches names in any case, and a rate-limited officer is told how long to wait |

## How the summer went

June was the frontend: the panel, translations, context detection, the sanitizer. In August I built the gateway and connected the two. Then came the part that taught me the most: Victor used it live and kept finding things I had not thought of.

Some real examples:

- He created a client whose first name was `999999999999999` and Fineract accepted it, because the web app's forms do that validation and the assistant was skipping it. That became #439.
- Writes started failing every evening because I was using the server's clock instead of Fineract's business date. That became #433.
- He searched for a client in lowercase and got "not found" even though the client existed. I fixed that in #443.
- He asked two questions quickly and the panel said the model was down, when really he was only rate limited for a few seconds.

Almost every PR after #421 exists because someone used the thing for real and it fell short somewhere.

## Current state

The Copilot works end to end against the community sandbox: reading client, loan and savings data, and creating clients and running the loan lifecycle behind the confirmation step. It is off by default and can be turned on with two environment variables. The gateway has 135 tests, the panel has 150, and a Playwright suite drives the panel in a real browser as part of the web app's CI.

## What is not finished

- Conversations and pending confirmation cards live in the gateway's memory, so they do not survive a restart. This is fine for a single instance but will not work for a cluster.
- The manifest covers individual lending only. Group and centre lending is the obvious next step.
- Running the model on-premise through Ollama works in the code but is not documented yet, for institutions that cannot use a cloud provider.
- PR #443 is still in review.

## About AI tools

I used Claude as a coding assistant throughout this project: for brainstorming designs, debugging, writing code and tests, and drafting PR descriptions. I want to be upfront about that. Every change was tested end to end against the community sandbox before it went up, every PR went through Victor's review, and the decisions about what to build and why were mine.

The biggest thing I gained this summer was not code, it was how Victor made me think. He never told me the fix. He would say something like "in production the API URL can be different from the UI URL" and leave me to work out what that meant for the design. Slowly I learned to read his comments as questions about the users, not complaints about my code. That changed how I work.

## Thanks

Thank you to Victor Romero for his reviews and his patience, and to the Mifos community for the sandbox and the help.
