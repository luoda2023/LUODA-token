# LUODA-TOKEN

AI Provider Proxy Management Panel built with Next.js.

## Requirements

- **Node.js** >= 18.0.0
- **npm** >= 9.0.0

## Quick Start

### 1. Clone

```bash
git clone https://github.com/luoda2023/LUODA-token.git
cd LUODA-token
```

### 2. Install

```bash
npm install
```

### 3. Configure

```bash
cp .env.example .env
```

Edit `.env`:

```ini
JWT_SECRET=your-random-secret-key
INITIAL_PASSWORD=your-password
```

### 4. Run Dev Server

```bash
npm run dev
```

Visit `http://localhost:20128`

## Production

```bash
npm run build
npm start
```

## Docker (1Panel)

### 1Panel Compose

```yaml
version: "3.8"
services:
  luoda-token:
    image: ghcr.io/luoda2023/LUODA-token:latest
    container_name: luoda-token
    restart: always
    ports:
      - "20128:20128"
    volumes:
      - ./data:/app/data
    environment:
      - DATA_DIR=/app/data
      - JWT_SECRET=your-secret
      - INITIAL_PASSWORD=your-password
      - PORT=20128
```

### Terminal

```bash
mkdir -p /opt/luoda-token/data
docker run -d \
  --name luoda-token \
  --restart always \
  -p 20128:20128 \
  -v /opt/luoda-token/data:/app/data \
  -e DATA_DIR=/app/data \
  -e JWT_SECRET=your-secret \
  -e INITIAL_PASSWORD=your-password \
  ghcr.io/luoda2023/LUODA-token:latest
```

## Features

- Unified API endpoint for all AI providers
- Token usage tracking
- 100+ providers support
- MITM proxy for CLI tools
- Model combos with fallback
- CLI tool integration

## License

MIT