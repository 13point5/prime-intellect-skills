# User API

User information and team management.

## Endpoints

### GET Whoami
```
GET /api/v1/user/whoami
```

Returns current user information.

Response:
```json
{
  "data": {
    "id": "user_id",
    "name": "John Doe",
    "email": "john@example.com",
    "role": "USER",
    "slug": "johndoe",
    "image": "https://...",
    "emailVerified": true,
    "hasBetaAccess": false,
    "isBanned": false,
    "skipPrepay": false,
    "createdAt": "2023-11-07T05:31:56Z",
    "blacklist": [],
    "scope": {}
  },
  "status": "success"
}
```

### GET List My Teams
```
GET /api/v1/user/teams
```

Returns teams the user belongs to.

### PATCH Set Username Slug
```
PATCH /api/v1/user/slug
```

Update the user's username slug.

Request body:
```json
{
  "slug": "new-username"
}
```

## User Roles

| Role | Description |
|------|-------------|
| USER | Standard user |
| ADMIN | Administrator |

## Team Usage

When using team resources, include the team ID header:

```bash
curl -X GET 'https://api.primeintellect.ai/api/v1/pods/' \
  -H 'Authorization: Bearer $API_KEY' \
  -H 'X-Prime-Team-ID: your_team_id'
```

This applies to:
- Creating pods/disks under team billing
- Listing team resources
- Using team API quotas
