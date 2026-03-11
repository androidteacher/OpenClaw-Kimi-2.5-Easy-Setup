# Telegram Bot Setup Guide

This guide walks you through creating a Telegram Bot and pairing your device so OpenClaw can communicate through it.

---

## Step 1: Create Your Telegram Bot

1. Open the Telegram app on your phone or desktop.

2. In the search bar, search for **@BotFather**
   *(Look for the official bot — it has a blue verification checkmark)*

3. Tap or click **START**, then send the following message:
   ```
   /newbot
   ```

4. BotFather will ask for a **display name** for your bot.
   Example: `My AI Assistant`

5. Next, BotFather will ask for a **username**. It MUST end in `bot`.
   Example: `MyAIAssistantBot`

6. BotFather will respond with your **API Token**. It looks like this:
   ```
   123456789:ABCdefGHIjklMNOpqrsTUVwxyz
   ```
   > **Keep this token secret.** Do not share it publicly or commit it to version control.

7. Open `data/openclaw.json` and find the `channels` section. Replace the placeholder with your token:

   ```json
   "telegram": {
     "botToken": "Insert_Telegram_Bot_Token"
   ```

   **Example:**
   ```json
   "botToken": "12345:abcdef"
   ```

---

## Step 2: Restart the OpenClaw Container

After saving `openclaw.json`, restart the container to apply the new token:

```bash
docker restart openclaw
```

---

## Step 3: Send a Message to Your Bot & Find Your User ID

1. Open Telegram and find your new bot by its username.
2. Send it any message (e.g., `hello`).
3. OpenClaw will register a pairing request. List pending requests to see it:

```bash
docker exec -it openclaw openclaw pairing list telegram
```

The output will include a pairing entry that contains your **Telegram User ID** — a number that identifies your account. It will look something like this:

```
Pending pairing requests:
  [1] User ID: 123456789  |  Code: ABC123  |  Device: MyPhone
```

4. Copy your **User ID** from this output.

5. Open `data/openclaw.json` and find the `groupAllowFrom` field:

   ```json
   "groupAllowFrom": [
     -INSERT_YOUR_USER_ID_HERE_FROM_TELEGRAM
   ],
   ```

   Replace the entire placeholder (including the `-` sign) with your User ID:

   ```json
   "groupAllowFrom": [
     123456789
   ],
   ```

   Save the file.

---

## Step 4: Approve the Pairing Request

Approve your device using the `CODE` from the pairing list output:

```bash
docker exec -it openclaw openclaw pairing approve telegram <CODE>
```

Replace `<CODE>` with the actual code shown in the list (e.g., `ABC123`).

Then restart once more to apply the allowlist change:

```bash
docker restart openclaw
```

---

## Done!

Your Telegram bot is now paired and your user ID is allowlisted. Any messages you send to the bot will be handled by the AI agent.

Next, add your Kimi API key — see `02_Setup_Kimi.md`.
