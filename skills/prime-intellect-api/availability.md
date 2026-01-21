# Availability API

Check GPU, cluster, and disk availability and pricing.

**Required Permission:** `Availability -> Read`

## Endpoints

### GET GPU Availability
```
GET /api/v1/availability/gpus
```

Query params:
| Parameter | Type | Description |
|-----------|------|-------------|
| regions | string[] | Filter by region(s) |
| gpu_count | integer | Desired number of GPUs |
| gpu_type | string | GPU model (e.g., H100_80GB) |
| socket | string | Socket type (PCIe, SXM4, etc.) |
| security | string | secure_cloud or community_cloud |
| data_center_id | string | Specific data center |
| cloud_id | string | Provider's cloud ID |
| disks | string[] | Disk IDs to filter by location |
| page | integer | Page number (default: 1) |
| page_size | integer | Results per page (max: 100) |

Example:
```bash
curl -X GET 'https://api.primeintellect.ai/api/v1/availability/gpus?regions=united_states&gpu_count=1&gpu_type=H100_80GB' \
  -H 'Authorization: Bearer $API_KEY'
```

Response:
```json
{
  "items": [{
    "cloudId": "NVIDIA H100 PCIe",
    "gpuType": "H100_80GB",
    "socket": "PCIe",
    "provider": "runpod",
    "region": "united_states",
    "dataCenter": "US-KS-2",
    "country": "US",
    "gpuCount": 1,
    "gpuMemory": 80,
    "disk": {
      "minCount": 80,
      "defaultCount": 80,
      "maxCount": 1000,
      "pricePerUnit": 0.00014
    },
    "vcpu": { "defaultCount": 16 },
    "memory": { "defaultCount": 251 },
    "stockStatus": "Low",
    "security": "secure_cloud",
    "prices": {
      "onDemand": 2.69,
      "communityPrice": null,
      "currency": "USD"
    },
    "images": ["ubuntu_22_cuda_12", "cuda_12_1_pytorch_2_2"]
  }],
  "totalCount": 247
}
```

### GET Cluster/Multi-node Availability
```
GET /api/v1/availability/clusters
GET /api/v1/availability/multi-node
```
Same parameters as GPU availability.

### GET Disk Availability
```
GET /api/v1/availability/disks
```

Query params: regions, page, page_size

### GET GPU Summary
```
GET /api/v1/availability/gpu-summary
```
Returns pricing summary grouped by GPU type.

### GET Multi-node Summary
```
GET /api/v1/availability/multi-node-summary
```
Returns cluster pricing summary.

## Cost Calculation

```
Total = GPU price + (disk_units × disk_price_per_unit)

Example:
GPU: $2.69/hr
Disk: 80 units × $0.00014 = $0.0112/hr
Total: $2.7012/hr
```

## Stock Status Values
- Available
- Low
- Out of Stock
