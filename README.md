# Journalist and Media List Builder MCP Server

[![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-journalist-media-list-builder)](https://www.npmjs.com/package/@mambalabsdev/mcp-journalist-media-list-builder) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-journalist-media-list-builder)](https://github.com/mambalabsdev/mcp-journalist-media-list-builder/blob/main/LICENSE)

<a href="https://mcprush.com/to/mcp-journalist-media-list-builder?ref=badge"><img width="380" height="200" src="https://mcprush.com/badge/mcp-journalist-media-list-builder/card.svg" alt="Journalist and Media List Builder MCP server" /></a>

An MCP server for the Mamba Labs Journalist and Media List Builder actor on Apify. Give it the beats or topics you want press for. It finds recent news articles on each one, reads the byline on each article page, and returns one row per journalist and outlet: name, outlet, author page, how many matching articles they wrote, their latest one, and the article links as proof.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Your keys](#your-keys)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

The articles come from the Mamba Labs News and Media Mention Monitor, which the actor runs on your Apify account. Press release wires are left out by default, and agency, desk, and staff bylines are never returned. When no journalist is found, one free summary row gives the article, page, and byline counts. All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-journalist-media-list-builder": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-journalist-media-list-builder"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `find_journalists` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "Which journalists wrote about sales automation in the last month?"
- "Build me a media list of reporters covering fintech funding at TechCrunch and Finextra."
- "Find reporters who wrote at least twice about revenue operations, with their author pages."

## Tool

`find_journalists`. One tool. Example arguments:

```json
{
  "topics": ["\"sales automation\""],
  "since_days": "30",
  "min_articles": "1"
}
```

## Inputs

Every buyer facing input of the actor, unchanged. Omitted inputs take the actor's own defaults. Numbers and yes or no values are sent as strings.

| Input | Type | Description |
|---|---|---|
| `topics` | array | 1 to 20 topics or beats. Required |
| `since_days` | string | Days back, 1 to 90. Default 30 |
| `country` | string | Google News country edition. Default US |
| `language` | string | Language code. Default en |
| `outlets_include` | array | Only these outlet domains |
| `outlets_exclude` | array | Never these outlet domains |
| `include_press_releases` | string | false (default) or true |
| `min_articles` | string | Least matching articles per journalist, 1 to 20. Default 1 |
| `max_articles_per_topic` | string | Newest articles read per topic, 1 to 100. Default 30 |
| `max_journalists` | string | Most journalist rows, 1 to 500. Default 50 |
| `max_charge_usd` | string | Optional cap on the whole run, the news run included |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `journalist-row`, per journalist and outlet | $0.008 | $0.0076 | $0.0072 | $0.0068 |
| `apify-actor-start`, per run start | $0.0025 | $0.0025 | $0.0025 | $0.0025 |
| News run `article-row`, per article read | $0.0023 | $0.002185 | $0.00207 | $0.001955 |
| News run `apify-actor-start`, per run | $0.0015 | $0.0015 | $0.0015 | $0.0015 |

About half of news article pages name a journalist, so expect roughly 3 to 4 articles per journalist row. A summary row is free.

## Your keys

The actor needs no key and holds none. Proxy traffic adds nothing to your price: Mamba Labs pays the platform costs of the run.

## Full actor documentation

[apify.com/mambalabs/journalist-media-list-builder](https://apify.com/mambalabs/journalist-media-list-builder)

## License

MIT. See [LICENSE](LICENSE).
