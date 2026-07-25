# Custom Search Engine

![E2E Tests](https://github.com/z3r0-02/Custom-search-engine/actions/workflows/cypress.yml/badge.svg)

A search interface built with vanilla HTML, CSS and JavaScript, covered end to end by a
[Cypress](https://www.cypress.io/) test suite that runs in CI on every push.

**▶ [View live demo](https://z3r0-02.github.io/Custom-search-engine/)**

## ✨ Features

- 🔍 **Search** — triggered by the search icon or the Enter key, with a loading indicator and
  validation that rejects empty or whitespace only queries.
- 🕘 **Search history** — previous queries are stored in `localStorage` and offered in a dropdown
  that filters as you type, caps at 5 suggestions, and lets you delete entries individually.
- 📄 **CSV export** — results can be downloaded as a `Title,Link,Snippet` CSV file.
- ↩️ **State handling** — results are cleared on reload but restored when navigating back to the page.

## 🛠️ Built With

- **HTML / CSS / JavaScript** 
- **[Cypress](https://www.cypress.io/)** — end-to-end test suite (27 tests)
- **[GitHub Actions](https://github.com/features/actions)** — tests run on every push and pull request
- **GitHub Pages** — hosting for the live demo

## 🧪 E2E Test Suite

27 tests covering the full behaviour of the page:

| Area | Tests | What is covered |
| --- | --- | --- |
| **Page load** | 4 | Initial heading, empty input, visible export button, empty results area |
| **Search interaction** | 4 | Search via icon and via Enter, alerts for empty and whitespace only queries |
| **Results content** | 6 | Titles, snippets and `href` values match the query, loading indicator, re-searching replaces previous results, URL encoding of multi word queries |
| **Navigation & persistence** | 3 | Results clear on reload, restore on browser back, result links point to the right target |
| **CSV export** | 2 | Alert when there is nothing to export, and a real downloaded file asserted row by row |
| **History dropdown** | 8 | Suggestions appear only after a search, filter as you type, fill and trigger a search on click, close on Escape, cap at 5, and stay open while deleting entries |

```bash
npm test        # headless run
npm run test:open   # interactive Cypress runner
```

### Testing approach

- **Page Object Model** (`cypress/pages/SearchPage.js`)
- **Custom commands** (`cypress/support/commands.js`) — `cy.search()`, `cy.expectResults()` and
  `cy.buildHistory()` keep the specs focused on behaviour rather than setup.

## 🚀 Getting Started

Requires [Node.js](https://nodejs.org/) 18, 20 or 22.

```bash
npm install
npm test
```

`npm test` is self-contained: it boots a static server on `http://localhost:8080`, waits for it,
runs the suite, and shuts the server down afterwards. To only serve the page, run `npm start`.

## 📁 Project Structure

```
index.html                  # the application (static HTML/CSS/JS)
styles.css                  # styling
cypress.config.js           # Cypress config (baseUrl: http://localhost:8080)
cypress/
  e2e/search.cy.js          # the test specs
  pages/SearchPage.js       # Page Object Model
  support/                  # custom commands + global hooks
.github/workflows/          # CI pipeline
```
