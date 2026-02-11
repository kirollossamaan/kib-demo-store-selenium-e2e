# UI E2E Tests (KIB Demo Store)

End-to-end UI test suite for the KIB Shopify demo store using Selenium + TestNG.

## Description

This project provides automated end-to-end (E2E) tests for the **KIB Connect demo store** — a Shopify-based storefront. The tests run in a real browser (Chrome, Edge, or Firefox) and cover the main user flows: logging in with a password, browsing products, adding items to the cart, and completing checkout, including form validation and error handling. The suite uses the **Page Object Model** for maintainability and **TestNG** for test organization and reporting. Run the tests locally or in CI to validate the store UI before releases.

## Quick Start

1. **Clone the repository**
   ```bash
   git clone <your-repo-url>
   cd kib-connect-demo-store-4-e2e-tests
   ```
2. **Install prerequisites** — see [Prerequisites](#prerequisites) below (Java 17 and Maven). You do **not** need to install Selenium or TestNG; Maven downloads them when you run the tests.
3. **Run all tests** (from the project root):
   ```bash
   mvn test -Dsurefire.suiteXmlFiles=testng.xml
   ```
4. **View results** — open `target/surefire-reports/index.html` or `target/surefire-reports/emailable-report.html` in a browser.

## Tech Stack

- Java 17
- Selenium WebDriver
- TestNG
- Maven

## Prerequisites

- **Java 17** (Temurin recommended) — [Download](https://adoptium.net/) or install via package manager (e.g. `brew install openjdk@17` on macOS). Set `JAVA_HOME` if needed.
- **Maven 3.8+** — [Download](https://maven.apache.org/download.cgi) or install via package manager (e.g. `brew install maven` on macOS).
- **Chrome, Edge, or Firefox** — at least one installed (used by the tests).

**Verify installations** (in a terminal):

```bash
java -version   # should show version 17.x
mvn -version    # should show Maven 3.8 or higher
```

Selenium and TestNG are **not** installed separately; Maven downloads them when you run the tests.

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

This runs the TestNG suite defined in `testng.xml` (located in the project root, same folder as `pom.xml`) and generates the reports in `target/surefire-reports/`.

**Other options:**

Run a single test class:

```
mvn -Dtest=kib.tests.CheckoutPageTest test
```

### Troubleshooting

| Issue | What to do |
|-------|------------|
| `mvn: command not found` | Install Maven and add it to your PATH (see Prerequisites). |
| `JAVA_HOME` not set or wrong Java version | Install Java 17 and set `JAVA_HOME` to the JDK 17 installation directory. |
| Tests fail with browser/driver errors | Ensure Chrome, Edge, or Firefox is installed and that `browser` in `src/main/java/kib/config/config.properties` matches the browser you have. |

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
- `testng.xml` (project root) - TestNG suite definition
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
