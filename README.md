# README: Nuxt Setup with ESLint, Tailwind, and Plugins

This README provides guidance on setting up a Nuxt project with ESLint, TailwindCSS, and additional plugins. Follow the steps below to properly configure the necessary modules and plugins.

## Prerequisites

Before proceeding, ensure that you have the following installed:

-   Node.js (v14 or above)
-   npm or yarn as the package manager
-   Nuxt.js framework

## Installed Plugins and Modules

The following plugins and modules are currently installed in this project. As the project evolves, more modules may be added, and version numbers should be updated.

| Plugin/Module                 | Version | Description                                                          |
| ----------------------------- | ------- | -------------------------------------------------------------------- |
| `Nuxt`                        | ^3.13   | Vue.js framework                                                     |
| `@nuxtjs/eslint-module`       | ^4.x.x  | ESLint module for Nuxt.js                                            |
| `eslint`                      | ^9.12   | Linter to enforce code standards                                     |
| `@nuxtjs/tailwindcss`         | ^x.x.x  | TailwindCSS module integration for Nuxt.js                           |
| `prettier-plugin-tailwindcss` | ^x.x.x  | Prettier plugin for TailwindCSS class sorting                        |
| `eslint-plugin-tailwindcss`   | ^x.x.x  | ESLint plugin for TailwindCSS class validation and sorting           |
| `nuxticon module`             | ^x.x.x  | Icon module for Nuxt with 200,000+ ready to use icons from Iconify.  |
| `nuxtfonts module`            | ^x.x.x  | Plug-and-play web font optimization and configuration for Nuxt apps. |
| `vueUse module`               | ^x.x.x  | Collection of essential Vue Composition                              |

To update the versions, simply run `npm outdated` and install the latest versions where necessary using `npm install <package>@latest`.

## Installation Steps

### 1. Nuxt Project Setup

Start by creating a Nuxt project. You can use the following commands:

```bash
npx nuxi init my-nuxt-project
cd my-nuxt-project
npm install # or `yarn install`
```

### 2. ESLint Module

Nuxt supports ESLint, a tool for identifying and fixing problems in JavaScript code.

#### Install @nuxt/eslint

<https://nuxt.com/modules/eslint>

Documentation:
<https://eslint.nuxt.com/packages/module>
<https://nuxt.com/blog/eslint-module> # blog on new integration of flat config

```bash
npx nuxi module add eslint
```

nuxt.config.ts is automatically updated to add eslint module.

#### Configure ESLint

In your project, create or update the `eslint.config.js` file @root of the project, with the following configuration:

```javascript
// @ts-check
import withNuxt from './.nuxt/eslint.config.mjs'

export default withNuxt()
// Your custom configs here
// your custom flat configs go here, for example:
// {
//   files: ['**/*.ts', '**/*.tsx'],
//   rules: {
//     'no-console': 'off' // allow console.log in TypeScript files
//   }
// },
// {
//   ...
// }
```

### 3. Add TailwindCSS to Nuxt

To add TailwindCSS to your Nuxt project, follow the official documentation: [TailwindCSS for Nuxt](https://tailwindcss.nuxt.dev/)

documentation:

<https://tailwindcss.com/docs/guides/nuxtjs#modules>
<https://tailwindcss.nuxtjs.org/getting-started/installation>

installation via nuxt module

Run:

```bash
npx nuxi module add @nuxtjs/tailwindcss
npx tailwindcss init  ## initiation of tailwind config file
```

Add the module to your `nuxt.config.ts`:

```ts
export default defineNuxtConfig({
    modules: ['@nuxtjs/tailwindcss'],
})
```

### 4. Optional Plugins

You may want to add additional plugins or modules such as `@nuxtjs/eslint-module` for automatic linting during development.

#### Install ESLint Module

```bash
npm install --save-dev @nuxtjs/eslint-module
```

Update the `nuxt.config.ts` file to include it:

```ts
export default defineNuxtConfig({
    modules: ['@nuxtjs/tailwindcss', '@nuxtjs/eslint-module'],
    eslint: {
        fix: true, // Automatically fix linting issues on save
    },
})
```

#### Prettier Tailwind Plugin

prettier-plugin-tailwindcss

<https://www.npmjs.com/package/prettier-plugin-tailwindcss/v/0.0.0-insiders.d539a72>
that automatically sorts classes based on our recommended class order.

Installation:
To get started, install prettier-plugin-tailwindcss as a dev-dependency:

```bash
npm install -D prettier prettier-plugin-tailwindcss
```

Then add the plugin to your Prettier configuration:

```javascript
// .prettierrc
{
  "plugins": ["prettier-plugin-tailwindcss"]
}
// .prettierrc
{
  "trailingComma": "es5",
  "tabWidth": 4,
  "semi": false,
  "singleQuote": true,

  "plugins": ["prettier-plugin-tailwindcss"]
}
// .prettierrc
{
  // ..
  "plugins": [
    "prettier-plugin-svelte",
    "prettier-plugin-organize-imports",
    "prettier-plugin-tailwindcss" // MUST come last
  ],
  "pluginSearchDirs": false
}
```

#### Eslint Tailwind Plugin (not yet installed)

For TailwindCSS-specific linting, we will add the `eslint-plugin-tailwindcss` package.
<https://www.npmjs.com/package/eslint-plugin-tailwindcss>

```bash
npm i -D eslint eslint-plugin-tailwindcss
```

Use eslint.config.js file to configure rules.
See also: <https://eslint.org/docs/latest/use/configure/configuration-files-new>.

```javascript
//eslint.config.js

import tailwind from 'eslint-plugin-tailwindcss'

export default [...tailwind.configs['flat/recommended']]
```

```javascript
//eslint.config.js

import tailwind from 'eslint-plugin-tailwindcss'

export default [
    ...tailwind.configs['flat/recommended'],
    {
        settings: {
            tailwindcss: {
                // These are the default values but feel free to customize
                callees: ['classnames', 'clsx', 'ctl'],
                config: 'tailwind.config.js', // returned from `loadConfig()` utility if not provided
                cssFiles: [
                    '**/*.css',
                    '!**/node_modules',
                    '!**/.*',
                    '!**/dist',
                    '!**/build',
                ],
                cssFilesRefreshRate: 5_000,
                removeDuplicates: true,
                skipClassAttribute: false,
                whitelist: [],
                tags: [], // can be set to e.g. ['tw'] for use in tw`bg-blue`
                classRegex: '^class(Name)?$', // can be modified to support custom attributes. E.g. "^tw$" for `twin.macro`
            },
        },
    },
]
```

If you would like to know about configuration, Learn more in ESLint docs

### 5. Install modules from Nuxt Devtool

-   nuxticon
-   nuxtfonts
-   vueUse

### 6. ShadcnUI

<https://www.shadcn-vue.com/docs/installation/nuxt>

```bash
  npx nuxi@latest module add shadcn-nuxt
```

Configure nuxt.config.ts

```javascript
export default defineNuxtConfig({
    modules: ['@nuxtjs/tailwindcss', 'shadcn-nuxt'],
    shadcn: {
        /**
         *Prefix for all the imported component
         */
        prefix: '',
        /**
         *Directory that the component lives in.
         * @default "./components/ui"
         */
        componentDir: './components/ui',
    },
})
```

Follow documentation to add components.

### 7. Run the Development Server

Once everything is set up, run your Nuxt project using:

```bash
npm run dev
```

## Conclusion

By following the steps above, you have successfully configured ESLint, TailwindCSS, and related plugins for your Nuxt project. This setup ensures your code is consistently formatted and compliant with the best practices while leveraging the power of TailwindCSS for styling.

For more information, visit the official documentation:

-   [Nuxt.js Documentation](https://nuxtjs.org/docs/get-started/installation)
-   [ESLint Configuration](https://eslint.org/docs/user-guide/configuring)
-   [ESlint Nuxt module](https://eslint.nuxt.com/packages/module)
-   [Nuxt ESlint blog article, new flat config](https://nuxt.com/blog/eslint-module)
-   [TailwindCSS for Nuxt](https://tailwindcss.nuxt.dev/)
