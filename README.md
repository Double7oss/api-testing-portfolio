# API Testing Portfolio

A small, runnable API testing project built with Postman, Newman, and GitHub Actions. The example suite tests the public [JSONPlaceholder](https://jsonplaceholder.typicode.com/) API and demonstrates functional checks, negative testing, response validation, and automated HTML reporting.

## Project structure

```text
api-testing-portfolio/
├── README.md
├── postman/
│   ├── collection.json
│   └── environment.json
├── test-cases/
│   └── api-test-cases.md
├── reports/
│   └── test-report.html
├── bug-reports/
│   └── bugs.md
└── .github/
    └── workflows/
        └── api-tests.yml
```

## What is covered

- Retrieve a collection of posts
- Retrieve one post and validate its fields
- Create a post and validate the submitted values
- Verify a missing resource returns `404`
- Check JSON content types and response times

## Run locally

Requirements: Node.js 20 or newer.

```bash
npx newman run postman/collection.json \
  -e postman/environment.json \
  -r cli,html \
  --reporter-html-export reports/test-report.html
```

Open `reports/test-report.html` in a browser after the run. The committed report is a lightweight placeholder and is replaced by Newman when the suite runs.

## Continuous integration

The GitHub Actions workflow runs on pushes, pull requests, and manual dispatches. It uploads the generated HTML report as a workflow artifact even when an API assertion fails.

## Notes

JSONPlaceholder simulates write operations: a `POST` request returns a created representation but does not permanently store it. This is expected behavior, not a defect.

