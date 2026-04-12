# mc-server

A Dockerized Minecraft Java Edition server using the [itzg/minecraft-server](https://github.com/itzg/docker-minecraft-server) image, with external access via [playit.gg](https://playit.gg).

## Features

- ✅ Latest Minecraft version
- ✅ Whitelist enabled for player access control
- ✅ Custom server icon
- ✅ Death counter scoreboard
- ✅ Ping scoreboard
- ✅ Normal difficulty
- ✅ Persistent data storage
- ✅ External access via playit.gg tunnel (bypasses ISP port blocking)

## Prerequisites

- [Docker](https://www.docker.com/get-started) installed
- [Docker Compose](https://docs.docker.com/compose/install/) installed
- At least 2GB of available RAM
- A [playit.gg](https://playit.gg) account

## Quick Start

1. **Clone or download this repository**
2. **Set up your playit secret key** (see [Playit Setup](#playit-setup))
3. **Start the server**
   ```bash
   docker compose up -d
   ```
4. **View logs**
   ```bash
   docker compose logs -f
   ```
5. **Stop the server**
   ```bash
   docker compose down
   ```
6. **Restart the server**
   ```bash
   docker compose restart
   ```

## Configuration

### Server Settings

The server is configured via environment variables in `compose.yaml`:

- **VERSION**: `LATEST` - Automatically uses the latest Minecraft version
- **DIFFICULTY**: `normal` - Server difficulty level
- **EULA**: `TRUE` - Accepts Minecraft EULA agreement

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

The server automatically sets up:

- **Death counter** — displays in the player list (TAB menu)
- **Ping display** — shows each player's ping in the TAB menu

## Playit Setup

This server uses [playit.gg](https://playit.gg) to expose the Minecraft server to the internet without requiring port forwarding. This is necessary because Claro (the ISP) blocks inbound ports on residential plans.

### First-time setup

1. Create an account at [playit.gg](https://playit.gg)
2. Create a tunnel:
   - **Tunnel Type**: Minecraft Java
   - **Local IP**: `127.0.0.1`
   - **Local Port**: `25565`
   - **Proxy Protocol**: None
3. Copy your agent secret key from the playit dashboard
4. Create a `.env` file in this directory:
   ```bash
   SECRET_KEY=your-secret-key-here
   ```
5. Start the containers normally with `docker compose up -d`

### Public address

Players connect using the address shown in your playit dashboard:

```
generated-name.gl.joinmc.link
```

## Data Persistence

Server data is stored in `~/minecraft_data` on your host machine. This includes:

- World files
- Player data
- Server configuration
- Plugins/mods (if added)

## Connecting to the Server

1. Open Minecraft Java Edition
2. Click "Multiplayer"
3. Click "Add Server"
4. Enter the server address: `generated-name.gl.joinmc.link`
5. Your username must be in the whitelist to join

---

### Disclaimer

I had to opt to using playit.gg, since my ISP modem is so bad that it wouldn't let me do any port-forwarding and that was driving me mad, so this other service does the job and its way easier to set it up.
