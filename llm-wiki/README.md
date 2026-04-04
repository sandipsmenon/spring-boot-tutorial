# LLM Wiki

A scaffold for building personal knowledge bases maintained by LLMs — based on [Andrej Karpathy's LLM Wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f).

## What is this?

Most LLM + document workflows are RAG: upload files, retrieve chunks at query time, generate an answer. The LLM re-derives everything from scratch on every question. Nothing accumulates.

**LLM Wiki is different.** Instead of querying raw documents, the LLM incrementally builds and maintains a persistent wiki — a structured, interlinked collection of markdown files. When you add a new source, the LLM reads it, extracts key information, and integrates it into the wiki: updating entity pages, revising summaries, noting contradictions, strengthening the synthesis. The knowledge is compiled once and kept current.

> The wiki is a persistent, compounding artifact. The cross-references are already there. The contradictions have already been flagged. The synthesis already reflects everything you've read.

## Repository layout

```
llm-wiki/
├── README.md          # This file
├── CLAUDE.md          # Schema: tells the LLM how to operate this wiki
├── sources/           # Raw, immutable source documents (you curate these)
│   └── .gitkeep
└── wiki/              # LLM-generated and maintained markdown pages
    ├── index.md       # Content catalog — updated on every ingest
    └── log.md         # Append-only timeline of ingests, queries, and lints
```

## The three layers

| Layer | Owner | Description |
|-------|-------|-------------|
| `sources/` | You | Immutable raw documents: articles, papers, transcripts, data files |
| `wiki/` | LLM | Generated markdown: summaries, entity pages, concept pages, comparisons |
| `CLAUDE.md` | Both | Schema: structure conventions, workflow rules, output formats |

## The three operations

**Ingest** — Drop a new file in `sources/` and say "ingest `sources/my-file.md`". The LLM reads it, writes a summary page in `wiki/`, updates relevant entity and concept pages, updates `wiki/index.md`, and appends an entry to `wiki/log.md`. A single source often touches 10–15 wiki pages.

**Query** — Ask questions against the wiki. The LLM reads `wiki/index.md` to find relevant pages, drills into them, and synthesizes an answer with citations. Good answers get filed back as new wiki pages — your explorations compound just like ingested sources do.

**Lint** — Ask the LLM to health-check the wiki. It looks for contradictions, stale claims, orphan pages, missing cross-references, and data gaps. Keeps the wiki clean as it grows.

## Getting started

1. Clone this repo
2. Open it in [Obsidian](https://obsidian.md) (or any markdown editor) for browsing
3. Open a Claude Code (or Codex / any LLM agent) session pointed at this directory
4. The agent will read `CLAUDE.md` automatically and know how to operate the wiki
5. Drop a source file in `sources/` and tell the agent to ingest it

## Recommended tools

| Tool | Purpose |
|------|---------|
| [Obsidian](https://obsidian.md) | Browse and view the wiki; graph view for link topology |
| [Obsidian Web Clipper](https://obsidian.md/clipper) | Convert web articles to markdown for `sources/` |
| [Marp](https://marp.app) | Generate slide decks from wiki pages |
| [qmd](https://github.com/tobi/qmd) | Local BM25/vector search over markdown at scale |
| [Dataview](https://github.com/blacksmithgu/obsidian-dataview) | Dynamic tables from page frontmatter |

## Why this works

The tedious part of maintaining a knowledge base is not the reading or thinking — it's the bookkeeping: updating cross-references, keeping summaries current, noting when new data contradicts old claims, maintaining consistency across dozens of pages. Humans abandon wikis because the maintenance burden grows faster than the value.

LLMs don't get bored, don't forget to update a cross-reference, and can touch 15 files in one pass. The wiki stays maintained because the cost of maintenance is near zero.

**The human's job:** curate sources, direct the analysis, ask good questions, think about what it all means.  
**The LLM's job:** everything else.

---

> *Inspired by Vannevar Bush's Memex (1945) — a personal, curated knowledge store with associative trails between documents. Bush's vision was closer to this than to what the web became: private, actively curated, with the connections between documents as valuable as the documents themselves. The part he couldn't solve was who does the maintenance. The LLM handles that.*
