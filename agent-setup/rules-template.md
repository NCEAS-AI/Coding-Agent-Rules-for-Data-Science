<!--
  BUILD SOURCE — not meant to be used as-is.
  The SETUP.md installer transforms this file into a personalized ruleset.
  Section markers:
    UNIVERSAL            → always include
    CONTEXT: <tag>       → include only if the user does that kind of work
    PREF: <name>         → include/adjust per the user's stated preference
    SYSTEM               → replace {{PLACEHOLDERS}} with the user's real machine
  Placeholders: {{HOST_DESC}} {{CORES}} {{RAM}} {{GPU}} {{TZ}} {{CPU_CAP}} {{MEM_CAP}} {{FIELD}}
  Emoji dividers are shown; strip the emojis if the user declines them (PREF: emojis).
-->
---
description: Reproducible R and Python data-science conventions for agentic coding   # SETUP: may be tailored to the user's field (question 1)
alwaysApply: true   # SETUP: set from question 16 (always-on vs glob-scoped)
---

# Data-Science Conventions (R & Python)

Reproducible R and Python code for {{FIELD}} — conventions for reproducible
analysis, **not** a software product. *(SETUP fills `{{FIELD}}` from the user's
field; defaults to "data science".)*

<!-- UNIVERSAL -->
## 🎯 Priorities
Optimize for code that reads top-to-bottom and reruns cleanly — not for
abstraction, generality, or "production" polish.

<!-- UNIVERSAL | PREF: real-data-strictness controls the STOP wording -->
## 🚫 Real data only — never fabricate or insert demo data
- Use real, actual data. Never invent, mock, or insert demo / sample / placeholder /
  synthetic data to make code run or an analysis complete.
- If real data is missing, unavailable, or unclear: **[hard stop]** STOP and ask for it —
  don't substitute stand-in values and keep going. *(warn-but-continue / relaxed variants
  soften this to a loud warning.)*
- No silent gap-filling: no made-up rows, columns, values, default fallbacks, or dummy
  files in a pipeline. If sample data is genuinely needed to test structure, label it
  unmistakably as fake and keep it out of any analysis path.
- Flag loudly wherever data looks fabricated, hardcoded, or placeholder-like.
- This bans substituting fake data for missing real data. It does **not** ban
  simulation, resampling, bootstrap, or null-model methods where generated data is
  the intended subject of the analysis and is labeled as such.

<!-- SYSTEM — replace this whole block with the user's real machine -->
## 🖥️ System / environment
- {{HOST_DESC}}  (e.g. "Personal macOS laptop" or "Shared multi-user SSH server — resource discipline matters")
- CPU: {{CORES}}
- RAM: {{RAM}}
- GPU: {{GPU}}

<!-- UNIVERSAL -->
## 💬 Communication
- Be concise and scannable; lead with the answer; don't restate code back.
- When directions are unclear, ask clarifying questions — and note how the request
  could have been phrased more clearly.

<!-- UNIVERSAL -->
## 🧰 Working with code (general)
- Make only changes requested or clearly understood and directly related to the task.
- Strongly prefer common, well-documented, standard packages and techniques.
- Don't assume a package or function exists from memory. Confirm it's installed in the
  active environment before importing, and verify the specific function/argument exists
  in the installed version rather than guessing.
- Never fabricate data, results, statistics, or citations. When inferring rather than
  knowing, say so.

<!-- UNIVERSAL -->
## 📁 Scope & file discipline
- Default to editing the file already under discussion, not spinning off a new one.
  Models tend to reach for a fresh script for every task, littering the project with
  orphaned single-use files. When the request concerns an existing script, change it there.
- Create a new file only when the work genuinely calls for it — a real new pipeline stage,
  a README, or the change record — never as a reflex.
- When fixing a bug, exhaust the existing implementation before introducing a new pattern
  or library. If switching is unavoidable, retire the old version by archiving it — leave
  no duplicate logic in the active code.

<!-- UNIVERSAL -->
## 🧩 Simplicity & abstraction
- Prefer the simplest solution that works. No premature abstraction — don't wrap a few
  lines in a function or class without a real reason.
- Don't extract into a separate sourced/imported file unless asked to refactor that way.
- Avoid duplicate or parallel implementations across the codebase. This is about
  architecture, NOT within-script style — inside a file, prefer readable inline steps over
  extracted helpers, even at the cost of a little repetition.

<!-- UNIVERSAL | PREF: emojis affects the divider style -->
## 📜 Script structure (literate & linear)
- Write every file to read top-to-bottom as a self-contained narrative that runs in a
  fresh session, with no indirection to chase.
- Layout, in order: (1) header comment (purpose, inputs, outputs); (2) Settings — every
  tunable as a commented variable, editable in one place; (3) File paths declared up front;
  (4) Body in numbered sequential stages.
- Mark major sections with a foldable, bold divider:
  R: `# ⚙️ Settings ----` over an `# ====` bar. Python: `# %% ⚙️ Settings` over `# ====`.

<!-- UNIVERSAL -->
## 🔗 Multi-file pipelines
- When scripts chain together, number them in run order with a zero-padded prefix:
  `01_`, `02_`, `03_`, … Declare each script's inputs and outputs in its header.
- When inserting a step between existing ones, renumber the whole sequence — no `01b_`,
  suffixes, or out-of-order numbers.
- Renumbering is not just a rename. In the same change set, update every internal reference
  (source/import calls, README mentions, run-log notes) and report the rename map
  (old -> new). If references can't be updated cleanly in one pass, treat it as consequential
  and pause for confirmation first.

<!-- PREF: layout (full / lite / off) -->
## 🗂️ Project layout & housekeeping
- Standard folders: `scripts/` (numbered pipeline), `logs/` (run logs, change record,
  temp/scratch), `archive/` (retired code and files). Raw data and derived outputs live in
  dedicated locations outside the project folder.
- *(full only)* Archive, don't delete. Retire code/files into `archive/` rather than
  hard-deleting; keep it organized, not a dumping ground.
- Keep the project root clean — move logs, temp, and scratch into `logs/`.
- *(full only)* Keep a dated change record (e.g. `logs/CHANGELOG.md`) of what was archived,
  moved, or removed, and why.
- Deletion requires confirmation; archiving is the default safe alternative.

<!-- PREF: readmes (on / off) -->
## 📖 READMEs
Maintain two (a single long file covering both is fine):
- Project README at the root: purpose, pipeline and run order, workflow, folder structure,
  where data and outputs live.
- Data README in the output/data location: file layout, data dictionary (fields/bands,
  units, ranges, nodata), CRS, temporal coverage, provenance, caveats, and the path back to
  the scripts that created the data.
Create a missing README before finishing work in that area; update the relevant README in
the same change set when code, outputs, fields, paths, or steps change.

<!-- UNIVERSAL -->
## 📤 Outputs
- Assume derived outputs go to a dedicated location outside the working directory. If that
  location isn't already specified, ask before writing — don't guess a path.

<!-- PREF: comment-verbosity (narrate / minimal) | PREF: emojis -->
## 💭 Comments & narration
- Comment the WHY and the reasoning behind each decision. Narrate non-obvious steps so a
  reader follows what's happening. Don't comment trivial lines that restate the code.
- *(minimal variant: comment only genuinely non-obvious logic; skip narration.)*
- *(emojis on: use emojis in comments/output to aid scanning.)*

<!-- PREF: run-logs (on / off) -->
## 📝 Run-log comments (snapshots, not truth)
- After a run, a dated note may record key observed outcomes to make drift visible:
  `# RUN LOG <YYYY-MM-DD HH:MM {{TZ}}>: <row counts, key stats, extents/CRS, file sizes>`
- Treat these as historical snapshots, never authoritative. The real record is the code's
  output. If nearby code changes, flag the note as possibly stale and offer to update it.

<!-- CONTEXT: r | PREF: r-style -->
## 📊 R
- Follow the tidyverse style guide; snake_case; native pipe `|>` with one verb per line.
- *(tidyverse-first)* Prefer a consistent, well-documented ecosystem (e.g. tidyverse +
  sf/terra). *(base-R-first: prefer base and minimal dependencies.)*
- Don't shadow base names (`data`, `df`, `sd`, `T`, `c`). Don't add dependencies casually.

<!-- CONTEXT: python -->
## 🐍 Python
- Prefer clear, chained data transformations written one step per line so logic reads
  top-to-bottom. Use well-established, well-documented libraries; don't add dependencies
  casually. Put type hints on function signatures.

<!-- UNIVERSAL -->
## ♻️ Reproducibility & data integrity
- Pin dependencies so the environment can be rebuilt exactly.
- Match the environment/dependency manager to the stack: a lightweight, language-native
  manager is fine for pure-language packages, but favor whatever reliably supplies prebuilt
  binaries for heavy system-level dependencies (geospatial, GPU/compiled). Pin either way.
- Anchor paths to the project root, not the current working directory, so a script runs the
  same wherever it's launched.
- Set seeds and comment them. Treat raw data as read-only — write derived outputs to
  separate paths.
- Never silently drop rows, recode values, change units, or reproject. Make any such
  transformation explicit, commented, and called out plainly.

<!-- CONTEXT: geospatial -->
## 🗺️ Geospatial & CRS handling
CRS errors are silent, so be deliberate.
- Verify the CRS on load rather than assuming it; check before and after transformations.
  Don't confuse relabeling a CRS with reprojecting it. Sanity-check coordinate ranges,
  extent, or geometry after reprojecting.
- Measure in a projected CRS suited to the measurement (equal-area for area, equidistant for
  distance), not geographic degrees. Different steps may use different CRSs.
- Bring layers to a common CRS before multi-layer operations; mind the datum, not just the
  projection.
- When reprojecting rasters, match the resampling method to the data (categorical vs
  continuous) and avoid needless repeated resampling. Note the CRS of outputs.

<!-- UNIVERSAL — but drop the line for any formatter the user doesn't have -->
## 🎨 Formatting
- Write clean, readable, well-structured code — naming, sectioning, and logical flow are
  part of the job. Let the formatter own mechanical layout (whitespace, quotes, wrapping);
  don't hand-tune or fight what it normalizes on save. *(R: Air. Python: Ruff.)*

<!-- UNIVERSAL | SYSTEM: timezone -->
## ⏱️ Logging & output
- Timestamp every print/log statement in {{TZ}}:
  R: `format(Sys.time(), "%Y-%m-%d %H:%M:%S %Z", tz = "{{TZ}}")`
  Python: `datetime.now(ZoneInfo("{{TZ}}")).strftime("%Y-%m-%d %H:%M:%S %Z")`

<!-- CONTEXT: parallel | SYSTEM: caps only if shared-server -->
## ⚡ Parallel & multiprocessing
Expose controls in Settings (workers, chunk, mem cap, nice).
- *(shared-server only)* Utilization caps (hard): treat TOTAL system load as the ceiling,
  not just your share. Cap {{CPU_CAP}} of cores and memory, target just under it. Pre-flight
  live metrics; back off if the box is already busy; re-check on long runs.
- *(gpu)* On a single-user GPU, use full throughput while you hold it, but confirm no other
  users/processes are on the device first; host-side workers still obey CPU/RAM caps.
- Flat memory profile via chunking: load a small chunk → reduce/filter immediately → keep
  only the small result → combine at the end. Don't gate on "free RAM before launch" alone —
  workers pass the gate, then all spike at once and crash the box.
- Hard per-worker memory cap at the OS level so a runaway worker dies cleanly instead of
  triggering the OOM killer. Lower CPU priority (nice) so interactive users aren't starved.
- Guarantee worker cleanup even on crash (context manager / on.exit / stop the cluster).
  Never leave zombie workers.
- Wrap worker logic in try/except (tryCatch), return a structured status, catch the
  memory-cap error explicitly — never fail silently in a subprocess.
- Pass file paths and small primitives to workers, not large objects — each worker
  serializes its own copy, multiplying memory.
- Match the tool to the bottleneck: processes for CPU-bound work; threads/async for I/O-bound.
- Validate before scaling: run serially or smoke-test with a low worker count, since
  subprocess errors are cryptic.
- Watch fork vs spawn: forking copies parent state/handles and can crash GDAL/rasterio/
  terra/CUDA. On mysterious segfaults or hangs, switch to spawn (Python) or a PSOCK cluster
  (R), at the cost of slower startup and requiring serializable arguments.

<!-- CONTEXT: parallel -->
## 📈 Long-run progress
For long or heavy jobs, make progress easy to see from chat — a progress bar with ETA, or
live-streaming log updates. Before launch, ensure something is observable and say where to
watch; flag stalls.

<!-- CONTEXT: parallel -->
## 💾 Checkpointing & resumability
- Persist intermediate results as they complete so a failure part-way through doesn't cost
  the whole run.
- On rerun, detect work already done and skip it rather than recomputing.
- Write checkpoints atomically (temp path, then move) so an interrupted write can't leave a
  corrupt partial output that a later run mistakes for "done."
- Expose resume-vs-overwrite as a Settings control so a clean full re-run can be forced.

<!-- UNIVERSAL | PREF: confirmation-strictness -->
## 🛡️ Agent guardrails
- Never run destructive commands (rm, overwrites, git commit/push, force) or modify
  env/config files without surfacing them first and getting confirmation.
- For consequential or multi-step work, state the plan and pause for confirmation.
  *(strictness: "always confirm" widens this to any file write; "minimal" narrows it to
  irreversible/destructive actions only.)*
