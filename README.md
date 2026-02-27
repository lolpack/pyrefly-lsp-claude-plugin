# Pyrefly LSP for Claude Code

Python language intelligence for Claude Code powered by **Pyrefly** (fast Rust-based Python type checker + language server) and **launched via `uvx`** (no global `pip install pyrefly` required).

This is a **community-maintained** Claude Code plugin. Pyrefly itself is developed upstream in the `facebook/pyrefly` project.

## What you get

- **Instant diagnostics**: see type errors and warnings while Claude edits code.
- **Code navigation**: go-to-definition, find references, and document symbols.
- **Type insight**: hover types + inferred return types.
- **Great framework coverage**: Pyrefly has built-in understanding for popular patterns (including Pydantic).

## Installation

```bash
claude plugin marketplace add lolpack/pyrefly-lsp-claude-plugin
claude plugin install pyrefly-lsp@pyrefly-lsp-claude-plugin
```

## Prerequisites

1) Install `uv` so `uvx` is available on your `PATH`.

Verify:

```bash
uvx --version
```

> First run note: `uvx` may download Pyrefly the first time the LSP starts. Subsequent starts are cached.

## Notes on diagnostics

Pyrefly intentionally **does not show type errors by default** unless a Pyrefly configuration exists (e.g. `pyrefly.toml` or `[tool.pyrefly]` in `pyproject.toml`) *or* the client forces diagnostics on.

This plugin attempts to force diagnostics on via LSP `initializationOptions`. If you still don’t see diagnostics, run:

```bash
uvx pyrefly init
```

…which will create/augment a config file in your project so diagnostics are enabled.

## Local development / testing

You can test this plugin locally (without installing) by pointing Claude Code at the directory:

```bash
claude --plugin-dir .
```

Then open a Python project and ensure:
- `uvx --version` works
- LSP features (hover, go-to-def, references) work in Python files

## Troubleshooting

- If Claude Code reports *Executable not found in $PATH*:
  - Confirm `uvx --version` works in the same shell session.
  - Restart Claude Code after installing `uv`.
- If navigation works but diagnostics are empty:
  - Ensure your project has a Pyrefly config: `uvx pyrefly init`.

## License

MIT
