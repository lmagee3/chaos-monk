# Chaos Monk — Workspace Sitemap for Notion

**Your workspace. Indexed.**

A local-first Python tool that generates a complete, navigable sitemap of your entire Notion workspace. One command. Every page. Organized by hierarchy.

[![Live](https://img.shields.io/badge/Site-chaosmonk.netlify.app-E63946?style=flat-square)](https://chaosmonk.netlify.app)
[![Get It](https://img.shields.io/badge/Buy-$10%20on%20Gumroad-36A9AE?style=flat-square)](https://mageelawrence.gumroad.com/l/ocnvh)
[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat-square&logo=python&logoColor=white)](https://python.org)
[![License](https://img.shields.io/badge/License-Proprietary-gray?style=flat-square)]()

---

## The Problem

Notion workspaces grow fast. Pages multiply, context fragments, retrieval slows. You built a system — now you can't navigate it. Notion doesn't give you a map.

## The Solution

Chaos Monk crawls your workspace via the Notion API, builds a hierarchical tree of every page, and writes a linked, navigable sitemap directly to a Notion page you designate. Run it once, run it on a schedule — your workspace stays indexed.

## How It Works

```
┌─────────────┐     ┌──────────────┐     ┌───────────────┐     ┌─────────────┐
│ Config JSON  │────▶│ Notion API   │────▶│ Tree Builder  │────▶│ Sitemap Page│
│ (local)      │     │ Search/Crawl │     │ (recursive)   │     │ (in Notion) │
└─────────────┘     └──────────────┘     └───────────────┘     └─────────────┘
```

1. **Configure** — Point the tool at your workspace with your Notion integration token
2. **Crawl** — The indexer searches all pages via the Notion API with pagination and rate limit handling
3. **Build** — Pages are organized into a parent-child tree, sorted alphabetically per level
4. **Write** — A clean, linked bulleted list is written to your designated sitemap page in Notion

## Architecture

```
indexer.py (single-file, ~250 lines)
├── Config loader (JSON-based, no env vars)
├── Notion API client (notion-client SDK)
├── Recursive page crawler (paginated search, 2000 page cap)
├── Tree builder (parent-child mapping, cycle detection)
├── Markdown generator (hierarchical indented links)
├── Notion page writer (batched block API, 100-block chunks)
└── Rate limit handler (429 retry with backoff)
```

**Key design decisions:**

- **Single file** — No framework, no build step, no complexity. `pip install notion-client` and go.
- **Local-first** — Your token stays on your machine. No server, no account, no telemetry.
- **Deterministic** — Same workspace state = same output. No randomness, no caching artifacts.
- **Dry-run mode** — Preview the sitemap in terminal before writing to Notion.
- **Batch writes** — Notion API limits 100 blocks per append. The tool chunks automatically.
- **Cycle detection** — Visited-set prevents infinite recursion on circular page references.

## Tech Stack

| Component | Technology |
|-----------|-----------|
| Language | Python 3.10+ |
| Notion SDK | `notion-client` (official) |
| Config | JSON (no env dependency) |
| Output | Notion page (bulleted list with links) |
| Hosting | None — runs locally |
| Dependencies | 1 (`notion-client`) |

## What You Get

- `indexer.py` — The complete workspace indexer
- `config.json` — Template configuration file
- Setup guide (PDF + DOCX) — Step-by-step with screenshots
- Notion template — Pre-built sitemap page ready to duplicate

## Use Cases

- **Founders** — Map documentation, roadmaps, investor notes
- **Students** — Index coursework, research, projects across semesters
- **Operators** — Anyone who lives in Notion and has lost track of where things are
- **Teams** — Shared map of a collective workspace

## Privacy & Security

- **No server component** — Everything runs on your machine
- **No data export** — Pages are read via API and written back to Notion
- **No tracking** — No analytics, no telemetry, no phone-home
- **Token stays local** — Your integration secret never leaves `config.json`

---

## Get It

**[$10 — One-time purchase on Gumroad](https://mageelawrence.gumroad.com/l/ocnvh)**

Includes the indexer script, config template, setup guide, and Notion template. Pay once, use forever.

---

**Built by [Lawrence Magee](https://github.com/lmagee3)** — Part of the [Chaos Monk](https://chaosmonk.netlify.app) tool line by Malleus Prendere LLC.
