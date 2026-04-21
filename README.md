# Qwen AI Optimized API

OpenAI-compatible API wrapper for Qwen AI (chat.qwen.ai) - **Optimized Version**

## Features

- ✅ OpenAI-compatible interface
- ✅ Streaming and non-streaming responses
- ✅ Tool/function calling support
- ✅ Thinking mode support (qwen-thinking models)
- ✅ Token rotation support
- ✅ Proxy support
- ✅ **Improved error handling**
- ✅ **Better tool parsing reliability**
- ✅ **Robust JSON extraction**

## Installation

```bash
pip install -r requirements.txt
```

## Configuration

### Step 1: Obtain a Token

1. Visit https://chat.qwen.ai and log in
2. Press F12 to open browser dev tools
3. Navigate to Application → Local Storage → https://chat.qwen.ai
4. Copy the value of the `token` key

### Step 2: Create `.env` File

```bash
# Copy the example config file
cp .env.example .env
# Edit .env file and fill in your configuration
```

Edit `.env` and add your JWT token:
```
QWEN_TOKEN=your_jwt_token_here
```

### Step 3: Start the Service

```bash
python start_server.py
```

#### Startup Parameters

| Parameter | Description |
|-----------|-------------|
| `--host` | 监听地址 (默认: 0.0.0.0) |
| `--port` | 监听端口 (默认: 8000) |
| `--reload` | 开发模式自动重载 |
| `--no-proxy` | 禁用代理功能 |

#### Proxy Configuration

```bash
# Set in .env file
ENABLE_PROXY=true
PROXY_URL=http://127.0.0.1:7890

# Start service
python start_server.py
```

### Step 4: Test the API

```bash
curl -X POST http://localhost:8000/v1/chat/completions \
  -H "Authorization: Bearer <YOUR_JWT_TOKEN>" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen3.5-plus",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```

## API Endpoints

- `GET /v1/models` - List available models
- `POST /v1/chat/completions` - Chat completions
- `GET /health` - Health check
- `POST /v1/tokens/health` - Check token health

## Python Example

```python
import openai

client = openai.OpenAI(
    api_key="your-jwt-token",
    base_url="http://localhost:8000/v1"
)

response = client.chat.completions.create(
    model="qwen3.5-plus",
    messages=[{"role": "user", "content": "Hello!"}]
)
print(response.choices[0].message.content)
```

## Supported Models

- qwen3.5-plus
- qwen3.5-max
- qwen3.5-flash
- qwen3-max
- qwen3-coder
- qwen2.5-max
- And more...

## Optimizations

This version includes:
- Better error handling with detailed messages
- Improved tool parsing with multiple pattern support
- Robust JSON extraction from various formats
- Cleaner code structure with type hints
- More reliable streaming response handling

## License

MIT
