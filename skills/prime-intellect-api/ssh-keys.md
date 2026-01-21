# SSH Keys API

Manage SSH keys for pod access.

**Required Permission:** `SSH Keys -> Read and Write`

## Endpoints

### GET List SSH Keys
```
GET /api/v1/ssh_keys
```

Query params:
- offset (default: 0)
- limit (default: 100)

Response:
```json
{
  "data": [{
    "id": "key_id",
    "userId": "user_id",
    "name": "my-laptop",
    "publicKey": "ssh-rsa AAAAB3...",
    "isPrimary": true,
    "isUserKey": true,
    "createdAt": "2023-11-07T05:31:56Z",
    "updatedAt": "2023-11-07T05:31:56Z"
  }],
  "total_count": 1,
  "offset": 0,
  "limit": 100
}
```

### POST Upload SSH Key
```
POST /api/v1/ssh_keys
```

Request body:
```json
{
  "name": "my-key",
  "publicKey": "ssh-rsa AAAAB3NzaC1yc2E..."
}
```

Example:
```bash
curl -X POST 'https://api.primeintellect.ai/api/v1/ssh_keys/' \
  -H 'Authorization: Bearer $API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "my-laptop",
    "publicKey": "ssh-rsa AAAAB3NzaC1yc2E... user@host"
  }'
```

### DELETE SSH Key
```
DELETE /api/v1/ssh_keys/{key_id}
```

### PATCH Set Primary Key
```
PATCH /api/v1/ssh_keys/{key_id}/primary
```

Sets the specified key as the primary key for new pods.

## Getting Your Public Key

```bash
# View existing key
cat ~/.ssh/id_rsa.pub

# Or generate a new one
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

## Important Notes

- **Upload SSH key BEFORE creating pods** - otherwise you won't have access
- The primary key is automatically used for new pods
- Multiple keys can be uploaded for different machines
