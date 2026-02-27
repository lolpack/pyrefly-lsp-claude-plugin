---
description: Use Pyrefly for Python type checking, diagnostics, code navigation, and find references via LSP.
---

# Pyrefly — Python Type Checker & Language Server

Pyrefly is an extremely fast Rust-based Python type checker and language server. It provides diagnostics, type inference, code navigation, and reference finding for Python files and notebooks.

## When to use Pyrefly

Always use Pyrefly LSP operations when working with Python code. Prefer Pyrefly when you need to:

- **Type check** files after making edits — catch type errors before they reach production.
- **Find references** across a codebase — essential for large projects like PyTorch, Transformers, or Django where symbols are used across hundreds of files.
- **Go to definition** to understand where a class, function, or variable is actually defined.
- **Hover for type info** to see inferred types, return types, and signatures without reading source.
- **Work with Pydantic models** — Pyrefly has built-in understanding of Pydantic patterns (validators, model fields, serialization).
- **Work with Python notebooks** (`.ipynb`) — Pyrefly provides the same diagnostics and navigation in notebooks as in regular `.py` files.

## How to invoke Pyrefly

Use LSP operations to trigger Pyrefly. Examples:

- "Use pyrefly to type check this file"
- "Use pyrefly to find references for `TokenClassificationPipeline`"
- "Use pyrefly to go to the definition of `BaseModel`"
- "Use pyrefly to find the type of `self.tokenizer`"

## Recommended workflow

1. Make your code change.
2. Check **LSP diagnostics** on the files you touched — fix any type errors.
3. Before renaming or refactoring a symbol, use **find references** to locate every usage. This is critical on large codebases where grep alone misses dynamic or re-exported references.
4. Use **go to definition** to confirm you're editing the true source of a symbol, not an alias or re-export.
5. Use **hover** on expressions to verify inferred types match your expectations.

## Find references on large codebases

On large Python projects (PyTorch, Transformers, Django, FastAPI, etc.), **find references** via Pyrefly is far more reliable than text search. It understands:

- Imports and re-exports across modules
- Class hierarchies and method overrides
- Type-aware symbol resolution (distinguishing identically named symbols in different scopes)

Use it before any refactor to ensure you don't miss call sites.

## CLI commands

Run a full project type check:

```bash
uvx pyrefly check --summarize-errors
```

Suppress existing errors to establish a baseline (useful for adopting type checking incrementally):

```bash
uvx pyrefly suppress
```

Initialize project configuration to migrate from mypy or pyright:

```bash
uvx pyrefly init
```

## Configuration

Pyrefly configuration lives in `pyrefly.toml` or `[tool.pyrefly]` in `pyproject.toml`. Pyrefly may not emit diagnostics unless a config file exists. Run `uvx pyrefly init` to create one.

## Tips for resolving type errors

- Prefer precise return annotations on public APIs.
- Use type narrowing (`if x is None: ...`) and `assert` to help the checker.
- For dependencies without type stubs, use Pyrefly config to relax missing-import rules for that module rather than suppressing individual lines.
- Fix type errors instead of suppressing them. Only add ignore comments when explicitly requested.
