

# 🧱 Technology Stack & Rationale

This document outlines the technologies used in the project and the reasoning behind each choice. The stack is intentionally selected to be **simple, cost-effective, secure, and suitable for a student-driven, volunteer-based team in 2025**.

---

## Frontend & Backend

### Next.js (Frontend & Backend)

Both the **frontend and backend are built using Next.js**.

**Reasons for choosing Next.js:**

* Simpler development model compared to managing React separately with additional backend frameworks
* Built-in support for **SEO, Server-Side Rendering (SSR), and fast initial load times**
* Widely known and adopted by students and developers in **2025**
* Strong ecosystem with extensive **npm package** support
* Unified framework reduces architectural complexity and onboarding time

Using Next.js for both frontend and backend allows the team to maintain a **single, consistent technology stack**, which is critical for long-term maintainability in a volunteer project.

---

## Authentication & Security

### Firebase Authentication

Authentication is handled using **Firebase Authentication**.

**Reasons for choosing Firebase Auth:**

* Free to use within the project’s scope
* Authentication and security infrastructure is managed by **Google**
* Supports multiple authentication methods and additional security factors
* Eliminates the need to implement and maintain custom authentication logic
* Reduces risks related to **student and user data leakage**, which would be a serious concern

Firebase may also be used for limited storage or related services when appropriate.

---

## Database

### Neon (PostgreSQL)

The project uses **Neon** as the PostgreSQL database provider.

**Reasons for choosing Neon:**

* Generous **free-tier offering**
* Fully managed PostgreSQL with modern scaling capabilities
* Cost-effective for student projects
* Seamless integration with Next.js and modern JavaScript stacks

This choice aligns with the project’s goal of remaining **free-tier friendly while production-ready**.

---

## Hosting & Deployment

### Netlify

The application is hosted on **Netlify**.

**Hosting decision background:**

* Initially explored **Cloudflare Workers (Node.js runtime)**

  * Dropped due to limitations in full Node.js environment support

* Netlify was selected because:

  * Native integration with **GitHub organizations**
  * No requirement to fork repositories into personal accounts
  * Simplified CI/CD and deployment workflows

While platforms like Vercel are popular, **Netlify better fits the team structure, access control needs, and workflow constraints** of this project.

---

## Testing Strategy

### End-to-End (E2E) Testing

**Playwright** is recommended for E2E testing.

**Reasons for choosing Playwright:**

* Supports modern browser automation
* Can generate automation scripts from recorded user interactions
* Lighter and easier to configure than Selenium
* Suitable for both functional and UI testing

**Alternatives considered:**

* **Selenium** – Industry standard, but heavy and complex
* **Cypress** – Good option, but setup and configuration can be more opinionated

---

### Unit & Component Testing

* **Jest**
* **React Testing Library**

These tools are recommended for unit and component testing. Adoption may increase as team familiarity grows.

---

## CI / CD

### GitHub Actions

CI/CD is implemented using **GitHub Actions**.

**Reasons for choosing GitHub Actions:**

* Native integration with GitHub repositories
* Centralized automation within the GitHub ecosystem
* Matches the current skill level of the team
* Simplifies automation for:

  * Builds
  * Tests
  * Security checks
  * Deployments

---

## Analytics & Monitoring

### Google Analytics

The project integrates **Google Analytics** for usage and traffic analytics.

**Reasons for choosing Google Analytics:**

* Free and industry-standard analytics platform
* Provides **real-world usage data** (active users, sessions, engagement)
* Enables contributors to truthfully state analytics-related experience on their resumes
* Helps the team make **data-driven decisions** instead of assumptions

Having real production analytics allows contributors to present their experience in a **measurable and verifiable format** (e.g., *“Managed analytics for a production PWA with X monthly users”*).

---

## Security Tooling

### Dependency & Vulnerability Management

To maintain security without heavy operational overhead, the project integrates:

#### **Dependabot**

* Automated dependency updates
* Pull requests for vulnerable packages
* Native GitHub integration
* Helps keep dependencies up-to-date with minimal manual effort

#### **Snyk**

* Scans for vulnerabilities in:

  * npm dependencies
  * Application code
* Provides clear remediation guidance
* Acts as an additional security layer beyond Dependabot

These tools help ensure that **security issues are identified early**, which is critical for a publicly accessible student platform.

---

## Project Management & Collaboration

### GitHub-Native Tooling

The project relies entirely on **GitHub’s ecosystem**:

* **GitHub Issues** – Bug tracking and task management
* **GitHub Discussions** – Design discussions and community interaction
* **GitHub Projects** – Planning, roadmaps, and task boards

**Why not Slack, Jira, etc.?**

* This is a **college project with volunteer contributors**
* External tools introduce unnecessary complexity
* Such tools require high discipline and constant engagement
* GitHub provides sufficient functionality while keeping everything centralized

---

## Guiding Principles Behind Technology Choices

* Free-tier friendly
* Simple onboarding for new student contributors
* Secure by default
* Minimal operational overhead
* Fully GitHub-integrated workflow
* Practical and sustainable for a volunteer-driven academic project

---
