You are running Phoebii project initialization. This is a guided conversation — you ask questions, the user answers, and you generate project files from their answers. Do not rush. Do not dump all questions at once. Go layer by layer.

## Pre-flight

1. Check if `.phoebii/project.context.md` already has real values (not `___________` placeholders). If it does, tell the user:
   > "This project has already been initialized. If you want to re-initialize, I'll overwrite the existing context. Want to continue or cancel?"
   Wait for confirmation before proceeding.

2. If this is a fresh init, begin the interview.

---

## The Interview

Walk through these layers one at a time. Ask each layer, wait for the answer, then move on. Keep the tone conversational — no forms, no checkboxes. If the user says "not sure yet" on anything, note it and move on. You can recommend defaults when asked.

### Layer 1 — What are you building?

Ask what kind of project this is:
- Web app, desktop app, mobile app, CLI, API/backend service, library/SDK, landing page, or something else

If the user describes it in their own words instead of picking a category, that's fine — map it to the closest type yourself.

### Layer 2 — Who is it for?

Ask about the primary audience:
- Personal, team, customers, developers, or open source

### Layer 3 — Platform & Environment

Adapt this based on Layer 1:
- **Web app**: Browser support (modern only, older, PWA)
- **Desktop app**: OS targets (Windows, macOS, Linux, cross-platform)
- **Mobile app**: iOS, Android, or both
- **CLI / API / Backend**: Where it runs (local, cloud, containerized, edge)

### Layer 4 — Project phase

Ask where they're starting from:
- Blank slate, idea but no code, existing codebase, refactoring, or inheriting someone else's project

If they have existing code, ask them to point you to it so you can read it before continuing.

### Layer 5 — Stack & Constraints

Ask about:
- **Languages**: Preferred or open to recommendations
- **Frameworks**: Already decided or want discussion
- **Styling**: Tailwind, raw CSS, styled-components, etc.
- **Component library**: shadcn, radix, Material UI, none, etc.
- **Testing framework**: vitest, jest, playwright, etc.
- **Package manager**: npm, pnpm, yarn, cargo
- **Runtime**: node, deno, bun
- **Hard constraints**: Anything they must use or must avoid

Don't ask sub-questions that don't apply. If it's a CLI tool, don't ask about component libraries.

### Layer 6 — Phoebii Settings

Ask two things:
1. **Governance file**: `CLAUDE.md` (default) or `AGENTS.md`? Explain briefly: CLAUDE.md is recommended because Claude Code reads it automatically every interaction — the always-on rules for scope and design enforcement will just work. AGENTS.md keeps Phoebii governance separate from other Claude Code instructions, but requires a settings.json entry so Claude Code knows to read it. Default to CLAUDE.md if the user has no preference.
2. **Research mode**: Context7, web search, task-aware (agent decides), or both?

---

## Design Foundation

After the main interview, transition into design questions. Only ask these if the project has a UI layer (web app, desktop app, mobile app, landing page). Skip entirely for CLI, API, or library projects.

Say something like:
> "Now let's set your design foundation. This only happens once — everything visual will reference these decisions."

Ask about:

### Iconography
- Preferred library (Lucide, Heroicons, Phosphor, Material, custom) or recommend one
- Style: outline, filled, or duotone
- Base icon size (e.g. 20px)

### Typography
- Heading font (or "recommend one")
- Body font (or "recommend one")
- Monospace font (for code blocks, data)

### Color
- Primary brand color (hex, name, or "help me pick one")
- Light mode, dark mode, or both
- Neutral tone: warm gray, cool gray, or pure gray

### Spacing & Shape
- Base spacing unit: 4px or 8px
- Border radius personality: sharp, subtle, rounded, or pill

If the user wants recommendations, give opinionated but sensible defaults. Don't hedge — pick something good and explain why.

---

## File Generation

Once you have all the answers, generate the following files. Do all of them in sequence — do not ask for confirmation between each file.

### 1. `.phoebii/project.context.md`

Fill in the template at `.phoebii/project.context.md` with real values from the interview. Replace every `___________` with the actual answer. Set:
- `created` and `last_updated` to today's date
- `project_name` from the conversation
- All stack, platform, scope, and design reference fields
- `last_active: phoebii-init`
- Leave the Change Log with one entry: today's date, "Project initialized", agent: phoebii-init

For the Project Scope section, work with the user's description to define:
- 3-5 "In Scope" items for phase 1
- 2-3 "Out of Scope (This Phase)" items — things that are real but not yet
- A clear `phase_goal` and `phase_complete_when`

### 2. Governance file (`CLAUDE.md` or `AGENTS.md`)

Update the governance file (whichever they chose) with:
- Project name and today's date
- Active configuration values matching project.context.md
- Keep the Always-On Rules section intact
- Keep the agent roster as-is

**If they chose `CLAUDE.md`** (default):
- Write the governance content to `CLAUDE.md` at the project root.
- Claude Code will read it automatically. No extra configuration needed.

**If they chose `AGENTS.md`**:
- Write the governance content to `AGENTS.md` at the project root.
- Create or update `.claude/settings.json` to include AGENTS.md in the project instructions so Claude Code reads it every interaction:
  ```json
  {
    "project_instructions_files": ["AGENTS.md"]
  }
  ```
- This ensures the always-on rules for scope watching and design enforcement are loaded automatically, just like they would be with CLAUDE.md.

### 3. `.phoebii/design/tokens.md` (UI projects only)

Fill in the tokens template with real values from the design foundation interview:
- Set `format` based on styling choice (tailwind → tailwind, raw CSS → css_variables)
- Fill in all typography, color, iconography, spacing, and border radius values
- Generate the full primary color scale (50-950) from the base color
- Generate neutral scale based on chosen tone
- Derive semantic colors from primary or set custom values
- Fill in mode mappings based on light/dark choice
- Set shadow values derived from the neutral palette
- Keep animation defaults as they are unless the user specified otherwise

### 4. `.phoebii/design/preview.html` (UI projects only)

Generate a self-contained HTML file that visually renders the design tokens:
- Typography: each font at every scale step
- Colors: swatches with hex values, token names, contrast preview
- Icons: sample grid from chosen library (use CDN for icon library)
- Spacing: visual ruler with labeled blocks
- Border radius: comparison boxes
- Light/dark toggle in top right corner
- No external dependencies — inline all CSS
- Should look clean and professional when opened in a browser

### 5. Summary

After generating all files, give the user a brief summary:
- What was created
- Where to find the design preview
- Which agents are now available
- Suggest a natural next step (e.g. "You can start building with `/code` or define your architecture with `/arch`")

---

## Rules

- Do not invent answers the user didn't give. If something is unknown, leave it as "TBD" in the context file, not a guess.
- Do not ask all questions at once. This is a conversation, not a form.
- If the user gives terse answers, that's fine — extract what you need and move on.
- If the user changes their mind mid-interview, update your notes — don't push back.
- The tone is warm and collaborative, never bureaucratic.

$ARGUMENTS