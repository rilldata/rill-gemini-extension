# Rill Gemini Extension

Data analysis using Rill's metrics layer via Model Context Protocol for **Google Gemini CLI**.

This extension enables Google's Gemini AI assistant to query and analyze your Rill data directly through natural language conversations. Using the Google Gemini CLI and the Model Context Protocol (MCP), you can explore metrics, identify trends, and generate insights without writing queries manually.

## Prerequisites

- A Rill project or cloud account — get started [here](https://docs.rilldata.com/)
- [Rill CLI](https://docs.rilldata.com/install)
- [Google Gemini CLI](https://github.com/google-gemini/gemini-cli)

Before you install the extension, create a user token for the account that will run the Google Gemini CLI. Rill distinguishes "user" and "service" tokens — use a user token for interactive developer tooling and a service token for automation/CI. Tokens are sensitive — keep them secure and never commit them to source control.

Create a token in Rill Cloud (Settings → API Tokens) (see https://docs.rilldata.com/manage/user-tokens) or run:

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

When running the installer you may be asked for Organization, Project, and a user/service token — these are prompts to help populate the extension's configuration. The values will be saved to a `.env` file in the extension’s directory (e.g., `~/.gemini/extensions/rill/.env`).

- `Keychain not available` — this is informational, not fatal. It indicates the installer couldn't store credentials in the OS keychain and will fall back to file-based storage.

## Configuration

This extension reads configuration from environment variables. Prefer setting environment variables globally (e.g., export in your shell profile) so your Rill tooling is configured once per machine. A local `.env` file is supported as a fallback.

Priority (order of precedence):
1. Exported OS environment variables (recommended) — e.g. `export RILL_USER_TOKEN=...`
2. Global Gemini extension `.env` (machine-wide): `~/.gemini/extensions/rill/.env` — useful when you want the Google Gemini CLI to pick up settings automatically
3. Project level `.env` (folder-scoped)

```bash
# Recommended .env (global config only)
# Use a global/machine-scoped .env (eg. ~/.gemini/extensions/rill/.env) or export the values from your shell profile
RILL_USER_TOKEN=your-user-token
# Optional: you can also set organization/project globally, but prefer keeping tokens and per-user secrets out of project folders.
RILL_ORG=your-organization-name
RILL_PROJECT=your-project-name
```

> **Security**: Keep your global `.env` file secure and never commit it to version control.

> Note: This extension currently reads configuration from environment variables
> and the Gemini extension settings. It does not automatically parse `rill.yaml`
> to infer project/organization settings.

## Usage

> Examples used: [Production Examples](https://github.com/rilldata/rill?tab=readme-ov-file#production-examples)

```shell
gemini "Using Rill, tell me about any trends you see in the Ads Bids dataview"
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

This extension includes custom slash commands for common Rill analysis workflows. Use these commands in your Google Gemini CLI conversations to streamline your data exploration:

#### Available Commands

- **`/rill:metrics`** - List all available metrics views in your Rill project with descriptions
- **`/rill:explore`** - Start a comprehensive OODA loop analysis for a specific metrics view
- **`/rill:trends`** - Analyze time-based trends with automatic granularity selection
- **`/rill:compare`** - Compare metrics across dimensions or time periods
- **`/rill:timerange`** - Check the available time range and data freshness for a metrics view

#### Usage Examples

**List available metrics views:**
```shell
gemini /rill:metrics
```

**Start guided exploration:**
```shell
gemini /rill:explore
# The Google Gemini CLI will ask which metrics view to analyze if not specified
```

**Analyze trends over time:**
```shell
gemini /rill:trends
# Performs time-series analysis with visualizations
```

**Compare performance across dimensions:**
```shell
gemini /rill:compare
# Supports dimension comparison, time period comparison, and segment comparison
```

**Check data availability:**
```shell
gemini /rill:timerange
# Shows earliest and latest data points available
```


## Uninstallation

```bash
gemini extensions uninstall rill
```

## Troubleshooting

### Connection Issues

If you can't connect to your Rill project:

- Verify your `.env` file or inputs contain valid credentials
  - Confirm your user/service token has the necessary permissions
- Check that your organization and project names match your Rill Cloud URL

## Development

### Local Development

To test changes locally:

1. Make your changes to the extension files

2. Install the extension from your local development directory:

```bash
npm run link
```

3. Test the extension with the Google Gemini CLI, then unlink when done:

```bash
npm run unlink
```

### Releasing

This extension is distributed through [GitHub Releases](https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases)
