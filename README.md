# UI E2E Tests (KIB Demo Store)

End-to-end UI test suite for the KIB Shopify demo store using Selenium + TestNG.

## Description

This project provides automated end-to-end (E2E) tests for the **KIB Connect demo store** — a Shopify-based storefront. The tests run in a real browser (Chrome, Edge, or Firefox) and cover the main user flows: logging in with a password, browsing products, adding items to the cart, and completing checkout, including form validation and error handling. The suite uses the **Page Object Model** for maintainability and **TestNG** for test organization and reporting. Run the tests locally or in CI to validate the store UI before releases.

## Tech Stack

- Java 17
- Selenium WebDriver
- TestNG
- Maven

## Prerequisites

- Java 17 (Temurin recommended)
- Maven 3.8+
- Chrome / Edge / Firefox installed

## Configuration

Edit `src/main/java/kib/config/config.properties`:

```
browser=edge
headless=false
```

Supported values for `browser`: `chrome`, `firefox`, `edge`.

Set `headless=true` to run in the background.

## Running Tests

From the **project root directory** in a terminal, run:

```
mvn test -Dsurefire.suiteXmlFiles=testng.xml
```

This runs the TestNG suite defined in `testng.xml` and generates the reports in `target/surefire-reports/`.

**Other options:**

Run a single test class:

```
mvn -Dtest=kib.tests.CheckoutPageTest test
```

## Reports

After running `mvn test -Dsurefire.suiteXmlFiles=testng.xml` in the terminal (from the project directory), reports are generated in **`target/surefire-reports/`**.

**Important reports:**

| Report | Path |
|--------|------|
| TestNG main report | `target/surefire-reports/index.html` |
| Emailable report | `target/surefire-reports/emailable-report.html` |

Open these HTML files in a browser to view the results.

## Project Structure

- `src/main/java/kib/pageobjects` - Page Object classes
- `src/main/java/kib/abstractcomponents` - Shared UI helpers/waits
- `src/main/java/kib/config` - Test configuration
- `src/test/java/kib/testcomponents` - Base test setup/teardown
- `src/test/java/kib/tests` - Test classes
- `testng.xml` - TestNG suite definition
- `pom.xml` - Maven project definition
- **Reports** (generated after running tests) — see **Reports** section above.

## Test Coverage

Coverage includes **Login**, **Products**, **Card**, and **Checkout**. For the up-to-date list of test cases, counts, and results, run the suite and open the reports in `target/surefire-reports/` (see **Reports** above).

*The overview below is a snapshot and may change as tests are added or updated.*

| Area | Test class | Focus |
|------|------------|--------|
| **Login** | `LoginPageTest` | Valid/invalid password, product list visibility |
| **Products** | `ProductsPageTest` | Product list after login, product lookup |
| **Card** | `CardPageTest` | Buy Now visibility and checkout navigation |
| **Checkout** | `CheckoutPageTest` | Field validation, submit success, error handling |

