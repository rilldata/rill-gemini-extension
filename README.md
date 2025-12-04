# Rill Gemini Extension

Data analysis using Rill's metrics layer via Model Context Protocol for **Google Gemini**.

This extension enables Google's Gemini AI assistant to query and analyze your Rill data directly through natural language conversations. Using Gemini's CLI and the Model Context Protocol (MCP), you can explore metrics, identify trends, and generate insights without writing queries manually.

## Prerequisites

- A Rill project or cloud account - Get Started [here](https://docs.rilldata.com/)
- [Rill CLI](https://docs.rilldata.com/install)
- [Google Gemini CLI](https://github.com/google-gemini/gemini-cli)

Before you install the extension, create an access token for the user that will run Gemini. Tokens are user-level credentials — keep them secure and never commit them to source control.

Create a token in Rill Cloud (Settings → API Tokens) or run:

```bash
rill token issue --display-name "Gemini Extension"
```
> Save the token somewhere safe (see configuration below).

## Installation

Install the extension with the Google Gemini CLI:

```bash
gemini extensions install https://github.com/rilldata/rill-gemini-extension
# optional version tag --ref=v0.1.0
```

### What the installer prompts mean

When running the installer you may be asked for Organization, Project, and Access token — these are prompts to help populate the extension's configuration. The values will be saved to a `.env` file in the extension’s directory (e.g., `~/.gemini/extensions/rill/.env`).

- `Keychain not available` — this is informational, not fatal. It indicates the installer couldn't store credentials in the OS keychain and will fall back to file-based storage.

## Configuration

This extension reads configuration from environment variables. You can set these in either of two mutually exclusive ways:

- Folder-scoped `.env` file (project-specific). Place this in your project root.
- Global-scoped `.env` for the Gemini extension (user-wide). Place at: `~/.gemini/extensions/rill/.env`

Recommended `.env` example (project root or global):
```dotenv
# Best practice: keep tokens out of source control (add .env to .gitignore)
RILL_ORG=your-organization-name        # optional if project file already has org
RILL_PROJECT=your-project-name         # optional if your project uses rill.yaml
RILL_ACCESS_TOKEN=your-access-token    # user-level token — do not commit
```

How the extension decides:
- The extension reads environment variables first: `RILL_ORG`, `RILL_PROJECT`, `RILL_ACCESS_TOKEN`.
- If `RILL_PROJECT` is defined in `rill.yaml`, you don't need to repeat it in `.env` unless you intend to override it.
- Tokens are user-level: prefer storing them globally or in the OS keychain, not in project repositories.

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

### Custom Slash Commands

This extension includes custom slash commands for common Rill analysis workflows. Use these commands in your Gemini conversations to streamline your data exploration:

#### Available Commands

- **`/rill:metrics`** - List all available metrics views in your Rill project with descriptions
- **`/rill:explore`** - Start a comprehensive OODA loop analysis for a specific metrics view
- **`/rill:trends`** - Analyze time-based trends with automatic granularity selection
- **`/rill:compare`** - Compare metrics across dimensions or time periods
- **`/rill:timerange`** - Check the available time range and data freshness for a metrics view

#### Usage Examples

**List available metrics views:**
```shell
gemini> /rill:metrics
```

**Start guided exploration:**
```shell
gemini> /rill:explore
# Gemini will ask which metrics view to analyze if not specified
```

**Analyze trends over time:**
```shell
gemini> /rill:trends
# Performs time-series analysis with visualizations
```

**Compare performance across dimensions:**
```shell
gemini> /rill:compare
# Supports dimension comparison, time period comparison, and segment comparison
```

**Check data availability:**
```shell
gemini> /rill:timerange
# Shows earliest and latest data points available
```

## Troubleshooting

### Connection Issues

If you can't connect to your Rill project:

- Verify your `.env` file or inputs contain valid credentials
- Confirm your access token has the necessary permissions
- Check that your organization and project names match your Rill Cloud URL

## Development

### Local Development

To test changes locally:

1. Make your changes to the extension files

2. Install the extension from your local development directory:

```bash
npm run link
```

3. Test the extension with the Gemini CLI, then unlink when done:

```bash
npm run unlink
```

### Releasing

This extension is distributed through [GitHub Releases](https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases)
