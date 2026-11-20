# CLAUDE.md — claude-instructions

Two parts: **General** applies to any project, **Project** to this one only; where it overrides a
General rule, it wins. Instructions never go in HTML comments; they're stripped before this file is
loaded.

@shared/general.md

# Project

The shared parts of the `CLAUDE.md` files in the user's repositories, kept in one place so a rule
changes once. The repository is a public GitHub repository, `Sephiroth018/claude-instructions`.

## Structure

- **`shared/` holds the shared files**, and nothing else, in no subfolders: `general.md` (the
  General part), one file per language (`lua.md`, `csharp.md`), each starting with its part's `#`
  heading, and the configuration fragments a language part requires its repositories to copy
  (`csharp.editorconfig`). A consuming repository's `.claude/shared/` is a copy of this folder as a
  whole.
- **This repository has no `.claude/shared/`**: its `CLAUDE.md` imports `shared/general.md`
  directly, and it uses no language part.
- **A consuming repository's `CLAUDE.md`** holds its title, the imports
  (`@.claude/shared/general.md`, then its languages' files) and its Project part.
- **`.github/workflows/update-consuming-repositories.yml` lists the consuming repositories.** On a
  push to `main` that changes `shared/`, it opens an issue and a PR replacing `.claude/shared/` in
  each one whose copy differs, with a commit GitHub signs (GraphQL's `createCommitOnBranch`), and
  closes the older update PRs still open there, with their issues and branches. It writes to them
  with the secret `CONSUMING_REPOSITORIES_TOKEN`, a fine-grained personal access token of the
  user's with read and write access to their contents, issues and pull requests. A new consuming
  repository is added to its list and to the token.

## Writing shared files

- **`general.md` names no language, no language's tools and no consuming repository.** It does
  name what every repository's workflow uses: git, GitHub, 1Password and Claude Code. Where a rule
  depends on the language, it says "the language part" and every language file answers it: the
  formatter, the type checker or linter, the test framework and its parameterized tests, the
  mocking library, how tests reach internals, test names and layout, naming and casing, and the
  conventions that need judgment.
- **A language file names no project.** What only one repository does goes in that repository's
  Project part.
- **A change here changes every consuming repository's rules.** Its issue says which repositories
  it affects and what they have to change besides taking the update. Once it's merged, the
  workflow opens each one's update PR; check that its run succeeded.
- **Lines wrap at 100 characters**, like the consuming repositories' `CLAUDE.md` files.

## Verification

None beyond the Definition of done's steps 6 and 7: there's no code, so steps 1-5, `/simplify`,
`/code-review` and CI don't apply, and "New repository setup" step 6 adds no `ci.yml`. The
self-review also checks that the shared files still agree with each other and that every language
file still answers what `general.md` leaves to it. A change to the workflow can only be tried by
running it: after the merge, read its run and the PRs it opened.

## Versioning

None, and no releases: a consuming repository's update commit names the commit of this repository
it copied.
