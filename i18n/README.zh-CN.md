# LUODA-TOKEN Installation

AI Provider Proxy Management Panel built with Next.js.

## Environment

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
JWT_SECRET=replace-with-random-key
INITIAL_PASSWORD=set-your-login-password
```

### 4. Run

**Dev Mode:**

```bash
npm run dev
```

**Production:**

```bash
npm run build
npm start
```

Visit `http://localhost:20128`, login with INITIAL_PASSWORD.

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

- Unified endpoint for all AI providers
- Real-time token usage tracking
- 100+ providers support
- MITM proxy for CLI tools
- Model combos with fallback
- CLI tool integration (Cursor, Codex, Cline, etc.)

## Add Providers

Go to **Providers** -> **Add Provider**:
- OAuth: Google, GitHub, Anthropic
- API Key: Enter your key directly
- Cookie: Import from browser

## Get API Endpoint

After adding providers, visit **Endpoint** page:
```
http://localhost:20128/v1
```

## CLI Tools

Go to **CLI Tools** page, select your tool (Cursor, Codex, etc.), click **Apply**.

## Common Issues

### Port in use?

Edit `.env`, change `PORT=custom-port`, restart.

### How to update?

```bash
git pull
npm install
npm run build
npm start
```

### Forgot password?

Edit `.env` `INITIAL_PASSWORD`, restart. This only resets password, not provider data.

## Env Vars Reference

| Var | Description | Default |
|-----|-------------|---------|
| JWT_SECRET | JWT signing key |Required|
| INITIAL_PASSWORD | Login password |Required|
| PORT | Service port |20128|
| NODE_ENV | Environment |production|
| DATA_DIR | Data directory |~/.9router|

## License

MIT