# Disks API

Network-attached storage management for persistent data across instances.

**Required Permission:** `Disks -> Read and Write`

## Endpoints

### POST Create Disk
```
POST /api/v1/disks
```

Request body:
```json
{
  "disk": {
    "size": 500,
    "name": "ml-training-data",
    "dataCenterId": "US-1",
    "country": "US",
    "cloudId": "cloud_id"
  },
  "provider": {
    "type": "hyperstack"
  },
  "team": {
    "teamId": "team_id"
  }
}
```

Example:
```bash
curl -X POST 'https://api.primeintellect.ai/api/v1/disks/' \
  -H 'Authorization: Bearer $API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "disk": {"size": 500, "name": "training-data", "dataCenterId": "US-1"},
    "provider": {"type": "hyperstack"}
  }'
```

### GET List Disks
```
GET /api/v1/disks
```

Query params:
- offset (default: 0)
- limit (default: 100)

Response:
```json
{
  "data": [{
    "id": "disk_id",
    "name": "training-data",
    "userId": "user_id",
    "providerType": "hyperstack",
    "status": "ACTIVE",
    "size": 500,
    "priceHr": 0.07,
    "stoppedPriceHr": 0.02,
    "createdAt": "2023-11-07T05:31:56Z",
    "pods": [],
    "clusters": []
  }],
  "total_count": 1,
  "offset": 0,
  "limit": 100
}
```

### GET Disk Details
```
GET /api/v1/disks/{disk_id}
```

### PATCH Update Disk
```
PATCH /api/v1/disks/{disk_id}
```

Request body:
```json
{
  "name": "updated-name"
}
```

### DELETE Disk
```
DELETE /api/v1/disks/{disk_id}
```

## Disk Status Values

| Status | Description |
|--------|-------------|
| PROVISIONING | Being created |
| PENDING | Status changing |
| ACTIVE | Ready for use |
| STOPPED | Stopped |
| ERROR | Error occurred |
| DELETING | Being deleted |
| TERMINATED | Deleted |
| UNKNOWN | Unknown |

## Attaching Disks to Pods

Include disk IDs when creating a pod:
```json
{
  "pod": { ... },
  "provider": { ... },
  "disks": ["disk_id_1", "disk_id_2"]
}
```

**Important:** Disks must be in the same data center as the pod.
