# rdl-node-packagemanager-field

Test fixture for the `remove_duplicate_lockfiles` maintenance task.

## Scenario

Node conflict at repo root with **three** competing lockfiles:

- `package-lock.json` (npm)
- `yarn.lock` (yarn)
- `pnpm-lock.yaml` (pnpm)

`package.json` declares `"packageManager": "pnpm@9.0.0"`.

## Expected MT behaviour

- **Auto-detects** pnpm via the `packageManager` field — no user question needed.
- **Deletes** `package-lock.json` and `yarn.lock`.
- **Keeps** `pnpm-lock.yaml`.
- **Appends** the deleted filenames to `.gitignore` (under the Autar section header).
