<p align="center">
  <img alt="fleetlint's logo: nine dots on a dark blue tile, one repository in a fleet that stands out." src="https://raw.githubusercontent.com/fleetlint/.github/main/profile/logo.svg" width="112" />
</p>

<p align="center">
<strong>Policy for a fleet of repositories.</strong><br />
fleetlint checks how each repository is set up, and tells you or your coding agent how to close each gap.
</p>

<p align="center">
<a href="https://fleetlint.org">Documentation</a> · <a href="https://fleetlint.org/rules/">Rule reference</a> · <a href="https://github.com/fleetlint/fleetlint/releases">Releases</a>
</p>

## What is fleetlint? 🧭

fleetlint does not lint code. It checks that the things which lint, test, build and release the code are present, wired together and configured the way you decided: hooks, task runner, linter configuration, CI and the release pipeline. It reports how far a repository is from compliant against a catalog of rules, and repairs what it can.

```sh
fleetlint                  # zero config: discovers stacks, forge and tier, applies the recommended preset
fleetlint fix --apply      # writes the missing files; existing files are never overwritten
fleetlint check -f agent   # a task list for a coding agent, one commit per rule
fleetlint fleet --from github:your-org   # one report across every repository of an owner
```

The goals behind it:

- **The same baseline everywhere.** One decision about hooks, linting or release signing, applied to every repository the same way, instead of drifting per project.
- **Actionable, not just red.** Every finding says how to close it; findings marked fixable are written for you, and `-f agent` turns the rest into work a coding agent can pick up.
- **Policy as data.** Rules and templates live in a versioned, signed catalog. Organisations build on the presets, lock rules and set severity floors without restating them, and CI can require the baseline so no repository drops it unnoticed.
- **Honest exceptions.** Disabling a rule needs a reason, exceptions cover individual findings and expire, and every report shows which catalog defined or weakened each rule.

## Repositories

| Repository | What it is |
|---|---|
| [fleetlint](https://github.com/fleetlint/fleetlint) | The command-line tool (Go). Start here. |
| [catalog](https://github.com/fleetlint/catalog) | The rules and fix templates as data: presets, rule library, stacks. Published as a signed OCI artifact per tag. |
| [docs](https://github.com/fleetlint/docs) | Source of [fleetlint.org](https://fleetlint.org), including the generated reference for every rule. |
| [action](https://github.com/fleetlint/action) | GitHub Action, also for Gitea and Forgejo Actions: installs a verified release, annotates findings, writes the job summary. |
| [gitlab-components](https://github.com/fleetlint/gitlab-components) | GitLab CI/CD components: the check with Code Quality, and merge requests with onboarding and fixes. |
| [homebrew-tap](https://github.com/fleetlint/homebrew-tap) · [scoop-bucket](https://github.com/fleetlint/scoop-bucket) · [nur](https://github.com/fleetlint/nur) | Homebrew, Scoop and Nix packaging, written by the release workflow. |

Every release ships checksums, a cosign signature and an SBOM per archive; the container image is signed as well. [Install instructions](https://github.com/fleetlint/fleetlint#install) cover the install script, Homebrew, Scoop, Nix, mise, Docker and `go install`.

## Project status

fleetlint is released regularly but has not reached 1.0: releases may still change the configuration, catalog and JSON formats. Every change is listed in the [changelog](https://github.com/fleetlint/fleetlint/blob/main/CHANGELOG.md) with a compatibility note, and what comes next is in the [roadmap](https://github.com/fleetlint/fleetlint/blob/main/docs/ROADMAP.md).

## Contributing 🤝

Contributions are welcome: new rules and stack profiles belong in the [catalog](https://github.com/fleetlint/catalog), changes to discovery, reporting and fixes in [fleetlint](https://github.com/fleetlint/fleetlint). Read the [contribution guide](https://github.com/fleetlint/fleetlint/blob/main/CONTRIBUTING.md) first.

Security issues go through the process in [SECURITY.md](https://github.com/fleetlint/fleetlint/blob/main/SECURITY.md), not public issues.

## Tech stack

fleetlint is a single Go binary. Rule predicates are written in [CEL](https://cel.dev) over discovered facts and file accessors, the catalog is distributed as an OCI artifact, and the documentation is built with Hugo, versioned per release.

fleetlint is licensed under MIT. Files it writes into your repository belong to that repository, with no attribution required.
