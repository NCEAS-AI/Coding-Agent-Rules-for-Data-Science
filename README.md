<!-- DOI-BADGE-PLACEHOLDER: replace after first Zenodo release with the badge markdown Zenodo provides -->

# Reproducible R and Python data-science conventions for agentic coding

A reproducible R/Python data-science conventions ruleset for agentic coding in environmental, ecological, and geospatial work, written to be dropped into a Cursor project as an always-on rules file that steers agentic tools toward code that reads top-to-bottom and reruns cleanly.

## Repository contents

- `.cursor/rules/data-science-rules.mdc` — the conventions themselves: a Cursor rules file (Markdown body with YAML front matter, including `alwaysApply: true`).
- `LICENSE` — the full CC0 1.0 Universal public domain dedication.
- `CITATION.cff` — Citation File Format metadata that powers GitHub's "Cite this repository" button.
- `README.md` — this file.

## How to use

The conventions live in a single Cursor rules file, `.cursor/rules/data-science-rules.mdc`. To use them in your own project, copy that file into your project's `.cursor/rules/` directory, keeping the `.mdc` extension:

```bash
mkdir -p .cursor/rules
cp data-science-rules.mdc <your-project>/.cursor/rules/
```

The `alwaysApply: true` front matter loads the rules on every request, so agentic tools follow them automatically. The file's body is plain Markdown, so you can also read it directly here on GitHub or in any editor.

The conventions cover:

- Script structure
- File discipline
- Project layout
- Reproducibility and data integrity
- Geospatial/CRS handling
- Shared-server parallel/multiprocessing discipline
- Checkpointing
- Agent guardrails

## License

Released under [CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/) (public domain). Use it for any purpose, no attribution required. See the [LICENSE](LICENSE) file for the full text.

## How to cite

Attribution isn't required, but citation metadata is provided in [CITATION.cff](CITATION.cff). GitHub renders a "Cite this repository" button from it, and a Zenodo DOI will appear at the top of this README once the repository is archived.

Text citation:

> Broderick, C. (2026). Reproducible R and Python data-science conventions for agentic coding (Version v1.0.0) [Software]. https://github.com/NCEAS-AI/Carlo-Broderick
