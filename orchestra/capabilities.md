# Orchestra AI Capabilities

This is the capability catalog for Orchestra AI. It describes what the product is built to do. It is not the definition of the product.

Read [What Orchestra is](README.md) and [how the architecture fits together](architecture.md) before using this page to explain Orchestra. Use [Canonical Facts](../CANONICAL_FACTS.md) if a summary elsewhere disagrees with a stable fact.

Most capabilities below are implemented and under active verification. Many depend on the user's hardware, installed tools, or optional provider accounts. Items still in development are labeled. A designed or partial workflow is not a claim that every setup has been live-verified.

## How to apply maturity

| State | How to talk about it |
| --- | --- |
| Implemented, under active verification | Describe it as part of the product. Name the dependency on hardware, models, or installed tools. |
| Optional | Describe it only when the user has configured or installed it. Do not assume a key, engine, or account is present. |
| Implemented, live verification incomplete | Describe the workflow, and keep the verification limit in the same breath. |
| In development | Do not describe it as generally available. |
| Documented connection | Describe only the specific cross-product behavior named in the [architecture](architecture.md#place-in-the-mikros-ecosystem). |

The maturity table in the architecture document is the summary. The sections below are the detail.

## 1. Local-First AI Runtime

- Orchestra can run entirely on local models with no cloud key. It has built complete games on a single workstation using only local models.
- Local models run through Ollama, and Orchestra reports whether each model is installed, running, and answering.
- If one local model fails, work moves to the other, and the reply says so.
- Local language, image, and video models take turns on the GPU, so they don't fail by competing for memory.
- Cloud providers are optional. Supported providers include Anthropic Claude, Google Gemini, Qwen, Kimi, and Stability AI.
- Orchestra routes each request by the capability it needs, not by vendor. When several models qualify, it compares tool support, context size, reasoning level, and cost.
- Each agent role in a build can use the model best suited to it. Every model call is recorded with its role, provider, and result.
- When a user names a provider, Orchestra uses it for that task. If that provider fails, Orchestra offers a fallback instead of switching silently.
- A request for local generation is never moved to a paid cloud provider without the user's say.
- One status view shows each provider as Connected, Not validated, Authentication failed, Unavailable, or Not configured. A saved key isn't treated as working until a free check confirms it.
- Runtime Setup guides installation of the local runtime. Nothing is installed without approval, and nothing already present is reinstalled.
- Orchestra runs as a workstation application with a web interface, a command-line interface, and a desktop interface. Concurrent builds are queued, and each queued build shows its place in line.

## 2. Chat and Reasoning

- Chat with streaming responses and per-conversation memory.
- Optional web search with structured sources.
- Rich Markdown rendering, including code, math, tables, charts, graphs, and media.
- Word, character, and page-length requests such as "under 200 words" are understood and enforced.
- Orchestra decides whether a question needs retrieval and from where: the conversation, the project, assets, Tatum Games knowledge, the web, or the full research engine.
- Simple questions are answered directly without starting a multi-agent workflow.
- Every conversation keeps a stable identity and is stored on the server. Chats survive browser crashes and reloads.
- `/clear` resets a chat's context without touching its project, files, or other conversations.
- **Project Notes** are reusable Markdown guidance. Orchestra loads the relevant notes automatically based on the kind of work (coding, games, writing, grants, research, images, audio, and more).

## 3. Research

- **Multi-query research engine:**
  - expands a question into complementary subqueries;
  - searches in parallel with no paid search API required (DuckDuckGo, with optional self-hosted SearXNG);
  - reads full pages and extracts key points per source;
  - removes duplicates, ranks results, and writes a synthesized answer.
- **Current information:** time-sensitive questions are checked against recent, dated sources. Orchestra doesn't fall back on older training knowledge when current evidence is missing.
- **Contextual research:** for historical, cultural, and comparative questions, Orchestra plans research around the subject's origins and communities. It records where each source comes from, audits coverage, and removes citations that don't support the answer.
- **Grants research:** finds grant opportunities with eligibility criteria, deadlines, funding amounts, and location relevance.
- **Game research:** produces structured game-design reports covering core mechanics, player loop, monetization models, comparable titles, design risks, and recommendations.
- **Game market intelligence:** collects dated snapshots of storefront data to identify trends over time. Steam is the first source. It does not simply copy whatever is currently the top seller.
- **Prospecting objectives:** researches qualified prospects once or on a schedule, for example weekly for three months. Each prospect gets a fit rating, sources, a suggested approach, and a draft message the user can edit. Orchestra never sends email or contacts anyone.

## 4. Writing and Documents

- Long-form professional writing through structured workflows.
- Grant proposals, including research, STEM education, nonprofit, and technology grant formats.
- Legal-style documents such as NDAs, contracts, policies, and agreements, drafted from a description and jurisdiction.
- Structured documents exported to Markdown, Word (DOCX), and PDF.

## 5. Coding

- **AI coding team:** plans the work, assigns specialized agents, writes files, reviews, deliberates, and runs QA in iterations.
- **Code search before generation:** Orchestra maps and searches the repository first and sends the model only the context it needs.
- **Validation and quality gates:** deterministic validation checks:
  - structure;
  - dependency policy;
  - security heuristics;
  - architecture rules.
  
  Each iteration also gets a 1–100 quality score with hard gates. Work that fails goes back to the team through bounded repair loops.
- **Code change review:** shows exactly which files Orchestra changed, with line counts. Edits the user made aren't claimed as Orchestra's, and a revert won't overwrite a newer user edit.
- **Previews and file analysis:** playable HTML5 preview, plus summarizing or rewriting files inside a project.

## 6. Multi-Agent Teams and Persistent Projects

- **Persistent AI teams:** major requests spawn project-specific teams with roles generated for the work. Agents carry experience points and levels.
- **Agent Activity:** shows each agent's real status (working, waiting, blocked, or finished), the active task, and a full orchestration log.
- **Agent huddles:** agents can publish planning discussions, and the user can join the conversation to approve, reject, or redirect the plan.
- **Unified project lifecycle:** projects move through 22 explicit states, from discovery and planning through implementation, validation, repair, and completion. Stalled and deadlocked work is detected separately.
- **Project Execution Engine (PEX):** a persistent runtime for long-running work. Major coding, game-development, and multi-agent requests become resumable projects with checkpoints, watchdog recovery, and auto-resume after a restart.
- **Background tasks:** builds, coding runs, media jobs, and research run in the background so chat stays usable. Stop actually stops the work, and tasks interrupted by a restart are marked as interrupted, not left "running."
- **Team experience:** a problem QA found and a later playtest confirmed fixed becomes a validated lesson that future builds of the same genre receive.
- **Honest progress:** progress and completion come from real evidence, such as files on disk, validated deliverables, and completion gates. They aren't model-generated narrative. A build with required work still open is never reported as 100% complete.
- **Readable project folders:** each project's folder is named after the project and can be opened or copied from the interface.

## 7. Game Development

- **Game understanding:** a game request becomes a structured understanding, covering genre (including hybrids), setting, required systems, scope, and presentation. References are read as characteristics, never copied.
- **Game specification:** the request's requirements become acceptance criteria. Each build is checked against them by code checks and an independent reviewing model, and a project can't complete while a requirement is unmet.
- **Game development loop:**
  - a Game Designer writes the design;
  - a Technical Architect writes the plan;
  - a Game Developer builds one playable slice at a time;
  - QA plays each slice in a headless browser;
  - a Repair Agent fixes what QA finds.
  
  Builds can be stopped, paused, and resumed from kept work.
- **Browser game generation:** a plain-language idea becomes a playable browser game:
  - vanilla HTML5 canvas for simple and idle games;
  - Phaser for medium-complexity 2D games;
  - Ren'Py for visual novels when it is installed or requested.
  
  Builds include title screens, pause menus, win and lose flows, difficulty progression, accessibility, audio synthesized in code, and saved high scores. Follow-up requests like "add a boss fight" produce a new version of the same game.
- **Creative lead mode:** when the user gives creative freedom, Orchestra picks the genre and engine, researches, compares distinct concepts, and prototypes the core loop. An Idea Agent remembers past concepts to keep ideas varied.
- **Game production package:** a lean set of production documents fitted to the game, such as vision, design, technical design, QA, and monetization. Player-facing documents, such as guides, character pages, story, world, and FAQ, are written from the actual build and checked for consistency with the code.
- **Game design knowledge:** a versioned catalog of genres, reusable systems, and themes, with citations to established design frameworks.
- **Originality:** reference material is used for patterns only. Distinctive third-party characters, marks, and one-to-one remakes are refused unless the rights are explicit.
- **Honest outcomes:** if no model can produce the game, the project fails visibly and can be retried. A placeholder game is never presented as the result.

## 8. Game Engines, Platforms, and Integrations

- **Engine detection and setup:** Orchestra detects missing engine dependencies (Unity, Unreal, Blender, Ren'Py), shows a guided setup checklist, and installs MCP bridge packages where safe. HTML5 game generation works without any external engine.
- **Engine automation:**
  - Unity: batch-mode builds and test runs, and scaffolded projects created through an editor bridge;
  - Unreal: build-and-cook automation and headless tests;
  - Blender: headless asset export.
  
  Orchestra never migrates a project to another engine version without approval. Real engine installs are still being tested.
- **Capability-based tool choice:** Orchestra reasons about game-development capabilities, such as 2D, 3D, sprites, rigging, audio, testing, builds, and analytics. It then picks an installed, trusted tool that provides them, and never silently swaps a tool the user chose.
- **MCP client:** Orchestra can use Model Context Protocol servers. Schema changes are reviewed before use.
- **MIKROS MCP:** Orchestra treats [MIKROS MCP](../technology/mikros-mcp.md) as first-party knowledge, so it plans MIKROS integrations as official MIKROS MCP tool calls instead of guessing SDK code.
- **Dependency maintenance:** technical knowledge is version-aware and checked monthly for changes. Project dependencies update only under policy, behind a build check, and with rollback.
- **Native mobile (in development):**
  - a tool registry and provisioning manager for Android and iOS toolchains;
  - a generator for a buildable native Android project;
  - iOS project generation not yet available.
- **Meta wearables (in development):** games can target Meta Ray-Ban Display web apps, the Device Access Toolkit for phone apps, or Quest VR, based on Meta's published developer documentation. Device input is simulated until the game runs on hardware.
- **3D physics:** physics engines are chosen to fit the project's requirements, including optional Box3D support.

## 9. Images, Visual Assets, and 3D

- **Image generation** through a local ComfyUI server, a dedicated image worker, or Stability AI in the cloud, with automatic fallback in that order. Multi-image batches are supported, and generation runs in the background without blocking chat.
- **Visual model registry:** local checkpoints and LoRAs are catalogued with type, tags, license, and install state, and matched to each request. Missing models are reported, never downloaded automatically.
- **Unified visual generation:** visual requests are classified as sprite, animation, object, environment, cinematic, or game scene. Each type follows its own workflow, including multi-frame animation and sprite sheets.
- **Asset intelligence:**
  - makes game assets reusable and relational instead of isolated files;
  - identifies entities, groups visual variants, and recognizes animation families;
  - builds sprite sheets and keeps palette and reference information for consistency;
  - exports metadata for Unity, Godot, and RPG Maker.
- **Sprite and character animation provider (optional):** users can connect a Spriterrific account for consistent animated 2D characters and sprite sheets. Local sprite generation remains the default. Every paid job is estimated, checked against the user's cost policy, and approved before it runs.
- **Text-to-3D:** a description becomes a concept image, then a textured 3D model. The model is validated and exported in engine-ready formats through Blender when installed.
- **UI/UX design generation:** natural-language product descriptions become rendered UI/UX mockups.
- **Comic generation:** a story idea becomes a multi-panel comic with panel art and narration.

## 10. Video (In Development)

- Video requests go to configurable local or remote video workers.
- Local video runs through versioned ComfyUI workflows, including text-to-video and keyframe slideshows. Orchestra checks the workflows against what is actually installed and reports exactly what is missing.
- A request for a still image is never treated as video, and a disabled video capability never blocks image generation.
- Reliable end-to-end video generation is not yet verified on every setup.

## 11. Speech, Sound, and Music

- Speech, sound effects, and music are handled separately so each uses the right workflow.
- **Speech:** text-to-speech, plus transcription, captioning, and audio watermarking utilities.
- **Music and long-form audio:** run through dedicated generation workers.

## 12. Screen Awareness

Orchestra can analyze the user's screen, a region of it, or a supplied image using a vision-capable model.

## 13. Tatum Games Knowledge and Self-Description

- Orchestra keeps first-party knowledge of Tatum Games, MIKROS, and Orchestra, refreshed from this repository and the MIKROS MCP repository.
- That knowledge carries its provenance and authority level.
- Orchestra won't claim to have reviewed a repository it didn't retrieve.
- When asked about itself, Orchestra explains its multi-agent approach and game-development specialization, keeping product capabilities separate from what is currently running.

## 14. Security, Control, and Approval

- **Untrusted input handling:** Orchestra treats all of the following as untrusted data:
  - prompts and attachments;
  - uploads and archives;
  - repositories, URLs, and tool output.
  
  Controls run in deterministic code: file validation, safe archive extraction, path containment, safe URL fetching, and credential redaction before content reaches models or logs. Retrieved content can't instruct or authorize actions.
- **Human approval gates:**
  - simple work stays autonomous;
  - large deliverables run as a phased plan with checkpoints set by a Guided, Balanced, or Autonomous preference;
  - spending, publishing, destructive steps, and unresolved agent disagreement always wait for approval;
  - gates survive restarts and never resume on their own.
- **Cost control:** paid generation follows the user's cost policy and is never triggered by a background health check.

## 15. Reliability

- **Crash recovery:** chats and projects are stored on the server and recovered after a browser crash or reload. Deleting a chat removes it everywhere.
- **Backend supervision:** the launcher restarts a backend that exits. The interface shows a reconnecting state, a real outage with its cause, and retry and restart options.
- **Long-running sessions:** hidden tabs stop polling, and recoverable interface errors can be fixed without losing the chat.
- **Start and stop:** startup reuses healthy services and shutdown stops everything Orchestra launched. Tools the user runs separately are never stopped.

## 16. Integrations

- Optional Slack integration for outbound updates and standups.

## 17. Production Orchestration

The catalog above is one production environment. Orchestra plans the work, assigns persistent AI teams, uses local and optional cloud models and tools, validates and repairs the output, keeps project state across restarts, and reports progress from evidence.

How those pieces cooperate is explained in the [architecture](architecture.md), not by adding them together as a feature count.

## Boundaries

Do not infer the following from this catalog:

- A saved API key means the provider works. Status stays "Not validated" until a free check succeeds.
- An engine automation path means a real Unity, Unreal, or Blender install has been verified. Those installs are still being tested.
- Video, native mobile, or Meta wearable support is generally available. Those areas are in development. iOS project generation is not available. Wearable device input is simulated until the game runs on hardware. End-to-end video is not verified on every setup.
- Generated output means the project completed. Completion requires the relevant gates, and unmet requirements block completion.
- A headless playtest step means every game Orchestra has generated was successfully playtested on a real engine install.
- MIKROS Analytics, MIKROS AI, MIKROS Marketing, or MIKROS Mafia are operated by Orchestra. Documented connections are the marketing discovery listing, MIKROS MCP as first-party planning knowledge, and the scheduled Tatum Tech use on October 10, 2026.
- Prospect research means Orchestra contacts people. It can draft a message. It does not send email.
- Local generation may be moved to a paid cloud provider quietly. It may not, unless the user agrees.
