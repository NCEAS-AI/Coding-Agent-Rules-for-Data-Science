[![DOI](https://zenodo.org/badge/1297838124.svg)](https://doi.org/10.5281/zenodo.21364494)

# Coding-Agent Rules for Data Science

A reusable, IDE-agnostic ruleset that steers AI coding agents toward
**reproducible, analysis-first** data-science work in R and Python — for
scientists and researchers doing agentic coding across any field (ecology,
genomics, economics, physics, ML, general data science, and more). Instead of
copying a one-size config, you point your agent at this repo and it **installs a
personalized copy** tuned to your field, your tools, your machine, and your
preferences.

This is a **living document**: the ruleset is actively maintained and will keep
evolving over time. An installed copy is a static snapshot, so re-run the setup
whenever you want to pull the latest.

## Quick start

Paste this repository's URL into your coding agent (Cursor, Claude Code,
Windsurf, Copilot, Cline, Codex/AGENTS.md, and others) and tell it:

> **"Read `agent-setup/SETUP.md` in this repo and follow it to set these rules up for me."**

The agent will:

1. Ask how you want to run setup — let it probe your machine and auto-answer what it can, or answer everything yourself; fast path or full interview.
2. Figure out which tool you're using and where that tool expects rules files.
3. Inspect (or ask about) *your* system — cores, RAM, GPU, OS, installed languages — never assume anyone else's.
4. Ask the parts that are genuinely your call (your field, languages, geospatial/parallel/GPU work, server vs. laptop, emoji comments, strictness, layout, and more).
5. Assemble a personalized ruleset from `agent-setup/rules-template.md`, write it into the correct location and format for your tool, and print the whole thing back for you to review.

Prefer to do it by hand? `agent-setup/SETUP.md` is readable on its own — the phases and the full questionnaire are right there.

## What's in here

| Path | What it is |
|---|---|
| `agent-setup/SETUP.md` | The interactive installer protocol the agent follows. Start here. |
| `agent-setup/rules-template.md` | The build source — the full ruleset, annotated with markers the installer uses to include/exclude/fill sections. |
| `personal-rules/data-science-rules.mdc` | The author's own ruleset, kept current over time. A concrete example of what a filled-in result looks like, and usable as-is. |
| `LICENSE` | CC0 1.0 — public domain. |
| `CITATION.cff` | Citation metadata. |

## Design notes

- **IDE-agnostic by construction.** The installer detects the target tool and
  writes natively for it, falling back to the cross-tool `AGENTS.md` standard when
  you use several tools or aren't sure.
- **Universal floor vs. your call.** Safety and reproducibility items (real-data
  integrity, rebuildable environments, worker cleanup, CRS verification, guardrails)
  are included for everyone. Cosmetic and workflow choices (emojis, layout, README
  discipline, strictness) are asked, not assumed.
- **Your machine, not mine.** The system section is rewritten from a live inspection
  of your hardware, so utilization caps and worker sizing fit what you're actually on.
- **Living source.** This repo is actively maintained — the rules will be refined
  and expanded over time. It's the evolving source; see *Static once installed*
  below for how that interacts with a copy you've already generated.
- **Static once installed.** The generated ruleset is a snapshot. It does not phone
  home or auto-update from this repo — re-run the setup yourself if you want a refresh.

## License

Released under [CC0 1.0 Universal](LICENSE) — public domain. Copy, modify, and use
it for any purpose, no attribution required.

---

## Cite us!

<div align="center">

✨🎉🫶 &nbsp; **Citation isn't required, but if you're a true homie you will!** &nbsp; 🫶🎉✨

[![cite us — be a homie](https://img.shields.io/badge/cite%20us-be%20a%20homie-ff69b4?style=for-the-badge&logo=github)](CITATION.cff)
&nbsp;
[![public domain — CC0 1.0](https://img.shields.io/badge/license-CC0%201.0-gold?style=for-the-badge)](LICENSE)

</div>

Citation metadata lives in [`CITATION.cff`](CITATION.cff) — GitHub renders a **"Cite this
repository"** button from it, and a Zenodo DOI will appear at the top of this README once
archived.

📋 **Copy-paste citation:**

> Broderick, C. (2026). *Coding-Agent Rules for Data Science* (Version v1.0.0)
> [Software]. Zenodo. https://doi.org/10.5281/zenodo.21364495

---
