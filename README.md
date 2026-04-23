# The Chief Tribe

> A three-layer architecture for working with AI coding agents — without locking yourself into any single tool.

The Chief Tribe is an ecosystem of three open-source projects that together address **harness engineering** — the practice of designing what wraps around an AI model to turn it into a useful agent. Each layer serves a different purpose, and you can adopt them independently or as a full stack.

```
┌─────────────────────────────────────────────────────┐
│  chieftain                                          │  👑
│     Fully harnessed runtime + opinionated defaults  │
│  ┌───────────────────────────────────────────────┐  │  ⚔️
│  │  chief                                        │  │
│  │     Portable framework + workflow structure   │  │
│  │  ┌─────────────────────────────────────────┐  │  │
│  │  │  sage                                   │  │  │  🧙 
│  │  │     Baseline behavior principles        │  │  │
│  │  └─────────────────────────────────────────┘  │  │
│  └───────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────┘
```

## Members of the Tribe

| Project | Role | Opinion Level | Status |
|---------|------|---------------|--------|
| **[sage](https://github.com/thaitype/sage)** 🧙 | Baseline behavior principles for any agent | None | Planned |
| **[chief](https://github.com/thaitype/chief)** ⚔️ | Portable multi-agent workflow framework | Low | Active (formerly `chief-agent-framework`) |
| **[chieftain](https://github.com/thaitype/chieftain)** 👑 | Opinionated runtime + distribution | High | Planned |

## Why Three Layers?

Different people need different things. A developer trying out an agent for the first time has nothing in common with a developer who wants a ready-to-ship workflow for their Azure project. Forcing them into the same tool produces something that serves neither well.

The tribe separates concerns:

- **sage** gives you baseline behavior principles for any agent — think before acting, keep things simple, make surgical changes, work toward verifiable goals
- **chief** gives you a structured workflow (plan → build → verify) without opinion about your tech stack
- **chieftain** gives you the full package — runtime, presets, integrations — opinionated for a specific way of working

Each layer builds on the one below. You can stop at any layer depending on how much you want to bring yourself.

## Which One Should I Use?

### Use `sage` if...

- You want sensible baseline behavior from your agent, regardless of which one you use
- You're evaluating different agents and want consistent behavior across them
- You want a quick, no-commitment improvement to agent output quality
- You have your own workflow and just want good defaults underneath

### Use `chief` if...

- You want a structured workflow for AI coding agents (chief/builder/tester pattern)
- You work across multiple agents (Claude Code, OpenCode, Copilot, Codex, etc.) and want one framework that works with all of them
- You want milestone-based planning, review gates, and retrospectives
- You're happy to configure your own tech stack rules in `AGENTS.md`

### Use `chieftain` if...

- You want everything set up — CLI, team orchestration, persistent state, HUD, hooks
- You want a productivity system, not a framework to configure
- You're comfortable adopting someone else's opinions about workflow, tooling, and conventions
- You want parallel agent execution (tmux-based team runtime)

### Still not sure?

| You are... | Start with |
|------------|-----------|
| A developer who wants better agent behavior today | `sage` |
| A developer who wants structure but hates lock-in | `chief` |
| A developer who wants the full experience out of the box | `chieftain` |
| Experimenting and want to learn the philosophy | Read this repo first, then pick |

## The Philosophy

### Harness Engineering

The AI engineering community has evolved through three phases:

1. **Prompt engineering** — crafting individual prompts to get better outputs
2. **Context engineering** — managing what goes into the model's context window
3. **Harness engineering** — designing the entire system that wraps the model

Modern coding agents are defined by the equation:

```
Agent = Harness + Model
```

The harness is everything around the model: system prompt, tools, agent loop, context management, UI, session handling, permission layer, integrations. Two agents running the same model can behave completely differently depending on their harness.

The tribe exists because **harness engineering deserves the same rigor as model development**. That means:

- Separating baseline behavior from framework and opinion
- Making frameworks agent-agnostic where possible
- Letting users control what goes into their model's context
- Providing clear opt-in layers for more opinion

### Human-AI-Rule Triangle

The tribe is built around a simple principle: AI agents work best when responsibilities are clearly divided between humans, AI, and the rules system.

- **Humans** define direction and rules
- **AI** executes against clear specifications
- **Rules** (files) are the persistent artifact that bridges the two

This means fewer tokens wasted re-explaining context every session, clearer escalation paths when agents get stuck, and a project that stays coherent as it grows.

### Agent-Agnostic Design

The tribe never assumes a specific coding agent. Every layer is designed to work with:

- Claude Code
- OpenCode
- Codex CLI
- GitHub Copilot
- Gemini CLI
- Amp
- Cursor
- Pi
- Windsurf, Kiro, Aider, and any tool that reads `AGENTS.md`

When something is agent-specific (e.g., Claude Code's `.claude/` directory), it's handled through an adapter layer — not baked into the core.

## Architecture

### Dependency Chain

```
chieftain  ──uses──▶  chief  ──uses──▶  sage
```

- **sage** has no dependencies — it's a standalone baseline useful on its own
- **chief** uses `sage` as its behavioral foundation, adds framework structure
- **chieftain** uses `chief` as its framework, adds runtime + opinion

You can use any layer standalone. Each one works without the layers above it.

### What Each Layer Contains

**sage**
- Four behavior principles: Think Before Acting, Simplicity First, Surgical Changes, Goal-Driven Execution
- Agent-agnostic — works with any tool that reads an instructions file
- No directory structure, no workflow, no tooling — just behavior

**chief**
- Everything in `sage`
- 3-agent architecture (chief, builder, tester) + optional review-plan agent
- Rules hierarchy (AGENTS.md > .chief/\_rules > milestone goals)
- File-based state management (`.chief/` directory with milestones, goals, contracts, plans, reports)
- Core skills: `plan-milestone`, `autopilot-chief`, `retro-chief`, `dump-commit`, `grill-me`
- Adapters for Claude Code, Copilot, OpenCode, and others

**chieftain**
- Everything in `chief`
- CLI wrapper with opinionated defaults
- tmux-based team runtime for parallel workers
- Persistent state (`.chieftain/` with sessions, memory, logs)
- HUD / status line integration
- Pre-configured MCP servers
- Opinionated presets (tech stack, language, conventions)
- Hooks system for quality gates

## Getting Started

Each layer has its own installation guide. Pick your entry point:

- 🧙 **[Install sage](https://github.com/thaitype/sage#setup)** — drop baseline principles into any agent
- ⚔️ **[Install chief](https://github.com/thaitype/chief#setup)** — set up the framework
- 👑 **[Install chieftain](https://github.com/thaitype/chieftain#setup)** — get the full distribution

## Roadmap

- [x] v2 of `chief-agent-framework` released (now renamed to `chief`)
- [ ] Extract baseline behavior principles into `sage`
- [ ] Refactor `chief` to use `sage` as its baseline
- [ ] Ship `chieftain` v0.1 with CLI + tmux runtime
- [ ] Cross-tribe benchmark suite (test harness+model combos)
- [ ] Blog series on harness engineering

## Contributing

Each repository has its own contributing guide. This repo (`chief-tribe`) accepts contributions to:

- Documentation and philosophy
- Architecture diagrams
- Translation (currently English + Thai)
- Cross-cutting concerns that affect multiple layers

For code contributions, head to the relevant layer's repo.

## Acknowledgements

The tribe's design draws on many sources:

- [Andrej Karpathy's observations on LLM coding pitfalls](https://x.com/karpathy/status/2015883857489522876) — the root inspiration for the behavior principles in `sage`
- Forrest Chang's [andrej-karpathy-skills](https://github.com/forrestchang/andrej-karpathy-skills) — packaged those observations into a Claude Code `CLAUDE.md`, which `sage` adapts into an agent-agnostic baseline
- Mario Zechner's [pi](https://pi.dev/) and his [blog post on minimal coding agents](https://mariozechner.at/posts/2025-11-30-pi-coding-agent/) — the clearest articulation of harness engineering principles
- The `AGENTS.md` convention pioneered across OpenCode, Amp, and others
- oh-my-\* ecosystem (oh-my-zsh, oh-my-codex, oh-my-openagent) — inspiration for the distribution layer pattern
- Matt Pocock's `grill-me` skill — embedded in `chief`

## License

MIT — see individual repositories for specifics.

---

*"Harness engineering, done tribally."*
