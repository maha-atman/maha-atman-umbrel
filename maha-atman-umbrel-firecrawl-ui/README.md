# Firecrawl UI for Umbrel

This Umbrel app package runs the official Firecrawl UI Docker image from
`obeoneorg/firecrawl-ui` and proxies it through Umbrel.

## What it does

- Serves the Firecrawl UI web interface on port `8080`
- Provides a browser-based interface for the Firecrawl API
- Lets you configure the Firecrawl Base URL and optional API key in the UI

## Installation

1. Install this app from the Umbrel App Store.
2. Open the app from the Umbrel dashboard.
3. Configure the Firecrawl Base URL in the UI settings.

## Recommended Firecrawl API URL

If you also install `maha-atman-umbrel-firecrawl`, use:

```text
http://<your-umbrel-ip>:10080/v0
```

If your Firecrawl API is hosted elsewhere, use the matching base URL for that
service.

## Upstream repository

This package is based on the official Firecrawl UI project:
https://github.com/obeone/firecrawl-ui

## Notes

- The UI is frontend-only and requires a Firecrawl API endpoint to function.
- The app uses the official Docker image from Docker Hub:
  `obeoneorg/firecrawl-ui:latest`.

## Support

For upstream project issues, open an issue here:
https://github.com/obeone/firecrawl-ui/issues
