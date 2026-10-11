# Test Coverage Matrix

| ID | Request | Scenario | Key checks |
|---|---|---|---|
| API-001 | GET /users | Retrieve users | 200, JSON content type, response time, non-empty array, required fields and types |
| API-002 | GET /users/{userId} | Retrieve known user | 200, requested ID, name/email, address and company objects |
| API-003 | GET /users/999999 | Unknown user | JSONPlaceholder-specific response behavior; verify returned body and status against the live service |
| API-004 | POST /posts | Create demo post | 201, JSON content type, generated ID, returned fields |
| API-005 | PUT /posts/{postId} | Update demo post | 200, ID, updated title/body, userId |
| API-006 | DELETE /posts/{postId} | Delete demo post | 200 and an empty representation or empty object; no persistence claim |
| API-007 | GET /not-a-valid-resource | Unknown route | 404 and empty JSON object |

## Coverage notes
- This is functional API contract coverage, not a full security or performance test suite.
- JSONPlaceholder has simplified behavior. API-003 and API-007 encode service-specific behavior.
- Update and delete use the configured postId (default 1). The create scenario captures createdPostId but does not affect later requests.
- The collection uses the requestTimeoutMs environment variable for a response-time assertion.
