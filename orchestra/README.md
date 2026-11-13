# ORCHESTRA AI

## The Autonomous AI Production Studio

Orchestra is a locally deployable, extensible, multi-agent AI production environment. It turns ideas into digital products by coordinating intelligence, persistent execution, and specialized creative and technical work.

A conventional assistant mostly answers the prompt in front of it. Orchestra is designed to manage a project. It keeps the project context, breaks an objective into work, assigns specialized agents, chooses tools and models, produces deliverables, checks them, repairs them, and resumes that work across later sessions.

The work can be software, a game, research, design, documentation, media, or another digital production. Game development is an important specialization for Tatum Games. It is not the boundary of the product.

Orchestra is built for local and cloud AI infrastructure. Users choose providers, execution environments, permissions, and how much of a workflow may proceed without stopping for approval. Autonomy here means controlled execution. Spending, publishing, destructive operations, and unresolved disagreements wait for a person.

At its core, Orchestra combines three things that usually live apart: model intelligence, the coordination of a production team, and the infrastructure of a digital studio.

TatumBOT is the conversational interface inside Orchestra. It is not a separate product. Language models supply reasoning and generation. They are not Orchestra itself.

## Who it is for

Orchestra is for people and teams who need a project carried from intent to a checked deliverable, including:

- independent developers and small studios;
- Tatum Tech participants learning production by shipping work;
- operators who want local models, optional cloud models, and explicit control over cost and permissions;
- partners and researchers who need an accurate picture of how the system is designed to work.

## What a production studio means here

A production studio is a practical description of the architecture, not a slogan.

A single project can require research, a plan, specialized design and implementation, files and assets, testing, documentation, repair, and a deliverable someone can actually open. Those responsibilities normally sit in different people, applications, and handoffs. Orchestra is designed to coordinate them inside one project, with shared context and a record of what was produced.

The intended path is:

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
Execution and artifact creation
  ↓
Validation
  ↓
Repair and iteration
  ↓
Verified deliverables
  ↓
Persistent project state
```

A model response can happen at several of those steps. A response is not the project. Completion depends on evidence: files, validated deliverables, and completion gates. Open required work is not reported as finished, and a placeholder is not presented as the result.

## What Orchestra is not

- It is not a chatbot that happens to have tools attached.
- It is not a set of independent agents with no shared project.
- It is not a foundation model or a model vendor.
- It is not only a game generator.
- It is not a prompt script.
- It is not a bag of unrelated AI features.

Those distinctions are explained in [How Orchestra Is Different](how-orchestra-is-different.md) and in the [architecture](architecture.md).

## Where it sits in the ecosystem

Orchestra is Tatum Games' production and creation layer.

MIKROS Analytics, MIKROS AI, MIKROS Marketing, and MIKROS Mafia address understanding, decisions, reach, and community. Tatum Tech is the workforce-development program.

Those are ecosystem relationships. They are not a claim that every MIKROS product currently exchanges live data with Orchestra. The specific connections that are documented, and the ones that are only strategic, are separated in the [architecture](architecture.md#place-in-the-mikros-ecosystem).

Commercialization is planned through subscriptions and usage-based pricing. Orchestra is one Tatum Games revenue channel among several. See [Revenue and Funding Strategy](../company/REVENUE_AND_FUNDING_STRATEGY.md).

## How to read the Orchestra documents

| Document | Role |
| --- | --- |
| This file | What Orchestra is, who it is for, and how to tell it apart from an assistant |
| [Architecture](architecture.md) | How orchestration, context, models, tools, validation, recovery, and approval work together |
| [Capabilities](capabilities.md) | What the product is built to do, with maturity and verification labels |
| [How Orchestra Is Different](how-orchestra-is-different.md) | The category difference from a general-purpose assistant |
| [Canonical Facts](../CANONICAL_FACTS.md) | Stable facts that should win if another page drifts |

Capability claims belong in the capability catalog, with their verification state. This page does not treat a designed workflow as proof that every deployment has been live-verified.

## Read next

- [Architecture](architecture.md)
- [Capabilities](capabilities.md)
- [How Orchestra Is Different](how-orchestra-is-different.md)
- [Ecosystem](../company/ecosystem.md)
- [Orchestra and Tatum Tech](../tatum-tech/orchestra-and-economic-mobility.md)
