# Ollama Setup Guide — Local LLM on Your Machine

## What is Ollama?

Ollama is a lightweight runtime to download, manage, and serve open-source LLMs locally. No cloud, no API keys, no monthly bills.

## System Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| RAM | 8 GB | 16–64 GB |
| Storage | 10 GB free | 50+ GB SSD |
| GPU | Not required | NVIDIA RTX 3060+ / Apple Silicon |
| OS | macOS 14+, Win 10+, modern Linux | — |

## Installation

### macOS
```bash
curl -fsSL https://ollama.com/install.sh | sh
```
Alternatively: `brew install ollama` or download from [ollama.com/download](https://ollama.com/download).

### Windows
Download the installer from [ollama.com/download](https://ollama.com/download) and run `OllamaSetup.exe`.
Or: `winget install Ollama.Ollama`

### Linux
```bash
curl -fsSL https://ollama.com/install.sh | sh
sudo systemctl enable ollama
sudo systemctl start ollama
```

### Verify
```bash
ollama --version
```

## Run Your First Model
```bash
ollama run llama3.1:8b
```

## Model Recommendations by RAM

| RAM | Model Size | Recommended Models |
|-----|-----------|-------------------|
| 8 GB | 3–8B | `llama3.2:3b`, `llama3.1:8b`, `qwen3:8b`, `gemma3:4b` |
| 16 GB | 12–14B | `qwen3:14b`, `gemma4:12b`, `deepseek-r1:14b` |
| 24–32 GB | 27–32B | `qwen3:30b`, `gemma4:26b`, `deepseek-r1:32b` |
| 64 GB+ | 70B+ | `llama3.3:70b`, `qwen3:32b` (Q8) |

## Essential Commands

| Command | Description |
|---------|-------------|
| `ollama run <model>` | Download and start interactive chat |
| `ollama pull <model>` | Download without running |
| `ollama list` | List downloaded models |
| `ollama ps` | Show running models (CPU/GPU) |
| `ollama stop <model>` | Unload from memory |
| `ollama rm <model>` | Delete a model |
| `ollama serve` | Start the HTTP server |

## Local API Server

Ollama serves an API at `http://localhost:11434` with two interfaces:

### Native API
```bash
curl http://localhost:11434/api/chat -d '{
  "model": "qwen3:14b",
  "messages": [{"role": "user", "content": "Hello!"}],
  "stream": false
}'
```

### OpenAI-Compatible Endpoint
```python
from openai import OpenAI
client = OpenAI(base_url="http://localhost:11434/v1", api_key="ollama")
response = client.chat.completions.create(
    model="qwen3:14b",
    messages=[{"role": "user", "content": "Explain quicksort in Python"}]
)
```

## Environment Configuration

| Variable | Purpose | Example |
|----------|---------|---------|
| `OLLAMA_HOST` | Bind address | `0.0.0.0` for LAN access |
| `OLLAMA_MODELS` | Model storage path | `/path/to/external/ssd` |
| `OLLAMA_KEEP_ALIVE` | Model residency | `-1` to keep loaded always |
| `OLLAMA_CONTEXT_LENGTH` | Context window | `8192` |
| `OLLAMA_FLASH_ATTENTION` | Flash attention | `1` to enable |

## Custom Models (Modelfile)
```dockerfile
FROM qwen3:14b
PARAMETER temperature 0.3
PARAMETER num_ctx 8192
SYSTEM "You are a terse senior engineer."
```
```bash
ollama create my-coder -f Modelfile
ollama run my-coder
```

## Troubleshooting

| Symptom | Fix |
|---------|-----|
| Connection refused | Start the app or run `ollama serve` |
| Model needs more memory | Pull smaller model or lower quant |
| Sluggish / stuck on CPU | Check `ollama ps`; update GPU drivers |
| Pause before every reply | Set `OLLAMA_KEEP_ALIVE=-1` |
| Garbled output | `ollama rm <model>` then pull again |
| Disk filling up | `ollama rm` unused models |
