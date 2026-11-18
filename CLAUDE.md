# CLAUDE.md — claude-instructions

Two parts: **General** applies to any project, **Project** to this one only; where it overrides a
General rule, it wins. Instructions never go in HTML comments; they're stripped before this file is
loaded.

@shared/general.md

# Project

The shared parts of the `CLAUDE.md` files in the user's repositories, kept in one place so a rule
changes once. The repository is a public GitHub repository, `Sephiroth018/claude-instructions`.

## Structure

- **`shared/` holds the shared files**, and nothing else: `general.md` (the General part) and one
  file per language (`lua.md`, `csharp.md`), each starting with its part's `#` heading. A consuming
  repository's `.claude/shared/` is a copy of this folder as a whole.
- **This repository has no `.claude/shared/`**: its `CLAUDE.md` imports `shared/general.md`
  directly, and it uses no language part.
- **Consuming repositories:** `Sephiroth018/Factorio-Info-Export` (`lua.md`) and
  `Sephiroth018/BattleTechInfoExporter` (`csharp.md`). Each one's `CLAUDE.md` holds its title, the
  imports (`@.claude/shared/general.md`, then its languages' files) and its Project part.

## Writing shared files

- **`general.md` names no language, tool or project.** Where a rule depends on the language, it
  says "the language part" and every language file answers it: the formatter, the type checker or
  linter, the test framework and its parameterized tests, the mocking library, how tests reach
  internals, test names and layout, naming and casing, and the conventions that need judgment.
- **A language file names no project.** What only one repository does goes in that repository's
  Project part.
- **A change here changes every consuming repository's rules.** Its issue says which repositories
  it affects and what they have to change besides taking the update; once it's merged, each of
  them gets the update (`general.md`'s "Hygiene") through an issue and PR of its own.
- **Lines wrap at 100 characters**, like the consuming repositories' `CLAUDE.md` files.

## Verification

None beyond the Definition of done's steps 6 and 7: there's no code, so steps 1-5, `/simplify`,
`/code-review` and CI don't apply, and "New repository setup" step 6 adds no `ci.yml`. The
self-review also checks that the shared files still agree with each other and that every language
file still answers what `general.md` leaves to it.

## Versioning

None, and no releases: a consuming repository's update commit names the commit of this repository
it copied.
