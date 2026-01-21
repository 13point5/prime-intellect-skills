# Evals API

Evaluation management for model benchmarking.

## Endpoints

### GET List Evaluations
```
GET /api/v1/evaluations
```

Query params:
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| team_id | string | null | Filter by team |
| environment_id | string | null | Filter by environment |
| environment_name | string | null | Filter by environment name |
| suite_id | string | null | Filter by suite |
| skip | integer | 0 | Items to skip |
| limit | integer | 50 | Max items (1-100) |

Response:
```json
{
  "evaluations": [{
    "evaluation_id": "eval_id",
    "name": "GPT-4 Benchmark",
    "status": "COMPLETED",
    "eval_type": "suite",
    "total_samples": 1000,
    "created_at": "2023-11-07T05:31:56Z",
    "updated_at": "2023-11-07T05:35:00Z",
    "user_id": "user_id",
    "team_id": "team_id",
    "environment_ids": ["env1"],
    "environment_names": ["production"],
    "avg_score": 0.85,
    "min_score": 0.72,
    "max_score": 0.95
  }],
  "total": 10,
  "skip": 0,
  "limit": 50
}
```

### POST Create Evaluation
```
POST /api/v1/evaluations
```

### GET Evaluation Details
```
GET /api/v1/evaluations/{evaluation_id}
```

### PUT Update Evaluation
```
PUT /api/v1/evaluations/{evaluation_id}
```

### DELETE Evaluation
```
DELETE /api/v1/evaluations/{evaluation_id}
```

### POST Finalize Evaluation
```
POST /api/v1/evaluations/{evaluation_id}/finalize
```

Marks evaluation as complete and calculates final scores.

## Samples

### GET Evaluation Samples
```
GET /api/v1/evaluations/{evaluation_id}/samples
```

Returns individual test samples and their results.

### POST Push Samples
```
POST /api/v1/evaluations/{evaluation_id}/samples
```

Add new samples to an evaluation.

## Evaluation Status Values

| Status | Description |
|--------|-------------|
| PENDING | Not started |
| RUNNING | In progress |
| COMPLETED | Finished |
| FAILED | Error occurred |
