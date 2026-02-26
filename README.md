# mc-server

A Dockerized Minecraft Java Edition server using the [itzg/minecraft-server](https://github.com/itzg/docker-minecraft-server) image.

## Features

- ✅ Latest Minecraft version
- ✅ Whitelist enabled for player access control
- ✅ Auto-pause when no players online (saves resources)
- ✅ Custom server icon
- ✅ Death counter scoreboard
- ✅ Normal difficulty
- ✅ Persistent data storage

## Prerequisites

- [Docker](https://www.docker.com/get-started) installed
- [Docker Compose](https://docs.docker.com/compose/install/) installed
- At least 2GB of available RAM
- Port 25565 available

## Quick Start

1. **Clone or download this repository**

2. **Start the server**

   ```bash
   docker compose up -d
   ```

3. **View logs**

   ```bash
   docker compose logs -f
   ```

4. **Stop the server**

   ```bash
   docker compose down
   ```

5. **Restart the server**

   ```bash
   docker compose restart
   ```

## Configuration

### Server Settings

The server is configured via environment variables in `compose.yaml`:

- **VERSION**: `LATEST` - Automatically uses the latest Minecraft version
- **DIFFICULTY**: `normal` - Server difficulty level
- **EULA**: `TRUE` - Accepts Minecraft EULA agreement
- **ENABLE_AUTOPAUSE**: `TRUE` - Pauses the server when no players are online

### Whitelist Management

The server uses whitelist mode. To add players:

1. Edit `whitelist.json` and add player entries:

   ```json
   [
     {
       "uuid": "player-uuid-here",
       "name": "PlayerName"
     }
   ]
   ```

2. Restart the server for changes to take effect:

   ```bash
   docker compose restart
   ```

**Tip**: You can get player UUIDs from [mcuuid.net](https://mcuuid.net/)

### Custom Server Icon

Replace `logo.jpg` with your own 64x64 pixel image to customize the server icon that appears in the Minecraft client's server list.

### Scoreboard

The server automatically sets up a death counter that displays in the player list (TAB menu).

## Data Persistence

Server data is stored in `~/minecraft_data` on your host machine. This includes:

- World files
- Player data
- Server configuration
- Plugins/mods (if added)

## Memory Management

By default, the container uses available system memory. To limit memory usage, uncomment the deploy section in `compose.yaml`:

```yaml
deploy:
  resources:
    limits:
      memory: 1.5G
```

## Connecting to the Server

1. Open Minecraft Java Edition
2. Click "Multiplayer"
3. Click "Add Server"
4. Enter your server address:
   - **Local**: `localhost:25565`
   - **Remote**: `your-server-ip:25565`
5. Your username must be in the whitelist to join

## How to set up DNS

<img width="899" height="602" alt="Image" src="https://github.com/user-attachments/assets/ba6efbc0-5f44-4579-948a-06793859c847" />
