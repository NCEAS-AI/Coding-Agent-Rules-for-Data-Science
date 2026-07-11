# Data-Science Agent Rules & Conventions

A portable set of **reproducible R and Python data-science conventions** for
environmental, ecological, and geospatial work. These rules guide an AI coding
assistant (or a human) toward analysis code that reads top-to-bottom, reruns
cleanly, and treats data with integrity — optimized for reproducible analysis
rather than "production" software polish.

They are tool-agnostic: the same rules can drive any AI/IDE coding agent, or
simply serve as a written style guide for the team.

## What's inside

- `.cursor/rules/data-science-rules.mdc` — the full ruleset, covering:
  - **Real data only** — never fabricate, mock, or insert demo/placeholder data.
  - Script structure (literate, linear, self-contained, top-to-bottom).
  - Settings- and file-path-first layout, numbered multi-file pipelines.
  - Project layout, housekeeping, archiving, and change records.
  - README maintenance (project README + data README).
  - Reproducibility & data integrity (pinned deps, seeds, read-only raw data).
  - Geospatial & CRS handling.
  - Parallel/multiprocessing discipline on shared servers.
  - Logging in Pacific Time, comments that explain the *why*.
  - Agent guardrails for destructive or consequential actions.

> The file uses an `.mdc` extension with a small YAML front-matter header, but the
> body is plain Markdown and readable as-is in any editor or on GitHub.

## Point your AI agent straight at this repo (easiest)

Because this repository is **public**, you don't have to download anything by
hand. Just point your IDE agent or AI coding assistant at the repo URL and ask it
to read the rules and install them in the right place for your setup — that
usually works:

```
https://github.com/NCEAS-AI/Carlo-Broderick
```

Example ask:

> "Read the data-science rules from
> https://github.com/NCEAS-AI/Carlo-Broderick and add them to my project's
> agent-rules location."

The agent can fetch `.cursor/rules/data-science-rules.mdc` directly from the repo
and insert its contents into the appropriate location itself.

## Manual install (generic)

Most AI/IDE coding agents load "rules" or "conventions" from a known location.
Copy the ruleset into whichever your tool uses. A few common examples:

```bash
# Cursor (project- or user-level rules)
mkdir -p .cursor/rules
cp .cursor/rules/data-science-rules.mdc <your-project>/.cursor/rules/

# Generic "agent instructions" convention
cp .cursor/rules/data-science-rules.mdc <your-project>/AGENTS.md

# Or keep it as a plain style guide anywhere in your repo/docs
cp .cursor/rules/data-science-rules.mdc <your-project>/docs/data-science-conventions.md
```

Adjust the destination to match your assistant's expected rules path. The content
is the same regardless of where it lives.
