# ZAC — Zomniverse Agent for Code

> **A local-first AI workspace for controlled software investigation and human-supervised document editing.**

[![Status](https://img.shields.io/badge/status-active%20private%20development-6f42c1)](#development-status)
[![.NET](https://img.shields.io/badge/.NET-8-512BD4)](#technical-profile)
[![Local AI](https://img.shields.io/badge/AI-local--first-0f766e)](#local-first-by-design)
[![Platform](https://img.shields.io/badge/platform-Windows-0078D4)](#technical-profile)
[![Review](https://img.shields.io/badge/human%20review-first-0f766e)](#supervised-document-editing)

**ZAC** is a private AI-software project exploring a simple product principle:

> **Use the model where judgement helps. Use deterministic software where correctness matters. Keep the user in control.**

The implementation remains private. This repository shows the product capabilities, engineering direction and design thinking without publishing the internal architecture.

---

## What ZAC can do now

ZAC has evolved from a read-only repository assistant into a broader local AI workspace.

| Capability | Current state |
|---|---:|
| Investigate a selected repository | ✅ |
| Read files and search code/text | ✅ |
| Answer questions using local model inference | ✅ |
| Show software-confirmed activity rather than model claims alone | ✅ |
| Cancel bounded agent work | ✅ |
| Attach local files to a conversation | ✅ |
| Read DOCX content | ✅ |
| Render a rich Word-like DOCX preview | ✅ |
| Download attached/generated documents | ✅ |
| Understand natural-language document edit requests | ✅ |
| Accept explicit FIND / REPLACE batches | ✅ |
| Preserve Word formatting while replacing text | ✅ |
| Review document changes side-by-side with the chat | ✅ |
| Edit FIND / REPLACE text before applying it | ✅ |
| Apply one reviewed change and see the document update immediately | ✅ |
| Step through many changes one by one | ✅ |
| Stop review without publishing a final file | ✅ |
| Preflight large edit batches before creating output | ✅ |
| Diagnose missing, ambiguous, overlapping or dependent edits | ✅ |
| Repair problematic edits without restarting the whole batch | ✅ |
| Choose the exact occurrence when text appears multiple times | ✅ |
| Handle batches of up to **64 requested edits** | ✅ |
| Create a new final DOCX while preserving the original | ✅ |
| Autonomous repository modification | **Not exposed** |
| Unrestricted shell/process execution | **Not exposed** |
| Unsupervised Git mutation | **Not exposed** |

---

# Two core workflows

## 1. Repository investigation

ZAC can work as a local, bounded coding assistant for understanding an unfamiliar or evolving codebase.

~~~mermaid
flowchart LR
    A[Ask a repository question] --> B[Local AI reasoning]
    B --> C[Controlled investigation]
    C --> D[Read / search selected workspace]
    D --> E[Observed evidence]
    E --> F[Answer]
~~~

Typical uses include:

- locating where a feature is implemented;
- tracing a behavior across files;
- understanding a repository before making changes manually;
- finding relevant configuration or tests;
- investigating why a workflow behaves unexpectedly;
- asking architecture or codebase questions without giving the model unrestricted machine authority.

---

## 2. Supervised document editing

This has become one of ZAC's strongest practical workflows.

Attach a Word document and describe the changes naturally:

> “Change this heading, replace this sentence, and update these three skill rows.”

ZAC can turn that intent into a structured edit review while keeping the document visible beside the conversation.

~~~mermaid
flowchart TD
    A[Attach DOCX] --> B[Describe requested edits]
    B --> C[Interpret literal edit intent]
    C --> D[Deterministic preflight]
    D --> E{Everything clean?}

    E -->|Yes| F[Review changes]
    E -->|No| G[Show every issue]
    G --> H[Repair / choose occurrence / adjust text]
    H --> F

    F --> I[Apply selected change]
    I --> J[Live document preview updates]
    J --> K{More changes?}

    K -->|Yes| F
    K -->|No| L[Create updated DOCX]
    L --> M[Download new file]
~~~

### The review experience

The document viewer sits beside the chat rather than covering it.

You can:

- see **Change 4 of 23**;
- inspect the exact FIND text;
- edit the replacement at the last second;
- jump to the matching location in the document;
- apply the change;
- see the updated document immediately;
- move to the next change;
- go back;
- stop review;
- create the final file only when satisfied.

The original document remains preserved.

---

# Large-batch editing without blind trust

A long document can contain dozens of requested edits. Traditional “all-or-nothing” replacement is fragile: one bad instruction can make it difficult to know what happened.

ZAC now preflights the entire batch first.

### Example

A user supplies 38 edits to a CV, manuscript or report.

Instead of stopping at the first problem, ZAC can present a full review picture:

| Edit | Result | What the user can do |
|---:|---|---|
| 1 | Ready | Leave it for final creation |
| 2 | Ready | Leave it |
| 3 | Already applied | No action needed |
| 4 | Missing | Correct the FIND text |
| 5 | Ambiguous | Choose the intended occurrence |
| 6 | Ready | Leave it |
| 7 | Overlap / dependency | Review ordering or wording |
| … | … | … |
| 38 | Ready | Leave it |

This makes the workflow useful for documents where checking every line manually would be tedious.

~~~mermaid
flowchart LR
    B[Large edit batch] --> P[Preflight all changes]
    P --> R[Ready changes]
    P --> I[Issues requiring review]

    I --> M[Missing text]
    I --> A[Ambiguous text]
    I --> O[Overlapping / dependent edits]

    M --> FIX[Repair in review]
    A --> PICK[Choose exact occurrence]
    O --> FIX

    FIX --> DONE[Resolved]
    PICK --> DONE
    R --> FINAL[Final creation]
    DONE --> FINAL
~~~

---

# Ambiguous text is reviewable, not a dead end

If the same phrase appears several times, ZAC does not need to guess silently.

The review can expose:

**Previous occurrence · Occurrence 2 of 4 · Next occurrence**

The document view moves to each candidate so the user can choose the intended one before applying the replacement.

That turns ambiguity into an explicit user decision instead of an invisible model assumption.

---

# Natural language when useful, deterministic editing when necessary

ZAC deliberately separates two jobs.

| Job | Best suited to |
|---|---|
| Understand what the user means | Local language model |
| Extract literal requested wording | Model / deterministic parsing |
| Determine whether text actually matches | Deterministic software |
| Decide which ambiguous occurrence is intended | Human |
| Apply the approved replacement | Deterministic software |
| Decide when the final document should exist | Human |

For explicit FIND / REPLACE instructions, the model can be bypassed entirely.

For conversational requests, the model helps translate the user's language into literal intent, while the actual document operation remains constrained and reviewable.

---

# Formatting preservation

A useful document editor cannot destroy the document while changing its words.

ZAC's current DOCX workflow is designed to preserve the surrounding Word document rather than rebuilding a document from extracted plain text.

In live testing it has preserved:

- multi-page CV layouts;
- headings and typography;
- colored section styles;
- tables;
- aligned role/date rows;
- hyperlinks;
- paragraph spacing;
- structured skill sections;
- surrounding formatting when replacement text changes.

This makes the workflow practical for CV tailoring, structured reports, research material and other formatted Word documents.

---

# Product philosophy

## The model is not the authority

ZAC treats language-model output as interpretation or proposal, not proof that an action occurred.

## Human review is not a failure mode

For consequential document changes, review is part of the product.

The user can inspect, correct, continue or stop without surrendering the entire workflow.

## Deterministic software complements AI

The interesting part of applied AI is often deciding **where not to use the model**.

ZAC uses AI for ambiguity and language understanding while keeping exact validation, matching and controlled transformations in conventional software.

## Local-first changes the trust model

Local inference enables workflows around:

- private repositories;
- unpublished code;
- CVs and professional documents;
- research material;
- internal drafts;
- sensitive working files.

## Capability expands deliberately

More autonomy is not automatically better.

New abilities are added only when the surrounding validation, UX and testing make them useful and inspectable.

---

# What this project demonstrates

ZAC is also an engineering portfolio project showing work across several disciplines.

| Area | Demonstrated work |
|---|---|
| **AI agent engineering** | Tool-using language models, structured actions, bounded multi-step behavior |
| **Agent evaluation** | Live-model failure analysis, reproducible failures and regression-driven improvement |
| **Human-AI interaction** | Review, interruption, editable proposals, visible state and explicit confirmation |
| **Developer tooling** | Repository investigation and workflow-oriented product UX |
| **Applied AI product design** | Combining model judgement with deterministic application logic |
| **Document intelligence** | Natural-language editing, structured review and format-preserving DOCX transformation |
| **Software engineering** | C#/.NET, asynchronous workflows, browser interfaces, state management and validation |
| **Local AI systems** | Mistral-family local inference with llama.cpp/CUDA |
| **Reliability engineering** | Bounded operations, failure handling and extensive automated regression coverage |

The private project now has **close to 500 automated tests** across unit, integration, boundary, adversarial and UI-contract scenarios.

---

# Example product journeys

### “Help me understand this repository”

~~~text
Ask ZAC
→ local investigation
→ visible activity
→ evidence-based answer
~~~

### “Change one sentence in this CV”

~~~text
Attach DOCX
→ ask naturally
→ validate exact wording
→ review
→ apply
→ preview
→ create updated DOCX
~~~

### “Apply 40 changes to this report”

~~~text
Attach DOCX
→ provide batch
→ preflight all edits
→ review only the problematic ones
→ resolve ambiguity / missing text / dependencies
→ inspect live results
→ create final document
~~~

### “This phrase appears five times — change only the third one”

~~~text
Find phrase
→ show occurrence 1 of 5
→ navigate candidates
→ choose occurrence 3
→ apply
→ verify visually
~~~

---

# Technical profile

| Layer | Public technical profile |
|---|---|
| **Primary implementation** | C# / .NET 8 |
| **AI** | Local Mistral-family inference |
| **Serving / acceleration** | llama.cpp / CUDA |
| **Interface** | Browser-based Windows workspace |
| **Document workflows** | DOCX / Open XML |
| **Testing** | Unit, integration, boundary, adversarial and UI-contract testing |
| **Development approach** | AI-assisted implementation, live-model evaluation and regression-driven refinement |

This intentionally describes the technology surface rather than the private implementation architecture.

---

# Development status

**ZAC is in active private development.**

The project began as a constrained local coding agent and has evolved into a supervised AI workspace combining:

- repository investigation;
- local model reasoning;
- observable execution;
- attachments;
- document understanding;
- format-preserving DOCX editing;
- side-by-side live review;
- large-batch preflight;
- interactive repair;
- deterministic occurrence selection.

Current development continues to focus on:

- agent answer quality;
- retrieval quality;
- larger real-world document workflows;
- editing UX;
- live-model evaluation;
- reliability;
- carefully reviewed capability expansion.

ZAC is **not presented as a finished autonomous coding platform**, and the private implementation is not published as open source.

---

# Public / private boundary

This repository intentionally shows **what the product can do** without exposing how the private implementation is assembled.

### Public here

- user-facing capabilities;
- product direction;
- engineering principles;
- selected technologies;
- high-level workflows;
- non-sensitive development progress.

### Kept private

- source code;
- internal architecture;
- implementation composition;
- security internals;
- prompts and schemas;
- operational configuration;
- private test fixtures;
- internal endpoints and storage design;
- deployment-specific material.

---

# Project links

- **CodBio Hub:** https://home.codbiohub.com/
- **GitHub:** https://github.com/wilderruiz
- **LinkedIn:** https://www.linkedin.com/in/wilder-ruiz/

---

### Project note

ZAC is a private implementation / active-development project. Public documentation describes product behavior and engineering direction only.

Copyright © Wilder Ruiz. All rights reserved. Public documentation in this repository does not grant a licence to the private ZAC implementation.
