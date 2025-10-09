# Repository Guidelines

## Project Structure & Module Organization
This Nx workspace centers on the Expo mobile app located in `apps/mobile`. Application code lives under `apps/mobile/src/app`, co-locating screens, components, and hooks beside their tests. Shared assets such as icons and splash art reside in `apps/mobile/assets`. Workspace-wide tooling (Metro, ESLint, Jest, Expo configs) is checked into the app folder and the repo root, while `tools/` hosts automation scripts like the EAS post-install helper. Reserve `libs/` and `packages/` for reusable modules once code needs to span projects; keeping cross-cutting utilities there helps Nx enforce clean dependency boundaries.

## Build, Test, and Development Commands
- `pnpm install` — synchronize workspace dependencies before any build or test.
- `pnpm exec nx run @bhasha-monorepo/mobile:start` — launch the Expo development server for iOS and Android simulators.
- `pnpm exec nx run @bhasha-monorepo/mobile:serve` — start the web-targeted Expo preview with cache clearing.
- `pnpm exec nx run @bhasha-monorepo/mobile:typecheck` — validate the TypeScript project graph without emitting JS.
- `pnpm exec nx run @bhasha-monorepo/mobile:test` — execute the Jest suite; append `--watch` locally for TDD.
- `pnpm exec nx run @bhasha-monorepo/mobile:build` — trigger the configured EAS build pipeline for release artifacts.

## Coding Style & Naming Conventions
Code is TypeScript-first; prefer `.tsx` files for React Native components and hooks. Follow Prettier defaults (two-space indent, single quotes) and run `pnpm exec prettier --write .` before committing when formatting drifts. Keep components and screens in PascalCase (`HomeScreen.tsx`), hooks prefixed with `use`, and utilities in camelCase. Enforce linting with `pnpm exec nx run @bhasha-monorepo/mobile:lint`; address module boundary warnings instead of suppressing them. Favor functional components, React hooks, and Expo/React Native primitives.

## Testing Guidelines
Jest with `jest-expo` and Testing Library drives unit and interaction tests. Co-locate specs beside their subjects using the `*.spec.tsx` suffix (`App.spec.tsx` is the pattern). Add focused tests for navigation, important state transitions, and bespoke hooks. Run `pnpm exec nx run @bhasha-monorepo/mobile:test -- --coverage` before merging significant features; no hard threshold is enforced yet, but aim to cover new surface area and regressions.

## Commit & Pull Request Guidelines
Follow the conventional commit style already in history (`feat(mobile): ...`, `fix: ...`, `chore: ...`). Scope commits to a single concern, tie issues in the summary when possible, and keep body lines wrapped at 72 characters. Pull requests should describe the user-facing change, list Nx commands executed (build, lint, test), and include screenshots or screen captures for UI updates. Request a reviewer familiar with the affected area and wait for green CI before merging.


<!-- nx configuration start-->
<!-- Leave the start & end comments to automatically receive updates. -->

# General Guidelines for working with Nx

- When running tasks (for example build, lint, test, e2e, etc.), always prefer running the task through `nx` (i.e. `nx run`, `nx run-many`, `nx affected`) instead of using the underlying tooling directly
- You have access to the Nx MCP server and its tools, use them to help the user
- When answering questions about the repository, use the `nx_workspace` tool first to gain an understanding of the workspace architecture where applicable.
- When working in individual projects, use the `nx_project_details` mcp tool to analyze and understand the specific project structure and dependencies
- For questions around nx configuration, best practices or if you're unsure, use the `nx_docs` tool to get relevant, up-to-date docs. Always use this instead of assuming things about nx configuration
- If the user needs help with an Nx configuration or project graph error, use the `nx_workspace` tool to get any errors

# CI Error Guidelines

If the user wants help with fixing an error in their CI pipeline, use the following flow:
- Retrieve the list of current CI Pipeline Executions (CIPEs) using the `nx_cloud_cipe_details` tool
- If there are any errors, use the `nx_cloud_fix_cipe_failure` tool to retrieve the logs for a specific task
- Use the task logs to see what's wrong and help the user fix their problem. Use the appropriate tools if necessary
- Make sure that the problem is fixed by running the task that you passed into the `nx_cloud_fix_cipe_failure` tool


<!-- nx configuration end-->