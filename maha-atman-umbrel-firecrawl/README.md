# Firecrawl for Umbrel

Firecrawl is a web scraping and crawling platform built with performance and reliability in mind. This is the Umbrel app package for easy installation on your Umbrel server.

## Features

- **Web Scraping API** - Extract structured data from websites via REST API
- **Headless Browser Automation** - Automated browsing with Playwright
- **Concurrent Crawling** - Highly parallelized crawling with configurable concurrency
- **Proxy Support** - Route requests through proxies
- **LLM Integration** - Extract and structure data using language models
- **Webhook Support** - Receive notifications when crawls complete
- **Rate Limiting** - Built-in rate limiting per API key

## Installation

### Via Umbrel UI

1. Open Umbrel dashboard
2. Navigate to **App Store** → **Settings**
3. Click **Add custom app store**
4. Paste the repository URL: `https://github.com/maha-atman/maha-atman-umbrel`
5. The store will appear in your App Store
6. Find **Firecrawl** and click **Install**
7. Wait for the services to start (2-3 minutes for initial setup)

### Via Umbrel CLI

```bash
umbrel app-store add https://github.com/maha-atman/maha-atman-umbrel
umbrel app install maha-atman-umbrel-firecrawl
```

## Configuration

After installation, you can configure Firecrawl via environment variables. To customize settings:

1. Stop the app: `umbrel app stop maha-atman-umbrel-firecrawl`
2. Edit the environment in Umbrel's app-data directory or via the dashboard
3. Restart: `umbrel app start maha-atman-umbrel-firecrawl`

### Environment Variables

#### Core Settings
- `NUM_WORKERS_PER_QUEUE`: Number of workers per queue (default: 4)
- `CRAWL_CONCURRENT_REQUESTS`: Concurrent browser requests (default: 5)
- `MAX_CONCURRENT_JOBS`: Maximum concurrent crawl jobs (default: 3)
- `BROWSER_POOL_SIZE`: Size of browser pool (default: 3)
- `LOGGING_LEVEL`: Log level - `debug`, `info`, `warn`, `error` (default: `info`)

#### Database
- `POSTGRES_USER`: PostgreSQL username (default: `firecrawl`)
- `POSTGRES_PASSWORD`: PostgreSQL password (default: `firecrawl`)
- `POSTGRES_DB`: Database name (default: `firecrawl`)

#### LLM Features (Optional)
- `OPENAI_API_KEY`: OpenAI API key for data extraction
- `OPENAI_BASE_URL`: Custom OpenAI base URL
- `MODEL_NAME`: LLM model name (e.g., `gpt-4`)
- `MODEL_EMBEDDING_NAME`: Embedding model name

#### Proxy Support (Optional)
- `PROXY_SERVER`: Proxy server URL (e.g., `http://proxy.example.com:8080`)
- `PROXY_USERNAME`: Proxy username
- `PROXY_PASSWORD`: Proxy password

#### Webhooks (Optional)
- `SLACK_WEBHOOK_URL`: Slack webhook for notifications
- `SELF_HOSTED_WEBHOOK_URL`: Custom webhook URL for job completions

## Usage

Once installed, Firecrawl will be accessible at `http://your-umbrel-ip:10080`

### API Endpoints

- `POST /v0/scrape` - Scrape a single URL
- `POST /v0/crawl` - Start a crawl job
- `GET /v0/crawl/:jobId` - Get crawl status
- `GET /health` - Health check

### Example Request

```bash
curl -X POST http://localhost:10080/v0/scrape \
  -H "Content-Type: application/json" \
  -d '{
    "url": "https://example.com",
    "formats": ["markdown", "html"]
  }'
```

## Resource Requirements

- **CPU**: Minimum 2 cores, 4+ cores recommended
- **RAM**: Minimum 4GB, 8GB+ recommended for concurrent crawls
- **Disk**: Minimum 10GB for database and cache

## Troubleshooting

### Services failing to start
- Check Umbrel logs: `umbrel logs`
- Ensure sufficient disk space and RAM
- Restart the app: `umbrel app restart maha-atman-umbrel-firecrawl`

### Database errors
- Clear data: `rm -rf ~/umbrel/app-data/maha-atman-umbrel-firecrawl/data/postgres`
- Restart: `umbrel app restart maha-atman-umbrel-firecrawl`
- This will reinitialize the database

### Out of memory
- Reduce concurrency settings in environment variables
- Increase available RAM
- Check other running apps

### API not responding
- Check if all services are healthy: `docker-compose ps`
- View service logs: `docker-compose logs api`
- Ensure port 10080 is not in use by another app

## Support

- **GitHub Issues**: https://github.com/maha-atman/maha-atman-umbrel/issues
- **Firecrawl Docs**: https://firecrawl.dev/
- **Firecrawl GitHub**: https://github.com/mendableai/firecrawl

## License

Firecrawl is available under its original license. This Umbrel app package maintains compatibility with Umbrel's app store system.
