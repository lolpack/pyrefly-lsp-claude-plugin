# Contributing

Thanks for helping improve the Pyrefly LSP plugin for Claude Code!

## Development workflow

1. Clone the repo
2. Make changes
3. Validate the plugin manifest (optional but recommended):

   ```bash
   claude plugin validate
   ```

4. Test locally:

   ```bash
   claude --plugin-dir .
   ```

## Guidelines

- Keep the plugin minimal: it should only configure Claude Code and document how to install prerequisites.
- Prefer changes that improve reliability across different machines (macOS/Linux/Windows).
- Update `CHANGELOG.md` for user-visible changes.
