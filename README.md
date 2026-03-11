# OpenClaw — Kimi Moonshot AI Agent

This project deploys **OpenClaw** as a self-hosted AI agent powered by the **Kimi K2.5** model from Moonshot AI, accessible through your personal **Telegram** bot.

Everything runs locally in a Docker container, bound exclusively to `127.0.0.1` for security. All persistent data lives in the `data/` directory on your host machine — nothing is lost when the container is updated or recreated.

---

## Quick Start

```bash
cd App_Deploy
chmod +x setup.sh update.sh
./setup.sh
```

That's it. The script pulls the OpenClaw image and starts the container. Then follow the setup guides below to configure your credentials.

---

## Setup Guides

| File | Purpose |
|---|---|
| `Setup_Telegram.md` | Create a Telegram bot and pair your device |
| `Setup_Kimi.md` | Add your Kimi Moonshot API key |
| `Sensitive_Data.md` | How your sensitive data is stored and secured |

---

## Updating

To update OpenClaw to the latest version without losing your data:

```bash
./update.sh
```

This stops the container, removes it, pulls the latest image, and restarts with the same volume mapping. Your workspace and configuration are fully preserved.

---

## Project Structure

```
App_Deploy/
├── setup.sh            # One-stop deploy script
├── update.sh           # Update to latest image, preserves data
├── README.md           # This file
├── Setup_Telegram.md   # Telegram bot creation and pairing guide
├── Setup_Kimi.md       # Kimi Moonshot API key configuration
├── Sensitive_Data.md   # Data security and access guide
└── data/               # Persistent host volume → /home/node/.openclaw in container
    └── openclaw.json   # Main configuration file
```

---

## Architecture

- **AI Model:** Kimi K2.5 via Moonshot AI API
- **Interface:** Telegram (your personal bot)
- **Container:** OpenClaw, bound to `127.0.0.1` only
- **Data persistence:** `./data` on host maps to `/home/node/.openclaw` in the container
