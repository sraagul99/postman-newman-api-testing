# Postman + Newman API Testing

A portfolio-ready API testing project demonstrating request authoring, reusable environment configuration, JavaScript assertions, test-data handling, command-line execution with Newman, and CI automation with GitHub Actions.

> **API under test:** [JSONPlaceholder](https://jsonplaceholder.typicode.com), a public demo REST API. It is intended for learning and testing—not production use. JSONPlaceholder simulates writes, so POST, PUT, and DELETE responses do not persist server-side changes.

## Project goals

- Validate REST API contracts through status codes, headers, response schemas/fields, and business-relevant assertions.
- Demonstrate positive and negative test scenarios.
- Extract response data into collection variables and reuse it across requests.
- Keep configuration outside request definitions using a Postman environment.
- Run the collection locally with Newman and automatically on pushes and pull requests.
- Avoid committing API keys, personal tokens, or generated reports.

## Repository structure

```text
postman-newman-api-testing/
├── .github/workflows/api-tests.yml
├── docs/
│   ├── test-strategy.md
│   └── test-coverage.md
├── postman/
│   ├── collections/QA Practice API.postman_collection.json
│   └── environments/JSONPlaceholder QA.postman_environment.json
├── test-data/users.csv
├── reports/.gitkeep
├── .gitignore
├── package.json
└── package-lock.json
```

## Prerequisites

- Node.js 20 or later
- npm
- Optional: Postman Desktop to inspect and run the collection interactively

## Run locally

1. Clone the repository.
2. Install dependencies: `npm ci`
3. Run the collection: `npm test`
4. Run with a JUnit report: `npm run test:ci`

The JUnit XML report is written to `reports/newman-junit.xml` and is ignored by Git. No API key is required for the configured public demo API.

## Run in Postman

1. Import `postman/collections/QA Practice API.postman_collection.json`.
2. Import `postman/environments/JSONPlaceholder QA.postman_environment.json`.
3. Select **JSONPlaceholder QA** as the active environment.
4. Run the collection. Requests are grouped into user retrieval, post creation/update/deletion, and negative validation scenarios.

## Test coverage

| Area | Examples |
|---|---|
| Retrieval | List users, fetch a specific user, fetch a missing user |
| Creation | Create a post and validate the response contract |
| Update | Update a post and verify changed fields in the response |
| Deletion | Delete a post and validate the demo API response |
| Negative testing | Unknown resource and missing-resource behavior |
| Assertions | Status codes, response time, JSON content type, required fields, data types, and values |
| Data handling | Environment variables and dynamically captured IDs |
| Execution | Postman Runner, Newman CLI, GitHub Actions |

See [Test Coverage](docs/test-coverage.md) for the request-level matrix and [Test Strategy](docs/test-strategy.md) for scope and approach.

## CI/CD

GitHub Actions runs on every push and pull request targeting `main`, and can also be run manually from the **Actions** tab. The workflow installs locked dependencies, executes Newman, uploads a JUnit report even when tests fail, and marks the run failed when assertions fail.

## Quality and security practices

- Environment-specific values are stored in Postman environment files rather than hard-coded in requests.
- No API key or secret is required for this public demo API.
- Generated reports and local environment overrides are excluded by `.gitignore`.
- CI uses `npm ci` for reproducible dependency installation.
- Negative cases are included alongside happy paths.
- Demo API limitations are documented so simulated write behavior is not misrepresented as persistence.

## Known limitations

JSONPlaceholder is a mock/demo service. A successful write response proves that the request and response contract were handled as expected by the demo, but does not prove persisted data changed. For a production-style extension, point the collection at an API that supports authenticated CRUD operations and add contract checks for authorization, pagination, schema compatibility, rate limits, and state persistence.

## Author

**Raagul — QA Engineer**

This repository showcases API testing practices with Postman, Newman, JavaScript assertions, test documentation, and CI automation.
