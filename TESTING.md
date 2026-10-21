# Testing

This fork adds a test suite on top of the original [Library-DB-Express](https://github.com/jlayher/Library-DB-Express) by jlayher. The application code is unchanged; the only edits are the `test` database in `config/config.json` (in-memory SQLite, so tests never touch `library.db`) and the `test` script / `jest` block in `package.json`.

The tests were written for the SE 2226 – Software Quality Assurance and Testing course project. The full report and the SauceDemo tests are in the companion repository.

## What is included

| File | Purpose |
|------|---------|
| `books.test.js` | 48 Jest + Supertest tests against the real routes (`GET /books`, `POST /books/new`, `POST /books/:id`, `POST /books/:id/delete`, search, pagination, validation, 404) |
| `stryker.config.json` | Mutation testing of `routes/index.js` and `errorHandlers.js` |
| `jmeter/Test Plan.jmx` | JMeter load test plan (`GET /books` on `localhost:3000`) |
| `jmeter/JmeterLoadTesting.docx` | Screenshots of the 10-, 50- and 100-user runs |

## Run the tests

```bash
npm install
npm install --save-dev jest supertest @stryker-mutator/core @stryker-mutator/jest-runner
npm test                  # run the 48 tests
npx jest --coverage       # coverage report
npx stryker run           # mutation testing
```

For load testing, start the app with `npm start` (port 3000), then open `jmeter/Test Plan.jmx` in Apache JMeter.

## Results reported in the course project

- Jest: 48/48 passed, 97.39 % statement and 78.26 % branch coverage
- Stryker: 105 mutants, 60.19 % mutation score
- JMeter: 10, 50 and 100 users, 0.00 % error rate
