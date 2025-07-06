# Discord to Matrix Bridge

A Node.js application that relays messages between multiple Discord and Matrix channels.

## Prerequisites

- Node.js 18 or higher (for local development)
- A Discord bot token and application
- A Matrix homeserver and access token
- Docker and Docker Compose (for containerized deployment)

## Setup

### Local Setup

1. Clone this repository
2. Install dependencies:
   ```bash
   npm install
   ```
3. Copy the `.env.example` file to `.env`:
   ```bash
   cp .env.example .env
   ```
4. Configure your environment variables in `.env`:
   - `DISCORD_TOKEN`: Your Discord bot token
   - `MATRIX_HOMESERVER_URL`: Your Matrix homeserver URL (e.g., https://matrix.org)
   - `MATRIX_ACCESS_TOKEN`: Your Matrix access token
   - `CHANNEL_CONNECTIONS`: A JSON array of channel pairs, each containing:
     - `discord`: Discord channel ID
     - `matrix`: Matrix room ID
   
   Example configuration:
   ```
   CHANNEL_CONNECTIONS=[
     {"discord":"111111111111111111","matrix":"!roomid:matrix.org"},
     {"discord":"222222222222222222","matrix":"!anotherroomid:matrix.org"}
   ]
   ```

### Docker Setup

1. Clone this repository
2. Copy the `.env.example` file to `.env` and configure it as described above
3. Build and start the container:
   ```bash
   docker-compose up -d
   ```

To view logs:
```bash
docker-compose logs -f
```

To stop the container:
```bash
docker-compose down
```

### Discord Bot Setup
1. Go to the [Discord Developer Portal](https://discord.com/developers/applications)
2. Create a new application
3. Go to the Bot section and create a bot
4. Enable the "Message Content Intent" under Privileged Gateway Intents
5. Copy the bot token and add it to your `.env` file
6. Use the OAuth2 URL Generator to create an invite link with the following permissions:
   - Read Messages/View Channels
   - Send Messages
7. Invite the bot to your server

### Matrix Setup
1. Create a Matrix account on your preferred homeserver (e.g., matrix.org)
2. Generate an access token:
   - Log into your Matrix client (Element, etc.)
   - Go to Settings > Help & About > Advanced
   - Click "Access Token" to reveal your token
   - Copy the token and add it to your `.env` file
3. Get your user ID (format: @username:homeserver.org)
4. Join the rooms you want to bridge to
5. Get the room IDs:
   - In Element, go to the room settings
   - Look for "Internal room ID" or use the room alias
   - Room IDs start with `!` and end with `:homeserver.org`

## Running the Application

### Local Development

Development mode with auto-reload:
```bash
npm run dev
```

Production mode:
```bash
npm start
```

### Docker Production

Start the container:
```bash
docker-compose up -d
```

## Features

- Relays messages between multiple Discord and Matrix channels
- Supports configurable channel-to-channel connections
- Preserves username information
- Handles basic error cases
- Logs successful message relays and errors
- Containerized deployment with Docker 