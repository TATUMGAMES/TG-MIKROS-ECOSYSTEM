# Orchestra Architecture

This is the canonical explanation of how Orchestra is designed to work.

[The Orchestra README](README.md) defines the product. [Capabilities](capabilities.md) lists production domains and their verification state. [Canonical Facts](../CANONICAL_FACTS.md) holds the stable facts. This page explains the system behind those capabilities.

Orchestra should be understood as a production environment. Models answer questions. Orchestra coordinates work toward deliverables that persist after the conversation.

## Design and demonstrated state

Every section below describes the architecture as documented from the product. That is not the same thing as a universal production proof.

- A workflow can be implemented and still depend on the user's hardware, installed tools, or optional accounts.
- A saved provider key is not evidence that the provider works. Orchestra treats a provider as working only after a free validation check.
- An engine automation path is not evidence that a real Unity, Unreal, or Blender install has been fully verified. Those installs are still being tested. Browser games do not need them.
- Video, native mobile, and Meta wearable targets are in development. See [Capabilities](capabilities.md) before describing them as available.
- A generated file is not evidence that a project completed. Completion is a gate.
- Knowledge of MIKROS MCP is not evidence that every MIKROS operation has been executed live from Orchestra.

The local runtime has a documented result: Orchestra has built complete games on a single workstation using only local models. That result does not extend, by itself, to engine-install verification, video, native mobile, or scale.

## From a prompt to a project

A conventional assistant follows a short path.

```text
User request
  ↓
Model response
  ↓
Conversation ends
```

Orchestra is designed around a longer path.

```text
User intent
  ↓
Project understanding
  ↓
Planning
  ↓
Specialized agent coordination
  ↓
Tool and model selection
  ↓
Execution
  ↓
Artifact creation
  ↓
Validation
  ↓
Repair and iteration
  ↓
Verified deliverables
  ↓
Persistent project state
```

Simple questions stay on the short path. Orchestra answers them directly and does not start a multi-agent workflow when the request does not need one.

When the request is a project, the long path is the product. The model is one participant in that path. Files, tests, review, and stored project state are the others.

## Six layers, one production loop

Orchestra is easier to misread as a feature list than as a stack. The stack has six layers. They are useful only because each one hands work to the next.

**Intelligence.** Language models reason, draft, analyze, and choose. They can be local or cloud. They do not own the project.

**Orchestration.** The system turns an objective into work, assigns specialized roles, orders that work, and tracks execution. A team of agents without this layer is a set of separate conversations.

**Production.** Agents use tools and execution environments to create software, games, media, research, and documents. The output is an artifact, not only a message.

**Quality control.** Requirements, deterministic checks, independent review, tests, and repair loops decide whether the artifact meets the objective. Generation and completion are different states.

**Continuity.** Projects, decisions, files, agent activity, and execution history outlive the chat turn, the browser session, and a process restart.

**Human direction.** The user sets how autonomous a run may be, and keeps authority over spending, publishing, destructive operations, and disagreements the agents cannot resolve.

A coding request shows the handoff. Intelligence reads the goal. Orchestration plans the change and assigns roles. Production edits the repository. Quality control runs structural and policy checks and can send the work back. Continuity stores the project, the diff, and the run. Human direction stops the run when a step is destructive or otherwise gated. None of those layers replaces the others.

## Multi-agent orchestration

Having several models available is not orchestration. Having several named agents is not orchestration either.

Orchestration, in Orchestra, means four concrete responsibilities:

1. Understand the objective well enough to know what kind of work it is.
2. Create a project-specific team whose roles match that work, rather than a fixed cast for every request.
3. Give those roles tasks, and surface each agent as working, waiting, blocked, or finished.
4. Carry the shared project forward only when the artifacts those tasks depend on actually exist.

Agents can publish a planning discussion. The user can enter that discussion and approve, reject, or redirect the plan. That huddle is part of coordination. It is not a second product.

Dependencies are expressed by ordering the work. A game slice is designed before it is built. A build is checked before it can complete. A later request such as "add a boss fight" continues the same game instead of starting an unrelated one. Agents that are waiting or blocked are reporting a dependency, not decorating a chat transcript.

The difference from a group of independent agents is the shared deliverable. Independent agents each return an answer. An orchestrated team returns a project whose parts are supposed to agree: the design, the files, the test result, and the recorded state.

Major requests create these teams. Experience from a defect that QA found and a later playtest confirmed can be stored as a lesson for a later build of the same genre. That memory belongs to the production system, not to a single prompt.

## Persistent execution

Orchestra treats a project as something that can still be in progress after the model stops talking.

The project lifecycle is explicit. Work moves through states from discovery and planning into implementation, validation, repair, and completion. Stalled work and deadlocked work are detected as their own conditions, rather than left looking active. The documented lifecycle has 22 states.

The Project Execution Engine is the persistent runtime for long-running work. Major coding, game-development, and multi-agent requests become resumable projects with checkpoints, watchdog recovery, and auto-resume after a restart. Builds, coding runs, media jobs, and research run in the background so the conversation stays usable. Stop stops the work. A task interrupted by a restart is marked interrupted. It is not left in a false "running" state.

Chats and projects are stored on the server side of the workstation application. They can be recovered after a browser crash or reload. Deleting a chat removes it everywhere. `/clear` resets one conversation's context and does not delete the project, its files, or other conversations.

Progress is computed from evidence: files on disk, validated deliverables, and completion gates. It is not taken from a model's narrative of how far along the project feels. A project with required work still open is not reported as complete.

Each project lives in a readable folder named for the project. The interface can open or copy that folder. The folder is the production record, not a hidden transcript.

## Context and knowledge

A model is only as useful as the context it is given. Orchestra decides whether a question needs retrieval, and from where.

Sources include:

- the current conversation;
- the project;
- project assets;
- Project Notes, which are reusable Markdown guidance loaded according to the kind of work;
- Tatum Games knowledge, with provenance and an authority level;
- the web;
- the full research engine, when the question needs more than a single lookup.

For code, Orchestra maps and searches the repository first and sends the model the context it needs, rather than the whole tree by default.

For research, a question can be expanded into complementary subqueries, searched in parallel, read at page level, de-duplicated, and written up with sources. Time-sensitive questions are checked against recent dated sources. The system is not supposed to fill a gap in current evidence with older training knowledge. Citations that do not support the answer are removed.

Tatum Games knowledge is refreshed from this ecosystem repository and from the MIKROS MCP repository. Orchestra does not claim to have reviewed a repository it did not retrieve. When it describes itself, it is supposed to keep the product's capabilities separate from what is currently running on that workstation.

This is the context engine in product terms: assemble the relevant material, label where it came from, and do not pretend that whatever fit in the prompt was the whole project.

## Model and provider independence

The model is the intelligence. Orchestra is the system that employs it.

That split is deliberate. A production environment that can run on only one vendor stops when that vendor changes price, availability, or policy. Orchestra is designed to keep the production loop and swap the intelligence underneath it.

Local models run through Ollama. Orchestra reports whether each model is installed, running, and answering. If one local model fails, work can move to another local model, and the reply says so. Local language, image, and video models take turns on the GPU so they do not fail by competing for memory. A request for local generation is not moved to a paid cloud provider unless the user agrees.

Cloud providers are optional. The documented set includes Anthropic Claude, Google Gemini, Qwen, Kimi, and Stability AI. Routing is by capability. When several models qualify, Orchestra compares tool support, context size, reasoning level, and cost. A user who names a provider gets that provider for the task. If it fails, Orchestra offers a fallback instead of switching silently.

Each agent role in a build can use the model suited to that role. Every model call is recorded with its role, provider, and result.

Provider status is explicit: Connected, Not validated, Authentication failed, Unavailable, or Not configured. A key saved in configuration is not treated as a working provider until a free check confirms it.

The same separation applies to image generation. The documented order is a local ComfyUI server, then a dedicated image worker, then Stability AI, with fallback in that order. Missing visual models are reported. They are not downloaded automatically.

## Tools and execution

Models propose. Tools do.

Where tool use is enabled, agents can select a tool, run it, evaluate the result, and retry. The production value of Orchestra is this loop: intelligence plus an execution environment. A paragraph of code in a chat window is not the same artifact as a file written, checked, and left in the project folder.

Tool choice is capability-based. For games, Orchestra reasons about needs such as 2D or 3D presentation, sprites, rigging, audio, testing, builds, and analytics, then picks an installed, trusted tool that provides them. A tool the user already chose is not silently replaced.

Orchestra can use Model Context Protocol servers. Schema changes are reviewed before use. MIKROS MCP is treated as first-party knowledge, so MIKROS work is planned as official MIKROS MCP tool calls instead of guessed SDK code. That is a planning rule. It is not, by itself, a report that every MIKROS API has been called successfully from a live Orchestra session.

External engines and optional accounts are tools in the same sense. If Unity, Unreal, Blender, or Ren'Py is missing, Orchestra shows a setup checklist and installs MCP bridge packages only where that is safe. HTML5 game generation does not require an external engine. Paid tools, such as an optional Spriterrific account for animated sprites, are estimated against the user's cost policy and approved before they run. A background health check does not spend money.

Untrusted content stays data. Prompts, attachments, uploads, archives, repositories, URLs, and tool output do not get to instruct or authorize actions. File validation, archive extraction, path containment, URL fetching, and credential redaction run in deterministic code before that content reaches a model or a log.

## Quality, validation, and repair

A model producing something does not mean the project is finished. Orchestra is designed to manage the distance between those two events.

For software, the coding team plans, writes, reviews, and runs QA in iterations. Deterministic checks cover structure, dependency policy, security heuristics, and architecture rules. Each iteration receives a 1–100 quality score with hard gates. Failed work returns to the team through a bounded repair loop. The review shows which files Orchestra changed. Edits the user made are not claimed as Orchestra's, and a revert does not overwrite a newer user edit.

For games, the request becomes a structured understanding: genre, including hybrids, setting, required systems, scope, and presentation. References are read as characteristics. They are not copied, and distinctive third-party characters, marks, and one-to-one remakes are refused unless the rights are explicit. The requirements become acceptance criteria. Code checks and an independent reviewing model test the build against those criteria. A project cannot complete while a requirement is unmet.

The game team is a sequence, not a pile of job titles:

1. A Game Designer writes the design.
2. A Technical Architect writes the plan.
3. A Game Developer builds one playable slice at a time.
4. QA plays each slice in a headless browser.
5. A Repair Agent fixes what QA finds.

Builds can be stopped, paused, and resumed from the work already kept. If no model can produce the game, the project fails visibly and can be retried.

Player-facing documents, when a production package includes them, are written from the actual build and checked against the code. The document is not allowed to describe a game the files do not contain.

That is the verification model: requirements, evidence, an independent check, a bounded repair, and a gate. The gate is what makes a deliverable different from a draft.

## Human-guided autonomy

Autonomous, for Orchestra, means the system can continue a project without a new prompt at every step. It does not mean unrestricted authority.

The user chooses a Guided, Balanced, or Autonomous preference. That preference sets how often large deliverables pause at checkpoints. Four situations always wait, regardless of preference:

- spending;
- publishing;
- destructive steps;
- unresolved disagreement between agents.

Those gates survive a restart. They do not resume themselves. Runtime Setup does not install software without approval, and it does not reinstall something already present. Orchestra does not migrate a project to another engine version without approval. Prospecting can draft a message. Orchestra does not send email or contact anyone.

The user can also stop a background task, reject a plan in an agent huddle, or keep a run on local models. Controlled execution is the design. Silent escalation is not.

## How a game request uses the whole architecture

Game development is the clearest example of the layers working together, because a game is rarely one kind of file.

A plain-language idea enters as intent. Orchestra builds a structured understanding and a specification with acceptance criteria. That is project understanding, not a chat reply.

Planning assigns the designer, architect, developer, QA, and repair roles. The developer does not start from an empty slogan. The designer’s artifact is a dependency. Simple and idle games target vanilla HTML5 canvas. Medium-complexity 2D games target Phaser. A visual novel can target Ren'Py when it is installed or requested. If the user gives creative freedom, Orchestra selects a genre and engine, compares concepts, and prototypes the core loop, using an Idea Agent to avoid repeating past concepts.

Execution writes the slice. Tooling may include code, synthesized audio, and assets from the visual pipeline. QA plays the slice in a headless browser. Repair consumes the QA result. Validation holds completion until the acceptance criteria are met. The project folder, checkpoints, and execution log remain after the session ends. A follow-up request versions the same game.

A production package can add the lean documents the game actually needs, such as vision, design, technical design, QA, and monetization, plus player-facing pages checked against the code.

The same request can involve optional engine automation. Unity batch builds, Unreal build-and-cook, and Blender headless export are part of the design. Real engine installs are still being tested. The browser path is the one that does not depend on that verification.

Native Android packaging, iOS projects, Meta wearable targets, and video are outside this verified loop. They are in development and are described that way in [Capabilities](capabilities.md).

This is why "game generator" is the wrong name. The generator, if that word is used at all, is one tool inside a specification, a team, a playable slice, a playtest, a repair cycle, and a stored project.

## Runtime and infrastructure

Orchestra runs as a workstation application with a web interface, a command-line interface, and a desktop interface. Concurrent builds are queued, and each queued build shows its place in line.

The local runtime is sufficient for supported workflows. No cloud key is required to run on local models. Not every feature is fully offline. Cloud services are optional enhancements, not a hidden requirement for every deployment.

Operational behavior that matters to the architecture:

- The launcher restarts a backend that exits, and the interface distinguishes reconnecting from a real outage.
- Startup reuses healthy services. Shutdown stops what Orchestra launched. Tools the user started separately are left alone.
- Hidden tabs stop polling. Recoverable interface errors can be fixed without losing the chat.
- Image, music, speech, and video use separate workers so one media type does not pretend to be another. A still image is not treated as video, and a disabled video capability does not block image generation.
- Optional Slack can carry outbound updates. It is not part of the core production loop.

Video workers, native mobile toolchains, and Meta wearable targets exist in the product direction and in partial implementation. Reliable end-to-end video is not verified on every setup. iOS project generation is not available. Wearable device input is simulated until the game runs on hardware.

## Place in the MIKROS ecosystem

Orchestra is the production and creation layer of Tatum Games. The rest of the ecosystem covers other jobs in a game's life. The relationship type matters.

### Inside Orchestra

| Concept | Relationship |
| --- | --- |
| Tatum Games | Orchestra is a Tatum Games product. |
| TatumBOT | Conversational interface of Orchestra, not a competing product. |
| Language models | Intelligence providers. Local via Ollama, or optional cloud providers. |
| Agents, tasks, projects, tools | Parts of the orchestration model defined above. |

### Strategic and lifecycle relationships

These products reinforce Orchestra in the company strategy. Do not describe them as modules Orchestra currently operates.

| Product | Role beside Orchestra |
| --- | --- |
| MIKROS Analytics | Understand players after a game exists. |
| MIKROS AI | Explain game data and recommend what to test next. MIKROS AI is not the intelligence layer inside Orchestra. |
| MIKROS Marketing | Promote and distribute games. |
| MIKROS Mafia and MIKROS Bot | Community discovery and distribution. |
| Tatum Tech | Workforce program. Orchestra is becoming part of its production model. |

A game can be built with Orchestra and later instrumented with MIKROS, marketed with MIKROS Marketing, and discussed in MIKROS Mafia. That sequence is the ecosystem thesis. It is not a statement that those handoffs are automated today.

### Documented connections

These are narrower than the strategy, and they are the ones that should be repeated as fact.

- **MIKROS Marketing discovery.** A campaign can add a game to Orchestra AI's discovery database. Active campaigns receive priority in eligible discovery results. After the campaign, the game can remain listed without that priority. This is a discovery listing. It is not the production studio building the game, and listing does not guarantee traffic or sales. See [MIKROS Marketing](../mikros-marketing/README.md).
- **MIKROS MCP knowledge.** Orchestra plans MIKROS integrations as official MCP tool calls when that knowledge applies. See [MIKROS MCP](../technology/mikros-mcp.md).
- **Tatum Tech schedule.** Participants are scheduled to use Orchestra during the October 10, 2026 Tatum Tech cycle. The program integration is underway, not a completed rollout. See [Orchestra and Tatum Tech](../tatum-tech/orchestra-and-economic-mobility.md).

## Terminology

| Term | Meaning |
| --- | --- |
| Orchestra | The product. The production environment as a whole. |
| TatumBOT | The conversational interface inside Orchestra. |
| Model | A reasoning or generation system Orchestra can call. Not the product. |
| Provider | The local or cloud infrastructure that serves a model or a media capability. |
| Agent | A specialized role coordinated inside a project. |
| Task | A unit of work assigned inside the orchestration. |
| Project | The persistent context: goals, files, state, history, and deliverables. |
| Tool | A capability an agent executes against an environment, file, engine, worker, or MCP server. |
| Deliverable | An actual output of production, such as code, a playable build, a document, or an asset. |
| Validation | The check that a deliverable meets the requirements. |
| Repair | Bounded rework after validation fails. |
| Approval gate | A stop that preserves human authority over a consequential action. |
| Project Execution Engine | The persistent runtime that checkpoints and resumes long-running projects. |

## What Orchestra is not

**Not a chatbot with tools.** Tools matter because they sit inside a project with validation and memory. A tool palette without that loop is still a chat product.

**Not a collection of independent agents.** Agents in Orchestra share a project, an order of work, and a completion gate. Without those, they are separate assistants.

**Not a model provider or a foundation model.** Orchestra routes work to models. Replacing or adding a model does not replace the orchestration, the project record, or the gates.

**Not exclusively a game generator.** Games are a demanding specialization, and Tatum Games cares about them. The same architecture covers software, research, writing, and media. Describing Orchestra as only a game tool hides the production environment and over-claims a single pipeline.

**Not a prompt automation framework.** Prompts are an input. The product is the managed path from intent to a verified deliverable.

**Not a collection of disconnected features.** Research, coding, assets, and playtests are valuable because the project can carry them together. Listed apart, they are just features. The architecture is the reason they belong in one system.

## Capability maturity

Use these labels when answering what Orchestra can do. The catalog and its exceptions live in [Capabilities](capabilities.md).

| State | Meaning | Examples documented today |
| --- | --- | --- |
| Implemented, under active verification | The workflow is part of the product. Results still depend on hardware, installed models, and tools. | Local runtime, chat and retrieval, research and writing, coding team and quality gates, project lifecycle, browser game loop, approval gates, local image generation |
| Optional | Present only when the user configures or installs it. Absence must be reported, not silently replaced. | Cloud providers, ComfyUI, SearXNG, Ren'Py, Spriterrific, Slack, external engines |
| Implemented, live verification incomplete | The workflow exists, and the documentation still withholds a blanket success claim. | Unity, Unreal, and Blender automation on real installs; end-to-end video on every setup |
| In development | Do not describe as generally available. | Native mobile toolchains, iOS project generation (not available), Meta wearable targets, video as a product capability |
| Scheduled or strategic | A company or program intention with a stated status. | Tatum Tech use on October 10, 2026; subscription commercialization |
| Documented connection | A specific cross-product behavior that is already described. | Marketing discovery listings; MIKROS MCP as first-party planning knowledge |

Do not promote a row downward in this table into a higher row because an adapter, a key, a design, or a generated file exists.
