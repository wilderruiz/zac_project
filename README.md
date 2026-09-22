# ZAC — Zomniverse Agent for Code

> **A local-first AI workspace for controlled software investigation and human-supervised document workflows.**

[![Status](https://img.shields.io/badge/status-active%20private%20development-6f42c1)](#development-status)
[![.NET](https://img.shields.io/badge/.NET-8-512BD4)](#technical-profile)
[![Local AI](https://img.shields.io/badge/AI-local--first-0f766e)](#local-first-by-design)
[![Platform](https://img.shields.io/badge/platform-Windows-0078D4)](#technical-profile)
[![Authority](https://img.shields.io/badge/model%20authority-bounded-success)](#design-principles)

**ZAC** explores a practical question at the intersection of AI agents, developer tooling, reliability and product design:

> **How can an AI system be useful without making model output equivalent to authority?**

The implementation is private while the system is under active development. This repository is a public product and engineering overview only.

---

## The product idea

ZAC treats the model as an **interpreter and reasoning component**, not as the operating system.

The model can understand a request, propose what should happen and help structure intent. Deterministic software remains responsible for validating scope, enforcing boundaries, carrying out approved operations and reporting what actually happened.

~~~mermaid
flowchart LR
    U[Developer] --> Q[Natural-language task]
    Q --> Z[ZAC workspace]

    Z --> L[Local AI reasoning]
    L --> P[Structured proposal]

    P --> V{Deterministic validation}
    V -->|Allowed| A[Controlled action]
    V -->|Needs review| H[Human decision]
    V -->|Rejected| R[Safe failure]

    A --> O[Observable result]
    H --> O
    O --> U
~~~

The core principle remains:

> **The model proposes. Deterministic software validates. The user stays in control.**

---

## What ZAC can do today

| Product capability | Current state |
|---|---:|
| Understand and investigate a selected codebase | ✅ |
| Read repository files and search code/text | ✅ |
| Use a locally hosted language model | ✅ |
| Show software-confirmed activity instead of relying on model claims | ✅ |
| Bound long-running agent work and support cancellation | ✅ |
| Attach local documents to a conversation | ✅ |
| Rich DOCX preview inside the ZAC workspace | ✅ |
| Download generated documents | ✅ |
| Natural-language DOCX find/replace intent | ✅ |
| Multi-change DOCX batches | ✅ |
| Deterministic exact-match validation before document changes | ✅ |
| Preserve the original DOCX while creating an updated version | ✅ |
| Side-by-side chat + live document review | ✅ |
| Step through changes one at a time | ✅ |
| Edit FIND / REPLACE text during review | ✅ |
| Apply a reviewed change to a temporary working version and immediately preview it | ✅ |
| Stop review without publishing a final document | ✅ |
| Explicit final creation of the updated DOCX | ✅ |
| Autonomous repository modification | **Not exposed** |
| Unrestricted shell/process execution | **Not exposed** |
| Unsupervised Git mutation | **Not exposed** |

The goal is not maximum autonomy at any cost. The goal is **useful AI with visible authority boundaries**.

---

## Human-supervised document editing

One of ZAC's current product experiments extends the same control philosophy beyond repository investigation.

A user can attach a formatted Word document and ask naturally for one or many changes. ZAC interprets the request, validates the literal edits, and presents them in a side-by-side review workspace.

~~~mermaid
sequenceDiagram
    participant U as User
    participant Z as ZAC
    participant M as Local model
    participant D as Deterministic document engine
    participant V as Live document view

    U->>Z: Change this wording...
    Z->>M: Extract literal edit intent
    M-->>Z: FIND / REPLACE proposal
    Z->>D: Validate against document
    D-->>Z: Exact validated change
    Z->>V: Show location in context
    U->>Z: Review / edit / apply / continue
    Z->>V: Refresh working preview
    U->>Z: Create updated DOCX
    Z-->>U: New document; source preserved
~~~

### Why this matters

For a two-page CV, a batch replacement can be inspected manually. For a long report, manuscript or structured document, that stops scaling.

ZAC's review flow is designed around **progressive supervision**:

| Step | User experience |
|---|---|
| **Interpret** | Natural language can be converted into literal edit intent |
| **Validate** | The requested text must resolve deterministically |
| **Locate** | ZAC brings the matching content into view |
| **Review** | FIND and REPLACE are visible before application |
| **Adjust** | The user can alter the proposed text without abandoning the session |
| **Apply** | The working preview changes immediately |
| **Continue** | Move through the remaining edits one at a time |
| **Stop** | End the review session without publishing a final file |
| **Create** | Explicitly generate the updated DOCX when satisfied |

The original document remains the reference point; the workflow is built around review rather than silent rewriting.

---

## Local-first by design

ZAC is designed for workflows where source code and working documents may be private.

The current system uses local model inference so repository and document workflows can remain developer-controlled.

~~~mermaid
flowchart TB
    subgraph Local[Developer-controlled local environment]
        UI[ZAC workspace]
        AI[Local language model]
        DATA[(Selected code / attached documents)]
        RULES[Deterministic controls]
        UI <--> AI
        UI <--> RULES
        RULES <--> DATA
    end

    USER[Developer] <--> UI
~~~

- local language-model inference;
- explicit workspace scope;
- source documents preserved during transformation workflows;
- no assumption that model narration equals execution truth;
- bounded operations and explicit completion;
- private implementation and configuration remain outside this public repository.

---

## Engineering focus

ZAC brings together agent engineering and conventional software controls rather than treating them as competing approaches.

| Area | What the project demonstrates |
|---|---|
| **Agent systems** | Structured model actions, multi-step reasoning and tool-using workflows |
| **Evaluation & reliability** | Failure analysis, regression coverage, bounded execution and observable outcomes |
| **Human-in-the-loop UX** | Approval, review, interruption and last-second editing before final output |
| **Local AI** | Private-code workflows with developer-controlled model inference |
| **Document intelligence** | Natural-language editing backed by deterministic matching and preserved formatting |
| **Product systems** | Browser-based interaction, live state, asynchronous operations and reusable workflows |
| **Security mindset** | Capability expansion is treated as a design decision, not a default permission |
| **Developer experience** | Making system state visible instead of hiding agent behavior behind a chat box |

The private codebase currently carries **480+ automated tests** spanning unit, integration, boundary, adversarial and UI-contract scenarios. The exact internal test suite and implementation details remain private.

---

## Product thesis

Many AI coding products frame progress primarily as **more autonomy**.

ZAC is exploring a complementary direction.

### Useful autonomy should be inspectable
The user should be able to distinguish what the model suggested from what software actually validated and performed.

### Deterministic systems still matter
Language models are excellent at interpretation, reasoning and ambiguity. Exact matching, permission checks, document transformation and final state are often better owned by conventional software.

### Human review can be a product feature
Approval is not necessarily friction. In high-value workflows, the ability to inspect, edit, stop and continue can be the difference between an AI demo and software people trust.

### Local AI enables different products
Developer-controlled inference makes it practical to explore AI assistance around private repositories, unpublished research material and working documents without making hosted-model access a prerequisite.

### Capability should grow deliberately
ZAC starts from constrained authority and expands only when the surrounding validation, UX and testing are ready for it.

---

## Current interaction model

~~~mermaid
flowchart TD
    A[Ask ZAC] --> B{What kind of task?}

    B -->|Repository question| C[Investigate selected workspace]
    C --> D[Return evidence-based answer]

    B -->|Document edit| E[Interpret requested changes]
    E --> F[Validate exact matches]
    F --> G[Review changes side-by-side]
    G --> H{User decision}

    H -->|Edit| G
    H -->|Continue| I[Apply to working preview]
    I --> G
    H -->|Stop| J[Leave without final export]
    H -->|Create| K[Generate updated DOCX]
~~~

This interaction model is intentionally more explicit than a generic “AI changed your file” experience.

---

## Technical profile

| Layer | Public technical profile |
|---|---|
| **Primary implementation** | C# / .NET 8 |
| **Model integration** | Local Mistral-family inference through an OpenAI-compatible serving layer |
| **Acceleration** | llama.cpp / CUDA development environment |
| **Interface** | Browser-based desktop workspace |
| **Canonical platform** | Windows |
| **Document processing** | Open XML / DOCX workflows |
| **Testing** | Unit, integration, boundary, adversarial and UI-contract testing |
| **Development style** | AI-assisted development, rapid prototyping, live-model evaluation and regression-driven refinement |

This table intentionally describes the technology surface without publishing the private implementation architecture.

---

## What the project demonstrates professionally

For engineering teams, ZAC is evidence of work across:

- **AI agent design** — tool-using models, structured actions, context design and controlled multi-step behavior;
- **agent evaluation** — observing live-model failures, reproducing them and converting them into tests;
- **software engineering** — C#/.NET, asynchronous workflows, state management, validation and browser interfaces;
- **developer tooling** — repository investigation, review-oriented UX and local workflows;
- **product thinking** — turning real workflow friction into focused features rather than adding autonomy for its own sake;
- **human-AI interaction** — keeping users in the loop where correctness and intent matter;
- **local AI infrastructure** — integrating local inference into a practical application rather than a standalone model demo.

---

## Development status

**ZAC is in active private development.**

Current work has progressed from a read-only local coding-agent foundation into a broader supervised workspace that includes repository investigation, local document understanding and interactive document transformation.

The project is **not presented as a finished autonomous coding platform** and is **not currently published as an open-source implementation**.

Near-term development continues to focus on:

- real-world answer quality;
- retrieval and context quality;
- supervised editing UX;
- document workflow reliability;
- live-model evaluation;
- regression coverage;
- carefully reviewed capability expansion.

---

## Public / private boundary

This repository intentionally documents **what ZAC does and why the design matters** without publishing the private implementation.

### Public here

- product direction;
- capability progress;
- design principles;
- high-level technology choices;
- screenshots / demonstrations when appropriate;
- non-sensitive engineering outcomes.

### Kept private

- source code;
- internal architecture and composition;
- security implementation details;
- operational configuration;
- prompts and schemas;
- private test fixtures;
- internal routes, storage details and deployment-specific material.

That boundary makes the work visible to employers, collaborators and potential partners without turning the public overview into an implementation map.

---

## Project links

- **CodBio Hub:** https://home.codbiohub.com/
- **GitHub:** https://github.com/wilderruiz
- **LinkedIn:** https://www.linkedin.com/in/wilder-ruiz/

---

### Project note

ZAC is a private implementation / active-development project. Public documentation describes product behavior and engineering direction only.

Copyright © Wilder Ruiz. All rights reserved. Public documentation in this repository does not grant a licence to the private ZAC implementation.
