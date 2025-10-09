# @solariq/devconfig

**Unified development configuration for the Solariq ecosystem.**

Reusable ESLint, Prettier, TypeScript, VS Code, and git hook configs to keep all `@solariq/*` repos consistent.

---

## Installation

```bash
npm install --save-dev @solariq/devconfig
```

---

## Usage

- **ESLint**: reference the shared flat config.

  Create `eslint.config.js` in your repo:

  ```js
  import config from "@solariq/devconfig/eslint";
  export default config;
  ```

- **Prettier**: extend the shared options.

  Create `prettier.config.js`:

  ```js
  import config from "@solariq/devconfig/prettier";
  export default config;
  ```

- **TypeScript**: extend the strict base.

  Create `tsconfig.json`:

  ```json
  {
    "extends": "@solariq/devconfig/tsconfig",
    "include": ["src"],
    "exclude": ["node_modules", "dist"]
  }
  ```

- **VS Code settings**: optionally reference workspace defaults.

  Copy from the package export into your repo as needed:

  ```
  node_modules/@solariq/devconfig/.vscode/settings.json
  ```

- **Git hooks (Husky) + lint-staged**: plug in exports.
  1. Install and initialize Husky:

  ```bash
  npm pkg set scripts.prepare="husky install"
  npm run prepare
  ```

  2. Add `lint-staged`:

  ```bash
  npm install --save-dev lint-staged
  ```

  3. Create `.husky/pre-commit` using the shared hook:

  ```bash
  npx husky add .husky/pre-commit "node .husky/pre-commit"
  ```

  4. Add `lint-staged` config to `package.json` or `lint-staged.config.js`:

  ```js
  export default {
    "**/*.{ts,tsx,js,jsx,json,md,css,scss}": [
      "prettier --write",
      "eslint --fix",
    ],
  };
  ```

---

## Exports

This package exposes convenient entry points:

- `@solariq/devconfig/eslint` → `eslint.config.js`
- `@solariq/devconfig/prettier` → `prettier.config.js`
- `@solariq/devconfig/tsconfig` → `tsconfig.json`
- `@solariq/devconfig/vscode/settings` → optional workspace settings
- `@solariq/devconfig/lint-staged` → example lint-staged config
- `@solariq/devconfig/husky/pre-commit` → example pre-commit hook

Refer to the files under `node_modules/@solariq/devconfig/` if you need to copy-and-tweak locally.

---

## License

MIT © Andrew Orlov
