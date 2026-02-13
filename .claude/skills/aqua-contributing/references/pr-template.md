# PR Template

Source: aquaproj/aqua-registry `.github/pull_request_template.md`

## Title

```
feat: add <org/repo>
```

## Body

```markdown
## Check List

- [x] Read [CONTRIBUTING.md](https://aquaproj.github.io/docs/products/aqua-registry/contributing)
  - [x] Read [OSS Contribution Guide](https://github.com/suzuki-shunsuke/oss-contribution-guide/blob/main/README.md)
- [x] [All commits are signed](https://github.com/suzuki-shunsuke/oss-contribution-guide/blob/main/docs/commit-signing.md)
  - This repository enables `Require signed commits`, so all commits must be signed
- [x] [Avoid force push](https://github.com/suzuki-shunsuke/oss-contribution-guide?tab=readme-ov-file#dont-do-force-pushes-after-opening-pull-requests)
- [x] Install and execute the package and confirm if the package works well
- [x] [Execute `cmdx s` to scaffold code](https://aquaproj.github.io/docs/products/aqua-registry/contributing/#use-cmdx-s-definitely)

Add [<org>/<repo>](https://github.com/<org>/<repo>)
```

## Checklist Verification

Before checking each item, verify it was actually done:

| Item | How to verify |
|------|--------------|
| Read CONTRIBUTING.md | Read `references/contributing-guide.md` in this skill |
| Read OSS Contribution Guide | Key points: sign commits, no force push, enable maintainer push |
| All commits signed | `git log --show-signature -1` |
| Avoid force push | Never force push after PR is open |
| Package works well | `cmdx s` and `cmdx t` both passed |
| Execute `cmdx s` | Scaffold commit exists in git log |
