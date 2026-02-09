# Documentation project instructions

## About this project

This is the documentation site for [OpenData](https://github.com/opendata-oss/opendata), built on [Mintlify](https://mintlify.com). OpenData is a family of four databases — TimeSeries, Log, Vector, and Key-Value — that share a common storage foundation built on [SlateDB](https://github.com/slatedb/slatedb), an object-store-native LSM tree.

- Pages are MDX files with YAML frontmatter
- Configuration lives in `docs.json`
- Run `mint dev` to preview locally
- Run `mint broken-links` to check links

## Source repo structure

The source repo at `github.com/opendata-oss/opendata` contains:

- Per-database READMEs in each crate directory (e.g. `crates/timeseries/README.md`)
- RFCs in `rfcs/` organized by database
- Rust API docs generated from doc comments

Use these as primary sources when writing documentation content.

## Terminology

- **OpenData** — the umbrella project; always capitalize both words
- **SlateDB** — the shared LSM-tree storage engine; always capitalize the S and DB
- **TimeSeries** (or **TSDB**) — the time series database; one word, capital T and S
- **Log** — the event streaming database; capitalize when referring to the database
- **Vector** — the approximate nearest neighbor search database
- **Key-Value** — the simple key-value store; always hyphenated

## Style preferences

- Use active voice and second person ("you")
- Keep sentences concise — one idea per sentence
- Use sentence case for headings
- Bold for UI elements: Click **Settings**
- Code formatting for file names, commands, paths, and code references
- Use Rust for code examples unless the context is language-agnostic
- Use realistic values in examples (real metric names, plausible vectors) rather than `foo`/`bar`

## Content boundaries

- Do not document roadmap items as if they are existing features
- Clearly label experimental or unreleased functionality
- Keep implementation details in the Design sections; keep Usage sections task-oriented
