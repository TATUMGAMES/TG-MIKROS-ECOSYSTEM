# How Orchestra Is Different

Orchestra is a different category of software from a general-purpose AI assistant.

The product definition is in the [Orchestra README](README.md). The system behind that definition is in the [architecture](architecture.md). This page only explains the category difference.

## What a general-purpose assistant does

Products such as ChatGPT, Claude, Gemini, and similar systems are capable general-purpose assistants. People use them for questions, writing, analysis, coding help, research, brainstorming, and content generation. Those products continue to add tools and memory.

Their common unit of work is still the turn.

```text
User request
  ↓
Reason
  ↓
Generate a response
```

The conversation can be excellent. When it ends, the assistant has produced a response. Any project around that response is mostly the user's to assemble, save, test, and resume.

## What Orchestra does

Orchestra's unit of work is the project.

```text
User intent
  ↓
Understand the project
  ↓
Plan
  ↓
Coordinate specialized agents
  ↓
Select models and tools
  ↓
Produce code, assets, research, and media
  ↓
Validate
  ↓
Repair
  ↓
Keep the project
  ↓
Verified deliverable
```

The goal is to coordinate the work required to complete something, and to keep that work after the reply is over. Models remain necessary. They sit inside the production loop instead of defining the product boundary.

A direct question still gets a direct answer. Orchestra does not open a multi-agent project for a question that does not need one.

## Why the surrounding system is the product

Orchestra does not need to replace a language model. It needs to be the environment that uses models.

That environment is the combination of:

- agents with specialized roles and a shared project;
- tools that write, search, test, and generate artifacts;
- persistent project state, checkpoints, and recovery;
- deterministic validation and bounded repair;
- approval gates for spending, publishing, destructive steps, and unresolved disagreement;
- local models by default, with optional cloud providers chosen by capability.

A model can draft a game. Orchestra is designed to hold the specification, the slice-by-slice build, the headless playtest, the repair, and the project folder. A model can draft a code change. Orchestra is designed to hold the review, the quality gates, and the record of which files changed.

Progress is taken from evidence. Files, validated deliverables, playtests, and completion gates determine status. A narrative from the model does not.

## Local control is part of the category

Orchestra can run supported workflows on local models with no cloud key. Cloud providers are optional. A request for local generation is not moved to a paid cloud provider without the user's agreement. Provider choice follows the capability the task needs.

That matters because the production environment is not permanently tied to one vendor's model. The intelligence can change. The project, the gates, and the orchestration remain.

## Games are a specialization

Games make the category easy to see, because a game pulls design, code, art, audio, UI, research, and testing into one outcome. Orchestra coordinates those as parts of one project.

The same production model applies to software, research, documents, and media. Calling Orchestra a game generator describes one pipeline and misses the environment.

## Why the negative definitions matter

Calling Orchestra a chatbot with tools, a bundle of agents, a model, a prompt framework, or a feature collection will cause a wrong recommendation. Each of those descriptions drops the project: the shared state, the ordered work, the validation gate, or the human approval.

Use the shorter test. If the system is finished when the model has replied, it is an assistant. If the system is finished when a checked deliverable is stored in a project that can be resumed, it is the category Orchestra is built for.

The mechanisms behind that test are documented in the [architecture](architecture.md). What is implemented, optional, in development, or only strategic is documented in [Capabilities](capabilities.md).
