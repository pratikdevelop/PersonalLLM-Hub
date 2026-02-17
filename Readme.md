# PersonalLLM-Hub

A simple, self-hosted, private **Personal LLM Hub** running completely offline on your machine using **Ollama** + **Open WebUI** + optional reverse proxy (Caddy for HTTPS).

Perfect for local AI chat, coding assistance, document Q&A (RAG), voice interactions, and more — no cloud APIs, no subscriptions.


## Features

- Fully local & private LLM inference with **Ollama**
- Beautiful ChatGPT-like web UI via **Open WebUI**
- Voice input (Speech-to-Text) & spoken output (Text-to-Speech)
- GPU support (NVIDIA via Docker)
- Reverse proxy with self-signed HTTPS via **Caddy** (for better browser compatibility & voice features)
- Easy model switching (e.g. qwen2.5-coder:7b, gemma3, llama3.2, etc.)
- Persistent storage for models and chat history
- One-command startup with Docker Compose

## Prerequisites

- Docker & Docker Compose installed
- (Optional but recommended) NVIDIA GPU + NVIDIA Container Toolkit for acceleration
- At least 8–16 GB RAM (more for larger models)

## Quick Start

1. Clone the repository:

   ```bash
   git clone https://github.com/pratikdevelop/PersonalLLM-Hub.git
   cd PersonalLLM-Hub
   ```

2. Start everything:

   ```bash
   docker compose -f docker-compose.prod.yml up -d
   ```

3. Access the UI:

   - Open **http://localhost:3000** (first time: create admin account)
   - For HTTPS (recommended for voice): **https://localhost** (accept self-signed cert warning)

4. Pull a model (example – do this once):

   ```bash
   docker exec -it ollama-server ollama pull qwen2.5-coder:7b
   ```

   Or pull others like `llama3.2:3b`, `gemma3`, `qwen2.5:14b`, etc. directly in the WebUI.

5. Start chatting!

   - Select model in the top dropdown
   - Use microphone icon for voice input
   - Upload documents for RAG (chat with your PDFs/notes)

## Project Structure

```
PersonalLLM-Hub/
├── docker-compose.prod.yml     # Main compose file (Ollama + Open WebUI + Caddy)
├── Caddyfile                   # Self-signed HTTPS reverse proxy config
├── package.json                # (if you have any Node.js scripts/cli tools)
└── ... (your future scripts, .env, etc.)
```

## Useful Commands

- Check running containers:

  ```bash
  docker compose ps
  ```

- Pull/update images:

  ```bash
  docker compose pull
  ```

- View logs:

  ```bash
  docker compose logs -f ollama-server
  docker compose logs -f open-webui
  ```

- Stop everything:

  ```bash
  docker compose down
  ```

## Recommended Models to Try

- `qwen2.5-coder:7b` — Excellent coding & programming assistant
- `qwen2.5:14b` — Strong general knowledge & reasoning
- `llama3.2:3b` — Very fast & lightweight
- `gemma3` — Good balanced performance

Pull them with:

```bash
docker exec -it ollama-server ollama pull <model-name>
```

## Tips & Next Steps

- **Voice not working?** → Use HTTPS (https://localhost) and allow mic in browser
- **RAG (chat with documents)** → Upload files in Workspace → Documents
- **Better TTS** → Configure local TTS (e.g. Piper/Kokoro) or use OpenAI TTS key in settings
- **Backup** → Copy volumes: `ollama-models` & `open-webui-data`

## Contributing

Feel free to open issues or PRs if you want to add features like:
- Auto-model pulling script
- Backup/restore automation
- Custom prompt templates
- Multi-user support tweaks

## License

MIT License – feel free to use, modify, and share.

Made with ❤️ in Ujjain by [decision](https://github.com/pratikdevelop)

Happy local LLM-ing! 🚀
