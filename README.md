
# Technologies Used

- **Playwright**: A versatile library tailored for browser automation with a focus on reliability.
- **TypeScript**: A statically typed superset of JavaScript.
- **npm**: The package manager for JavaScript.


# Demo site - E-commerce

The [demo website](https://ovcharski.com/shop/) is using WooCommerce - an open-source e-commerce plugin for WordPress. It is designed for small to large-sized online merchants using WordPress.

The website has few pages - Home, Shop, Login, Registration, Profile.

The products (37) are in 4 categories - Clothing (23), Decor (1), Jenkins Artwork (10), Music (2). Clothing has few subcategories - Accessories (8), Hoodies (4), Jackets (1), Shirts (4), Sweater (1), Tshirts (5).

The Registration form has 10 fields: username, first name, last name, email, password, gender, birth date, coutry, phone number. Some of the fields are required, some are optional. Different type of fields are used - text box, password, radio, date picker, dropdown, telephone box.

The payment provider is Stripe.

# Test suite

The tests in the framework cover:

- User login and registration
- Search
- Making an order
- Using Page Object Model
- GitHub Actions with HTML report
- API Testing - Playwright is not the most comprehensive tool for API testing, but it can be used to get access to the REST API of your application. ([Official Documentation - API testing](https://playwright.dev/docs/test-api-testing))

# Project Structure

```bash
playwright-e2e/
├── pages/
│   ├── BasePage.ts
│   ├── CheckoutPage.ts
│   ├── HomePage.ts
│   ├── LoginPage.ts
│   ├── ProductPage.ts
│   ├── RegisterPage.ts
├── tests/
│   ├── api/
│   ├── e2e/
│   ├── ui/
├── global-setup.js
├── playwright.config.js
└── ...
```

# Configuration
The framework can be configured through `playwright.config.ts`. Key configurations include:
- Browsers: Chromium, Firefox, WebKit
- Viewport sizes
- Test timeouts
- Parallel execution settings

# For future improvements and considerations

- Using Environment Variables - to create .env file and use library like dotenv to load the sensitive data.
- Visual Regression Testing (VRT)
- Performance testing - Playwright is not designed for performance testing, but there are various ways to do it (Navigation and Resource Timing API, Paint Timing API, Largest Contentful Paint API, Layout Instability, Long Task API). ([Blog post](https://ray.run/blog/measuring-website-performance-with-playwright-tests)). These types of tests are not included in this repo/framework.
- BDD - Playwright does not support natively BDD / Gherkin, but various integrations and plugins are available (Cucumber.js, Playwright-Cucumber, Jest-Cucumber, Playwright-BDD). 

A repo with Postman collection for API testing of the same website is available at [ovcharski/postman-wp](https://github.com/ovcharski/postman-wp). The repo is just for an idea for combination of Playwright UI and Postman API testing in a one whole package.

# Checklist

| Task                          | Status              | 
|-------------------------------|---------------------| 
| GitHub Actions                | :white_check_mark:  |
| Page Object Model             | :white_check_mark:  |
| E2E tests                      | :white_check_mark:  |
| API tests                     | :white_check_mark:  |
| Mobile ViewPorts tests        | :white_check_mark:  |
| FakerJS                       | :white_check_mark:  |
| Reuse authentication state    | :white_check_mark:  |
| Multiple browser tabs         | :white_check_mark:  |
| Data driven tests             | :white_check_mark:  |
| Accessibility - Axe-core      | :white_check_mark:  |
| Visual Comparisons            | :black_square_button: |

# Page Object Model (POM)

Page Object Model (POM) is a design pattern that creates a repository for storing all web elements. In POM, consider each web page of an application as a separate class file. Each class file will contain only corresponding web page elements. Page objects are organized under the `/pages/` directory, making the test code more readable, maintainable, and less prone to duplication.

## Benefits of POM
- **Maintainability**: Changes in the UI require updates only in the page classes.
- **Reusability**: Common operations can be reused across different tests.
- **Readability**: Tests are more readable and easier to understand.

# E2E test

The e2e tests are located in `/tests/e2e/` folder. They cover scenarios such as user authentication, navigation, and interactions with different pages.

# API test

Site API Swagger doc is located [here](https://ovcharski.com/shop/rest-api/docs/).

The API tests are located in `/tests/api/`

# Locators

Playwright comes with multiple built-in locators. To make tests resilient, Playwright recommend prioritizing user-facing attributes and explicit contracts. These are the recommended built in locators.

**page.getByRole()** to locate by explicit and implicit accessibility attributes.

**page.getByText()** to locate by text content.

**page.getByLabel()** to locate a form control by associated label's text.

**page.getByPlaceholder()** to locate an input by placeholder.

**page.getByAltText()** to locate an element, usually image, by its text alternative.

**page.getByTitle()** to locate an element by its title attribute.

**page.getByTestId()** to locate an element based on its data-testid attribute (other attributes can be configured).

# Usage

Get started by installing Playwright using npm or yarn. Alternatively you can also get started and run tests using the VS Code Extension.
```bash
npm init playwright@latest
```
```bash
yarn create playwright
```

## Running tests

```bash
npx playwright test
```

## The most common options available in the command line

Run a single test file
```bash
npx playwright test tests/todo-page.spec.ts
```

Run a set of test files
```bash
npx playwright test tests/todo-page/ tests/landing-page/
```

Run tests in headed browsers
```bash
npx playwright test --headed
```

Run all the tests against a specific project
```bash
npx playwright test --project=chromium
```

Disable parallelization
```bash
npx playwright test --workers=1
```

Choose a reporter
```bash
npx playwright test --reporter=dot
```

Run in debug mode with Playwright Inspector
```bash
npx playwright test --debug
```

Ask for help
```bash
npx playwright test --help
```

Complete set of Playwright Test options is available in the configuration file.

# How to Update Playwright version

Checking Playwright version
```bash
npx @playwright/test --version
```

Check if package needs update
```bash
npm outdated @playwright/test
```

Playwright updade can be made by running
```bash
npm i @playwright/test
```

Update to specific version
```bash
npm install @playwright/test@1.36.2
```

Usually after Playwright update, browsers need to be updated
```bash
npx playwright install
```
