# API Test Strategy

## Objective
Demonstrate a repeatable API test approach that validates response contracts through Postman assertions and executes the same collection with Newman in CI.

## Scope
In scope: HTTP status and response-header validation; JSON structure and required fields; data types and values; response-time thresholds; positive retrieval and CRUD-style responses; negative scenarios; environment and collection variables; CI reporting.

Out of scope: authentication tests because this demo API does not require authentication; persistence verification because JSONPlaceholder simulates writes; load, stress, penetration, or destructive production testing.

## Test design
Assertions go beyond status codes. Negative cases cover a missing user and unknown route. Environment variables centralize the base URL, IDs, and response-time threshold. The create request captures its returned ID as an example of dynamic extraction.

## Entry criteria
- Node.js 20+ and npm are installed for local Newman runs.
- The exported environment is selected in Postman or passed to Newman.
- JSONPlaceholder is reachable.

## Exit criteria
- Newman completes all collection assertions without failures.
- The JUnit report is generated for CI runs.
- Failures are investigated and documented rather than hidden by weakening assertions.

## Test data
The environment points to JSONPlaceholder and uses public demo data. The CSV under test-data provides sample data for a future data-driven extension; the current collection does not consume it.

## Risks and limitations
JSONPlaceholder is a demo service and write operations are not persisted. Response-time thresholds may need adjustment for network conditions. Missing-resource behavior is specific to JSONPlaceholder and should be re-baselined for another API.
