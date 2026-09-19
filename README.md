# AI Chat

A standalone, single-file AI chatbot — **one `index.html`, zero dependencies, no build step**.

Chat with OpenAI, OpenRouter, Groq, Google Gemini, Mistral, or any OpenAI-compatible endpoint (including local ones like Ollama).

## The secure API key system

This app has **no backend of its own**. The only HTTP request it makes goes directly from the browser to the model provider (e.g. `api.openai.com`) over HTTPS.

How your key stays private:

| | |
|---|---|
| **Where the key lives** | Only in *your* browser's `localStorage` — or nowhere at all (session-only mode, uncheck "Remember key"). |
| **In the repo / HTML file?** | Never. The app ships with an empty key field. |
| **In the URL?** | Never. No query params, no third-party services. |
| **Sent anywhere?** | Only as an `Authorization: Bearer …` header to the model provider you configured, over TLS. |
| **If you share the app** (e.g. via GitHub Pages) | Visitors see the same empty setup screen. They cannot see, extract, or use your key — they'd have to bring their own. |

Honest caveats:

- A key stored in `localStorage` is readable by anyone with access to **that same device and browser profile** (DevTools → Application → Local Storage). Don't use a machine/browser you don't trust.
- Browsers block mixed content: from an HTTPS page (GitHub Pages) you can only call HTTPS endpoints. For a local LLM, open the file via `http://localhost` (e.g. `python3 -m http.server`).

## Use it

1. Open `index.html` in any browser (or deploy it, below).
2. Paste your API key, pick a provider/model, click **Start chatting**.
3. Manage the key, model, system prompt, temperature, streaming, and data in **Settings** (gear icon).

## Deploy to GitHub Pages

1. Push this repo (the file is already at the repo root).
2. In the repo: **Settings → Pages → Deploy from a branch** → pick `main` / root.
3. Done — no configuration, no env vars, no server.

## Features

- Streaming responses (with a Stop button), Markdown + code blocks with copy buttons
- Provider presets + custom base URL/model, temperature, system prompt
- Conversation persisted locally, "New chat", clear-all
- Strict Content-Security-Policy (no remote scripts/frames), everything inline in one file
