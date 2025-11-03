# Playwright Actions - Login Testing Project

![poster](./.github/poster.png)

> 🎭 **Educational project demonstrating continuous testing workflows with Playwright and GitHub Actions for the QA Xperience course**

[![Playwright Tests](https://github.com/rafaeltmanso/playwright-actions/actions/workflows/playwright.yml/badge.svg)](https://github.com/rafaeltmanso/playwright-actions/actions/workflows/playwright.yml)

## 📋 About the Project

This is a demonstration project that implements end-to-end automated tests for login form validation using Playwright. The project is part of the QA Xperience course and demonstrates continuous integration practices with GitHub Actions.

### 🎯 Objective

Demonstrate how to implement and execute automated tests continuously, validating login scenarios in a real web application available at [https://loginxp.vercel.app](https://loginxp.vercel.app).

## 🏗️ Project Architecture

```
playwright-actions/
├── .github/
│   └── workflows/
│       └── playwright.yml          # CI/CD Pipeline
├── e2e/
│   └── login.spec.ts              # Test specifications
├── playwright-report/             # Generated HTML reports
├── test-results/                  # Test results and artifacts
├── playwright.config.ts           # Playwright configuration
└── package.json                   # Dependencies and scripts
```

## 🧪 Test Scenarios

### ✅ Implemented Test Cases

| Scenario | Description | Validation |
|---------|-----------|-----------|
| **Required field - Username** | Login attempt without entering username | Message: "Informe o seu nome de usuário!" |
| **Required field - Password** | Login attempt without entering password | Message: "Informe a sua senha secreta!" |
| **Non-existent user** | Login with non-existent user | Message: "Oops! Credenciais inválidas :(" |
| **Incorrect password** | Login with incorrect password | Message: "Oops! Credenciais inválidas :(" |
| **Successful login** | Valid credentials (qa/xperience) | Modal: "Suas credenciais são válidas :)" |

## 🚀 Technologies Used

- **[Playwright](https://playwright.dev/)** - End-to-end testing framework
- **[TypeScript](https://www.typescriptlang.org/)** - Programming language
- **[GitHub Actions](https://github.com/features/actions)** - CI/CD pipeline
- **[Node.js](https://nodejs.org/)** - JavaScript runtime

## 📦 Installation and Setup

### Prerequisites

- Node.js 18+ installed
- Git configured

### 🔧 Installation Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/rafaeltmanso/playwright-actions.git
   cd playwright-actions
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Install Playwright browsers**
   ```bash
   npx playwright install
   ```

## 🎮 Running Tests

### Local Execution

```bash
# Run all tests (headless)
npx playwright test

# Run tests with UI
npx playwright test --ui

# Run in debug mode
npx playwright test --debug

# Run specific test file only
npx playwright test e2e/login.spec.ts
```

### View Reports

```bash
# Open HTML report from last test run
npx playwright show-report
```

## 🔄 CI/CD with GitHub Actions

The project includes an automated workflow that:

### 🚀 Execution Triggers

- Push to `main` or `master` branches
- Pull Requests to `main` or `master`
- Manual execution via GitHub Interface

### ⚙️ Pipeline Configuration

- ✅ Runs on Ubuntu Latest
- ⏱️ 60-minute timeout
- 🔄 2 retries on failure
- 👤 Sequential execution (1 worker on CI)
- 📦 Upload reports as artifacts

### 📊 Generated Artifacts

- HTML reports (available for 30 days)
- Failure screenshots
- Execution videos
- Traces for debugging

## 🧩 Code Structure

### Helper Functions

The project uses reusable helper functions following the established pattern:

```typescript
// Parameterized login function
const login = async (page: Page, user: string, pass: string) => {
  await page.goto('/')
  // Conditional filling based on empty parameters
  user ? await username.fill(user) : null
  pass ? await password.fill(pass) : null
  await page.click('css=button >> text=Entrar')
}

// Toast message validation
const toast = async (page: Page, message: string) => {
  const target = page.locator('div[role=status]')
  await expect(target).toHaveText(message)
}

// Success modal validation (SweetAlert2)
const modal = async (page: Page, message: string) => {
  const target = page.locator('.swal2-html-container')
  await expect(target).toHaveText(message)
}
```

### Selector Patterns

- **Input fields**: `[name=user]`, `[name=pass]`
- **Buttons**: `css=button >> text=Entrar`
- **Error messages**: `div[role=status]`
- **Success modals**: `.swal2-html-container` (SweetAlert2)

## 📈 Playwright Configuration

```typescript
export default defineConfig({
  testDir: './e2e',
  fullyParallel: true,                    // Local parallel execution
  retries: process.env.CI ? 2 : 0,        // 2 retries on CI
  workers: process.env.CI ? 1 : undefined, // 1 worker on CI
  reporter: 'html',                       // HTML report
  use: {
    baseURL: 'https://loginxp.vercel.app',
    trace: 'on-first-retry',              // Trace on first retry
    video: 'on',                          // Video recording
  },
  projects: [
    { name: 'chromium', use: { ...devices['Desktop Chrome'] } },
    { name: 'firefox', use: { ...devices['Desktop Firefox'] } },
    { name: 'webkit', use: { ...devices['Desktop Safari'] } },
  ],
})
```

## 🐛 Debugging and Troubleshooting

### Debug Commands

```bash
# Interactive debug mode
npx playwright test --debug

# Run with UI
npx playwright test --ui

# Generate trace for analysis
npx playwright test --trace on

# Run only failed tests
npx playwright test --last-failed
```

### Analyze Failures

1. **Check screenshots** in `test-results/`
2. **Watch videos** of the executions
3. **Analyze traces** with `npx playwright show-trace`
4. **Check HTML report** with complete details

## 📚 Resources and Useful Commands

### Updates and Maintenance

```bash
# Update Playwright to latest version
npm install @playwright/test@latest

# Run with real-time reporting
npx playwright test --reporter=dot

# Run on specific browser
npx playwright test --project=chromium

# Clear cache and previous results
npx playwright test --clean
```

### Official Documentation

- [Playwright Documentation](https://playwright.dev/docs/intro)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)


## 👨‍💻 Author

**[Fernando Papito](https://github.com/papitodev)** 

**Fork by Rafael Manso**

---

## 📄 License

This project is under the MIT license. See the [LICENSE](LICENSE) file for more details.

---

> 💡 **Tip**: This project is ideal for learning about automated testing, CI/CD, and QA best practices. Feel free to fork and experiment!

