# CLAUDE.md

Guidance for AI assistants working in this repository.

## What this repo is

A practice repository for the [GitHub Flow](https://docs.github.com/en/get-started/using-github/github-flow) workflow. There is no application code, build system, dependency manifest, or CI — changes are documentation only.

## Layout

```
.
├── README.md                                                  # repo description
├── .github/instructions/
│   └── *.instructions.md                                      # literal filename, contents: "commit"
└── content/copilot/how-tos/get-code-suggestions/
    └── get-ide-code-suggestions.md                            # GitHub Docs-style article
```

The `content/` tree mirrors the structure of [github/docs](https://github.com/github/docs). Treat files under `content/` as if they were going to be rendered by that site.

## Editing `content/` articles

These are not plain Markdown. They are Liquid-templated and rely on conventions from the docs site:

- **Frontmatter** — required keys include `title`, `intro`, `versions`, `contentType`, `category`. Don't drop or rename keys without reason. `defaultTool` selects which tool-conditional section renders first.
- **Variables** — write product/feature names as `{% data variables.product.prodname_copilot %}`, not as literal strings. Reuse the variable names already present in the file rather than inventing new ones.
- **Reusables** — `{% data reusables.copilot.accept-suggestion %}` pulls in shared snippets. Don't expand them inline.
- **Tool-conditional blocks** — `{% vscode %} … {% endvscode %}`, `{% jetbrains %} … {% endjetbrains %}`, `{% visualstudio %}`, `{% vimneovim %}`, `{% azure_data_studio %}`, `{% xcode %}`, `{% eclipse %}`. When adding instructions for a tool, put them inside the matching block; mirror the structure (Introduction → Prerequisites → Getting code suggestions → …) used by the other tools in the same file.
- **Cross-links** — internal links use `[AUTOTITLE](/path/to/article)`; the title is resolved by the docs build. Don't hand-write the title.
- **Code fences** — keep the `copy` modifier (e.g. ```` ```javascript copy ````) on snippets meant to be copied.
- **Keyboard shortcuts** — use `<kbd>` tags and the existing macOS / Windows-or-Linux table format.

If a change touches a shortcut, an OS table, or a keyboard combination, double-check both rows of the table — the existing file has a history of asymmetric edits (see commit `e0b76fb`).

## Workflow

The branch for the current task is set by the harness in the system prompt; develop, commit, and push there. Do not push to `main`. After pushing, open a draft PR if one doesn't exist.

Commits in history are short imperative subjects (`Add instructions markdown file`, `Fix JetBrains partial suggestions section: …`). Match that style.

## What not to do

- Don't add a package manager, build config, linter, or CI workflow — this repo intentionally has none.
- Don't rewrite `content/` files as plain Markdown by stripping the Liquid tags; the templating is the point.
- Don't rename `.github/instructions/*.instructions.md` — the asterisk is the literal filename in this repo, not a glob.
