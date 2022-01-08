# Up Next

A [Next.js](https://nextjs.org/) project with [TypeScript](https://www.typescriptlang.org/) and [Sass](https://sass-lang.com/).

* [Prerequisites](#prerequisites)
* [Start a Next.js project](#start-a-nextjs-project)
* [Add TypeScript](#add-typescript)
* [Add Sass](#add-sass)
* [Organize the project files](#organize-the-project-files)
* [Run it](#run-it)
* [Resources](#resources)

## Prerequisites

### Install brew

1. Check if `brew` is already installed
   ```sh
   which brew # e.g. /usr/local/bin/brew
   ```
2. If `brew` is already installed, then consider an update...
   ```sh
   brew update && brew upgrade && brew cleanup
   ```
3. Otherwise, follow the installation instructions at https://brew.sh/

### Install yarn

1. Check if `yarn` is already installed
   ```sh
   which yarn # e.g. /usr/local/bin/yarn
   ```
2. Otherwise, install `yarn`
   ```sh
   brew install yarn
   ```

## Start a Next.js project

1. Create the project directory, e.g.
   ```sh
   mkdir moonbeam
   ```
2. Navigate into the project directory, e.g.
   ```sh
   cd moonbeam
   ```
3. Create a Next.js application
   ```sh
   yarn create next-app .
   ```

## Add TypeScript

1. Add `typescript` to the project
   ```sh
   yarn add --dev typescript @types/react @types/node
   ```
2. Generate a TypeScript configuration file
   ```sh
   touch tsconfig.json && yarn dev # enter `control + c` after `compiled successfully`
   ```
3. Edit `tsconfig.json` (add `baseUrl` and `paths` to the `compilerOptions`), e.g.
   ```sh
   {
     "compilerOptions": {
       "baseUrl": ".",
       "paths": {
         "~/*": ["./*"]
       },
       "other": "options"
     }
   }
   ```

## Add Sass and Normalize.css

1. Add `sass` and `normalize.css` to the project
   ```sh
   yarn add --dev sass && yarn add normalize.css
   ```
2. Create a Next.js configuration file
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
     // trailingSlash: true,
   }
   ```

## Organize the project files

### Housekeeping

1. Remove the `pages`, `public` and `styles` directories
   ```sh
   rm -rf pages && rm -rf public && rm -rf styles
   ```

### Public files

1. Create the `public` directory and `favicon.svg` file
   ```sh
   mkdir public && touch public/favicon.svg
   ```
2. Download the [full moon](https://upload.wikimedia.org/wikipedia/commons/e/ee/Weather_icon_-_full_moon.svg) to `public/favicon.svg`

### Application styles

1. Create the `styles` directory and files
   ```sh
   mkdir styles && touch styles/_variables.scss && touch styles/app.scss
   ```
2. Edit `styles/_variables.scss`
   ```scss

   // layout

   $container-width: 1080px;
   ```
3. Edit `styles/app.scss`
   ```scss
   @use "/styles/variables" as var;
   @import "normalize.css"; // TODO: figure out how to `@use` normalize.css   

   // utility styles

   .container {
     margin: 0 auto;
     max-width: var.$container-width;
   }

   .section {
     padding: 72px 36px;
   }

   .visually-hidden {
     position: absolute;
     overflow: hidden;
     clip: rect(0 0 0 0);
     height: 1px; width: 1px;
     margin: -1px; padding: 0; border: 0;
   }
   ```

### Components

1. Create the `components/common` directories and files
   ```sh
   mkdir -p components/common && touch components/common/layout.module.scss && touch components/common/layout.tsx
   ```
7. Edit `components/common/layout.module.scss`
   ```scss
   .page {
     display: flex;
     min-height: 100vh;
     flex-direction: column;
   }

   .main {
     flex: 1;
   }
   ```
8. Edit `components/layout.tsx`
   ```ts
   import styles from "./layout.module.scss"
   import Head from "next/head"

   export const Layout = ({ children, footer=</>, header=</> }: {
     children: React.ReactNode
     footer?: React.ReactNode
     header?: React.ReactNode
   }) => {
     return (
       <div className={styles.page}>
         <Head>
           <title>Moonbeam</title>
           <link rel="icon" type="image/svg+xml" href="/favicon.svg" />
         </Head>
         {header}
         <main className={styles.main}>
           {children}
         </main>
         {footer}
       </div>
     )
   }
   ```

### Pages

1. Create the `pages` directory and files
   ```sh
   mkdir pages && touch pages/_app.tsx && touch pages/index.tsx
   ```
2. Edit `pages/_app.tsx`
   ```ts
   import { AppProps } from "next/app"
   import "../styles/app.scss"

   const MyApp = ({ Component, pageProps }: AppProps) => <Component {...pageProps} />

   export default MyApp
   ```
3. Edit `pages/index.tsx`
   ```ts
   import Head from "next/head"
   import { Layout } from "~/components/layout"

   const HomePage = () => (
     <Layout>
       <Head>
         <title>Welcome to Moonbeam</title>
       </Head>
       <section className="section">
         <div className="container">
           <h1 style={{ margin: 0 }}>Shoot for the moon!</h1>
         </div>
       </section>
     </Layout>
   )

   export default HomePage
   ```

## Run it

1. Edit `package.json` (add `test` to `scripts`), e.g.
   ```json
   {
     "scripts": {
       "dev": "next dev",
       "build": "next build",
       "start": "next start",
       "test": "jest"
     },
     "other": "configs"
   }
   ```
2. Install all of the dependencies defined in the `package.json` file
   ```sh
   yarn install
   ```
3. Run the development environment
   ```sh
   yarn dev
   ```
4. Navigate to http://localhost:3000

## Resources

* [Getting Started](https://nextjs.org/docs/)
* [Hiding Content for Accessibility](https://snook.ca/archives/html_and_css/hiding-content-for-accessibility)
* [Introducing JSX](https://reactjs.org/docs/introducing-jsx.html)
* [NextJS Typescript Boilerplate](https://github.com/vercel/next.js/tree/canary/examples/with-typescript-eslint-jest)
* [Normalize.css](https://necolas.github.io/normalize.css/)
* [Sticky Footer](https://philipwalton.github.io/solved-by-flexbox/demos/sticky-footer/)
* [SVG, Favicons, and All the Fun Things We Can Do With Them](https://css-tricks.com/svg-favicons-and-all-the-fun-things-we-can-do-with-them/)
* [Weather Icon: Full Moon](https://commons.wikimedia.org/wiki/File:Weather_icon_-_full_moon.svg)
