# How Orchestra Is Different

Orchestra belongs to a different category from a general-purpose AI chat assistant.

This distinction matters.

## General-Purpose AI Assistants

Products such as ChatGPT, Claude, Gemini, and similar systems are extremely capable general-purpose assistants.

They are commonly used for:

- questions;
- writing;
- analysis;
- coding assistance;
- research;
- brainstorming;
- and content generation.

Their features continue to evolve rapidly.

## Orchestra

Orchestra is designed around **production orchestration**.

The goal is not only to answer a prompt.

The goal is to coordinate the work required to complete a project.

## Category Difference

```text
GENERAL-PURPOSE ASSISTANT

Prompt
  ↓
Reason
  ↓
Generate Response
```

```text
ORCHESTRA

Goal
  ↓
Plan
  ↓
Create / Assign Agents
  ↓
Use Models + Tools
  ↓
Generate Code + Assets + Research + Media
  ↓
Validate
  ↓
Repair
  ↓
Checkpoint
  ↓
Continue
  ↓
Production Output
```

## Local-First

Orchestra can run entirely on local models on the user's own workstation, with no cloud key required. Cloud providers are optional and are chosen by the capability a task needs, not by vendor. A request for local generation is never moved to a paid cloud provider without the user's say.

## Evidence-Based Progress

Orchestra reports progress from evidence: files on disk, validated deliverables, playtests, and completion gates. A build with required work still open is never reported as complete, and a placeholder is never presented as the result.

## Persistent Projects

One of Orchestra's most important design goals is persistence.

Complex production work should not disappear because:

- a chat ends;
- the application restarts;
- one agent fails;
- or the task requires multiple execution stages.

The Project Execution Engine is designed to preserve project state and resume work.

## Game-Specific Production

Orchestra is also being built with game development in mind.

Games require many different production disciplines.

Orchestra can coordinate code, assets, music, sound, UI, game research, engine workflows, testing, and other production tasks as parts of one project.

A game build moves through a team loop: a designer writes the design, an architect plans it, a developer builds it slice by slice, QA playtests each slice in a headless browser, and a repair agent fixes what QA finds.

## Orchestra Does Not Need to Replace LLMs

Orchestra can use and orchestrate language models.

Its value comes from the system around the models:

- agents;
- tools;
- project state;
- deterministic validation;
- asset intelligence;
- production workflows;
- and game-engine integration.

A concise definition is:

> Orchestra is not designed to replace an LLM. It is designed to orchestrate models, agents, tools, assets, validation, and persistent execution into a production environment.
