<h1 align="center">Gamze Ozakinci</h1>

<p align="center">
  <b>QA Engineer</b> &nbsp;·&nbsp; Manual, API &amp; Automation Testing
</p>

<p align="center">
  <a href="https://gamzeozakinci.github.io"><b>🌐 Portfolio</b></a> &nbsp;·&nbsp;
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

### ▸ SKILLS

**Testing & API**  
`Manual` `Functional` `Smoke & Integration Testing` `End-to-End` `Regression` `SDLC / STLC` `Kanban` `Test Planning` `Test Case Design & Execution` `Bug Reporting` `Defect Life Cycle` `REST API` `Postman (pm.test scripting)` `RestAssured`

**Automation & Tools**  
`Java` `Selenium WebDriver` `Playwright` `TestNG` `Cucumber (BDD/Gherkin)` `Page Object Model` `Jira` `Git / GitHub` `Maven` `Jenkins` `CI/CD`

**Data & Languages**  
`SQL (MySQL)` `JDBC` `Turkish (Native)` `English (Advanced)`

<img src="assets/divider.png" width="100%" alt="">

### ▸ FEATURED PROJECTS

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

<p align="center"><sub>♥ made with pixels &amp; test cases</sub></p>
