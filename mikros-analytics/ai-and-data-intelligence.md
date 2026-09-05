# MIKROS AI and Data Intelligence

MIKROS AI is designed as a decision-support layer on top of structured game data.

Its purpose is not to let a language model freely inspect raw telemetry and guess.

The architecture separates deterministic data work from language-model reasoning.

## Core Principle

**AI should not be responsible for basic math.**

The backend should calculate facts first.

The AI should reason over structured facts.

## Conceptual Pipeline

```text
Game Telemetry
    ↓
Normalized KPIs
    ↓
Discovery Engine
    ↓
Statistically Relevant Relationships
    ↓
Narrative Memory
    ↓
AI Reasoning Layer
    ↓
Structured Explanation + Experiments
    ↓
MIKROS UI
```

## Discovery Engine

The Discovery Engine identifies possible statistical relationships.

Examples:

- retention and high-value users;
- platform and crash rate;
- genre and user quality;
- achievements and session length;
- purchase behavior and retention;
- time-to-first-purchase and long-term value.

The Discovery Engine creates hypotheses and observations.

It does not automatically establish causation.

## Deterministic Data Preparation

Before an AI model receives context, the system should calculate:

- deltas;
- ratios;
- percentage differences;
- segments;
- rankings;
- competitor comparisons;
- normalization;
- trend direction.

This produces a structured factual layer.

## Trust Model

MIKROS AI separates output into categories:

1. **Facts** — directly supported by measured data.
2. **Observed Relationships** — statistical relationships identified in the data.
3. **Interpretation** — AI-generated reasoning about what those relationships may mean.
4. **Recommended Experiments** — actions that can be tested.

This structure helps developers distinguish measurement from interpretation.

## Narrative Memory

MIKROS AI is designed to remember how important themes evolve.

Instead of producing isolated monthly reports, the system can track a business or game-performance story over time.

For example:

```text
Theme: High-value iOS audience
Started: March
Month 1: Relationship discovered
Month 2: Relationship strengthened
Month 3: Relationship stabilized
Month 4: Relationship weakened
Current confidence: High
Next recommendation: Investigate Android parity
```

This concept is sometimes described internally as **storybook prompting**.

The goal is for MIKROS AI to become part of the institutional memory of a game's business.
