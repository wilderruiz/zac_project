# ZAC — Zomniverse Agent for Code

**Private developer-AI research presented through a public project overview.**

ZAC explores a practical question: how can an AI coding assistant help investigate a software repository while keeping authority, permissions, and final decisions under human control?

The project is an actively developed C#/.NET workspace for local, read-only code investigation. It combines AI-assisted reasoning with explicit operating boundaries, observable activity, cancellation, auditability, and automated verification.

> **The model proposes. The controller validates. Only the controller acts.**

## Why ZAC exists

AI can accelerate software understanding, but useful developer tooling must do more than generate plausible text. It must respect the workspace, communicate what it is doing, fail safely, and preserve a clear boundary between a model's suggestions and actions performed by software.

ZAC is being developed to examine that boundary in a real developer workspace. Its current focus is trustworthy repository investigation rather than unrestricted autonomy.

## Current capabilities

The private development build currently demonstrates:

- Local AI-assisted investigation of source repositories.
- Read-only file discovery, inspection, and code search.
- Structured, permission-bounded operations.
- Workspace containment and explicit scope control.
- Visible progress, cancellation, and recorded activity.
- Browser-based interaction within a Windows-first developer workflow.
- Automated testing of expected behavior and failure conditions.
- Local inference support, allowing sensitive project material to remain within the developer-controlled environment.

ZAC does **not** currently present autonomous editing, unrestricted shell access, arbitrary network activity, or unsupervised Git mutation as available capabilities.

## What the project demonstrates

ZAC is portfolio evidence of end-to-end engineering across:

- C# and .NET 8 application development.
- Local language-model integration.
- Human-centered developer experience.
- Security-conscious agentic software design.
- Asynchronous and cancellable workflows.
- Validation, observability, and audit-oriented behavior.
- Windows tooling and browser-based product interfaces.
- Automated regression and boundary testing.

The emphasis is not simply on connecting an application to a language model. It is on turning probabilistic model output into a controlled, understandable, and testable software experience.

## Who it is relevant to

ZAC may be of interest to:

- **Employers** looking for evidence of AI systems engineering, .NET development, security-minded implementation, and product ownership.
- **Research and engineering partners** exploring private, local, or governed AI-assisted development workflows.
- **Investors and product collaborators** interested in trustworthy developer tooling and human-controlled agentic systems.
- **Organizations with sensitive codebases** evaluating ways to gain AI assistance without treating unrestricted autonomy as the default.

## Development status

ZAC is in **active private development**. The present milestone concentrates on read-only repository understanding and dependable operating boundaries. Broader capabilities will only be considered when they can preserve explicit authorization, traceability, and human control.

This repository is a public project facade. It intentionally does not contain ZAC's private source code, internal architecture, operational configuration, security controls, prompts, test fixtures, or deployment material.

## Collaboration

Conversations about engineering roles, research collaboration, product partnerships, responsible AI tooling, and potential investment are welcome.

- [CodBio Hub](https://home.codbiohub.com/)
- [Wilder Ruiz on LinkedIn](https://www.linkedin.com/in/wilder-ruiz/)
- [Wilder Ruiz on GitHub](https://github.com/wilderruiz)

---

Copyright © Wilder Ruiz. All rights reserved. Public documentation in this repository does not grant access to, or a licence for, the private ZAC implementation.
