# LLM Wiki

A template for a personal knowledge base that an LLM agent builds and maintains for you.
This is my take on [Andrej Karpathy's LLM wiki idea](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f).

- The repository is a persistent, cross-referenced wiki that compounds over time.
- You curate the sources and ask the questions.
- The agent does the writing, linking, and housekeeping.

Everything is plain markdown in a git repo.
No database, no vector store, no server.

## Getting started

```sh
git clone <this repo> my-wiki
cd my-wiki
rm -rf .git && git init
```

Then open the repo with an agent (Claude Code, or any agent that reads `CLAUDE.md` — symlink it to `AGENTS.md` if yours expects that name) and start feeding it things:

```
> ingest https://dn760108.eu.archive.org/0/items/Simplesabotage/Simplesabotage.pdf
> bookmark https://github.com/lachaloupe/cli
> record that @fil recommends the movie Planes, Trains and Automobiles
> add lunch next Friday
```
