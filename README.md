# claude-instructions

The parts of my repositories' `CLAUDE.md` files (the instructions
[Claude Code](https://claude.com/claude-code) works by) that are the same in every project, kept in
one place so a rule changes once:

- [`shared/general.md`](shared/general.md): the working agreement, source control workflow,
  definition of done, engineering principles, naming, comments and testing rules for any project.
- [`shared/lua.md`](shared/lua.md) and [`shared/csharp.md`](shared/csharp.md): toolchain, naming
  and conventions for projects in that language.
- [`shared/repository-setup.md`](shared/repository-setup.md): how a new repository is set up and
  gets its copy of these files. Read once per repository, so no `CLAUDE.md` imports it.
- [`shared/csharp.editorconfig`](shared/csharp.editorconfig): the `.editorconfig` settings every
  C# project shares, copied into its own `.editorconfig`.

## Use

A repository carries a copy of `shared/` as `.claude/shared/` and imports what applies to it at the
top of its own `CLAUDE.md`, which then only holds what's specific to the project:

```markdown
# CLAUDE.md — <repository name>

@.claude/shared/general.md
@.claude/shared/lua.md

# Project
```

The copy is committed, so the instructions are there wherever the repository is checked out. It's
never edited in place: changes are made here, and a workflow then opens a pull request replacing
the copy in every repository on its list. A new repository makes its first copy with the commands
in `shared/repository-setup.md`.

## AI disclaimer

This project is AI-assisted: [Claude Code](https://claude.com/claude-code) does most of the
implementation, under the direction and review of the maintainer. Commits written by Claude
carry a `Co-Authored-By: Claude` trailer, and everything it posts on GitHub is marked as
generated with Claude Code.

## License

[MIT](LICENSE)
