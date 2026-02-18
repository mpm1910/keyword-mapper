# 🗺️ Keyword Mapper — Claude Code Agent

> Autonomous SEO keyword research & URL mapping agent for [Claude Code](https://code.claude.com/docs/en/overview). Fetches your sitemap, queries DataForSEO, analyzes competitors, and produces a complete keyword-to-URL map with anti-cannibalization — all in one prompt.

---

## ✨ What It Does

| Phase | Description |
|-------|-------------|
| **1. URL Recon** | Parses your XML sitemap (or crawls JS-rendered SPAs via crawl4ai) and extracts clean page URLs |
| **2. Data Ingestion** | Queries DataForSEO for ranked keywords, keyword ideas, competitor domains, content gaps, search intent & keyword difficulty |
| **3. Deterministic Mapping** | Maps Primary KW → URL (1:1, no duplicates), assigns Secondary KWs, validates intent match, runs anti-cannibalization checks |
| **4. Gap Analysis** | Suggests additional keywords for weak pages, proposes new pages for uncovered transactional/commercial queries |

### Output Sections

- **A.** Complete Keyword → URL map (every sitemap URL included)
- **B.** 20-30 additional keyword suggestions for existing URLs
- **C.** Content gap — new page proposals with slug, H1, title & meta description
- **D.** Competitor analysis matrix
- **E.** Strategic SEO recommendations with priority levels

---

## 🚀 Quick Start

### Prerequisites

- [Claude Code](https://code.claude.com/docs/en/overview) (Claude's CLI agent)
- **DataForSEO** MCP server configured (`dfs-mcp`)
- **crawl4ai** MCP server (optional, for JS-rendered sites)

### Installation

Copy the agent file into your Claude Code agents directory:

```bash
# Create the agents directory if it doesn't exist
mkdir -p .claude/agents

# Copy the agent
cp keyword-mapper.md .claude/agents/keyword-mapper.md
```

### Usage

Invoke the agent in Claude Code with `@keyword-mapper`:

```
@keyword-mapper

Biznes: Sklep internetowy z alkomatorami profesjonalnymi dla firm i policji.
Sprzedajemy alkomaty Lion, Promiler, AlkoHit. Działamy w Polsce.

Sitemap: https://example.com/sitemap.xml

Konkurenci: promiler.pl, alko-tester.pl, alkotest.pl
Filtr: KD max 60, Volume min 200, język pl, lokalizacja Polska
```

The agent will produce a `keyword-map-{domain}.md` file in your working directory.

---

## ⚙️ Configuration

| Parameter | Default | Description |
|-----------|---------|-------------|
| `KD max` | 70 | Maximum keyword difficulty |
| `Volume min` | 100 | Minimum monthly search volume |
| `Język` | pl | Language code |
| `Lokalizacja` | Polska (2616) | DataForSEO location code |
| `Konkurenci` | auto-detected | Competitor domains for gap analysis |

---

## 🔧 Required MCP Tools

The agent uses these MCP tool endpoints:

| Tool | Purpose |
|------|---------|
| `WebFetch` | Fetching sitemap XML |
| `Bash` | Saving output to file |
| `crawl4ai → crawl` | Crawling JS-rendered pages |
| `crawl4ai → map` | Mapping site topology |
| `dfs-mcp → ranked_keywords` | Current domain rankings |
| `dfs-mcp → keyword_ideas` | Seed keyword expansion |
| `dfs-mcp → related_keywords` | Related keyword discovery |
| `dfs-mcp → search_intent` | Intent classification |
| `dfs-mcp → competitors_domain` | Competitor detection |
| `dfs-mcp → domain_intersection` | Content gap analysis |
| `dfs-mcp → bulk_keyword_difficulty` | KD scoring |
| `dfs-mcp → serp_organic_live_advanced` | Live SERP data |

---

## 📋 Output Example

The agent generates a Markdown dashboard:

```
# 🗺️ Keyword Map – example.com | 2026-02-17

## Podsumowanie
| Metric              | Wartość               |
|---------------------|-----------------------|
| URL-e przeanalizowane | 87                  |
| URL-e zmapowane     | 72                    |
| Frazy użyte łącznie | 215                   |
| Content gaps        | 12                    |
| Top konkurent       | rival.pl (45 fraz)    |

## A. Mapa Keyword → URL
| URL | Primary KW (Vol) | Secondary KWs (Vol) | Intent | KD | Pozycja |
|-----|-------------------|---------------------|--------|----|---------|
| /   | alkomaty (1200)   | alkomat (800)       | Komercyjna | 34 | 5  |
| ... | ...               | ...                 | ...    | ...| ...     |
```

---

## 🌍 Language

The agent's interface and output are in **Polish** 🇵🇱 — designed for the Polish SEO market. It uses Polish intent labels (*Transakcyjna, Komercyjna, Informacyjna, Nawigacyjna*) and defaults to Polish language/location settings in DataForSEO.

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.

---

## 🤝 Contributing

1. Fork the repo
2. Create your feature branch (`git checkout -b feature/my-improvement`)
3. Commit your changes (`git commit -m 'Add my improvement'`)
4. Push to the branch (`git push origin feature/my-improvement`)
5. Open a Pull Request

---

Made with ❤️ for SEO professionals using Claude Code.
