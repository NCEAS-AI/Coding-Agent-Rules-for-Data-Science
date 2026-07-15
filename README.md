[![DOI](https://zenodo.org/badge/1297838124.svg)](https://doi.org/10.5281/zenodo.21364494)

# Coding-Agent Rules for Data Science

A reusable, IDE-agnostic ruleset that steers AI coding agents toward
**reproducible, analysis-first** data-science work in R and Python — for
scientists and researchers doing agentic coding across any field (ecology,
genomics, economics, physics, ML, general data science, and more). Instead of
copying a one-size config, you point your agent at this repo and it builds a
**personalized copy** tuned to your field, your tools, your machine, and your
preferences.

This is a **living document**: the ruleset is actively maintained and will keep
evolving over time. What you set up is a static snapshot, so re-run the setup
whenever you want to pull the latest.

## Quick Start Prompt

###  Copy-paste prompt to get started

Paste the prompt below into your coding agent:
(Cursor, Claude Code, Windsurf, Copilot, Cline, Codex/AGENTS.md, and others)

```text
Set up a personalized copy of these data-science coding rules for me.
The rules live in this public repo: https://github.com/NCEAS-AI/Coding-Agent-Rules-for-Data-Science
Read the setup guide at https://github.com/NCEAS-AI/Coding-Agent-Rules-for-Data-Science/blob/main/agent-setup/SETUP.md
and follow it: figure out which IDE/tool I'm using and where its rules files go,
inspect (or ask about) my system, ask me the preference questions, then build the
ruleset from agent-setup/rules-template.md and show me the whole thing before you
write any file.
```

> **Note:** GitHub can't put a real clipboard button in README text (it strips
> JavaScript for security), but every code block like the one above gets a
> built-in copy icon on hover — that's the 📋 to click.

The agent will:

1. Ask how you want to run setup — let it probe your machine and auto-answer what it can, or answer everything yourself; fast path or full interview.
2. Figure out which tool you're using and where that tool expects rules files.
3. Inspect (or ask about) *your* system — cores, RAM, GPU, OS, installed languages — never assume anyone else's.
4. Ask the parts that are genuinely your call (your field, languages, geospatial/parallel/GPU work, server vs. laptop, emoji comments, strictness, layout, and more).
5. Assemble a personalized ruleset from `agent-setup/rules-template.md`, write it into the correct location and format for your tool, and print the whole thing back for you to review.

Prefer to do it by hand? `agent-setup/SETUP.md` is readable on its own — the
phases and the full questionnaire are right there. And if you just want a ruleset
without any of the setup dance, copy
[`personal-rules/data-science-rules.mdc`](personal-rules/data-science-rules.mdc)
straight into your IDE's rules folder.

## What are these rules? (Nothing to install, nothing runs)

**These rules are just a text file.** A rules file is a plain Markdown document
that your coding agent reads and keeps in its context to guide how it behaves —
the same way you might paste standing instructions at the top of a chat, except
your IDE loads it automatically on every request. There's **nothing to install,
no software to run, and nothing that phones home.** "Setting it up" just means
putting the Markdown file where your IDE looks for its rules.

Because it's only text, **you can read every word before you use any of it.** If
you're wary of pointing an agent at a stranger's repo, don't take our word for
it — open the files and see exactly what the agent would be told to do:

- 👉 **[`personal-rules/data-science-rules.mdc`](personal-rules/data-science-rules.mdc)** —
  the author's own working ruleset. This is the best place to start: it's a real,
  filled-in example of what these conventions look like, and you can copy it as-is
  or just skim it to get the gist.
- **[`agent-setup/rules-template.md`](agent-setup/rules-template.md)** — the full
  build source the setup reads from, with every section it can include.
- **[`agent-setup/SETUP.md`](agent-setup/SETUP.md)** — the exact, human-readable
  steps the agent follows to tailor the rules to you.

## What's in here

| Path | What it is |
|---|---|
| `agent-setup/SETUP.md` | The interactive setup protocol the agent follows. Start here. |
| `agent-setup/rules-template.md` | The build source — the full ruleset, annotated with markers the setup uses to include/exclude/fill sections. |
| `personal-rules/data-science-rules.mdc` | The author's own ruleset, kept current over time. A concrete example of what a filled-in result looks like, and usable as-is. |
| `LICENSE` | CC0 1.0 — public domain. |
| `CITATION.cff` | Citation metadata. |

## Design notes

- **IDE-agnostic by construction.** The setup detects the target tool and
  writes natively for it, falling back to the cross-tool `AGENTS.md` standard when
  you use several tools or aren't sure.
- **Universal floor vs. your call.** Safety and reproducibility items (real-data
  integrity, rebuildable environments, worker cleanup, CRS verification, guardrails)
  are included for everyone. Cosmetic and workflow choices (emojis, layout, README
  discipline, strictness) are asked, not assumed.
- **Your machine, not mine.** The system section is rewritten from a live inspection
  of your hardware, so utilization caps and worker sizing fit what you're actually on.
- **Living source.** This repo is actively maintained — the rules will be refined
  and expanded over time. It's the evolving source; see *Static once set up*
  below for how that interacts with a copy you've already generated.
- **Static once set up.** The generated ruleset is a snapshot. It does not phone
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
