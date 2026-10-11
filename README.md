# Postman + Newman API Testing

![Postman](https://img.shields.io/badge/Postman-API%20Testing-FF6C37?logo=postman&logoColor=white)
![Newman](https://img.shields.io/badge/Newman-CLI%20Execution-6A5ACD)
![REST API](https://img.shields.io/badge/REST%20API-Contract%20Checks-007EC6)
![CI](https://img.shields.io/badge/CI-GitHub%20Actions-2088FF?logo=githubactions&logoColor=white)

A portfolio-focused API testing project demonstrating REST API contract validation with Postman, JavaScript assertions, environment configuration, reusable response data, command-line execution with Newman, and automated CI reporting.

> **Environment note:** The collection targets [JSONPlaceholder](https://jsonplaceholder.typicode.com), a public demo REST API for learning and testing. It is not a production service. POST, PUT, and DELETE responses simulate write operations; they do not demonstrate persisted server-side changes.

## Project at a glance

| Area | Approach |
| --- | --- |
| API under test | JSONPlaceholder public demo REST API |
| API client | Postman collection and environment |
| Command-line execution | Newman |
| Assertions | JavaScript tests for status, response headers, fields, data types, and response time |
| Test design | Positive and negative functional API scenarios |
| Test data | Environment configuration, CSV sample data, dynamically captured IDs |
| Reports | CLI output and JUnit XML |
| CI | GitHub Actions |
| Configuration | Postman environment; no API key required for this public demo |

## Test coverage

The collection covers representative API behaviours:

| Area | Scenarios |
| --- | --- |
| Retrieval | List users, retrieve a specific user, request an unknown user |
| Creation | Create a demo post and verify the response contract |
| Update | Update a demo post and validate returned fields |
| Deletion | Delete a demo post and validate the service response |
| Negative testing | Unknown resource and missing-resource behaviour |
| Assertions | Status codes, JSON content type, response time, required fields, data types, and values |
| Data handling | Environment variables and dynamically captured IDs |
| Execution | Postman Runner, Newman CLI, GitHub Actions |

This is functional API contract coverage, not a full security or performance test suite. See [Test Coverage](docs/test-coverage.md) for the request-level matrix and [Test Strategy](docs/test-strategy.md) for scope and approach.

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
├── package-lock.json
└── README.md
```

## Prerequisites

- Node.js 20 or newer
- npm
- Optional: Postman Desktop to inspect and run the collection interactively

## Setup

```bash
npm ci
npm run validate:exports
```

No API key is required for the configured public demo. The repository includes the Postman collection and the `JSONPlaceholder QA` environment. Keep personal tokens, local overrides, and generated reports out of source control.

## Run tests

```bash
npm test         # Validate exported JSON and run the collection with Newman
npm run test:ci  # Run with CLI and JUnit XML reporting
```

The JUnit XML report is written to `reports/newman-junit.xml` and is ignored by Git. Since the service is a shared demo endpoint, temporary network or service behaviour can affect live runs; review unexpected responses before changing assertions.

### Run interactively in Postman

1. Import `postman/collections/QA Practice API.postman_collection.json`.
2. Import `postman/environments/JSONPlaceholder QA.postman_environment.json`.
3. Select **JSONPlaceholder QA** as the active environment.
4. Run the collection and review the request-level assertions.

## CI and diagnostics

GitHub Actions runs on pushes and pull requests targeting `main`, and can also be started manually from the **Actions** tab. The workflow installs dependencies, validates the Postman JSON exports, executes Newman, and uploads a JUnit report as an artifact even when tests fail.

Check the Actions run for the actual assertion results and report artifact. A configured workflow does not itself prove that a test run passed.

## Quality principles

- Validate response contracts and meaningful fields, not status codes alone.
- Cover negative and missing-resource scenarios alongside successful requests.
- Keep environment-specific settings outside request definitions.
- Reuse captured data only when the scenario needs it, and keep dependencies explicit.
- Use `npm ci` for reproducible local dependency installation when a lockfile is available.
- Keep generated reports and credentials out of Git.
- Document demo API limitations so simulated write responses are not misrepresented as persistence.
- Report only results supported by actual execution output.

## Related QA portfolio projects

- [Playwright UI Automation — OrangeHRM](https://github.com/sraagul99/playwright-ui-automation)
- [Cypress BDD UI Automation — OrangeHRM](https://github.com/sraagul99/cypress-bdd-cucumber-typescript)

## Author

**Raagul Sivanathan** · Quality Assurance Engineer

- LinkedIn: [linkedin.com/in/sraagul](https://www.linkedin.com/in/sraagul)
- GitHub: [github.com/sraagul99](https://github.com/sraagul99)

*Independent learning project. JSONPlaceholder is the API under test; this repository is not affiliated with or endorsed by the service.*
