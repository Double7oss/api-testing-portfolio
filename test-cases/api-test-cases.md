# API Test Cases

| ID | Scenario | Method and endpoint | Expected result | Type |
|---|---|---|---|---|
| API-001 | Retrieve all posts | `GET /posts` | `200`; JSON array is not empty; every item contains `userId`, `id`, `title`, and `body` | Functional |
| API-002 | Retrieve an existing post | `GET /posts/1` | `200`; returned ID is `1`; main fields have valid types and non-empty text | Functional |
| API-003 | Create a post with valid data | `POST /posts` | `201`; response contains a numeric ID and echoes submitted values | Functional |
| API-004 | Retrieve a post that does not exist | `GET /posts/999999` | `404`; response body is an empty JSON object | Negative |
| API-005 | Validate response format | `GET /posts` | `Content-Type` contains `application/json` | Contract |
| API-006 | Validate response time | `GET /posts` | Response completes in less than 2,000 ms | Performance |

## Test data

- Base URL: `https://jsonplaceholder.typicode.com`
- Existing post ID: `1`
- Missing post ID: `999999`
- Valid create payload: title and body strings with numeric `userId`

## Entry and exit criteria

The target API must be reachable before execution. The suite passes when all requests complete and every assertion succeeds. Network failures and service rate limits should be distinguished from product defects in the final report.

