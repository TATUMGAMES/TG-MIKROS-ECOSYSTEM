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
