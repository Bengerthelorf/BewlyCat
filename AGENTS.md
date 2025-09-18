# Repository Guidelines

## Project Structure & Module Organization
- Core extension code lives in `src/`, with feature areas split between `background`, `contentScripts`, `inject`, `popup`, and `options`; shared logic sits in `composables`, `stores`, `utils`, and `constants`.
- Vue single-file components reside in `components/` with supporting styles in `styles/`; localized strings are under `_locales/` and extension manifests are generated from `manifest.ts`.
- UI assets are stored in `assets/`, reusable automation lives in `scripts/`, and contributor docs live in `docs/`; keep test helpers and specs inside `src/tests/`.

## Build, Test, and Development Commands
- `pnpm install` boots the workspace; re-run after dependency changes.
- `pnpm dev` serves the Chromium build with automatic reloads; `pnpm dev-firefox` mirrors this for Firefox.
- `pnpm build` produces a production Chromium bundle in `extension/`; use `pnpm build-firefox` or `pnpm build-safari` for platform-specific output.
- `pnpm build-pack` chains build, Firefox artifacts, and zip packaging; use when preparing store uploads.
- `pnpm start:chromium` and `pnpm start:firefox` launch the built extension in a disposable profile for smoke checks.

## Coding Style & Naming Conventions
- The project uses Vue 3 + TypeScript with the `@antfu/eslint-config`; run `pnpm lint` (and `pnpm lint:fix`) before pushing.
- Prettier formatting is enforced via ESLint (120 character width, double quotes); keep two-space indentation across `.ts` and `.vue` files.
- Follow `PascalCase` component filenames, `camelCase` composables/utilities, and uppercase snake case for exported constants.
- Group imports by intent and let `simple-import-sort` arrange them; avoid ad-hoc ordering.

## Testing Guidelines
- Write unit and integration specs with Vitest in `src/tests/` or next to the code as `*.spec.ts`.
- Prefer JS DOM-based tests for UI logic and mock Bilibili network calls to keep runs deterministic.
- Run `pnpm test` locally; add `--runInBand` when debugging flaky cases and ensure new features ship with coverage.

## Commit & Pull Request Guidelines
- Follow Angular-style Conventional Commits (`feat`, `fix(scope): detail`, `chore`, `docs`); review the history for tone (`fix(videoPage): …`).
- Each PR should describe the problem, the solution, and include store/build impacts plus manual test notes; attach before/after screenshots for visible UI changes.
- Link related issues, request review from maintainers, and confirm lint/tests pass in the PR checklist before merge.
