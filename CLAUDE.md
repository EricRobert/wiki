# Instructions

> This is a personal knowledge base. The owner reads it; you write it.

# Structure

The knowledge base is just a git repo of files.
The owner's job is to curate sources, direct the analysis, ask good questions, and think about what it all means.
Your job is everything else.

```
/
  source
  wiki
  index
    main.md
    summaries.md
    entities.md
    concepts.md
    projects.md
    bookmarks.md
    lists.md
    reading-queue.md
  log
    2026
      0801.md
  SCHEMA.md
  CLAUDE.md
```

Directories are created on demand — make them the first time a page needs them.

## Sources

The curated collection of raw source documents.
Articles, papers, images, data files.
These are immutable i.e. imported, reorganized but never modified.
This is the source of truth.

**Archival policy:**
- Any page marked `status: read` must have a local source file (even just a markdown extraction of the original).
- Pages with `status: todo` or `status: bookmark` may use `url` only — local copy is optional.
- If a source disappears from the web, the wiki summary is all that remains. Prefer saving locally.

## Wiki

A directory of generated markdown files with YAML frontmatter.
Summaries, entity pages, concept pages, comparisons, overviews, synthesis, journal entries, lists.
You own this layer entirely.
Create pages, update them when new sources arrive, maintain cross-references, and keep everything consistent.

Every page has:
- `domain` — coarse topic, see `SCHEMA.md` for the enumeration
- `related` — list of linked wiki pages (auto-derived from body cross-references)

Entity pages also have:
- `category` — entity subcategory, see `SCHEMA.md` for the enumeration

Bookmark pages also have:
- `url` — canonical source URL when no local source file exists

## Index

The index is a set of content-oriented files under `./index/`.
The root is `main.md` — a top-level TOC linking to sub-indexes.

| File | Contents |
|------|----------|
| main.md | TOC with page counts |
| summaries.md | Article/paper summaries, split by read/other/to-read |
| entities.md | People, organizations, and products (subsectioned) |
| concepts.md | Concept and overview pages |
| projects.md | Project ideas and active builds |
| bookmarks.md | Quick-reference bookmarks, grouped by domain |
| lists.md | Running lists — todos, wants, tracked items |
| reading-queue.md | `status: todo` pages grouped by domain |

All sub-indexes are regenerated on every ingest.

## Log

The log contains chronological entries.
It's an append-only record of what happened and when — ingests, queries, lint passes.
One file per day: `YYYY/MMDD.md` with timestamped `## HH:MM:SS` sections.

## Schema

The schema contains useful information about the wiki content like:

- possible tags
- frontmatter fields and their semantics
- domain and category enumerations
- file organization rules
- index structure

You own this file; update it as needed.
It starts deliberately small — grow it as real content arrives, don't pre-populate.

## Instructions

This file.
It contains the set of instructions to follow.
You own this file; update it as needed.

# Scope

This is a knowledge base only.
Record ideas, references, research, and inspiration for projects — but never start building or scaffolding projects here.
No code generation, no project setup, no implementation.
If a topic suggests a project, capture the idea and relevant links; leave execution for later, outside this repo.

# Operations

## Bookmark

When asked to bookmark or "just add" something (a tool, library, resource):

- reads the source
- writes a wiki page with `status: bookmark` — no impressions, no status questions
- includes the owner's stated reason/context if provided
- sets `domain`, `category` (for entities), and `url` (if no local source)
- updates the index (all relevant sub-indexes)
- updates relevant entity and concept pages across the wiki
- appends an entry to today's log file
- commits all changes with a short message: `Add <source description>`

## Ingest

When asked to ingest or deeply add a piece of knowledge:

**Non-consumable sources** (tools, libraries, products, resources) — treat as a bookmark automatically:

- reads the source
- writes a wiki page with `status: bookmark` — no status question, no impressions
- includes the owner's stated reason/context if provided
- sets `domain`, `category`, `url` as appropriate
- updates the index
- updates relevant entity and concept pages across the wiki
- appends an entry to today's log file
- commits all changes with a short message: `Add <source description>`

**Consumable sources** (articles, videos, papers, talks):

- reads the source
- writes a wiki page with the summary (status: `todo`, impressions left blank)
- sets `domain` and `related`
- updates the index
- updates relevant entity and concept pages across the wiki
- appends an entry to today's log file
- commits all changes with a short message: `Add <source description>`
- presents a short summary (a few sentences capturing the core argument and key takeaways)
- asks the owner: does this fit your reading of it (status: read), or should it stay as to-read (status: todo)?
- if the answer is `read`: amends the commit with updated status

## Note

When given a raw thought, journal entry, or list item with no external source:

- writes or updates the relevant wiki page (`type: journal`, `type: list`, or the fitting page)
- sets `domain` and `related`
- updates the index
- appends an entry to today's log file
- commits with a short message

## Queries

When asked a question against the wiki, do the following:

- reads the index first to find relevant pages, then drills into them
- read those relevant pages and synthesizes an answer with relevant citations
- answers can take different forms depending on the question:
  - a markdown page
  - a comparison table
  - a slide deck (Marp)
  - a chart (matplotlib)
  - a canvas
- good answers can be filed back into the wiki as new pages

## Lint

When asked, health-check the wiki.
Look for:

- contradictions between pages
- stale claims that newer sources have superseded
- orphan pages with no inbound links
- important concepts mentioned but lacking their own page
- missing cross-references
- data gaps that could be filled with a web search
- pages missing `domain` or `category` fields
- `related` fields that are stale (body links changed but related not updated)

## Batch Invocation

The agent may be invoked in a loop by an external driver script.
Each invocation receives a single line of text piped to stdin — no framing, no prefix.
The agent interprets the line and decides what operation applies (ingest, bookmark, note, etc.).

**Status line convention:**
The last line of output must be a structured status line:

```
STATUS: PASS | <n> files touched
STATUS: FAIL | <reason>
```

This line is parsed by the driver to produce a log.
Always emit exactly one STATUS line, always as the final line of output.
