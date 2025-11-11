# MCP Client for Rill Data

Data analysis using Rill's metrics layer via Model Context Protocol.

Rill delivers the fastest path from data lake to dashboard. **For data engineers and analysts**, it provides rapid, self-service dashboards built directly on raw data lakes, eliminating traditional BI complexity. **For data consumers**, it ensures reliable, fast-loading dashboards with accurate, real-time metrics.

## Prerequisites

- [Rill CLI](https://docs.rilldata.com/install) installed
- Active Rill project or cloud account
- Gemini with extension support

```bash
curl https://rill.sh | sh
```

## Gemini Extension

Gemini easily integrates with Rill's metrics layer, enabling users to leverage Rill's powerful data modeling and visualization capabilities within their Gemini workflows.

## Installation

Install the extension with Gemini CLI:

```bash
gemini extensions install https://github.com/rilldata/rill-gemini-extension # optional version tag --ref=v0.1.0
```

## Configuration

Set up your Rill credentials using environment variables:

**Create a `.env` file** in your project root:

```dotenv
RILL_ORG=your-organization-name
RILL_PROJECT=your-project-name
RILL_ACCESS_TOKEN=your-access-token
```

**Get your credentials**:

- **Organization & Project**: From your Rill Cloud URL: `https://ui.rilldata.com/{org}/{project}`
- **Access Token**: Generate in Rill Cloud under Settings > API Tokens, or use CLI:
  ```bash
  rill token issue --display-name "Gemini Extension"
  ```

**Environment setup**:

- **Folder scoped**: Gemini automatically picks up the `.env` file from your project root
- **Global scope**: Copy your `.env` file to `~/.gemini/extensions/rill/.env`

> **Security**: Keep your `.env` file secure and never commit it to version control.

## Usage

> Examples used: [Production Examples](https://github.com/rilldata/rill?tab=readme-ov-file#production-examples)

```shell
gemini "Using Rill tell me about any trends you see in the Ads Bids dataview"
```

> Example output: [Analysis](docs/sample.md)

```shell
gemini "Tell me about the top publishers by ad spend in the Ads Bids dataview"
```

```shell
Based on my initial analysis, I'll focus on the top named publishers: KrushMedia, Sinclair Broadcasting, and Taboola.

Here's a breakdown of the top 10 publishers by ad spend:

  ┌──────────────────────────────────────┬───────────────────┬─────────────┐
  │ Publisher                            │ Advertising Spend │ Impressions │
  ├──────────────────────────────────────┼───────────────────┼─────────────┤
  │ KrushMedia                           │ $755,058.21       │ 50,219      │
  │ Sinclair Broadcasting - Bally Sports │ $419,923.62       │ 30,002      │
  │ Taboola                              │ $408,628.51       │ 81,782      │
  │ PubWise                              │ $202,980.07       │ 26,089      │
  │ Disney                               │ $48,075.66        │ 4,055       │
  │ Connatix                             │ $40,485.67        │ 7,090       │
  │ Spot.IM                              │ $38,171.29        │ 6,576       │
  │ Pluto TV                             │ $36,175.64        │ 4,396       │
  │ fubo.TV New                          │ $23,563.37        │ 1,641       │
  └──────────────────────────────────────┴───────────────────┴─────────────┘
```


## Development

### Local Development

To test changes locally:

1. Make your changes to the extension files

2. Install the extension from your local development directory:

```bash
npm run link
```

3. Test the extension in Gemini, then unlink when done:

```bash
npm run unlink
```

### Releasing

This extension is distributed through [GitHub Releases](https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases)
