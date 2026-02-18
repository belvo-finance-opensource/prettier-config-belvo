# @belvo/prettier-config-belvo

Shareable Prettier config for Belvo FE projects.

---

## Installation

1. **Install required peer dependencies**

   Run this command to check which packages and versions you need:

   ```sh
   npm info "@belvo/prettier-config-belvo@latest" peerDependencies
   ```

   The easiest way is:

   ```sh
   npx install-peerdeps --dev @belvo/prettier-config-belvo
   ```

2. **Configure Prettier**

   Create a Prettier config file that extends this package:

   ```js
   // prettier.config.js
   import belvoConfig from "@belvo/prettier-config-belvo";
   export default belvoConfig;
   ```

   Or extend and override options:

   ```js
   // prettier.config.js
   import belvoPrettierConfig from "@belvo/prettier-config-belvo";

   const config = {
     ...belvoPrettierConfig,
     // add or override options here
   };

   export default config;
   ```

   Or in `package.json`:

   ```json
   {
     "prettier": "@belvo/prettier-config-belvo"
   }
   ```

---

## Usage

This configuration provides Belvo-standard Prettier formatting for frontend projects (single quotes, no semicolons, Tailwind CSS class sorting, and more).  
You can extend or override these options in your own config as needed.

---

## Updating

- To see current peers required:
  ```sh
  npm info "@belvo/prettier-config-belvo@latest" peerDependencies
  ```

- To interactively update your dependencies:
  ```sh
  npm run check-dependencies
  ```

---

## Resources

- [Prettier Configuration](https://prettier.io/docs/en/configuration.html)
- [Prettier + ESLint](https://prettier.io/docs/en/integrating-with-linters.html)
- [prettier-plugin-tailwindcss](https://github.com/tailwindlabs/prettier-plugin-tailwindcss)
