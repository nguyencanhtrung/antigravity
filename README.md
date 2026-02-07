# Antigravity Manager Setup Guide

Setup instructions for AI development tools with local proxy and API access.

## 1. Antigravity Manager (Local Proxy / API)

Run the Antigravity Manager to start a local proxy server on `http://localhost:8045/v1`.

## 2. Opencode Setup

Configure Opencode by editing `~/.config/opencode/opencode.json`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "google": {
      "npm": "@ai-sdk/openai-compatible",
      "models": {
        "claude-opus-4-5-thinking": { "name": "Claude Opus 4.5 (Thinking)" },
        "claude-sonnet-4-5-thinking": { "name": "Claude Sonnet 4.5 (Thinking)" },
        "claude-sonnet-4-5": { "name": "Claude Sonnet 4.5" },
        "gemini-3-pro-low": { "name": "Gemini 3 Pro Low" },
        "gemini-3-pro-high": { "name": "Gemini 3 Pro High" },
        "gemini-2.5-flash": { "name": "Gemini 2.5 Flash" },
        "gemini-2.5-flash-thinking": { "name": "Gemini 2.5 Flash (Thinking)" },
        "gemini-3-flash": { "name": "Gemini 3 Flash" },
        "gemini-3-pro-image": { "name": "Gemini 3 Pro Image" }
      },
      "options": {
        "baseURL": "http://localhost:8045/v1",
        "apiKey": "sk-774f22fd9c8c4aa4971a0a4716d96783"
      }
    }
  },
  "model": "google/gemini-2.5-flash",
  "mcp": {
    "notebooklm": {
      "type": "local",
      "command": ["notebooklm-mcp"],
      "enabled": true
    }
  }
}
```

## 3. Claude Code Setup

Use the provided configuration template for Claude Code integration.

## 4. Openclaw Setup

Configure Openclaw to use the same local proxy endpoint as Opencode.