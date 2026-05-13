# Local LLM Setup

> Run a local language model for Librarian and your Obsidian LLM Wiki.

This guide shows how to set up a local OpenAI-compatible LLM endpoint with Ollama. The goal is simple: keep your notes local by default while giving Librarian a model it can call through `http://127.0.0.1:11434/v1`.

> **¿Prefieres leer en español?** → [README.es.md](./README.es.md)

## Why Local?

Local models are useful for a personal knowledge base because:

- Your notes stay on your machine or local network.
- You can experiment without sending private material to a cloud provider.
- Librarian can use the same OpenAI-compatible API shape as many hosted models.
- You keep control over model choice, latency, and cost.

Local does not mean perfect privacy in every setup. If you expose Ollama over your network, treat that endpoint like sensitive infrastructure.

## Recommended Stack

Use Ollama first. It is the simplest local runtime for this ecosystem.

Recommended default:

```env
OLLAMA_BASE_URL=http://127.0.0.1:11434/v1
OLLAMA_MODEL=qwen3.5:4b
OLLAMA_FALLBACK_MODEL=llama3.1:8b
OLLAMA_TIMEOUT_MS=600000
```

If `qwen3.5:4b` is not available in your Ollama installation, use a model you already have, such as `llama3.1:8b`, `qwen2.5:7b`, or another instruction-tuned model.

## 1. Install Ollama

Download Ollama from:

```text
https://ollama.com/download
```

Install it for your operating system and make sure the `ollama` command is available in your terminal.

Verify:

```bash
ollama --version
```

## 2. Pull A Model

Start with one model:

```bash
ollama pull qwen3.5:4b
```

If that model is not available, use:

```bash
ollama pull llama3.1:8b
```

You can list installed models with:

```bash
ollama list
```

## 3. Start Ollama

Ollama usually runs as a background app after installation. If you need to start it manually:

```bash
ollama serve
```

The default endpoint is:

```text
http://127.0.0.1:11434
```

Librarian uses the OpenAI-compatible path:

```text
http://127.0.0.1:11434/v1
```

## 4. Test The Endpoint

Check that the OpenAI-compatible API is responding:

```bash
curl http://127.0.0.1:11434/v1/models
```

You should see JSON with the models Ollama knows about.

Then test a chat completion:

```bash
curl http://127.0.0.1:11434/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen3.5:4b",
    "messages": [
      {"role": "user", "content": "Say hello in one sentence."}
    ],
    "stream": false
  }'
```

If you pulled `llama3.1:8b`, replace the model name.

## 5. Configure Librarian

Librarian lives in a separate repository:

```bash
git clone git@github.com:Agents4Life/librarian.git
cd librarian
```

Then copy the environment template:

```bash
cp .env.example .env
```

Set your local model config:

```env
OLLAMA_BASE_URL=http://127.0.0.1:11434/v1
OLLAMA_MODEL=qwen3.5:4b
OLLAMA_FALLBACK_MODEL=llama3.1:8b
OLLAMA_TIMEOUT_MS=600000
LIBRARIAN_VAULT_PATH=/path/to/your/obsidian/vault
```

Do not set a cloud API key unless you intentionally want to use a cloud provider.

## 6. Run Librarian

From the separate Librarian repo:

```bash
npm install
npm run build
npm link
librarian "pregunta sobre mi wiki"
```

Or open the TUI:

```bash
librarian
```

## Model Choice

For a personal wiki agent, prefer reliable instruction-following over raw size.

| Machine | Starting point | Notes |
|---------|----------------|-------|
| 8 GB RAM | small 3B-4B model | Good for routing and simple summaries |
| 16 GB RAM | 7B-8B model | Better quality, still practical locally |
| 32 GB+ RAM | 14B+ model | Better synthesis, slower and heavier |

If latency is painful, use a smaller model for routing and a larger model only for curation/synthesis later.

## Security Notes

- Keep `OLLAMA_BASE_URL` on `127.0.0.1` unless you know you need network access.
- Do not expose Ollama directly to the public internet.
- If you run Ollama on another machine, use a trusted private network.
- Treat your vault as private data.
- Keep cloud API keys out of committed files.

## Troubleshooting

### `curl /v1/models` fails

Make sure Ollama is running:

```bash
ollama serve
```

### Model not found

Pull the model first:

```bash
ollama pull llama3.1:8b
```

Then set `OLLAMA_MODEL=llama3.1:8b`.

### Librarian times out

Use a smaller model or increase:

```env
OLLAMA_TIMEOUT_MS=600000
```

### Remote Ollama does not work

Prefer local first. If you intentionally use a remote machine, set:

```env
OLLAMA_BASE_URL=http://YOUR_PRIVATE_IP:11434/v1
```

Only do this on a trusted private network.

## Next Step

After your local model works, continue with [Next Level with AI](../second-brain/guides/en/07-next-level-with-ai.md) and configure Librarian against your Obsidian vault.
