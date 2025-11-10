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

Simply install with the `gemini extensions install https://github.com/rilldata/mcp` command.

Install the extension via GitHub using a specific release tag:

```bash
gemini extensions install https://github.com/rilldata/mcp --ref=v0.1.0
```

## Configuration

After installation, configure the extension with your Rill credentials. The extension will prompt you for the following information during setup:

- **Organization**: Your Rill organization name
- **Project**: Your Rill project name
- **Access Token**: Your Rill access token

To generate a Rill authentication token, run:

```bash
rill token issue --display-name "Gemini Extension"
```

> **Tip**: You can find your organization and project names in the Rill Cloud UI URL: `https://ui.rilldata.com/{organization}/{project}`

The extension configuration is handled automatically through Gemini's settings interface - no manual environment file setup is required.

  

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
