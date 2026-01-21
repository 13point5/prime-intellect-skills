# Inference API

Language model inference for chat completions.

**Base URL:** `https://api.pinference.ai/api/v1`

## Authentication

```
Authorization: Bearer <api_key>
X-Prime-Team-ID: <team_id>  # For team accounts
```

## Endpoints

### GET List Models
```
GET /api/v1/models
```

Response:
```json
{
  "object": "list",
  "data": [
    {
      "id": "meta-llama/llama-3.1-70b-instruct",
      "object": "model",
      "owned_by": "meta",
      "created": 1693721698
    },
    {
      "id": "anthropic/claude-3-5-sonnet-20241022",
      "object": "model",
      "owned_by": "anthropic",
      "created": 1693721698
    }
  ]
}
```

### GET Model Details
```
GET /api/v1/models/{model_id}
```

Example:
```bash
curl -X GET 'https://api.pinference.ai/api/v1/models/meta-llama/llama-3.1-70b-instruct' \
  -H 'Authorization: Bearer $API_KEY'
```

### POST Chat Completions
```
POST /api/v1/chat/completions
```

Request body:
```json
{
  "model": "meta-llama/llama-3.1-70b-instruct",
  "messages": [
    {"role": "system", "content": "You are a helpful assistant."},
    {"role": "user", "content": "What is the capital of France?"}
  ],
  "max_tokens": 1000,
  "temperature": 0.7,
  "stream": false,
  "stop": ["END"]
}
```

Parameters:
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| model | string | Yes | Model ID |
| messages | array | Yes | Conversation messages |
| max_tokens | integer | No | Max tokens to generate |
| temperature | number | No | Sampling temperature (0-2) |
| stream | boolean | No | Enable streaming |
| stop | string/array | No | Stop sequences |

Response:
```json
{
  "id": "chatcmpl-123",
  "object": "chat.completion",
  "created": 1693721698,
  "model": "meta-llama/llama-3.1-70b-instruct",
  "choices": [{
    "index": 0,
    "message": {
      "role": "assistant",
      "content": "The capital of France is Paris."
    },
    "finish_reason": "stop"
  }],
  "usage": {
    "prompt_tokens": 12,
    "completion_tokens": 8,
    "total_tokens": 20
  }
}
```

## Streaming

Enable with `stream: true`. Response is Server-Sent Events:

```python
from openai import OpenAI

client = OpenAI(
    base_url="https://api.pinference.ai/api/v1",
    api_key="your_api_key"
)

stream = client.chat.completions.create(
    model="meta-llama/llama-3.1-70b-instruct",
    messages=[{"role": "user", "content": "Tell me a story"}],
    stream=True
)

for chunk in stream:
    if chunk.choices[0].delta.content:
        print(chunk.choices[0].delta.content, end="")
```

## OpenAI SDK Compatibility

The API is compatible with the OpenAI Python SDK:

```python
from openai import OpenAI

client = OpenAI(
    base_url="https://api.pinference.ai/api/v1",
    api_key="your_prime_intellect_api_key"
)

response = client.chat.completions.create(
    model="meta-llama/llama-3.1-70b-instruct",
    messages=[{"role": "user", "content": "Hello!"}]
)
```
