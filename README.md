<div align="center">

# AutoPin-CS

English · [中文](README.zh.md) · [Español](README.es.md) · [Deutsch](README.de.md) · [Français](README.fr.md)

</div>

> **This repository is a showcase, not a source release.** AutoPin-CS is a private project, so there is no code here, only what it does, how it is built and what it looks like. To talk about it, get in touch through my [GitHub profile](https://github.com/frommmmmg).

**A scheduler and fleet manager for large-scale social-media content operations.** A central server hands out work to a fleet of Windows clients, and an AI-agent layer lets an operator drive the whole system in plain language.

![AutoPin-CS architecture](assets/autopin-architecture.svg)

**Highlights**

- **Central scheduling and admin.** A Flask/uWSGI service backed by MySQL manages tasks, clients, orders and analytics.
- **A client fleet of Python daemons** running browser-automation workflows, with several operating modes for different job types.
- **Safe releases.** Every client upgrade is built as a full package, registered, **verified on a real canary machine** and only then activated, with rollback ready. Full rollout without a canary is forbidden by design.
- **Operations as agent skills.** Provisioning a new machine, diagnosing a remote client, patrolling the schedulers and cutting a release are written as skills an AI agent can run, triggered by a one-line instruction from the operator.
- **Written-down engineering discipline.** ADRs, system contracts, runbooks and a bug-record process that checks for sibling defects before a bug is closed.
- **Scale.** Thousands of files across server, client, desktop control, deployment and test code.

**Stack:** Python · Flask · uWSGI · MySQL · Windows services · Playwright-style browser automation · FFmpeg

## Screenshots

*Screenshots are left out on purpose: the admin console shows client and account data.*

## How it works

![A release is only activated after a real canary machine passes every gate.](assets/autopin-release-gate.svg)
*A release is only activated after a real canary machine passes every gate.*

![The operator speaks plainly; the agent runs a fixed runbook and reads the evidence back.](assets/autopin-agent-loop.svg)
*The operator speaks plainly; the agent runs a fixed runbook and reads the evidence back.*

---

<div align="center">

<sub>Screenshots use sample or public data only. © All rights reserved. Descriptions may be quoted with attribution; the software itself is not for redistribution.</sub>

</div>
