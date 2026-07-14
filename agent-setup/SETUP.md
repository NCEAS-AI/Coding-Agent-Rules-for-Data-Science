# Coding-Agent Rules for Data Science — Interactive Setup

This repository holds a reusable ruleset for steering AI coding agents toward
reproducible, analysis-first data-science work in R and Python, for scientists
and researchers across any field. This file is the **installer**: it turns the
generic ruleset into a personalized one and drops it into your IDE in the right
place.

---

> ### If you are an AI coding agent
> Read this entire file, then run the setup workflow with the user. Your goal:
> install a **personalized** copy of this repo's ruleset into whatever tool the
> user is using, in that tool's correct location and format, tuned to *their*
> system and *their* stated preferences. Work through the phases in order.
> Build from `rules-template.md` (in this same folder), not from memory.

> ### If you are a human
> Paste this repo's URL into your coding agent and tell it: *"Read
> `agent-setup/SETUP.md` and follow it to set up these rules for me."* It will
> interview you and install the rules. You can also just read the phases below
> and do it by hand.

---

## Ground rules for the agent (read before starting)

- **Get approval before writing.** Before writing or overwriting any file, show
  the assembled result first and get a yes.
- **System inspection is announced once, not asked per command.** If the user
  chooses the auto-probe mode in Phase 0, tell them once that you're about to
  inspect their machine with read-only commands, then go — no need to ask before
  each one. If they choose the ask-me mode, don't probe at all.
- **Detect, then confirm — don't ask what you can inspect.** Read objective facts
  (cores, RAM, OS, installed languages); only *ask* things that are genuinely
  subjective.
- **One question at a time.** Offer a sensible default in `[brackets]`; accept
  "default" or "skip." Don't dump the whole questionnaire at once.
- **Don't trust your memory for tool conventions — they change.** Verify the
  target tool's *current* rules-file location, format, and limits against its own
  docs before writing. The table in Phase 1 is a starting hint, not gospel.
- **Skip questions made moot by earlier answers.** No R-style question if the user
  is Python-only; no server-citizenship caps if they're on a laptop.
- **Never put secrets, tokens, or credentials in a rules file.** These files are
  committed to git and read by external services.
- **This ruleset is opinionated but not sacred.** Where the user's stated
  preference conflicts with a default here, the user wins — record their choice.

---

## Phase 0 — Pick the setup mode (ask these two first)

Before anything else, ask the user two quick questions:

**A. How should I gather your system details?**
- **[Auto — recommended]** "I'll inspect your machine myself with read-only
  commands (OS, cores, RAM, GPU, installed languages, environment managers) and
  auto-answer every question I can from what I find — then only ask you the
  subjective preferences. Heads up: this means I'll run a handful of read-only
  probes on your system. If you'd rather I didn't, pick the other option."
- **Ask me instead** — "Don't probe anything. I'll give you the system specs and
  answer all the questions myself."

**B. Fast path or full interview?**
- **[Fast]** Use sensible defaults, and ask only the few questions that most
  change the outcome: your field; languages; geospatial / parallel / GPU work;
  server vs. laptop; and whether you want emoji comments. Everything else takes
  its default.
- **Full interview** — walk the complete questionnaire in Phase 3.

Record both answers and follow them for the rest of setup.

---

## Phase 1 — Identify the tool and where its rules live

Ask: **"Which coding tool are you setting these rules up for?"** If you can infer
it from the working directory (an existing `.cursor/`, `CLAUDE.md`, `.windsurf/`,
`.clinerules/`, `.github/copilot-instructions.md`, etc.), propose it and confirm.

Then determine, for that tool: (a) where rules files live, (b) the format and any
frontmatter, (c) project-level vs. user/global scope, (d) size limits, (e) how
activation/scoping works (always-on vs. glob-scoped vs. manual). Confirm against
current docs. Known conventions as of writing — **verify before relying on them:**

| Tool | Location | Format / notes |
|---|---|---|
| **Cursor** | `.cursor/rules/*.mdc` (project); user rules in settings | Markdown + YAML frontmatter: `description`, `globs`, `alwaysApply`. Legacy `.cursorrules` still works but is deprecated. |
| **Claude Code** | `CLAUDE.md` (repo root, committed); `CLAUDE.local.md` (gitignored); nested `CLAUDE.md`; `~/.claude/CLAUDE.md` (global) | Plain Markdown. Also reads `AGENTS.md`. |
| **Windsurf** | `.windsurf/rules/` (preferred); legacy `.windsurfrules`; global rules in settings | Markdown. **Size limits: ~6k chars/file, ~12k total** — this ruleset must be split/scoped. Activation: Always-On / Manual / Model-Decision. |
| **GitHub Copilot** | `.github/copilot-instructions.md` (repo-wide); `.github/instructions/*.instructions.md` (glob-scoped, `applyTo` frontmatter) | Plain Markdown. Also reads `AGENTS.md`. |
| **Cline** | `.clinerules/` directory of `.md` files | Modular Markdown; optional `paths` frontmatter to scope; numeric prefixes to order. |
| **Roo Code** | `.roo/rules/` or `.roo/rules-{mode}/` | Mode-scoped Markdown. |
| **Codex / Gemini / Aider / Zed / Jules / Junie** | `AGENTS.md` (repo root) | The cross-tool open standard — plain Markdown, no required frontmatter. Aider also reads `CONVENTIONS.md`; Gemini also `GEMINI.md`. |

**Portable default:** if the user uses several tools, isn't sure, or wants max
reach, write a root **`AGENTS.md`** (read natively by most agents) and add a thin
tool-specific file only where that tool needs its own format or features.

Also ask: **project-level (this repo only) or global (all your work)?** Most users
want project-level; global suits someone applying one house style everywhere.

---

## Phase 2 — Get the user's system details

**If the user chose Auto in Phase 0:** tell them once that you're about to inspect
their system, then run read-only probes and report back. Adapt to the OS. Gather:

- **OS / platform**, **physical & logical core count**, **total RAM**
- **GPU** present and model (if any)
- **Shared server vs. personal machine** (see the branch below)
- **Languages installed** and versions (R, Python)
- **Environment / dependency managers** present (uv, conda/mamba, renv, venv, pip)
- **Formatters** present (Ruff, Air) — so you only reference tools they actually have

Suggested read-only probes (pick per OS):

```bash
# Linux
nproc; lscpu | grep -E '^CPU\(s\)|Core|Thread|Socket'; free -h
nvidia-smi -L 2>/dev/null || echo "no NVIDIA GPU"
hostname; who | wc -l; uptime
command -v sinfo >/dev/null && echo "Slurm present (likely a shared cluster)"
R --version 2>/dev/null | head -1; python3 --version 2>/dev/null
for t in uv conda mamba ruff air; do command -v $t >/dev/null && echo "$t: yes"; done
```

```bash
# macOS
sysctl -n hw.physicalcpu hw.logicalcpu; sysctl -n hw.memsize
system_profiler SPDisplaysDataType | grep -i chipset
R --version 2>/dev/null | head -1; python3 --version 2>/dev/null
```

```powershell
# Windows (PowerShell)
Get-CimInstance Win32_Processor | Select NumberOfCores,NumberOfLogicalProcessors
(Get-CimInstance Win32_ComputerSystem).TotalPhysicalMemory
Get-CimInstance Win32_VideoController | Select Name
```

**If the user chose Ask-me in Phase 0:** don't run anything. Ask them for the same
facts directly — OS, cores/RAM, GPU, server vs. laptop, which languages and
managers they use.

**Server-vs-local branch (important — it flips the utilization caps on/off).**
Hints that it's a *shared* server: multiple logged-in users (`who`), a job
scheduler (Slurm/PBS), a cluster-style hostname, an MOTD, or the user saying they
SSH in. **Confirm either way.** If shared, the "shared-server citizenship" caps
apply. If it's their own machine, drop those caps entirely — they can use the
whole box.

Summarize everything and let the user correct it before continuing.

---

## Phase 3 — Interview the user

Ask in order, one at a time, skipping any rendered irrelevant by earlier answers.
Defaults in `[brackets]`. **If the user chose Fast in Phase 0, ask only questions
1–6 and 8, and take the default for everything else.**

### Context (decides which sections get included)

1. **What field or domain do you work in?** free-text, e.g. ecology, genomics, economics, physics, ML — **[general data science]** *(tailors the ruleset's framing and examples; does not force geospatial/parallel content)*
2. **Which languages here?** R only / Python only / **[both]**
3. **Do you do geospatial / spatial work** (rasters, vectors, CRS reprojection)? yes / **[no]**
4. **Will you run parallel or multiprocessing jobs?** yes / no / **[unsure — include it lightly]**
5. **GPU compute** (deep learning, CUDA)? yes / **[no]**
6. **Shared multi-user server, or your own machine?** *(confirm the Phase 2 finding)*
7. **Notebook-based, script-based, or both?** **[scripts]** / notebooks / both

### Preferences (genuinely your call — no universal right answer)

8. **Emojis in comments and section dividers?** **[yes]** / no *(cosmetic; dividers still fold either way)*
9. **How strict is "real data only — never fabricate"?** **[hard stop]** (refuse & ask) / warn-but-continue / relaxed
10. **Log-timestamp timezone?** *(propose the detected system tz)* **[detected]** / specify one / no timestamps
11. **Comment style:** narrate the *why* behind non-obvious steps **[yes]** / keep comments minimal
12. *(R only)* **R style:** tidyverse-first **[default]** / base-R-first / no preference
13. **Adopt the project layout** (`scripts/`, `logs/`, `archive/`, archive-don't-delete, CHANGELOG)? full **[yes]** / lite (just the folders) / no
14. **Two-README discipline** (a project README + a data README)? **[yes]** / no
15. **Confirmation strictness for destructive or multi-step actions?** always confirm **[default]** / confirm only destructive / minimal
16. **Where should the rules apply?** always-on **[default]** / scoped to file globs (e.g. only `*.R`, `*.py`) — *(maps to the tool's activation mechanism)*
17. *(shared server only)* **Utilization caps** — total-load ceiling / target. **[75% cap / ~70% target]** or specify your own.

*(Everything else — reproducibility, CRS discipline, worker cleanup, guardrails —
is treated as universally good and included without asking, unless the user
explicitly opts out.)*

---

## Phase 4 — Assemble the personalized ruleset

Build from `rules-template.md` (in this folder). Each section there is tagged:

- `<!-- UNIVERSAL -->` → always include.
- `<!-- CONTEXT: r|python|geospatial|parallel|gpu|shared-server -->` → include only
  if the matching context answer was yes.
- `<!-- PREF: ... -->` → include/adjust per the matching preference answer.
- `<!-- SYSTEM -->` → replace placeholders (`{{HOST_DESC}}`, `{{CORES}}`,
  `{{RAM}}`, `{{GPU}}`, `{{TZ}}`, `{{CPU_CAP}}`, `{{MEM_CAP}}`, `{{FIELD}}`) with
  real facts.

Assembly steps:

1. Start with all UNIVERSAL sections.
2. Add CONTEXT sections whose condition the user met.
3. Apply PREF toggles: strip emojis if declined; set the real-data strictness
   wording; keep/trim the layout, README, comment-verbosity, R-style, and
   confirmation-strictness sections to match.
4. Replace the entire "System / environment" block with the user's real machine
   (never leave anyone else's specs in the file).
5. **Tailor to the user's field (question 1):** substitute `{{FIELD}}` into the
   intro line, and lightly adjust the `description:` frontmatter and any examples
   to fit their domain. This is framing only — it does **not** add geospatial,
   parallel, GPU, or any other CONTEXT content. If they took the default, use
   "data science" and leave the framing generic.
6. Drop any formatter line for a formatter they don't have installed.
7. Set the log-timestamp timezone to theirs.
8. **Fit the target tool:** if it has size limits (e.g. Windsurf), split into
   scoped modules or trim to the ceiling; if it uses frontmatter (Cursor, Copilot
   glob files), generate the correct header and set `alwaysApply`/`globs` or
   `applyTo` from question 16.
9. Add a short provenance comment at the very top noting the source
   (`NCEAS-AI/Coding-Agent-Rules-for-Data-Science`) and that this is a **static
   snapshot** generated at setup — it does not auto-update.

---

## Phase 5 — Install, print, and review

1. Write to the confirmed location and format. If a rules file already exists
   there, **ask before overwriting** and offer to back it up (e.g. `*.bak`).
2. For directory-based tools, give the file a clear name (e.g.
   `data-science.mdc`, `.clinerules/20-data-science.md`).
3. Tell the user plainly: **what** you wrote, **where**, and **how to confirm**
   the tool picked it up (open a new agent session and ask it to state its active
   rules, or check the tool's rules panel).
4. **Print the entire generated ruleset into the chat** so the user can read it in
   full. Encourage them to actually read it top to bottom and give you comments or
   corrections — these rules shape everything the agent does, so it's worth the few
   minutes. Reading it isn't required, but say plainly that we'd really appreciate
   it if they did, rather than dropping it in unread.

*(Reminder: the installed file is static. It won't change unless the user re-runs
this setup or edits it themselves.)*

---

## Quick reference: universal vs. your-call

**Included for everyone (safety / reproducibility floor):** real-data integrity,
pinned/rebuildable environments, root-anchored paths, seeds, raw-data-read-only,
no silent transforms, worker cleanup & memory caps for any parallel work, CRS
verification (if geospatial), and agent guardrails around destructive actions.

**Tuned to preference:** emojis, real-data strictness level, project layout and
housekeeping, README discipline, comment verbosity, R style, confirmation
strictness, activation scope, and (on shared servers) the utilization caps.
