<div align="center">

# AutoPin-CS

English · [中文](README.zh.md) · [Español](README.es.md) · [Deutsch](README.de.md) · [Français](README.fr.md)

[GitHub @frommmmmg](https://github.com/frommmmmg)

✍️ By **姜芊泽 (Jiang Qianze)** · WeChat Official Account: **Pin海引航**

</div>

> **This repository is a showcase, not a source release.** AutoPin-CS is closed-source, so there is no code here, only what it does, how it is built and what it looks like. To talk about it, get in touch through my [GitHub profile](https://github.com/frommmmmg).

**A scheduler and fleet manager for large-scale social-media content operations.** A central server hands out work to a fleet of Windows clients, and an AI-agent layer lets an operator drive the whole system in plain language.

Running a large fleet of unattended desktop clients is mostly an operations problem. How do you roll out a new version without taking the fleet down? How do you bring a fresh machine online the same way every time? How do you find the one machine that is quietly failing? AutoPin-CS is the system built around those questions, and most of its code is about making answers repeatable, checkable and recoverable.

![Architecture](assets/autopin-architecture.svg)

| | |
|---|---|
| **Role** | Sole designer and maintainer of the server, the client, desktop control, deployment tooling and documentation |
| **Status** | In production. A private commercial system, so there is no public site |
| **Scale** | About 1,300 Python files, about 620 test files, 400+ architecture decision records and about 290 bug post-mortems |
| **Stack** | Python · Flask · uWSGI · MySQL · Windows services · browser automation · FFmpeg |

### What it does

**Server**
- **Central scheduling and administration.** A Flask/uWSGI service backed by MySQL manages tasks, orders, the client registry, task logs and results, backups and analytics.
- **Contracts and schema discipline.** Each table's schema is versioned and owned by one module, and the readiness check holds the schedulers back until the database is in the expected state.

**Client fleet**
- **Python daemons with several operating modes**, running browser-automation workflows: a long-running worker, a single-task mode driven by the server, and other task types.
- **A desktop agent that reaches through Windows session isolation.** It can see and drive the real user desktop, so remote diagnosis includes screenshots and process control instead of guesses from logs.
- **Video preparation.** A verified batch workflow normalises videos to a conservative H.264/AAC profile that even old Windows and browser combinations accept.

**Release engineering**
- **A release gate that never relaxes.** Every client upgrade is built as a full package, registered inactive, **verified on a real canary machine** and only then activated, with rollback ready. A green build, a unzipped package or a single heartbeat does not count as success.

**An AI-agent layer**
- **Operations as agent skills.** Bringing a new machine online, diagnosing a remote client, patrolling the schedulers, triaging unhealthy accounts and cutting a release are written as skills an AI agent can run. Each skill is a fixed sequence of steps with verification gates and an evidence read-back, started by one plain sentence from the operator.

## Screenshots

*Screenshots are left out on purpose: the admin console shows client and account data.*

## How it works

![A release is only activated after a real canary machine passes every gate.](assets/autopin-release-gate.svg)
*A release is only activated after a real canary machine passes every gate.*

![The operator speaks plainly; the agent runs a fixed runbook and reads the evidence back.](assets/autopin-agent-loop.svg)
*The operator speaks plainly; the agent runs a fixed runbook and reads the evidence back.*

<!--notes-->
## Engineering notes

- **Decisions are written down, and there are a lot of them.** More than 400 architecture decision records capture why things are the way they are, many of them about versioning and owning database schemas so that start-up and migrations stay predictable.
- **Bugs get a post-mortem and a sibling sweep.** Around 290 bug records each name the root cause, the regression test and a search for the same defect elsewhere. A bug is only closed once that sweep is done.
- **Evidence over hope.** A release counts as working only with real-machine evidence: stable process tree, desktop session, persisted success, no newer failure or rollback. Package checks include member lists, ZIP checksums, length, SHA-256 and compatibility with the oldest interpreter in the fleet.
- **Recovery is designed before it is needed.** Rollback paths, a verified restore route for the canary machine and a full-installer recovery playbook are written down, and the original failure logs are kept rather than overwritten.
- **Secrets stay out of code and command lines.** Credentials live in the operating system's keychain and are handed to tools at the moment of use.
- **Agents follow the same rules as people.** The agent skills are version-controlled in the repository, carry the same safety rules (no skipping the canary, no guessing which entry point a log came from) and must finish by confirming that the change was pushed.

<!--author-->
## About the author

<img src="assets/wechat-qr.png" alt="QR code of the WeChat Official Account Pin海引航" width="200" align="right">

**姜芊泽 (Jiang Qianze)** is a pen name. I am an independent developer who builds tools, data and automation for brands, merchants and creators going global. Every project in these showcases was designed, built and run end to end by me alone, from the product idea to the servers and the documentation.

I write about this work on my WeChat Official Account, **Pin海引航** (in Chinese). Scan the code to follow it, or find me on [GitHub](https://github.com/frommmmmg).

<br clear="right">
<!--/author-->

**Other showcases:** [AffProof](https://github.com/frommmmmg/AffProof-showcase) · [Tonu.app](https://github.com/frommmmmg/Tonu.app-showcase) · [AffiliateScraper](https://github.com/frommmmmg/AffiliateScraper-showcase)

---

<div align="center">

<sub>Screenshots use sample or public data only. © All rights reserved. Descriptions may be quoted with attribution; the software itself is not for redistribution.</sub>

</div>
