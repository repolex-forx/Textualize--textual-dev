# Repolex Knowledge Graph of Textualize/textual-dev

RDF knowledge graph data for [Textualize/textual-dev](https://github.com/Textualize/textual-dev), parsed by [repolex](https://repolex.ai).

> **Note**: This data is experimental and subject to change without notice.

## How to use this data

The easiest way to get started is to install the [rlex](https://github.com/repolex-ai/rlex) query tool:

```bash
cargo install --git https://github.com/repolex-ai/rlex
```

Verify the install:

```bash
rlex --help
```

**rlex is designed to be used primarily by LLMs in a terminal.** Start up your favorite AI assistant and ask it to use rlex. It handles the SPARQL — you just ask questions in plain English.

To load this repo's data:

```bash
rlex download Textualize/textual-dev
```

Consult `rlex --help` for other options, including SPARQL queries, HTTP server, and interactive visualization.

## Data structure

All data is stored as gzip-compressed [N-Quads](https://www.w3.org/TR/n-quads/) (`.nq.gz`), a standard RDF format that can be loaded into any triplestore or graph database.

```
.
├── aggregate
│   ├── ast
│   │   └── e563f96f32d582b7cf22622a401f537c40349adc
│   │       └── chunk-001.nq.gz
│   └── repolex
│       └── e563f96f32d582b7cf22622a401f537c40349adc
│           └── chunk-001.nq.gz
├── blob
│   ├── 00520e3ba732d373a53b90def1d7c742e0dc10e0.nq.gz
│   ├── 05af2bd691b80226d5a77e1884a139c0de5b1cf7.nq.gz
│   ├── 0c8b1e60e6d28a77466861914533f95bdac81ca2.nq.gz
│   ├── 0e333a94677c069f6cc2786bc014385150479d27.nq.gz
│   ├── 11aa98312980e560079e22bbebbe7ba460370126.nq.gz
│   ├── 185f0fb31982e5c8fccf7a3daec3a50cac54dd03.nq.gz
│   ├── 1c301c3b772fae22701d995fd3ff86ba5060f3a4.nq.gz
│   ├── 29a68ee512893e132f4120d32a26fe02326065fd.nq.gz
│   ├── 2e4af914d82cd89863ab9441af0b7e92e02031f5.nq.gz
│   ├── 2e933c92f5f04e29c6c77f633fccc8a76f3848b4.nq.gz
│   ├── 41919363233d32cc647e938dccd5df3e1a1cf3fd.nq.gz
│   ├── 43e79a0fdf4faa62ffda9a3894fab7b5d07c5f59.nq.gz
│   ├── 486dca3332fa989b88f49dc8c8873cab75a5d456.nq.gz
│   ├── 496f5fc75ad39f053a6170da20ee18d55f7e9301.nq.gz
│   ├── 5b73d2231172fce69a9ac1e2a6f213248a35d464.nq.gz
│   ├── 621641598632567b3058703d5b640c24d03fd9a5.nq.gz
│   ├── 63a2db69048a9c025251b06237cd58d8c017c3e1.nq.gz
│   ├── 68facdccb8a02d515ca3550e502f827dabe5f7d5.nq.gz
│   ├── 70d281b2c718b7314bfa70a278ba94abebf6bf4d.nq.gz
│   ├── 84b22ca4bf1e271249f4812641f3a49a150dd3ef.nq.gz
│   ├── 87607e7605f8082ec9ff2f416af7fef9a5f27dd2.nq.gz
│   ├── 87efd2bc841fa5a70a4d02767b336ca63b53c3b7.nq.gz
│   ├── 88dc79e277772d52b0e2c04b75531d9f035a84bf.nq.gz
│   ├── 96f53008959895f8f4e42ecd9fc3f1528d1b2523.nq.gz
│   ├── 9e35d1a25c61bcd3778475f67a4b255946aad855.nq.gz
│   ├── a5dc2a31df601f27c88114990cd6e6a79be40855.nq.gz
│   ├── ba51348ff573ff6a4df8ee1963b9d51b875572b7.nq.gz
│   ├── bb296aa2844fee6c5eb1dc0b9bdfe706d6db6da9.nq.gz
│   ├── bc9cd532ed20d40fab584b6af80e7536e1d40fe4.nq.gz
│   ├── c60895625337f3df8f3fd99c11e909cc809defdf.nq.gz
│   ├── cae0049e0d3d3db9f49d77975d50381b8df76c5d.nq.gz
│   ├── e0e83b6d3d42746b24d9f3222e6f3819112bcdd7.nq.gz
│   ├── e69de29bb2d1d6434b8b29ae775ad8c2e48c5391.nq.gz
│   ├── f4d86a460889d3fd08127a9f7dbd70c28f298e3b.nq.gz
│   └── fbf8c0b4025977ea9024c654d213893582aa1f4a.nq.gz
├── branch
│   └── branch.nq.gz
├── commit
│   └── commit.nq.gz
├── filetree
│   └── e563f96f32d582b7cf22622a401f537c40349adc.nq.gz
├── issue
│   └── issue.nq.gz
├── pr
│   └── pr.nq.gz
└── tag
    └── tag.nq.gz

13 directories, 43 files
```

| Directory | What it contains |
|-----------|-----------------|
| `blob/` | Per-file AST graphs, content-addressed by git blob SHA. Each file in the source repo gets its own graph. |
| `aggregate/ast/` | Combined AST graph per parsed commit. Merges all blob graphs for a snapshot of the entire codebase at that point. |
| `aggregate/lsp/` | Language Server Protocol enrichment: resolved symbols, definitions, references, and type information. |
| `aggregate/dataflow/` | Interprocedural data flow edges between functions and modules. |
| `aggregate/repolex/` | Combined graph (AST + LSP + dataflow) per commit. |
| `commit/` | Git commit metadata (author, date, message, parent links). |
| `branch/` | Branch metadata. |
| `tag/` | Tag metadata. |
| `filetree/` | File tree snapshots per commit (which files existed and their blob SHAs). |
| `audit/` | Code architecture and graph audit reports per commit. |

## Source repository

[Textualize/textual-dev](https://github.com/Textualize/textual-dev)

---
*Parsed on 2026-10-28 by [repolex](https://repolex.ai)*
