# @celluloid/toolkit-api

A TypeScript client library for the [Celluloid Toolkit](https://github.com/celluloid-camp/celluloid-toolkit), generated from the official OpenAPI specification. This package provides a fully type-safe fetch client for the Celluloid Toolkit.

## Installation

```bash
pnpm add @celluloid/toolkit-api
```

Or with npm:

```bash
npm install @celluloid/toolkit-api
```

## Usage

### Basic Example - Starting Video Analysis

```typescript
import { createClient } from '@celluloid/toolkit-api/client/client';
import { startDetectionAnalysePost } from '@celluloid/toolkit-api/client';

const client = createClient({
  baseUrl: 'https://toolkit.celluloid.me',
  headers: {
    'x-api-key': 'YOUR_API_KEY',
  },
});

const response = await startDetectionAnalysePost({
  client,
  body: {
    project_id: 'your-project-id',
    video_url: 'https://example.com/video.mp4',
    similarity_threshold: 0.5,
  },
});

console.log(response.data); // { job_id, status, queue_position, message, callback_url }
```

### Using the Default Client Instance

You can also use the pre-configured default client instance:

```typescript
import { client } from '@celluloid/toolkit-api/client/client.gen';
import { startDetectionAnalysePost } from '@celluloid/toolkit-api/client';

// Configure the default client
client.setConfig({
  baseUrl: 'https://toolkit.celluloid.me',
  headers: {
    'x-api-key': 'YOUR_API_KEY',
  },
});

const response = await startDetectionAnalysePost({
  client,
  body: {
    project_id: 'your-project-id',
    video_url: 'https://example.com/video.mp4',
  },
});
```

### Checking Job Status

```typescript
import { getJobStatusStatusJobIdGet } from '@celluloid/toolkit-api/client';

const status = await getJobStatusStatusJobIdGet({
  client,
  path: {
    job_id: 'your-job-id',
  },
});

console.log(status.data); // { status, progress, ... }
```

### Getting Job Results

```typescript
import { getJobResultsResultsJobIdGet } from '@celluloid/toolkit-api/client';

const results = await getJobResultsResultsJobIdGet({
  client,
  path: {
    job_id: 'your-job-id',
  },
});

console.log(results.data); // { version, metadata, frames, ... }
```

### Health Check

```typescript
import { healthCheckHealthGet } from '@celluloid/toolkit-api/client';

const health = await healthCheckHealthGet({ client });
console.log(health.data); // { status: 'ok' }
```

### Custom Configuration

```typescript
import { createClient } from '@celluloid/toolkit-api/client';

const client = createClient({
  baseUrl: 'https://toolkit.celluloid.me',
  headers: {
    'x-api-key': 'YOUR_API_KEY',
    'User-Agent': 'MyApp/1.0',
  },
  fetch: customFetch,
});

client.setConfig({
  baseUrl: 'https://another-instance.com',
});
```

## API Reference

The client is generated from the Celluloid Toolkit OpenAPI specification. All API endpoints are available through the SDK functions exported from `@celluloid/toolkit-api/client`.

### Available Endpoints

- `healthCheckHealthGet` - Health check endpoint
- `startDetectionAnalysePost` - Start video analysis (requires API key)
- `getJobStatusStatusJobIdGet` - Get the status of a detection job
- `getJobResultsResultsJobIdGet` - Get the results of a completed detection job

## Development

### Prerequisites

- Node.js (v18 or higher)
- pnpm (v9 or higher)

### Setup

1. Clone the repository
2. Install dependencies:

```bash
pnpm install
```

### Generate Client

```bash
pnpm run generate
```

### Build

```bash
pnpm run build
```

### Type Checking

```bash
pnpm run typecheck
```
## License

MIT
