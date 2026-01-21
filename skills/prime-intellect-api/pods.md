# Pods API

Create, manage, and monitor GPU instances.

**Required Permission:** `Instances -> Read` (or `Read and Write` for create/delete)

## Endpoints

### POST Create Pod
```
POST /api/v1/pods
```

Request body:
```json
{
  "pod": {
    "name": "My pod",
    "cloudId": "n3-H100x1",
    "gpuType": "H100_80GB",
    "socket": "PCIe",
    "gpuCount": 1,
    "image": "ubuntu_22_cuda_12",
    "dataCenterId": "CANADA-1",
    "country": "CA",
    "security": "secure_cloud",
    "diskSize": 200,
    "vcpus": 16,
    "memory": 128,
    "maxPrice": 3.00,
    "envVars": [{"key": "FOO", "value": "bar"}],
    "jupyterPassword": "secret",
    "autoRestart": false
  },
  "provider": {
    "type": "hyperstack"
  },
  "disks": ["disk_id_1"],
  "team": {
    "teamId": "team_id"
  }
}
```

Example:
```bash
curl -X POST 'https://api.primeintellect.ai/api/v1/pods/' \
  -H 'Authorization: Bearer $API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "pod": {
      "name": "My H100",
      "cloudId": "n3-H100x1",
      "gpuType": "H100_80GB",
      "socket": "PCIe",
      "gpuCount": 1,
      "image": "ubuntu_22_cuda_12",
      "dataCenterId": "CANADA-1",
      "security": "secure_cloud"
    },
    "provider": {"type": "hyperstack"}
  }'
```

### GET List Pods
```
GET /api/v1/pods
```

Query params:
- offset (default: 0)
- limit (default: 100)

Response:
```json
{
  "data": [{
    "id": "pod_id",
    "userId": "user_id",
    "name": "My pod",
    "providerType": "hyperstack",
    "gpuName": "H100_80GB",
    "gpuCount": 1,
    "socket": "PCIe",
    "priceHr": 2.69,
    "status": "ACTIVE",
    "installationStatus": "COMPLETE",
    "installationProgress": 100,
    "sshConnection": "root@135.23.125.123 -p 22",
    "ip": "135.23.125.123",
    "environmentType": "ubuntu_22_cuda_12",
    "resources": {
      "memory": "128",
      "disk": "200",
      "vcpus": "16"
    },
    "isSpot": false,
    "autoRestart": true,
    "primePortMapping": [
      {"internal": "22", "external": "22", "protocol": "TCP", "usedBy": "SSH"}
    ]
  }],
  "total_count": 1,
  "offset": 0,
  "limit": 100
}
```

### GET Pod Details
```
GET /api/v1/pods/{pod_id}
```

### GET Pod Status
```
GET /api/v1/pods/status?pod_ids=pod1&pod_ids=pod2
```

Response:
```json
{
  "podId": "pod_id",
  "providerType": "primecompute",
  "status": "ACTIVE",
  "sshConnection": "root@135.23.125.123 -p 22",
  "costPerHr": 3.52,
  "ip": "135.23.125.123",
  "installationProgress": 100
}
```

### GET Pod History
```
GET /api/v1/pods/history
```

Query params:
- limit (default: 100)
- offset (default: 0)
- sort_by: "terminatedAt" or "createdAt"
- sort_order: "asc" or "desc"

### GET Pod Logs
```
GET /api/v1/pods/{pod_id}/logs
```

### DELETE Pod
```
DELETE /api/v1/pods/{pod_id}
```

## Pod Status Values

| Status | Description |
|--------|-------------|
| PROVISIONING | Pod is being created |
| PENDING | Status is changing |
| ACTIVE | Running and accessible |
| STOPPED | Pod is stopped |
| ERROR | An error occurred |
| DELETING | Being deleted |
| TERMINATED | Deleted |
| UNKNOWN | Status unknown |

## Installation Status Values
- PENDING
- IN_PROGRESS
- COMPLETE
- FAILED

## Using Custom Templates

Set `image: "custom_template"` and provide `customTemplateId`:
```json
{
  "pod": {
    "image": "custom_template",
    "customTemplateId": "cm2szl4a20001tl3pyq7ua6o7"
  }
}
```
