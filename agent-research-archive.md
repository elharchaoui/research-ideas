# An Archive for Agent Research

> **Core hypothesis:** Agents now run huge amounts of research, and most of it — intermediate results, dead ends, small confirmations — never becomes a paper and dies in a chat log. A shared archive, written by agents, validated by agents, and queried by agents, would let them build on each other's work instead of reinventing the wheel.

---

## The Problem

Research agents produce far more results than humans can read or publish. Almost all of it is lost:

- Intermediate and negative results are never written up, so the same experiments get re-run again and again.
- What does get shared is shaped for human readers (PDFs, prose), not for an agent that needs to know "was this exact thing tried, and what happened?"
- Human peer review is already saturated and cannot absorb this volume.

---

## The Idea

A shared memory layer for research agents, something like an arXiv where the authors, the reviewers and the readers are all agents.

- **The claim is the unit, not the paper.** Each entry is a structured claim (hypothesis, method, setup, result) plus evidence: code, data and a run trace.
- **Every claim has a status:** unverified, reproduced, or contradicted.
- **Validation is by execution.** The platform re-runs the code in a sandbox and checks that the outputs match the claim, using different models than the one that produced the work.
- **Search is semantic and structured.** RAG-style retrieval finds related work; structured fields and trust signals tell the agent whether to rely on it.
- **Access is agent-native.** It ships as an MCP server, plugin and skills, so any agent can search before starting work and submit when it finishes.

### Minimal MCP surface

| Tool | Purpose |
| --- | --- |
| `search_prior_work(question)` | Returns matching claims with status and evidence links |
| `get_entry(id)` | Returns the full trace, code and environment |
| `submit_finding(...)` | Takes a structured claim plus artifacts |
| `report_outcome(id, reproduced \| contradicted)` | Agents that reuse an entry report back what happened |

`report_outcome` is the key one: validation then comes from usage, not only from the platform's own reviewers. Semantic search over documents is easy to copy; a graph of claims with reproduction history is not.

---

## Open Research Questions

- **Slop flood:** Generation is nearly free. What cost or bar on submission keeps quality above volume?
- **Correlated errors:** Agents validating agents share blind spots. How much validator diversity and human spot-auditing is enough?
- **Contamination:** How do we stop errors compounding when agents cite unverified agent work?
- **Security:** Every entry is text other agents will ingest, so the archive is a prompt-injection and poisoning target. How should entries be sanitized and served?
- **Incentives:** Everyone wants to read and few want to write. Can submission be automatic at the end of a research run, with one human approval?
- **Privacy:** How do we handle scrubbing, embargoes, and private or team scopes for unpublished work?
- **Scope:** "Reproduced" is cheap to check in ML experiments or computational maths. What does it mean in fields that need wet labs or judgment?
- **Cold start:** How many seeded, verified entries does one narrow domain need before the first search is useful?

---

## Why This Matters

- Less duplicated compute and time across the whole agent ecosystem
- Negative results finally get recorded, which is what prevents the most wasted work
- A trust layer for agent-produced science, with provenance (model, tools, prompts, human sponsor) on every claim
- A foundation for agents that cumulatively build knowledge instead of starting from zero each run

---

## Status

Idea stage. No code yet. The likely first step is one narrow, automatically verifiable domain, seeded with a few thousand verified entries.

---

## References

- arXiv, as the model for open pre-publication sharing
- aiXiv and the Agents4Science conference, as early attempts at agent-authored research venues
- Model Context Protocol (MCP), as the access layer
