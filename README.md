# Drive Tutorial Notes & TODO's

## TODO

- [ ] Set up database and data model
- [ ] Move folder open state to URL
- [ ] Add auth
- [ ] Add file uploading
- [ ] Add analytics
- [ ] Make sure sort order is consistent
- [ ] Add delete
- [ ] Real homepage + onboarding

## Note from 2-15-2025

Just finished up connecting database, next steps:

- [ ] Update schema to show files and folders
- [ ] Manually insert examples
- [ ] Render them in the UI
- [ ] Push and make sure it all works

# Project Overview

This document provides a comprehensive overview of the project, including its technology stack, setup instructions, and key concepts discussed.

## Technology Stack

- **Next.js:** A React framework for building web applications with server-side rendering and static site generation.
- **TypeScript:** A superset of JavaScript that adds static typing.
- **Tailwind CSS:** A utility-first CSS framework for rapid UI development.
- **Drizzle:** Object-Relational Mappers (ORMs) for database interactions. 
- **SingleStore:** A distributed SQL database for handling large-scale data and real-time analytics.
- **Zod:** A TypeScript-first schema declaration and validation library for runtime type checking.
- **npm:** Node package manager.
- **npx:** npm package executor.
- **GitHub Actions:** For Continuous Integration (CI).

## Key Concepts

### T3 Stack

- A modern web development stack focused on simplicity, modularity, and full-stack type safety.
- Core technologies: Next.js, tRPC, Tailwind CSS, TypeScript, Prisma/Drizzle, NextAuth.js.
- Emphasizes type safety, modularity, and rapid development.

### Modular Architecture

- A design approach that structures a system as a collection of independent modules.
- Benefits: Maintainability, reusability, testability, scalability, and improved teamwork.

### pnpm vs. npx

- **pnpm:** A package manager for managing project dependencies.
- **npx:** A package runner for executing Node.js packages.
- pnpm is used to install project dependencies, while npx is used to run packages or commands.

### GitHub Actions (CI)

- **Continuous Integration (CI):** An automated process for building, testing, and deploying code changes.
- `.github/workflows/ci.yaml` defines the CI workflow.
- The `jobs` section in `ci.yaml` defines the steps to be executed.
- The Actions tab on GitHub displays the results of the CI workflow.

### Zod

- A TypeScript-first schema declaration and validation library.
- Performs runtime data validation.
- Provides type safety and detailed error messages.
- Used to validate data from forms, APIs, and other external sources.
- Important to use Zod because Typescript types are erased at runtime.

### SingleStore

- A distributed SQL database designed for large-scale data and real-time analytics.
- Uses SQL as its query language.
- Highly scalable and optimized for performance.
- Drizzle ORM is used to interact with SingleStore database.

### `export function` vs. `export default function`

- **`export function` (Named Exports):** Allows multiple exports per file. Import using `{ name }`.
- **`export default function` (Default Export):** Allows only one default export per file. Import using `name`.

### `import type`

- Used to import TypeScript types specifically.
- Improves code readability and helps with tree-shaking.
- Avoids unintended side effects.

### `drizzle-kit push` vs `drizzle-kit generate`

- `drizzle-kit push` updates the database schema directly, but does not update the github repo.
- `drizzle-kit generate` generates migration files, which should be pushed to the github repo.

## Setup Instructions

1.  **Install pnpm (if using pnpm):**

    ```bash
    npm install -g pnpm
    ```

2.  **Verify pnpm installation:**

    ```bash
    pnpm --version
    ```

3.  **Create a new project (using npx or pnpm):**

    ```bash
    npx create-next-app@latest # or
    pnpm create-next-app@latest
    ```

4.  **Install dependencies:**

    ```bash
    npm install # or pnpm install
    ```

5.  **Configure `.env` files:**

    Copy `.env.example` files to `.env` files.

6.  **Run development server:**

    ```bash
    npm run dev # or pnpm run dev
    ```

7.  **Set up SingleStore:**

    - Create a SingleStore Database.
    - Configure connection strings in your `.env` file.
    - Use Drizzle to interact with the database.

8.  **Setup GitHub Actions:**
    - Create a `.github/workflows/ci.yaml` file.
    - Configure the CI workflow for your project.
    - Make sure to change pnpm commands to npm commands if your project uses npm.

## Example CI Configuration (`.github/workflows/ci.yaml`)

```yaml
name: CI

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v2

      - name: Install Dependencies
        run: npm install

      - name: Copy .env.example files
        shell: bash
        run: find . -type f -name ".env.example" -exec sh -c 'cp "<span class="math-inline">1" "</span>{1%.*}"' _ {} \;

      - name: Typecheck
        run: npm run typecheck

      - name: Lint
        run: npm run lint
```
