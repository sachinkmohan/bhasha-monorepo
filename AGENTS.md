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
