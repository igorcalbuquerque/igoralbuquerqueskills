---
name: dependency-upgrade
description: Use when upgrading, bumping, or updating a library, framework, runtime, or tool version, when a Dependabot or Renovate pull request fails, when fixing a CVE by changing a version, or when a lockfile conflict or peer dependency error (such as npm ERESOLVE) appears. Upgrades in small verified steps, reads the real changelog, and leaves a rollback.
---

# Dependency Upgrade

You upgrade dependencies so that the project ends up on the new version with proof that it still works, and with a one-line way back. Each upgrade is a **small verified step**: one package, or one group that must move together, per change.

This skill is provider-agnostic. Use the project's own package manager, lockfile, and test commands.

## Workflow

1. **Identify.** Read the current version from the lockfile (the manifest only gives a range), the target version, and the reason: a security advisory, a needed feature, end of support, or a failing automated PR. Note the runtime the target requires (Node, Python, Java version).
2. **Read the changes.** Open the release notes, changelog, and migration guide for every version between current and target. Places to find them: the package's repository releases page, a `CHANGELOG` file in the repository or in the installed package, and the project's docs site, located through the package registry metadata (`npm view <pkg> repository homepage`, the PyPI project page, and so on). Write down each breaking change, deprecation, and new peer requirement, with the link or path where you read it. Then check the target's issue tracker for regressions reported after release, because a fresh release can break a plugin you use. Done when every breaking change on your list has a source, or the sources confirm there are none. If no source is reachable, stop and report `BLOCKED`: an upgrade planned from memory misses the changes made after the versions the model remembers.
3. **Find the group.** Some packages only work together: a tool and its plugins, a framework and its adapter, a library and its type package. Peer dependency ranges and the migration guide tell you which. Upgrade the whole group in one step; upgrading one member alone fails at install or at runtime.
4. **Find usage.** Search the code and config for every API and option named in the breaking changes. Each hit is a change you make in the same step.
5. **Apply.** Change the manifest and regenerate the lockfile with the project's package manager, then make the code and config changes from step 4. Install from the lockfile, the same way CI and production install, so you test what will ship.
6. **Verify.** Run what the project runs in CI: tests, type check, lint, build. Then exercise the code paths that use the package directly, because a passing suite may not cover them. Compare warnings and deprecation messages before and after; a new deprecation is the next upgrade's breaking change.
7. **Rollback.** Write down the previous version and the exact command or revert that restores it. For a deployed service, also say whether the upgrade changes anything that a rollback would not undo, such as a database migration, a cache format, or a stored file format.
8. **Report** in the format below.

When the target version has a regression that blocks you, stay on the last version that works. Pin it, link the upstream issue, and state the condition to try again (a fixed release, a merged pull request). For automated update tools, add an ignore rule for that version so the same failing PR does not come back.

Majors and minors go in separate steps. Several patch updates with no breaking changes can share one step.

## Output Format

```markdown
## Upgrade

**DONE** — eslint 8.57.0 → 9.15.0, with @eslint/js and eslint-plugin-react-hooks.

| Package | From | To |
|---|---|---|
| eslint | 8.57.0 | 9.15.0 |
| @eslint/js | — | 9.15.0 |

**Breaking changes that hit this project**
1. `.eslintrc.json` replaced by `eslint.config.js` (flat config). Migrated.
2. `--ext` flag removed from the lint script. Removed.

**Verified:** `npm ci`, `npm test`, `npm run lint`, `npm run build`.
**Sources:** eslint.org/docs/latest/use/migrate-to-9.0.0, github.com/eslint/eslint/releases
**Rollback:** `git revert <commit>`; no persisted state changed.
```

The decision line is one of:

- `**DONE** — <what moved>.`
- `**HELD** — stayed on <version>: <reason, upstream link>. Retry when <condition>.`
- `**BLOCKED** — <what stops the upgrade and what the user must decide>.`

List only the breaking changes that touch this project, each with what you changed. The `Sources:` line lists what you read in step 2 and is always present. Add a `Not verified:` line when a check could not run.

## Rules

- Base every claim about a version on its release notes or source, not on memory of the API, because APIs change between the versions you remember and the one you install.
- Keep the lockfile in the change. Installing outside the lockfile resolves versions on the day of the deploy and ships something CI never tested.
- Resolve peer dependency conflicts by moving the group together. Flags that skip the resolver (`--force`, `--legacy-peer-deps`, `--no-deps`) hide the conflict until runtime; use one only with the user's agreement and say so in the report.
- Touch only the packages in scope. Unrelated updates make a failure harder to trace and a rollback wider.
