# REST API Testing & Automation Portfolio

An end-to-end QA case study combining test design, automated Postman assertions, Newman reporting, and continuous execution with GitHub Actions.

> **16 API test scenarios • 67 automated assertions • 0 failures**
>
> Functional, negative, boundary, contract, CRUD, query, relationship, header, performance, and response-validation testing using Postman and Newman.

## Objective

Demonstrate a client-reviewable API testing workflow: understand risk, document meaningful scenarios, automate regression checks, report evidence, and distinguish genuine defects from test-system limitations.

## System under test

[JSONPlaceholder](https://jsonplaceholder.typicode.com/) is a public fake REST API containing posts, comments, albums, photos, todos, and users. It supports testing resources, queries, relationships, contracts, and simulated writes without credentials or private data.

## Test coverage

| Category | Coverage |
|---|---|
| Functional | Retrieve, create, replace, partially update, and delete resources |
| Negative and boundary | Missing resources, oversized IDs, and non-numeric identifiers |
| Query behavior | User filtering, pagination limits, and total-count headers |
| Relationships | Post comments, user albums, and album photos |
| Contract validation | Required fields, nested objects, data types, email format, and HTTPS URLs |
| Response validation | Status codes, JSON content type, payload values, and empty error bodies |
| Performance | Shared response-time threshold below 2,000 ms |

## Test strategy and scope

The collection covers positive retrieval, missing and malformed identifiers, filtering, pagination, nested resources, data types, headers, response time, and simulated `POST`, `PUT`, `PATCH`, and `DELETE` operations. Authentication, authorization, persistence, concurrency, and load testing are out of scope because the system does not expose those capabilities.

The suite contains **16 request-level cases and 67 automated assertions**. Each request inherits JSON content-type and two-second response-time checks. See [the test cases](test-cases/api-test-cases.md) for the rationale and expected results.

## Tools

- Postman collection format 2.1
- Newman and the `htmlextra` HTML reporter
- GitHub Actions for push, pull-request, and manual CI runs

## Run locally

Install Node.js 20 or newer, then run:

```bash
npx --package newman --package newman-reporter-htmlextra \
  newman run postman/collection.json \
  --environment postman/environment.json \
  --reporters cli,htmlextra \
  --reporter-htmlextra-export reports/test-report.html
```

Open `reports/test-report.html` for the generated visual report.

## Results and findings

The verified run completed all **16 requests and 67 assertions with 0 failures**. Average response time was **335 ms**, with individual responses ranging from 65 ms to 464 ms. The generated [HTML test report](reports/test-report.html) is committed as execution evidence.

Confirmed defects belong in [the findings log](bug-reports/bugs.md) only after reproduction and comparison with documented behavior. JSONPlaceholder **simulates writes**: write responses do not permanently change server data. A later `GET` not reflecting a write is expected behavior, not a defect. Its permissive fake backend is also unsuitable for demonstrating real validation and authorization failures.

## CI/CD

The workflow runs on pushes to `main`, pull requests, and manual dispatches. It uploads the HTML report for 14 days even after assertion failures, preserving evidence for investigation.

## Repository structure

```text
api-testing-portfolio/
├── postman/                 # Executable collection and environment
├── test-cases/              # Client-readable test design
├── reports/                 # Generated HTML evidence
├── bug-reports/             # Findings and defect template
└── .github/workflows/       # CI execution
```

## Portfolio evidence

Capture the Postman folders, a successful Newman terminal run, the generated HTML summary, and the successful GitHub Actions job. Screenshots should come from a real execution rather than fabricated static proof.
