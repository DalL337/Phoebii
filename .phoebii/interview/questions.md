# Phoebii Interview
## Project Initialization Questions

Welcome! Before we spin anything up, I have a few questions to make sure everything we build together is set up the right way for *your* project. Take your time — there are no wrong answers, and you can always say "not sure yet" and we'll revisit it.

---

## Layer 1 — What are you building?

Let's start at the top. What kind of thing are you making?

- [ ] Web app
- [ ] Desktop app
- [ ] Mobile app
- [ ] CLI tool
- [ ] API / backend service
- [ ] Library, framework, or SDK
- [ ] Landing page or marketing site
- [ ] Something else — describe it in your own words

> **Note:** If you're not sure yet, that's okay. Describe it however feels natural and we'll figure it out together.

---

## Layer 2 — Who is it for?

Who's the primary audience?

- [ ] Just me — personal tool or experiment
- [ ] My team — internal use only
- [ ] Customers — public-facing product
- [ ] Developers — a tool built for other builders
- [ ] Open source community
- [ ] Not sure yet

---

## Layer 3 — Platform and Environment

*(This section adapts based on your Layer 1 answer)*

### If you chose Web App:
Which browsers or environments matter most?

- [ ] Modern browsers only (Chrome, Firefox, Safari, Edge)
- [ ] I need to support older browsers — specify if you can: ___________
- [ ] Progressive Web App (PWA)
- [ ] No preference — just make it work

### If you chose Desktop App:
Which operating systems are you targeting?

- [ ] Windows
- [ ] macOS
- [ ] Linux
- [ ] All three — stay as cross-platform as possible with minimal forking
- [ ] Not sure yet

### If you chose Mobile App:
Which platforms?

- [ ] iOS only
- [ ] Android only
- [ ] Both — cross-platform preferred
- [ ] Both — native for each is fine

### If you chose CLI Tool, API, or Backend Service:
Where will this run?

- [ ] Local machine only
- [ ] Cloud-hosted (AWS, GCP, Azure, etc.)
- [ ] Containerized (Docker, Kubernetes)
- [ ] Edge / serverless
- [ ] Not sure yet

---

## Layer 4 — Where are you in the journey?

Which of these best describes where you're starting from?

- [ ] Blank slate — nothing exists yet
- [ ] I have a clear idea but no code yet
- [ ] I have existing code I'm building on top of
- [ ] I'm refactoring or rebuilding something that already exists
- [ ] I'm picking up someone else's project

> If you have existing code, point me to it and I'll read it before we go any further.

---

## Layer 5 — Stack and Constraints

Let's talk technology. Answer what you know — skip what you don't.

**Languages:**
Do you have a preferred language, or are you open to recommendations?

- [ ] I have a preference — specify: ___________
- [ ] Open to recommendations
- [ ] Must match an existing codebase — I'll share it

**Frameworks:**
Any frameworks already decided or strongly preferred?

- [ ] Yes — specify: ___________
- [ ] No preference — recommend based on what I'm building
- [ ] Open to it but want to discuss options first

**Hard constraints:**
Anything I absolutely must use or must avoid?

- Must use: ___________
- Must avoid: ___________
- No hard constraints

---

## Layer 6 — Phoebii Settings

Almost done. These last two questions tell Phoebii how to behave across the whole project.

### Governance File

Claude Code sometimes looks for `CLAUDE.md`, other tools look for `AGENTS.md`. Which one do you want this project to use as its source of truth?

- [ ] `CLAUDE.md`
- [ ] `AGENTS.md`
- [ ] I don't have a preference — pick one and tell me

> **Note:** Whatever you choose here, Phoebii will use it consistently everywhere. If you ever change your mind, just let me know and I'll update all references automatically.

### Research Mode

When agents need to look something up, what's your preferred research source?

- [ ] **Context7** — best for library docs, framework references, and technical specs
- [ ] **Web search** — best for current info, pricing, news, and anything live
- [ ] **Let the agent decide** — task-aware routing, uses whichever fits the question
- [ ] **Both** — always check both sources

---

## Wrapping Up

Once you've answered these, I'll generate your `project.context.md` — the single source of truth for this project. It will capture everything above, set up your governance file, and get your agents ready to go.

You can always come back and change things. Nothing here is set in stone.

**Ready? Let's build something.**
