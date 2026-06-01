# YC Summer 2026: AI Coding Work Summary

**Author:** Diego Iruretagoyena  
**Project:** SCx, Supercomputer Explorer  
**Prepared for:** Y Combinator Summer 2026 application  
**Data sources:** Cursor parent-session transcripts, repository contribution metrics, and session evidence index. Subagent transcripts are excluded. Internal system names, exact paths, and local transcript IDs are generalized for external sharing.

## Executive Summary

I use AI coding agents as an execution partner inside a production engineering loop, not as a toy assistant. Over the SCx release cycle, I ran 68 parent AI coding sessions with sustained high-intensity usage, translating operator feedback into shipped functionality across desktop UX, backend orchestration, security remediation, and reliability work.

SCx is an internal operations platform for hyperscale GPU supercomputer infrastructure. It includes a WPF .NET desktop client for operators, an ASP.NET Core orchestration/service layer, shared contracts and auth components, and integrations with proprietary inventory, telemetry, and control-plane systems. The product is used in production-like operational contexts where correctness, access control, and safe execution matter.

My workflow with coding agents is structured: define acceptance criteria, split work into focused branches or worktrees, drive implementation, run validation and regression checks, review diffs, and ship in reviewable increments. I remain the system owner making architecture, safety, and release decisions while using agents to increase throughput.

## What I Built

My work centered on production operations for SCx:

- Led a release stream of SCx client improvements, including 11 PRs in the `scx-release-6` train.
- Improved operator workflows for node selection, right-click actions, copy/clipboard behavior, source transparency, sorting, empty states, and post-operation visibility.
- Advanced source-of-truth behavior for repave and node-state operations, reducing ambiguity around data source and operational execution paths.
- Built and refined operation result visualization so operators can understand failures, partial success, and follow-up action more quickly.
- Contributed security remediation follow-through, including CVE-related dependency and SDK updates with traceability back to backlog/work items.
- Used branch-per-feature and isolated worktree execution to parallelize development while keeping changes reviewable.

## AI Coding Usage Metrics

Parent-session transcript metrics:

- Total AI coding sessions: 68
- Total user turns: 882
- Total assistant turns: 4,024
- Total tool calls: 2,913
- Sessions with explicit tool traces: 35
- Sessions with coding work: 35
- Sessions with code edits: 24
- Multi-turn sessions: 58
- Average user turns per session: 12.97
- Average tool calls per session: 42.84

Session intent breakdown:

- Implementation: 36
- Bug fixing: 8
- Documentation writing: 4
- Analysis/review: 2
- Git/PR workflow: 2
- Other: 16

Most-used tools in recorded sessions:

- Shell: 1,128 calls
- Read: 610 calls
- StrReplace: 450 calls
- Grep: 348 calls
- TodoWrite: 95 calls
- Glob: 84 calls
- Task/subagent orchestration: 44 calls

## Repository Contribution Metrics

Git metrics scoped to `SCx`:

- Commits: 176
- Active development days: 46
- Date span: 2026-01-13 to 2026-05-29
- Lines changed: +32,655 / -15,161

Top touched implementation areas:

- Node operations client logic: 31 touches
- Fleet/node overview client logic: 19 touches
- Datacenter service integration: 18 touches
- Node operations UI: 17 touches
- Fleet/node overview UI: 16 touches
- Shared inventory/telemetry client: 15 touches
- Backend operations service: 12 touches

## How I Work With Coding Agents

My agent workflow is execution-oriented:

- I give concrete prompts tied to production context, branch targets, constraints, and acceptance criteria.
- I break large asks into multiple focused streams, then converge them into reviewable PRs.
- I use agents for repository navigation, implementation, refactoring, validation, regression review, PR hygiene, and release documentation.
- I keep loops tight: investigate, implement, build/test, review diffs, refine, and merge.
- I prioritize operational correctness and safety over broad refactors, especially in production-critical paths.

The agent is a force multiplier, but I remain accountable for technical direction, tradeoffs, and release quality.

## Representative Evidence

Representative parent sessions covered:

- Release decomposition and multi-branch execution
- Branch-scoped operations UX development
- Source-of-truth migration validation for repave workflows
- Inventory/telemetry source architecture review
- Reset node health feature implementation
- Regression-risk PR review
- Security CVE batch fixes
- Security backlog traceability
- Personal impact quantification workflow
- Contributor and system overview synthesis

High-intensity examples from the transcript metrics:

- Session A: 52 user turns, 333 assistant turns, 420 tool calls
- Session B: 25 user turns, 309 assistant turns, 376 tool calls
- Session C: 19 user turns, 202 assistant turns, 276 tool calls
- Session D: 7 user turns, 236 assistant turns, 229 tool calls

## Application Narrative

I have been using AI coding agents to compress the distance between operator feedback and shipped infrastructure software. On SCx, a production-focused supercomputer operations platform, I used agents across the full engineering loop: scoping, code search, implementation, validation, PR preparation, regression review, security remediation, and release documentation.

This was not one-off prompting. It was sustained agentic engineering across 68 parent sessions, 2,913 recorded tool calls, and 176 repository commits over 46 active development days. The work produced concrete product improvements for operators managing GPU supercomputer fleets: safer node operations, clearer operation results, better source transparency, improved selected-node workflows, and stronger security/dependency hygiene.

The important pattern is that I am not outsourcing judgment. I use AI to increase the number of high-quality build-debug-ship loops I can run while I stay responsible for architecture, production safety, validation, and final release decisions.
