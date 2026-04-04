# Wiki Schema

This file is the operating manual for the LLM maintaining this wiki. Read it at the start of every session.

## Directory structure

```
sources/          # Raw, immutable source documents — never modify these
wiki/             # All LLM-generated pages live here
wiki/index.md     # Master content catalog — update on every ingest
wiki/log.md       # Append-only session log — always append, never rewrite
```

## Page conventions

Every wiki page in `wiki/` should follow this structure:

```markdown
---
title: "Page Title"
tags: [tag1, tag2]
sources: [filename1.md, filename2.md]
updated: YYYY-MM-DD
---

# Page Title

One-sentence summary of this page.

## Section

...body...

## See also

- [[Related Page]]
- [[Another Page]]
```

- Use `[[WikiLink]]` syntax for internal links (Obsidian-compatible)
- Keep `sources:` frontmatter up to date as pages are revised
- Every page must be reachable from `wiki/index.md`

## Ingest workflow

When told to ingest a source (e.g. "ingest `sources/article.md`"):

1. Read the source file completely
2. Discuss key takeaways with the user if they are present; otherwise proceed
3. Create or update a summary page at `wiki/sources/<filename>.md`
4. Identify all entities (people, organizations, concepts, events) mentioned
5. Update or create a wiki page for each significant entity
6. Update `wiki/index.md`: add the new source summary + any new entity pages
7. Append an entry to `wiki/log.md`:
   ```
   ## [YYYY-MM-DD] ingest | <Source Title>
   Ingested `sources/<filename>`. Created/updated: <list of touched pages>.
   ```
8. Report a summary of all changes made

## Query workflow

When asked a question:

1. Read `wiki/index.md` to identify relevant pages
2. Read the relevant pages
3. Synthesize an answer with citations (link to wiki pages, not raw sources)
4. Ask the user: "Should I file this answer as a new wiki page?" — if yes, create it
5. If a new page is created, update `wiki/index.md` and append to `wiki/log.md`

## Lint workflow

When asked to lint the wiki:

1. Read all pages in `wiki/`
2. Check for and report:
   - Contradictions between pages
   - Stale claims superseded by newer sources
   - Orphan pages (no inbound links)
   - Important concepts mentioned but lacking their own page
   - Missing cross-references between related pages
   - Data gaps that could be filled with a web search
3. Propose fixes; apply them only with user approval
4. Append a lint entry to `wiki/log.md`

## index.md format

`wiki/index.md` is organized into sections. Each entry is:

```markdown
- [[Page Name]] — one-line summary _(N sources)_
```

Sections:
- **Sources** — one entry per ingested source
- **Entities** — people, organizations, products
- **Concepts** — ideas, frameworks, methodologies
- **Analyses** — comparison tables, syntheses, answers filed as pages

## log.md format

Each log entry uses a parseable header:

```
## [YYYY-MM-DD] <type> | <title>
```

Where `<type>` is one of: `ingest`, `query`, `lint`, `note`.

This makes entries greppable: `grep "^## \[" wiki/log.md | tail -10`

## Output formats

The wiki is primarily markdown, but queries can produce:

- **Markdown page** — default for most answers
- **Comparison table** — for "compare X and Y" questions
- **Marp slide deck** — add `<!-- marp: true -->` header for presentation output
- **Python/matplotlib chart** — for data visualization questions

## General principles

- **The wiki is the product.** Every session should leave the wiki better than it started.
- **Cite wiki pages, not raw sources.** Wiki pages are the synthesized, citable record.
- **File good answers.** If an answer required real synthesis, it belongs in the wiki.
- **Never truncate log.md.** It is append-only by design.
- **Update index.md on every structural change.** It is the LLM's navigation aid.
- **One source at a time** (by default). Go deep on each before moving on.
- **Ask before making large structural changes** to the wiki organization.
