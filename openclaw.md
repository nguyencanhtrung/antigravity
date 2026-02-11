# Setup Summary

## Successfully Configured

### 1. Antigravity-Manager (Docker)
- **Status:** Running
- **Port:** 8045
- **API Key:** `<your api key>`
- **Web Password:** `<your web password>`
- **Access:** http://localhost:8045
- **API Endpoint:** http://localhost:8045/v1
- **Network:** Isolated bridge network `antigravity-network`

### 2. OpenCode
- **Config:** `<path to opencode.json>`
- **Provider:** `google` (OpenAI-compatible)
- **Base URL:** http://localhost:8045/v1
- **API Key:** `<your web password>`
- **Default Model:** `google/gemini-2.5-flash`

### 3. OpenClaw
- **Config:** `<path to opencode.json>`
- **Provider:** `antigravity` (OpenAI-compatible)
- **Base URL:** http://localhost:8045/v1
- **API Key:** `<your api key>`
- **Default Model:** `antigravity/claude-sonnet-4-5`
- **Gateway Port:** 18789
- **Gateway Password:** `dobanbiet1A!`
- **Tailscale URL:** <your tailscale url>

**Channels:**
- **Telegram:** Enabled
- **Google Chat:** Enabled
  - Webhook: <your webhook>
  - Space ID: `spaces/<AAA..>`
  - Space URL: https://chat.google.com/app/chat/<AAA..>
  - Allowed User: `<your email>`
  - Service Account: `<path to opencode.json>`


## Commands Reference

### Start/Stop Services

```bash
# Antigravity-Manager
cd <path to antigravity manager>
docker-compose up -d          # Start
docker-compose down           # Stop
docker-compose logs -f        # View logs

# OpenClaw
openclaw                      # Start
pkill -f openclaw-gateway     # Stop
ps aux | grep openclaw        # Check status

# OpenCode
opencode                      # Start
```

### Tailscale Commands

```bash
# Check Tailscale status
tailscale status

# View serve configuration
tailscale serve status

# Reset serve configuration (requires sudo)
sudo tailscale serve reset

# Configure serve for OpenClaw (requires sudo)
sudo tailscale set --operator=$USER
tailscale serve --bg --https 443 http://127.0.0.1:18789
```

### OpenClaw Device Pairing

```bash
# List all devices and pending pairing requests
openclaw devices list

# Approve a pending device pairing request
openclaw devices approve --token <your token> --url ws://localhost:18789 <REQUEST_ID>

# List all paired devices
openclaw devices list
```

## Access URLs

- **Antigravity Web UI:** http://localhost:8045
- **Antigravity API:** http://localhost:8045/v1
- **OpenClaw (Local):** http://localhost:18789
- **OpenClaw (Tailscale):** https://mars.tail18b5c7.ts.net

## Configuration Files

- Antigravity: `/home/mars/workspace/ai/antigravity/docker-compose.yml`
- OpenCode: `/home/mars/.config/opencode/opencode.json`
- OpenClaw: `/home/mars/.openclaw/openclaw.json`


**When accessing from a new browser/device:**
1. The browser will show "pairing required" message
2. Run `openclaw devices list` on the server to see the pending request
3. Approve it using the command from the "OpenClaw Device Pairing" section above
4. Refresh the browser - connection should work immediately

**Tips:**
- Each new browser/device needs to be approved once
- After approval, the device stays paired unless explicitly revoked
- You can see all paired devices with `openclaw devices list`

## Google Chat Integration

**Setup Complete!** You can now interact with OpenClaw via Google Chat.

### Troubleshooting Google Chat

If the bot doesn't respond:

1. **Check OpenClaw gateway is running:**
   ```bash
   ps aux | grep openclaw-gateway
   ```

2. **View logs for errors:**
   ```bash
   tail -f /tmp/openclaw.log | grep -i 'google\|chat\|error'
   ```

3. **Restart OpenClaw gateway:**
   ```bash
   pkill -f openclaw-gateway
   nohup openclaw > /tmp/openclaw.log 2>&1 &
   ```

4. **Verify webhook is accessible:**
   ```bash
   curl https://mars.tail18b5c7.ts.net/googlechat
   ```

5. **Check OpenClaw status:**
   ```bash
   openclaw status
   ```
   Should show "Google Chat: configured"
