## Cursor Cloud specific instructions

### Overview

This is a React Native / Expo (SDK 52) mobile app demonstrating an Apple Intelligence-inspired immersive overlay animation. It uses `@shopify/react-native-skia`, `react-native-reanimated`, `expo-blur`, and `zustand`. Single `package.json` at root, no monorepo.

### Key commands

| Task | Command |
|------|---------|
| Install deps | `npm install` |
| Lint | `npx eslint .` (or `npx expo lint` — note first run auto-configures ESLint) |
| Test | `npx jest --passWithNoTests` (no test files exist currently) |
| Dev (web) | `npx expo start --web --port 8081` |
| Dev (native) | `npx expo run:ios` / `npx expo run:android` (requires native toolchains) |

### Caveats for Cloud agents

- **No lockfile**: The repo has no `package-lock.json`, `yarn.lock`, or `bun.lockb`. Use `npm install` to generate `node_modules`.
- **`expo lint` first-run**: On a clean checkout, `npx expo lint` will detect missing ESLint config and attempt to install `eslint` + `eslint-config-expo` using `bun`. Since `bun` is not available in the Cloud VM, install them first with `npm install --save-dev eslint@^8.57.0 eslint-config-expo@~8.0.1`, then run `npx expo lint` to generate `.eslintrc.js`. After that, `npx eslint .` works directly.
- **Web target only in Cloud**: The Skia-based overlay animations are designed for native iOS/Android. On web (`expo start --web`), the app loads and buttons are interactive, but the gradient overlay effects do not render due to Skia web compatibility limitations. This is expected.
- **No backend, no secrets, no Docker**: Purely client-side app with zero external service dependencies.
