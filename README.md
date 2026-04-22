# Nodots Backgammon — Community

The public home for conversations about the Nodots Backgammon platform
that span more than one package: roadmap, architecture, engine
integration, and anything else that doesn't belong to a single repo.

**App:** https://backgammon.nodots.com
**Documentation and white papers:** https://backgammon.nodots.com/docs

---

## What goes here

Use [Discussions](https://github.com/nodots/backgammon-community/discussions)
for anything platform-wide:

- **Announcements** — releases, schedule changes, outages
- **Ideas** — roadmap input, feature proposals, cross-package refactors
- **Q&A** — questions that touch more than one package, or where the
  right repo isn't obvious
- **Show and tell** — tools, engines, or integrations built on top of
  the Nodots stack

## What does *not* go here

- **Bugs and feature requests for a specific package.** Open those
  against the package repo directly — see the list below.
- **Support for your account, billing, or a specific game.** Use the
  in-app contact form rather than public Discussions.
- **Code changes.** This repo is prose only (discussions, roadmap,
  future meta-documentation). Code lives in the package repos.

---

## Documentation

All public documentation is published at the Developer Docs site:

**https://backgammon.nodots.com/docs**

The site's sidebar covers the overview, per-package reference
(core, types, ai, api-utils, gnubg-hints), guides (Getting Started,
Type System, Game State, Position ID, API Extensibility, Contributing),
operational references (Terraform/AWS, SSL proxy, scripts), and the
full white-paper series listed below.

### API reference

- **Interactive Swagger UI:** https://api.nodots.com/api-docs

---

## White papers

A technical architecture series describing how the platform is built.
Written for senior engineers: peer-to-peer tone, emphasis on rationale
and trade-offs rather than tutorials.

### Tier 1 — Foundations

- [Paper 1 — System Overview and Design Principles](https://backgammon.nodots.com/docs/white-papers/01-system-overview)
  The shape of the suite: packages, boundaries, the state machine at
  the center, and the design principles the rest of the series defends.

- [Paper 2 — The Type System: Discriminated Unions as State Machine Contracts](https://backgammon.nodots.com/docs/white-papers/02-type-system)
  How `@nodots/backgammon-types` encodes legal game states so illegal
  states are unrepresentable, and why that pays off across the stack.

### Tier 2 — Engine and Intelligence

- [Paper 3 — The Core Engine: Modeling Backgammon](https://backgammon.nodots.com/docs/white-papers/03-core-engine)
  The pure, deterministic game logic: board, moves, dice, cube,
  bearing off, and the rules of the road.

- [Paper 4 — AI Integration: Wrapping GNU Backgammon](https://backgammon.nodots.com/docs/white-papers/04-ai-integration)
  How Nodots embeds GNU Backgammon as a native addon, the position-ID
  contract between CORE and the evaluator, and where a third-party
  engine would slot in.

### Tier 3 — Real-Time Delivery and Operations

- [Paper 5 — The API: REST, WebSocket, and the Worker Bridge](https://backgammon.nodots.com/docs/white-papers/05-api-websocket-worker)
  The runtime: REST surface, WebSocket fan-out, and the Redis-backed
  worker that drives robot turns out-of-band from human requests.

- [Paper 6 — The Client: The Unified Presentation Layer](https://backgammon.nodots.com/docs/white-papers/06-client)
  Why every player sees the board as "white moving clockwise"
  regardless of backend configuration, and how the client derives its
  view from authoritative game state.

- [Paper 7 — Performance Rating at Scale: Offloading to Lambda](https://backgammon.nodots.com/docs/white-papers/07-pr-lambda)
  Moving PR computation off the request path onto Lambda, the queue
  contract, and how results rejoin the user-facing game history.

- [Paper 8 — Infrastructure, Deployment, and Environments](https://backgammon.nodots.com/docs/white-papers/08-infrastructure)
  How the platform is deployed and operated: AWS footprint, the
  GitHub Actions pipeline, and the three-environment discipline
  (development / test / production).

### Positions

- [Paper 9 — Open Source Positions: GPL as the Commons, Apps as the Differentiator](https://backgammon.nodots.com/docs/white-papers/09-nodots-open-source-positions)
  Where the line sits between what Nodots open-sources and what stays
  proprietary, and what that means for contributors, incumbent
  applications, and third-party engine authors.

---

## Public package repositories

Open issues and PRs against the specific package they affect:

| Package | Repository | Scope |
| --- | --- | --- |
| `@nodots/backgammon-types` | [nodots/backgammon-types](https://github.com/nodots/backgammon-types) | Shared TypeScript types |
| `@nodots/backgammon-core` | [nodots/backgammon-core](https://github.com/nodots/backgammon-core) | Game logic, state machine, PR calculator |
| `@nodots/backgammon-ai` | [nodots/backgammon-ai](https://github.com/nodots/backgammon-ai) | Robot move selection, evaluator plugin boundary |
| `@nodots/gnubg-hints` | [nodots/gnubg-hints](https://github.com/nodots/gnubg-hints) | Native addon wrapping GNU Backgammon evaluation |
| `@nodots/backgammon-api-utils` | [nodots/backgammon-api-utils](https://github.com/nodots/backgammon-api-utils) | Shared API types and utilities |
| `@nodots/backgammon-cli` | [nodots/backgammon-cli](https://github.com/nodots/backgammon-cli) | Command-line client |

The API server and web client source repositories are private. File
issues against the relevant concern (types, core, ai, api-utils, etc.)
or open a Discussion here if you're not sure where something belongs.

---

## For engine authors and incumbent applications

Paper 4 (AI Integration) and Paper 9 (Open Source Positions) are the
right starting points. The short version:

- GNU Backgammon is the default evaluator behind
  `@nodots/backgammon-ai`, but the plugin boundary is deliberate — a
  different engine (XG-style, a neural net, your own) can sit behind
  the same contract.
- If you want to wire an engine in or reuse pieces of the stack in
  another application, open a Discussion in the
  [Engine integration / ecosystem](https://github.com/nodots/backgammon-community/discussions)
  space and we'll work through the plugin shape together.

---

## License

Prose in this repository is licensed under
[CC-BY-4.0](./LICENSE). Reuse with attribution back to Nodots.
