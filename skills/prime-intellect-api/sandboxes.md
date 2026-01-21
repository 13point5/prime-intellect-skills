# Sandboxes API

Lightweight container environments for code execution.

**Rate Limit:** 1000 requests per 60 seconds per IP and token.

## Endpoints

### GET List Sandboxes
```
GET /api/v1/sandbox
```

Query params:
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| team_id | string | null | Filter by team |
| status | enum | null | PENDING, PROVISIONING, RUNNING, STOPPED, ERROR, TERMINATED |
| is_active | boolean | null | Exclude terminated when true |
| labels | string[] | null | Filter by labels (must have ALL) |
| page | integer | 1 | Page number |
| per_page | integer | 50 | Items per page (1-1000) |

Response:
```json
{
  "sandboxes": [{
    "id": "sandbox_id",
    "name": "my-sandbox",
    "dockerImage": "python:3.11",
    "startCommand": "python main.py",
    "cpuCores": 4,
    "memoryGB": 8,
    "diskSizeGB": 50,
    "gpuCount": 0,
    "networkAccess": true,
    "status": "RUNNING",
    "timeoutMinutes": 60,
    "environmentVars": {"FOO": "bar"},
    "labels": ["dev", "test"],
    "createdAt": "2023-11-07T05:31:56Z",
    "startedAt": "2023-11-07T05:32:00Z"
  }],
  "total": 1,
  "page": 1,
  "per_page": 50,
  "has_next": false
}
```

### POST Create Sandbox
```
POST /api/v1/sandbox
```

Request body:
```json
{
  "name": "my-sandbox",
  "dockerImage": "python:3.11",
  "startCommand": "python main.py",
  "cpuCores": 4,
  "memoryGB": 8,
  "diskSizeGB": 50,
  "gpuCount": 0,
  "networkAccess": true,
  "timeoutMinutes": 60,
  "environmentVars": {"API_KEY": "secret"},
  "labels": ["dev"]
}
```

### GET Sandbox Details
```
GET /api/v1/sandbox/{sandbox_id}
```

### DELETE Sandbox
```
DELETE /api/v1/sandbox/{sandbox_id}
```

### DELETE Bulk Delete Sandboxes
```
DELETE /api/v1/sandbox/bulk
```

### POST Get Auth Token
```
POST /api/v1/sandbox/{sandbox_id}/auth-token
```

### GET Sandbox Logs
```
GET /api/v1/sandbox/{sandbox_id}/logs
```

## Port Management

### GET List Exposed Ports
```
GET /api/v1/sandbox/{sandbox_id}/ports
```

### GET List All Exposed Ports (all sandboxes)
```
GET /api/v1/sandbox/ports
```

### POST Expose Port
```
POST /api/v1/sandbox/{sandbox_id}/ports
```

Request body:
```json
{
  "port": 8080
}
```

### DELETE Unexpose Port
```
DELETE /api/v1/sandbox/{sandbox_id}/ports/{port}
```

## Sandbox Status Values

| Status | Description |
|--------|-------------|
| PENDING | Queued for creation |
| PROVISIONING | Being created |
| RUNNING | Active and accessible |
| STOPPED | Stopped |
| ERROR | Error occurred |
| TERMINATED | Deleted |
