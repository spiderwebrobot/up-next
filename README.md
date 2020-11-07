# Up Next

* [Prerequisites](#prerequisites)
* [Project setup](#project-setup)
* [Application setup](#application-setup)
* [Resources](#resources)

## Prerequisites

### Install or update `brew`

1. Open a terminal
2. Check if brew already installed, e.g. /usr/local/bin/brew
   ```sh
   which brew
   ```
3. If already installed, update brew...
   ```sh
   brew update && brew upgrade && brew cleanup
   ```
4. Otherwise, follow the installation instructions at https://brew.sh/

### Install `yarn` (if not already installed)

1. Check if yarn already installed, e.g. /usr/local/bin/yarn
   ```sh
   which yarn
   ```
2. Otherwise, install yarn
   ```sh
   brew install yarn
   ```

## Project setup

### Create app

1. Open a terminal
2. Create a project directory, e.g.
   ```sh
   mkdir up-next
   ```
3. Navigate into the project directory, e.g.
   ```sh
   cd up-next
   ```
4. Create a Next.js application
   ```sh
   yarn create next-app .
   ```

### Install TypeScript

1. Create TypeScript configuration file
   ```sh
   touch tsconfig.json
   ```
2. Add TypeScript packages
   ```sh
   yarn add --dev typescript @types/react @types/node
   ```
3. Populate the `tsconfig.json` file
   ```sh
   yarn dev
   ```

### Edit `tsconfig.json`

1. Add `baseUrl` to the `compilerOptions`, e.g...
   ```sh
   {
     "compilerOptions": {
       "baseUrl": "."
     }
   }
   ```
2. Add `paths` to the `compilerOptions`, e.g...
   ```sh
   {
     "compilerOptions": {
       "paths": {
         "~/*": ["./*"]
       }
     }
   }
   ```

### Install Sass

1. Add sass package
   ```sh
   yarn add --dev sass
   ```
2. Add `next.config.js`
   ```sh
   touch next.config.js
   ```
3. Edit `next.config.js`
   ```js
   const path = require('path')

   module.exports = {
     sassOptions: {
       includePaths: [path.join(__dirname, 'styles')],
     },
   }
   ```

## Application setup

## Resources

* [Absolute Imports and Module path aliases](https://nextjs.org/docs/advanced-features/module-path-aliases)
* [Built-In CSS Support](https://nextjs.org/docs/basic-features/built-in-css-support)
