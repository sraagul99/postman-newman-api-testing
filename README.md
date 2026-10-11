# Postman + Newman API Testing

![CI](https://github.com/sraagul99/postman-newman-api-testing/actions/workflows/api-tests.yml/badge.svg?branch=main)
![Postman](https://img.shields.io/badge/Postman-API%20Testing-FF6C37?logo=postman&logoColor=white)
![Newman](https://img.shields.io/badge/Newman-CLI%20Automation-6C47FF)
![Node.js](https://img.shields.io/badge/Node.js-22-339933?logo=nodedotjs&logoColor=white)

A QA engineering portfolio project demonstrating functional REST API testing with **Postman**, **JavaScript assertions**, **environment variables**, **Newman**, and **GitHub Actions**.

**Application under test:** [JSONPlaceholder](https://jsonplaceholder.typicode.com/) — a public demo REST API for practice.

> **Execution integrity:** GitHub Actions results and Newman reports are the source of truth for executed tests. JSONPlaceholder simulates writes; a successful POST, PUT, or DELETE response does not prove server-side persistence.

## Project at a glance

| Item | Details |
|---|---|
| Test approach | Positive, negative, contract, data-type, header, and response-time checks |
| Toolchain | Postman, Newman, Node.js, GitHub Actions |
| API under test | JSONPlaceholder |
| Coverage | User retrieval, post CRUD-style responses, unknown-resource handling |
| Reports | CLI output and JUnit XML for CI |
| Credentials | No API key required for this public demo endpoint |

## Quality coverage

| ID | Request / workflow | Key checks |
|---|---|---|
| API-001 | List users | Status, JSON content type, response time, non-empty collection and required field types |
| API-002 | Get user by ID | Status, requested ID, name, email, address and company structure |
| API-003 | Request a missing user | Documented JSONPlaceholder missing-resource behavior |
| API-004 | Create a post | Status, content type, generated ID, and returned fields |
| API-005 | Update a post | Status, requested ID, revised fields and user ID |
| API-006 | Delete a post | Status and the demo API's empty/empty-object response representation |
| API-007 | Request an unknown route | Not-found status and response contract |

See [Test Coverage](docs/test-coverage.md) for the detailed matrix and [Test Strategy](docs/test-strategy.md) for the entry/exit criteria and known risks.

## Repository structure

```text
.
├── .github/workflows/api-tests.yml
├── docs/
│   ├── test-coverage.md
│   └── test-strategy.md
├── postman/
│   ├── collections/QA Practice API.postman_collection.json
│   └── environments/JSONPlaceholder QA.postman_environment.json
├── test-data/users.csv
├── reports/.gitkeep
├── .gitignore
├── package.json
└── README.md
```

The CSV file is prepared for a future data-driven extension; the current collection does not consume it yet.

## Getting started

### Prerequisites

- Node.js 22 (or a compatible supported LTS release)
- npm
- Network access to JSONPlaceholder

### Install dependencies

```bash
git clone https://github.com/sraagul99/postman-newman-api-testing.git
cd postman-newman-api-testing
npm install
```

### Run in Newman

```bash
# Validate exported Postman JSON, then execute the collection
npm test

# Run the CI command and produce a JUnit XML report
npm run test:ci

# Validate only the Postman exports
npm run validate:exports
```

The JUnit report is written to `reports/newman-junit.xml` and is excluded from Git.

### Run in Postman

1. Import `postman/collections/QA Practice API.postman_collection.json`.
2. Import `postman/environments/JSONPlaceholder QA.postman_environment.json`.
3. Select **JSONPlaceholder QA** as the active environment.
4. Run the collection and inspect request-level assertions.

## Reports and continuous integration

GitHub Actions runs the collection on pushes and pull requests targeting `main`, and supports manual dispatch from the **Actions** tab. The workflow validates the JSON exports, installs Newman, executes the collection, and uploads the JUnit report even when assertions fail.

A green CI run confirms only that the configured collection assertions completed against the external service at that time. Review the request-level failure and JUnit report before attributing a failure to the API or weakening an assertion.

## QA documentation

- [Test coverage matrix](docs/test-coverage.md)
- [Test strategy](docs/test-strategy.md)

## Scope and limitations

JSONPlaceholder is a mock/demo API. This project does not claim authenticated API coverage, persistence verification, security certification, schema governance, or load/performance testing. The API-003 and API-007 expectations are service-specific. Response-time assertions can be affected by network latency and shared-service behaviour.

For a production-oriented extension, reuse the collection structure against an API that supports authenticated CRUD operations and add authorization, pagination, schema compatibility, and persisted-state checks.

## Quality principles

1. Assert response contracts and business-relevant fields, not only status codes.
2. Keep environment-specific values in a Postman environment.
3. Preserve negative scenarios and investigate unexpected service behavior.
4. Report response limitations accurately.
5. Use CI results and generated reports as execution evidence.

## Author

**Raagul Sivanathan** · Quality Assurance Engineer

- LinkedIn: [https://www.linkedin.com/in/sraagul](https://www.linkedin.com/in/sraagul)
- GitHub: [https://github.com/sraagul99](https://github.com/sraagul99)

*Independent learning project. JSONPlaceholder is an external demo service; this repository is not affiliated with its maintainers.*
