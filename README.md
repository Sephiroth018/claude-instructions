# claude-instructions

The parts of my repositories' `CLAUDE.md` files (the instructions
[Claude Code](https://claude.com/claude-code) works by) that are the same in every project, kept in
one place so a rule changes once:

- [`shared/general.md`](shared/general.md): the working agreement, source control workflow,
  definition of done, engineering principles, naming, comments and testing rules for any project.
- [`shared/lua.md`](shared/lua.md) and [`shared/csharp.md`](shared/csharp.md): toolchain, naming
  and conventions for projects in that language.

## Use

A repository carries a copy of `shared/` as `.claude/shared/` and imports what applies to it at the
top of its own `CLAUDE.md`, which then only holds what's specific to the project:

```markdown
@.claude/shared/general.md
@.claude/shared/lua.md

# Project
```

The copy is committed, so the instructions are there wherever the repository is checked out. It's
never edited in place: changes are made here, and a workflow then opens a pull request replacing
the copy in every repository on its list. A new repository makes its first copy with the commands
under "Hygiene" in `shared/general.md`.

## AI disclaimer

These files are written and maintained with Claude Code, under my direction and review.

## License

[MIT](LICENSE)
