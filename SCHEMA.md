# Schema

Starter schema. Deliberately minimal — grow it as real content arrives.
Add a domain, category, or tag the first time a page actually needs it.

## Frontmatter Fields

| Field | Required | Description |
|-------|----------|-------------|
| title | yes | Page title |
| type | yes | One of: summary, entity, concept, journal, list, project |
| domain | yes | Coarse topic — see Domains below |
| category | no | Entity subcategory — see Entity Categories below |
| status | no | One of: read, todo, bookmark |
| source | no | Relative path to source file(s) |
| url | no | Canonical URL for bookmarks without a local source file |
| related | no | List of related wiki page filenames (without path) |
| tags | no | List of tags |
| date | no | Date page was added to the wiki |
| published | no | Original publication date of the source material |

## Domains

| Domain | Scope |
|--------|-------|
| tech | Software, tools, engineering, computing |
| science | Research, papers, theory, methods |
| work | Career, business, finance, professional projects |
| culture | Books, film, music, art, history, ideas |
| life | Health, home, travel, admin, journal, personal lists |

## Entity Categories

| Category | Scope |
|----------|-------|
| person | Individual humans |
| org | Companies, institutions, labs, nonprofits |
| product | Software tools, hardware, libraries, services |

## Tags

- reading
- tools
- howto
- idea
- todo

## File Organization

- Wiki filenames are lowercase kebab-case.
- One page per distinct entity, concept, or product.
- Summaries cover a single source document.
- Entity pages aggregate info across multiple sources.
- Journal pages are one per day: `journal-YYYY-MM-DD.md`.
- Lists are long-lived pages that get appended to, not replaced.

## Index Structure

The index is split into multiple files:

| File | Contents |
|------|----------|
| main.md | Top-level TOC linking to sub-indexes |
| summaries.md | Article/paper summaries (read and todo) |
| entities.md | People, organizations, and products (subsectioned) |
| concepts.md | Concept and overview pages |
| projects.md | Project ideas and active projects |
| bookmarks.md | Quick-reference bookmarks |
| lists.md | Running lists — todos, wants, tracked items |
| reading-queue.md | Generated list of `status: todo` pages sorted by date |
