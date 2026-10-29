<h1 align="center">Gamze Ozakinci</h1>

<p align="center">
  <b>QA Engineer</b> &nbsp;·&nbsp; Manual, API &amp; Automation Testing
</p>

<h3 align="center"><a href="https://gamzeozakinci.github.io">Visit my portfolio →</a></h3>

<p align="center">
  <a href="https://www.linkedin.com/in/gamzeozakinci/"><b>💼 LinkedIn</b></a> &nbsp;·&nbsp;
  <a href="mailto:gamze.ozakinci@gmail.com"><b>✉️ Email</b></a> &nbsp;·&nbsp;
  📍 İzmir, Turkey
</p>

<img src="assets/divider.png" width="100%" alt="">

### ▸ ABOUT

ISTQB-certified QA Engineer with 2+ years in QA, covering manual, API and integration testing of B2B and B2C applications with Postman, REST API, RestAssured and SQL, plus test automation in Java with Selenium, Playwright, Cucumber, TestNG and JDBC. Experienced in bug tracking with Jira, root-cause analysis and release verification with internal and global development teams.

<img src="assets/divider.png" width="100%" alt="">

### ▸ CERTIFICATION

**ISTQB Foundation Level (CTFL)** — Turkish Testing Board · [verify certificate](https://app.diplomasafe.com/en-US/certificates/ded106d21747fca0e2ebe83f3451364a18049c786)

<img src="assets/divider.png" width="100%" alt="">

### ▸ FEATURED PROJECTS

**[GitHub REST API — REST Assured + TestNG API Automation](https://github.com/gamzeozakinci/GithubApiProject)**
API test automation for the **GitHub REST API**, written in Java 17 with REST Assured and TestNG: 96 automated tests across authentication, rate limits, users, repositories, issues, comments, labels, file contents, branches, search, gists and cross-cutting contract checks. Every test carries a test case ID and TestNG groups (smoke, regression, negative, contract), and the full test plan is in the repository. It runs against the live API, so much of the work went into test data cleanup, eventual consistency and rate limits.

**96** tests · **12** areas · **4** suites · **3** JSON schemas

<details>
<summary><b>Coverage</b></summary>

- **Authentication (5 tests):** valid, missing and invalid token; a public resource without a token; the response checked against a user JSON schema.
- **Rate limit (3 tests):** the quota endpoint, rate limit headers on normal responses, and the *used* counter increasing between two calls.
- **Users (7 tests):** existing and non-existent user, a user's public repositories, pagination with *per_page* and *page*, the Link header and a conditional request with ETag.
- **Repositories (19 tests):** create with a minimal body, private, auto_init, no name, duplicate name, no auth and invalid characters; get by owner and name, non-existent and private without auth; list and filter by visibility; update description, rename, archive, update a repository owned by someone else; delete and delete twice; a repository JSON schema check.
- **Issues (15 tests):** create with labels and an assignee, without a title and without auth; get by number; update, close and reopen; list open and closed issues and filter by label; issue numbers increment; an issue JSON schema check.
- **Issue comments (7 tests):** add, empty body, list, update, delete, the comment count on the issue, and a comment on a non-existent issue.
- **Labels (6 tests):** create, duplicate, invalid color, list, update and delete.
- **Repository contents (8 tests):** create, read, update with and without the file SHA, delete, read a non-existent file, list a directory and reject content that is not Base64.
- **Branches and commits (7 tests):** list and get branches, a non-existent branch, list commits, create a branch through a git ref, a duplicate ref and delete a branch.
- **Search (7 tests):** repositories by keyword, the language qualifier, sort by stars, a missing *q*, no results, users and pagination.
- **Gists (6 tests):** create, create without files, get, update, delete and create without auth.
- **Contract checks (6 tests):** content type, response time, error body shape, an unsupported method, a wrong API version header and an unknown route.

</details>

<details>
<summary><b>Engineering decisions</b></summary>

- **Shared building blocks:** reusable request and response specifications, a class of endpoint constants and a *RepositoryApi* helper that creates and deletes test repositories keep the tests short.
- **Token safety:** the personal access token is read from an environment variable and never stored in the repository.
- **Test data:** the issue, comment, label, content and branch tests create one repository per class and delete it afterwards; the names contain a timestamp, so runs can be repeated. The gist tests create and delete their own gists.
- **Eventual consistency:** rename and issue list tests retry up to six times, two seconds apart, because the API can lag behind its own writes.
- **Rate limits:** creating one repository per test triggered GitHub's secondary rate limit, so the tests share one repository per class and run sequentially.
- **Suites and contracts:** separate TestNG suite files for smoke, regression, negative and contract tests; JSON Schema validation (user, repository, issue) plus checks on headers and error bodies.

</details>

[Test plan (PDF)](https://github.com/gamzeozakinci/GithubApiProject/blob/master/docs/GitHub-API-Test-Plan.pdf)

`Java 17` `REST Assured` `TestNG` `Maven` `JSON Schema`

**[Gratis.com — Playwright + TestNG UI Automation](https://github.com/gamzeozakinci/GratisProject)**
End-to-end UI test automation for gratis.com, a large Turkish cosmetics e-commerce site: 30 automated tests across 7 areas, written in Java 17 with Playwright and TestNG using the Page Object Model (7 page objects). It runs against the real, live production site, so most of the engineering went into reliability: OTP-only login, look-alike elements, flaky clicks and a third-party payment widget.

**30** tests · **7** areas · **3** suites · **6** smoke tests

<details>
<summary><b>Coverage</b></summary>

- **Authentication (5):** OTP-only phone login and registration, wrong-OTP and invalid-phone validation; the tests that need a real SMS code pause for manual entry.
- **Navigation (4):** hover-driven mega menu with URL assertions, mobile hamburger accordion on an emulated 390×844 viewport, basket counter sync and logo redirect.
- **Search (3):** autocomplete suggestions contain the typed keyword, valid-keyword results page, empty-results state.
- **Filter & Sort (3):** brand filter and sort order verified through URL parameters and the listed products, plus a list re-render check.
- **Catalog (6):** product page layout, image gallery with zoom lightbox, wishlist add/remove through a modal, guest-to-login redirect from three entry points.
- **Cart (6):** add from listing and product page, quantity changes, item removal, invalid promo code, persistence after reload and clear-all, with dependent tests chained through TestNG `dependsOnMethods`.
- **Checkout (3):** store-pickup and home-delivery flows and an empty-cart guard; stops when the payment modal opens, so no card is used and no order is placed.

</details>

<details>
<summary><b>Engineering decisions</b></summary>

- **Login without automating the OTP:** the site has no password and no sandbox code, so one manual login saves the session cookies with Playwright `storageState` and logged-in tests start already authenticated (the token lasts about 15 minutes, so it is re-captured before a run).
- **Finding the right element:** the same element often appears several times on a page, so locators are scoped to one product card, cart row or dialog, or to the visible copy only.
- **Web-first assertions:** auto-retrying assertions (`hasURL`, `hasText`, `isVisible`) instead of guessing at timing.
- **Retry with verification:** genuinely flaky actions, such as a header link and the payment step, are retried up to 3 times and the test continues only once the result (URL change or modal) is confirmed.
- **Structure & suites:** fresh browser per test, config-driven test data, desktop and mobile viewports, failure screenshots and TestNG HTML reports; full regression, a 6-test tagged smoke suite and a manual auth suite for the OTP tests.

</details>

`Java 17` `Playwright` `TestNG` `Maven` `Page Object Model`

**[Mersys Portal — Selenium + Cucumber UI Automation](https://github.com/gamzeozakinci/MersysProject)**
End-to-end UI test automation for the student portal of Mersys, a school management site: 25 user stories and 44 scenarios written in plain English (Gherkin) and run with Java 17, Selenium WebDriver, Cucumber and TestNG using the Page Object Model on Chrome, Edge and Firefox. It runs against the Mersys test site, so much of the work went into stable waits, file uploads, a third-party card form and known site bugs.

**25** user stories · **44** scenarios · **3** browsers · **2** site bugs found

<details>
<summary><b>Coverage</b></summary>

- **Login (1 story):** a valid login opens the dashboard; a wrong password shows an error.
- **Navigation (2):** the logo opens the school site in a new tab; all 10 top menu links open.
- **Messaging (4):** the Messaging menu; sending a message with a receiver, text and a file and finding it in the Outbox; moving a message to Trash, restoring it and deleting it for good.
- **Finance (5):** My Finance and the payment details, the Stripe card form, paying a fee and downloading the report (both blocked by site bugs).
- **Attendance (1):** sending an attendance excuse with a PDF file.
- **Profile (2):** uploading a profile picture; changing the theme to Purple, Dark Purple and Indigo.
- **Grading (2):** the Class Grade and Reports tabs; opening the transcript PDF and saving it.
- **Assignments (5):** assignment count, a discussion with a file, quick icons, sending homework in the text editor, search, filters and sorting.
- **Calendar (3):** the weekly course plan, the tabs of a finished class, and playing a class recording.

</details>

<details>
<summary><b>Engineering decisions</b></summary>

- **Page Object Model:** ten page classes extend one `ParentPage` with shared helpers (click waits until the element is clickable, hover, typing, presence checks), so a change on the site means fixing one file.
- **One browser per test:** a driver class opens and closes the browser and a setting picks Chrome, Edge or Firefox; Chrome runs headless on Jenkins and GitHub Actions.
- **Shared steps:** every feature starts with the same Background (open the site, log in), and parameterized steps such as *User navigates to {string} page* are reused across stories.
- **Date windows:** the Outbox, Trash and Assignments pages only show a window around today, so the tests widen the date range first and keep passing as the days go by.
- **Test account:** the login of the shared test account is read from a configuration file, and settings given on the command line (for example another username and password) override it, so another account can be used without editing the project.
- **Tags, suites & CI:** `@Smoke`, `@Regression`, `@Negative`, `@Bug` and `@NoCI` tags with TestNG suites per area; GitHub Actions runs a step-definition dry run and the 24-scenario CI suite in headless Chrome, and keeps stories that change data or need the keyboard out of CI.
- **Reports & bugs:** ExtentReports with a screenshot for every failed scenario; 2 site bugs documented (a student cannot pay a fee because the site requests an admin-only page and gets a 403, and the fee detail tab has no Excel or PDF download), with the blocked scenarios tagged `@Bug` and skipped by CI.

</details>

`Java 17` `Selenium` `Cucumber` `TestNG` `Maven` `GitHub Actions`

<img src="assets/divider.png" width="100%" alt="">

### ▸ SKILLS

**Testing & API**  
`Manual` `Functional` `Smoke & Integration Testing` `End-to-End` `Regression` `SDLC / STLC` `Kanban` `Test Planning` `Test Case Design & Execution` `Bug Reporting` `Defect Life Cycle` `REST API` `Postman (pm.test scripting)` `RestAssured`

**Automation & Tools**  
`Java` `Selenium WebDriver` `Playwright` `TestNG` `Cucumber (BDD/Gherkin)` `Page Object Model` `Jira` `Git / GitHub` `Maven` `Jenkins` `CI/CD`

**Data & Languages**  
`SQL (MySQL)` `JDBC` `Turkish (Native)` `English (Advanced)`

<img src="assets/divider.png" width="100%" alt="">

<p align="center"><sub>♥ made with pixels &amp; test cases</sub></p>
