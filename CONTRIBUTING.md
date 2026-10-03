# Contributing Guidelines

Thank you for considering contributing to the Full-Stack E-Commerce Web Application. Contributions are welcome to improve features, fix bugs, enhance documentation, or refactor code.

---

## Code of Conduct

Please maintain a respectful, inclusive, and professional environment for everyone participating in this project.

---

## How to Contribute

### 1. Reporting Issues
- Before opening an issue, search the issue tracker to ensure the bug or feature request has not already been reported.
- If creating a new issue, clearly describe the bug or feature, steps to reproduce, expected versus actual behavior, and environment details (OS, Java version, Node version, browser).

### 2. Proposing Changes
1. Fork the repository on GitHub.
2. Clone your fork locally:
   ```bash
   git clone https://github.com/<your-username>/<repo-name>.git
   cd <repo-name>
   ```
3. Create a descriptive topic branch:
   ```bash
   git checkout -b feature/new-feature-name
   # or
   git checkout -b fix/bug-description
   ```
4. Implement your changes following the coding standards.
5. Verify your changes locally:
   - For Backend: ensure Spring Boot builds without errors (`./mvnw clean compile`).
   - For Frontend: ensure ESLint passes (`npm run lint`) and the build completes successfully (`npm run build`).
6. Commit your changes with clear commit messages:
   ```bash
   git commit -m "feat(api): add pagination to products endpoint"
   ```
7. Push your branch to GitHub:
   ```bash
   git push origin feature/new-feature-name
   ```
8. Submit a Pull Request targeting the `main` branch.

---

## Coding Standards

### Backend (Java / Spring Boot)
- Follow standard Java naming conventions (CamelCase for classes, camelCase for methods/variables).
- Maintain clean separation between Controller, Service, and Repository layers.
- Use Lombok annotations appropriately without excessive boilerplate.
- Keep REST endpoints idempotent and return appropriate HTTP status codes.

### Frontend (React / JavaScript)
- Keep components modular and focused on a single responsibility.
- Use meaningful variable and function names.
- Clean up resources (e.g. object URLs created with `URL.createObjectURL`) when components unmount if applicable.
- Avoid committing `console.log` statements intended solely for temporary debugging.
