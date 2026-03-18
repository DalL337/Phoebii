# Phoebii

A human-first orchestration framework for Claude Code.

Most AI coding frameworks assume you already know what you're building. Phoebii solves the lead-in — it interviews you first, establishes a design foundation, keeps your project grounded in scope, and connects every agent decision back to a single source of truth.

## Install

Copy the contents of this folder into your project root:

```
your-project/
├── .claude/
│   └── commands/        ← Phoebii agent commands
├── .phoebii/
│   ├── design/          ← design tokens + preview (populated by init)
│   ├── docs/plans/      ← PRD, WBS, ADR, RFC, Spec templates
│   ├── futures/         ← ideation log (managed by /scope)
│   ├── interview/       ← interview questions reference
│   └── reference/       ← YAML agent specs (documentation only, safe to delete)
├── CLAUDE.md            ← governance file (read by Claude Code automatically)
└── README.md            ← this file
```

That's it. No dependencies. No build step. No runtime.

## Getting Started

After copying the files into your project:

```
/phoebii-init
```

This starts a guided interview that asks about your project, stack, platform, and design preferences. When it's done, it generates:

- `project.context.md` — the single source of truth every agent reads
- `CLAUDE.md` — populated governance file with always-on rules
- `tokens.md` — your design system (if the project has a UI)
- `preview.html` — visual preview of your design tokens

## Commands

| Command | What it does |
|---------|-------------|
| `/phoebii-init` | Initialize project — interview, context, design foundation |
| `/code` | Write, refactor, and wire up code |
| `/scope` | View project scope, review parked ideas |
| `/design` | View or edit design tokens |
| `/plan` | Write PRDs, ADRs, RFCs, WBS, or Tech Specs |
| `/arch` | Architecture decisions and structure |
| `/test` | Test strategy and writing |
| `/debug` | Failure investigation |
| `/review` | Multi-lens code and product audit |
| `/doc` | README, inline docs, changelog, API docs |
| `/research` | Look up libraries, frameworks, or market data |
| `/business` | Feature evaluation, personas, monetization |
| `/futures` | Review and manage parked ideas |
| `/tdd on/off` | Toggle test-driven development mode |

## How It Works

### Three Layers

**1. Interview** — Before any code, Phoebii asks what you're building, who it's for, what stack you're using, and what your design preferences are. The answers become your project context.

**2. Agents** — 13 purpose-built agents for different aspects of development. Each one reads your project context before acting, respects the scope, and knows when to hand off to another agent.

**3. Governance** — `CLAUDE.md` carries always-on rules that Claude Code reads every interaction. Scope watching catches ideation drift. Design enforcement catches token violations. No slash command needed — they run passively.

### Always-On Behavior

Two agents run passively through the governance file:

- **Scope Watcher** — When you suggest something outside the current phase, it parks the idea warmly in your futures log and keeps moving. Never blocks.
- **Design Enforcement** — When code touches UI, it checks that colors, fonts, spacing, and icons trace back to your design tokens. Flags drift, doesn't overwrite.

### Single Source of Truth

`.phoebii/project.context.md` is the brain. Every agent reads it before doing anything. Stack choices, platform targets, scope boundaries, design references — all in one file. Change it here and the change propagates.

## Governance File

By default, Phoebii uses `CLAUDE.md` because Claude Code reads it automatically. If you prefer `AGENTS.md` (to keep Phoebii governance separate), choose it during init and Phoebii will configure `.claude/settings.json` to point to it.

## Reference Specs

The `.phoebii/reference/` folder contains the original YAML agent specifications. These are documentation only — they describe the design intent behind each agent but have no effect on behavior. The executable versions are in `.claude/commands/`. The reference folder is safe to delete if you don't need it.

## Design System

For projects with a UI layer, Phoebii sets up a design token system during init:

- **tokens.md** — Single source of truth for colors, typography, spacing, icons, border radius, shadows, and animation
- **preview.html** — Self-contained HTML page that renders all tokens visually with a light/dark toggle

All UI code built by `/code` references these tokens. `/design` enforcement catches hardcoded values that should be tokens.

## Scope Management

Phoebii doesn't block ideas — it parks them. When you suggest something outside the current phase:

1. The scope watcher acknowledges the idea warmly
2. Parks it in `.phoebii/futures/ideation.md` with context
3. Adds a reference to the governance file
4. Resumes current work

Run `/futures` to review parked ideas. Pull them back in when the time is right.

### Enforcement Modes

The `scope.enforcement` setting in `project.context.md` controls how strictly scope is enforced:

- **`soft`** (default) — flags drift, parks the idea, but lets you override with no friction
- **`firm`** — requires explicit confirmation ("Yes, override scope") before building anything out of scope, and logs the override in the governance file

## Requirements

- Claude Code (Claude's CLI tool)
- That's it
