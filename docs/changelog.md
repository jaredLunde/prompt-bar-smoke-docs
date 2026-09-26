# Changelog

This page explains how releases of prompt-bar are announced: where the
changelog lives, what we consider a release, how versions are numbered, how
often they ship, how breaking changes are marked, and how to follow along.

## Where the changelog lives

The canonical changelog is `CHANGELOG.md` at the root of the repository. It is
the only source we treat as authoritative. Every entry there is generated from
the commits that went into the release tag, so the file and the Git history
never disagree. The GitHub Releases page mirrors it, but that is a copy: if
the two differ, the file wins.

Entries are ordered newest first. Each one carries the version number, the
release date in ISO form (`2026-03-14`), and the changes grouped under
**Added**, **Changed**, **Fixed**, **Deprecated**, and **Removed**.

## What counts as a release

A release is a tagged commit on `main` that has been published to the package
registry. Nothing else is a release. Merging a pull request is not a release;
neither is a deploy of the docs site, a change to CI, or a fix that only
touches tests. If you cannot install it by version number, it did not happen
as far as the changelog is concerned.

This keeps the changelog short and every line in it actionable. Internal
refactors appear only when they change observable behaviour.

## Versioning

We follow [semantic versioning](https://semver.org): `MAJOR.MINOR.PATCH`.

- **MAJOR** — we removed or changed something you depended on. You may have to
  edit your code to upgrade.
- **MINOR** — we added something. Existing code keeps working.
- **PATCH** — we fixed something. No new surface, no removals.

Pre-releases are tagged `-rc.N` and are published for anyone who wants to test
an upcoming major ahead of time. They are not covered by the stability
guarantees above.

## Cadence

Patch releases go out as fixes land, often several times a week. Minor
releases are cut roughly every two weeks, whenever there is a feature worth
shipping — we do not hold a release open waiting for one more thing. Major
releases are rare and deliberate; we aim for at most one or two a year, and
each is preceded by at least one release candidate.

## Breaking changes

Breaking changes appear only in major releases, and every one is flagged three
ways: the entry is prefixed **BREAKING**, it is listed first in the release
notes regardless of category, and it includes a migration note saying what to
change. Where an automatic migration is possible we ship a codemod and link it
from the entry.

Anything we plan to remove is deprecated at least one minor release before the
major that removes it. Deprecated APIs keep working and emit a warning that
names the replacement.

## Following releases

- **Watch the repository** on GitHub — choose *Custom* → *Releases* to get an
  email for each published release and nothing else.
- **Subscribe to the release feed** at
  `https://github.com/jaredLunde/prompt-bar-smoke-docs/releases.atom` in any
  RSS reader.
- **Pin a version** in your lockfile and read `CHANGELOG.md` before you bump.
  This is the approach we recommend for production use.
