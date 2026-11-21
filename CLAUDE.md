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
  heading, `repository-setup.md` (what's needed once per repository, so no `CLAUDE.md` imports
  it and `general.md` only points to it), and the configuration fragments a language part
  requires its repositories to copy (`csharp.editorconfig`). A consuming repository's
  `.claude/shared/` is a copy of this folder as a whole.
- **This repository has no `.claude/shared/`**: its `CLAUDE.md` imports `shared/general.md`
  directly, and it uses no language part.
- **A consuming repository's `CLAUDE.md`** holds its title, the imports
  (`@.claude/shared/general.md`, then its languages' files) and its Project part.
- **`.github/workflows/update-consuming-repositories.yml` lists the consuming repositories.** On a
  push to `main` that changes `shared/`, it opens an issue and a PR replacing `.claude/shared/` in
  each one whose copy differs, with a commit GitHub signs (GraphQL's `createCommitOnBranch`), and
  closes the older update PRs still open there, with their issues and branches. The issue gets a
  checklist of what the repository has to change besides: the merged PR's "Consuming repositories"
  section, an item per changed configuration fragment, and the items of the updates it closed,
  unticked again because their commits go with their branches. With a checklist the PR opens as a
  draft, without one ready for review. It writes to them with the secret
  `CONSUMING_REPOSITORIES_TOKEN`, a fine-grained personal access token of the user's with read and
  write access to their contents, issues and pull requests. A new consuming repository is added to
  its list and to the token.

## Writing shared files

- **`general.md` and `repository-setup.md` name no language, no language's tools and no consuming
  repository.** They do name what every repository's workflow uses: git, GitHub, 1Password and
  Claude Code. Where a rule of `general.md` depends on the language, it says "the language part"
  and every language file answers it: the formatter, the type checker or linter, the test
  framework and its parameterized tests, the mocking library, how tests reach internals, test
  names and layout, naming and casing, and the conventions that need judgment.
- **A language file names no project.** What only one repository does goes in that repository's
  Project part.
- **A change here changes every consuming repository's rules.** Its issue says which repositories
  it affects. Once it's merged, the workflow opens each one's update PR; check that its run
  succeeded.
- **A PR that changes `shared/` has a `## Consuming repositories` section** in its description,
  saying what they have to change besides taking the update: `None`, or a bullet list. The
  workflow copies the list into every consuming repository's issue and fails without the section,
  so it's written for a reader there: an item names the repositories it concerns when that isn't
  all of them, and refers to an issue here in full (`Sephiroth018/claude-instructions#11`).
- **Lines wrap at 100 characters**, like the consuming repositories' `CLAUDE.md` files.

## Verification

None beyond the Definition of done's steps 6 and 7: there's no code, so steps 1-5, `/simplify`,
`/code-review` and CI don't apply, and step 6 of `repository-setup.md` adds no `ci.yml`. The
self-review also checks that the shared files still agree with each other and that every language
file still answers what `general.md` leaves to it. A change to the workflow can only be tried by
running it: after the merge, read its run and the PRs it opened.

## Versioning

None, and no releases: a consuming repository's update commit names the commit of this repository
it copied.
