# API Test Cases

**Environment:** JSONPlaceholder public API

**Base URL:** `https://jsonplaceholder.typicode.com`

**Preconditions:** API is reachable, the supplied Postman environment is selected, and no authentication is required.
**Latest execution:** 2026-08-22 — 16 requests and 67 assertions passed; 0 failures; average response time 335 ms.

| ID | Test case | Steps | Expected result | Type | Actual result | Status |
|---|---|---|---|---|---|---|
| TC-001 | Get all posts | Send `GET /posts` | `200`; JSON; 100 records; each matches the post contract | Functional / Contract | As expected | Pass |
| TC-002 | Get an existing post | Send `GET /posts/1` | `200`; ID is `1`; required values have correct types | Functional | As expected | Pass |
| TC-003 | Get a missing post | Send `GET /posts/999999` | `404`; empty JSON object | Negative / Boundary | As expected | Pass |
| TC-004 | Use a non-numeric post ID | Send `GET /posts/not-a-number` | `404`; no server error | Negative | As expected | Pass |
| TC-005 | Filter posts by owner | Send `GET /posts?userId=1` | `200`; non-empty; every `userId` is `1` | Query | As expected | Pass |
| TC-006 | Paginate posts | Send `GET /posts?_page=1&_limit=5` | `200`; five rows; total-count header is `100` | Boundary / Headers | As expected | Pass |
| TC-007 | Get comments for a post | Send `GET /posts/1/comments` | `200`; every `postId` is `1`; email syntax is valid | Relationship / Contract | As expected | Pass |
| TC-008 | Get albums for a user | Send `GET /users/1/albums` | `200`; every album belongs to user `1` | Relationship | As expected | Pass |
| TC-009 | Get photos for an album | Send `GET /albums/1/photos` | `200`; image URLs use HTTPS | Relationship / Security | As expected | Pass |
| TC-010 | Validate todo values | Send `GET /todos?userId=1` | `200`; every `completed` value is Boolean | Contract / Query | As expected | Pass |
| TC-011 | Create a valid post | Send `POST /posts` with valid JSON | `201`; numeric ID; submitted values echoed | Functional | As expected | Pass |
| TC-012 | Replace a post | Send `PUT /posts/1` with all fields | `200`; replacement values echoed | Functional | As expected | Pass |
| TC-013 | Partially update a post | Send `PATCH /posts/1` with title | `200`; title changes; existing body remains | Functional | As expected | Pass |
| TC-014 | Delete a post | Send `DELETE /posts/1` | `200`; empty JSON acknowledgement | Functional | As expected | Pass |
| TC-015 | Get nested user data | Send `GET /users/1` | `200`; address/geo and company satisfy contract | Contract | As expected | Pass |
| TC-016 | Get a missing user | Send `GET /users/999999` | `404`; empty JSON object | Negative / Boundary | As expected | Pass |

## Shared assertions

Every request must return a JSON content type and complete in less than 2,000 ms. Collection-level tests apply these checks automatically.

## Entry and exit criteria

Collection/environment JSON must be valid and the API reachable. All assertions must execute; failures are rerun once to separate transient network errors from reproducible behavior. Confirmed defects require sanitized evidence. Known JSONPlaceholder limitations are observations, not defects.
