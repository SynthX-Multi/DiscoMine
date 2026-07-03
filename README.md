# DiscoMine 🎮

**DiscoMine** is a **24/7 Discord-controlled AFK bot** for Minecraft servers, powered by **Mineflayer** and designed for **WispByte** hosting.

It keeps your Minecraft server awake by automatically connecting an AFK bot whenever no real players are online. When someone joins, the bot disconnects so they have the server to themselves. DiscoMine also monitors player activity, manages idle shutdowns with LazyMC-style logic, and provides live server controls directly from Discord.

---

# ✨ Features

| Feature                        | Description                                                                             |
| ------------------------------ | --------------------------------------------------------------------------------------- |
| **`/start`**                   | Wake the Minecraft server and immediately connect the AFK bot.                          |
| **`/stop`**                    | Disconnect the AFK bot and allow the server to sleep.                                   |
| **`/status`**                  | View server status, player count, uptime, and idle timer.                               |
| **Automatic player detection** | Disconnects when a real player joins and reconnects when everyone leaves.               |
| **LazyMC-style idle logic**    | Automatically sleeps the server after it's been empty for a configurable time.          |
| **Anti-AFK behavior**          | Random movements, looking around, sneaking, and arm swings help prevent AFK kicks.      |
| **Automatic reconnects**       | Uses exponential backoff and continuously retries until successful or manually stopped. |
| **Discord presence**           | Displays the current player count in the bot's status.                                  |
| **Optional status channel**    | Automatically posts server events and status updates to Discord.                        |

---

# 🚀 Setup (WispByte)

> [!TIP]
> Need a more detailed walkthrough? See **[Setup.md](Setup.md)** for a complete step-by-step guide.

## 1. Create a Discord Bot

1. Visit https://discord.com/developers/applications
2. Create a new application.
3. Open the **Bot** tab and generate a bot token.
4. Enable the following **Privileged Gateway Intents**:

   * Presence Intent
   * Server Members Intent
   * Message Content Intent
5. Invite the bot with permissions to:

   * Send Messages
   * Use Slash Commands
   * Embed Links
   * Read Message History

---

## 2. Collect Your IDs

You'll need the following values:

| Variable                         | Where to find it                                                             |
| -------------------------------- | ---------------------------------------------------------------------------- |
| `CLIENT_ID`                      | Discord Developer Portal → **General Information**                           |
| `GUILD_ID`                       | Enable Developer Mode → Right-click your Discord server → **Copy Server ID** |
| `STATUS_CHANNEL_ID` *(optional)* | Right-click a channel → **Copy Channel ID**                                  |

---

## 3. Deploy to WispByte

1. Create a new **Node.js Bot** on WispByte.
2. Upload the project files or connect your GitHub repository.
3. Add the following environment variables:

```text
DISCORD_TOKEN      = your_bot_token
CLIENT_ID          = your_client_id
GUILD_ID           = your_server_id
MC_SERVER_IP       = yourserver.example.com
MC_SERVER_PORT     = 25565
MC_USERNAME        = DiscoMineAFK
MC_AUTH            = offline
STATUS_CHANNEL_ID  = (optional)
```

4. Set the start command:

```bash
node index.js
```

5. Start the bot.

---

## 4. First Launch

On its first startup, DiscoMine automatically:

* Registers the `/start`, `/stop`, and `/status` slash commands.
* Connects the AFK bot to your Minecraft server.
* Begins monitoring player activity.
* Updates its Discord presence with live server information.

---

# 🧠 How It Works

```text
No Players Online
        │
        ▼
AFK Bot Connects
        │
        ▼
Server Stays Awake
        │
        │
Player Joins
        ▼
AFK Bot Disconnects
        │
        ▼
Player Uses Server Normally
        │
        │
Everyone Leaves
        ▼
AFK Bot Reconnects
```

DiscoMine automatically manages your server:

* When the server is empty, the AFK bot connects to keep it awake.
* As soon as a real player joins, the bot disconnects.
* After everyone leaves, the bot reconnects automatically.
* If the server remains idle long enough, LazyMC-style logic can put it to sleep.
* Use `/stop` at any time to manually disconnect the bot.

---

# ⚙️ Configuration

All configuration is handled through environment variables—no code changes required.

| Variable            | Default        | Description                             |
| ------------------- | -------------- | --------------------------------------- |
| `DISCORD_TOKEN`     | **Required**   | Discord bot token                       |
| `CLIENT_ID`         | **Required**   | Discord application client ID           |
| `GUILD_ID`          | **Required**   | Discord server ID                       |
| `MC_SERVER_IP`      | **Required**   | Minecraft server address                |
| `MC_SERVER_PORT`    | `25565`        | Minecraft server port                   |
| `MC_USERNAME`       | `DiscoMineAFK` | AFK bot username                        |
| `MC_PASSWORD`       | *(empty)*      | Leave empty for offline/cracked servers |
| `MC_AUTH`           | `offline`      | `offline` or `microsoft`                |
| `STATUS_CHANNEL_ID` | *(optional)*   | Channel for automatic status messages   |

---

# 📁 Project Structure

```text
DiscoMine/
├── index.js          # Discord bot & slash commands
├── minecraft.js      # AFK bot & server monitoring
├── config.js         # Environment configuration
├── package.json      # Project dependencies
├── .env.example      # Environment template
├── LICENSE           # GNU GPL v3
├── WISPBYTE_SETUP.md # Detailed hosting guide
└── README.md         # Project documentation
```

---

# 🏠 Running Locally

```bash
npm install

cp .env.example .env

# Edit .env with your configuration

npm start
```

---

# 📄 License

Licensed under the **GNU General Public License v3.0**.

See the **[LICENSE](LICENSE)** file for full license details.

---

**DiscoMine** • A Discord-powered AFK bot that keeps Minecraft servers online, automatically manages player activity, and provides simple server control from Discord.
