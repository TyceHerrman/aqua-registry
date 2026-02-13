# aqua-registry Contributing Guide

Source: https://aquaproj.github.io/docs/products/aqua-registry/contributing

## Requirements

- All commits must be signed
- Must use `cmdx s` to scaffold — manually written PRs are not accepted
- No force pushes after opening a PR
- Do not amend the scaffold commit (`git commit --amend`, `git rebase`) — the scaffold commit must remain distinct from manual changes
- PR title format: `feat: add <org/repo>`
- No issue creation required before submitting a PR for new packages

## Tool Naming

Names must include `/` (namespace):
- `hashicorp/terraform` (correct)
- `terraform` (wrong)

Multiple tools in one repo: `winebarrel/cronplan/cronmatch`, `winebarrel/cronplan/cronplan`

Non-GitHub: `crates.io/{crate}`, `gitlab.com/<repo>`

## Unsupported Package Types

aqua cannot support tools with plugin mechanisms requiring installation in non-PATH locations:
- GitHub CLI Extensions
- Terraform providers
- Gauge plugins

## Fork Policy

Do not change an existing package source to a fork. Create a new package pointing to the fork instead.

## Package Structure

```
pkgs/<org>/<repo>/
  registry.yaml    # Installation config
  pkg.yaml         # Test versions
  scaffold.yaml    # Optional: customizes auto-generation
```

## Version Overrides

Use `version_overrides` with `version_constraint` for version-specific behavior. Use `overrides` for OS/arch-specific changes.

When adding older versions to pkg.yaml, use the non-shorthand syntax to prevent Renovate auto-updates:

```yaml
# Short syntax (gets auto-updated by Renovate):
- name: org/repo@v1.0.0

# Full syntax (stays pinned):
- name: org/repo
  version: v0.9.0
```

## Scaffold Configuration

Filter assets/versions with `aqua-generate-registry.yaml`:
- `version_filter`: Exclude non-matching versions
- `version_prefix`: Exclude versions without prefix
- `all_assets_filter`: Exclude non-matching assets

Example: `all_assets_filter: not ((Asset matches "rollouts-controller") or (Asset matches "rollout-controller"))`

## Troubleshooting

**Asset not found**: Asset naming may have changed or CI failed. Verify with the tool's repository.

**Command not found**: Check command name, version-specific name changes, path accuracy, or OS/arch exclusions in `supported_envs`.

**Checksum issues**: Modify extraction parameters, disable checksums, or verify correct algorithm (sha1, sha256, sha512, md5). Run `cmdx lsa -r <repo> "<version>"` to list actual assets.
