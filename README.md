# Turborepo Yarn Sandbox


## Installation

```sh
yarn dlx create-turbo@latest

? Where would you like to create your Turborepo? turborepo-yarn-sandbox
? Which package manager do you want to use? yarn

>>> Creating a new Turborepo with:

Application packages
 - apps/docs
 - apps/web
Library packages
 - packages/eslint-config
 - packages/typescript-config
 - packages/ui

>>> Success! Created your Turborepo at turborepo-yarn-sandbox

To get started:
- Change to the directory: cd turborepo-yarn-sandbox
- Enable Remote Caching (recommended): yarn dlx turbo login
   - Learn more: https://turbo.build/repo/remote-cache

- Run commands with Turborepo:
   - yarn run build: Build all apps and packages
   - yarn run dev: Develop all apps and packages
   - yarn run lint: Lint all apps and packages
- Run a command twice to hit cache
```

## Add package with resolutions

```jsonc
  // package.json
  "resolutions": {
    "@mui/styled-engine": "npm:@mui/styled-engine-sc@latest"
  }
```

```sh
yarn workspace @repo/ui add @mui/material@5.8.7 @mui/styled-engine @mui/styled-engine-sc@^5.8.0 styled-components@5.3.6
```

```jsonc
  // packages/ui/package.json
  "dependencies": {
    "@mui/material": "5.8.7",
    "@mui/styled-engine": "^7.0.1",
    "@mui/styled-engine-sc": "^5.8.0",
    // ...
    "styled-components": "5.3.6"
  }
```

The installed `dependencies` are kept in the form of specific versions rather than `npm:@mui/styled-engine-sc@latest`.
Also, when installing in the form of `@mui/styled-engine@5.0.0`, the version `5.0.0` is written in `packages/ui/package.json`.
However, `5.0.0` does not exist in `yarn.lock`, and instead the `latest` version (in this case `7.0.1`) is listed, suggesting that resolutions are working.