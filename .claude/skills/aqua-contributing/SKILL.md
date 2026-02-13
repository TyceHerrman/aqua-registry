---
name: aqua-contributing
description: "Add packages to the aqua-registry. Use when asked to add, scaffold, contribute, or register a CLI tool/package in aqua-registry. Triggers on: 'add org/repo to aqua', 'contribute to aqua-registry', 'scaffold a package', 'cmdx scaffold', 'new aqua package', 'register tool in aqua'."
---

# Contributing a Package to aqua-registry

This is a sequential workflow with strict ordering. Do not skip or reorder steps.

## Workflow

### Step 1: Scaffold

Run `cmdx s` with the package name. This creates a branch, generates files, and runs initial tests in Docker containers (Linux + Windows).

```bash
cmdx s <org/repo>
```

Flags:
- `-r` — recreate containers before scaffolding
- `-l 1` — limit to 1 version (use for non-github_release packages)
- `-c config.yaml` — use a custom scaffold config

**Do not amend the scaffold commit.** It must remain distinct from any manual changes.

If scaffold fails, debug with `cmdx con <os> <arch>` to connect to the container. See [references/contributing-guide.md](references/contributing-guide.md) for troubleshooting.

### Step 2: Test

Run `cmdx t` to verify installation across all platforms.

```bash
cmdx t <org/repo>
```

This tests `aqua i` for linux/darwin x amd64/arm64 and on a Windows container.

If tests fail: modify `pkgs/<org>/<repo>/registry.yaml` or `pkg.yaml` based on the error, then rerun `cmdx t`. Common fixes are in [references/contributing-guide.md](references/contributing-guide.md).

### Step 3: Push and Create PR

Push the branch to the fork:

```bash
git push -u origin feat/<org/repo>
```

Create PR against `aquaproj/aqua-registry` using `gh pr create`:
- **Title**: `feat: add <org/repo>`
- **Body**: Use the checklist from [references/pr-template.md](references/pr-template.md)
- Verify every checklist item is truthful before checking it — see the verification table in the PR template reference

Write the PR body to a temp file and use `--body-file` to avoid shell escaping issues:

```bash
gh pr create --repo aquaproj/aqua-registry --title "feat: add <org/repo>" --body-file /tmp/claude/pr-body.md
```
