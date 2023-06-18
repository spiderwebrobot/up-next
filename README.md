# Up Next

Start a [Next.js](https://nextjs.org) project on a Mac.

## Install Homebrew

[Homebrew](https://brew.sh) is a software package management system for macOS. We are going to use Homebrew to install Yarn.

1. Check if `brew` is already installed
   ```sh
   which brew # e.g. /usr/local/bin/brew
   ```
2. Otherwise, follow the installation instructions at https://brew.sh/
3. If `brew` is already installed, then consider an update...
   ```sh
   brew update && brew upgrade && brew cleanup
   ```

## Install Yarn

[Yarn](https://yarnpkg.com) is a package manager for JavaScript. We are going to use Yarn to create a Next.js application. We will also use Yarn to install the [sass](https://www.npmjs.com/package/sass) and [normalize.css](https://www.npmjs.com/package/normalize.css) packages.

1. Check if `yarn` is already installed
   ```sh
   which yarn # e.g. /usr/local/bin/yarn
   ```
2. Otherwise, install `yarn`
   ```sh
   brew install yarn
   ```

## Start a Next.js project

Next.js is a [React](https://reactjs.org) framework for building website applications. Please see the [Getting Started](https://nextjs.org/docs/getting-started) documentation for the latest instructions.

1. Create your project directory, e.g.
   ```sh
   mkdir mundo
   ```
2. Navigate into your project directory
   ```sh
   cd mundo
   ```
3. Create a Next.js application
   ```sh
   yarn create next-app --typescript .
   ```

## Add Sass and Normalize.css

[Sass](https://sass-lang.com) is a CSS extension language, while [Normalize.css](https://necolas.github.io/normalize.css/) provides cross-browser consistency for styling HTML elements.

1. Add `sass` and `normalize.css` to your project
   ```sh
   yarn add --dev sass && yarn add normalize.css
   ```
2. Make a `styles` directory
   ```sh
   mkdir styles
   ```
3. Create a stylesheet for your project’s app
   ```sh
   touch styles/app.scss
   ```
4. Edit `styles/app.scss`
   ```scss
   // utility styles

   .visually-hidden {
     position: absolute;
     overflow: hidden;
     clip: rect(0 0 0 0);
     height: 1px;
     width: 1px;
     margin: -1px;
     padding: 0;
     border: 0;
   }
   ```
5. Edit `next.config.js`
   ```js
   const path = require('path')

   /** @type {import('next').NextConfig} */
   const nextConfig = {
     sassOptions: {
       includePaths: [path.join(__dirname, 'styles')],
     },
   }

   module.exports = nextConfig
   ```
6. Edit `app/layout.tsx`
   ```tsx
   import 'normalize.css'
   import '@/styles/app.scss'
   import { Metadata } from 'next'

   export const metadata: Metadata = {
     title: {
       template: '%s | Mundo',
       default: 'Mundo',
     },
   }

   const RootLayout = ({ children }: { children: React.ReactNode }) => {
     return (
       <html lang="en">
         <body>{children}</body>
       </html>
     )
   }

   export default RootLayout
   ```

## Update the favicon

A [favicon](https://developer.mozilla.org/en-US/docs/Glossary/Favicon) is the tiny icon displayed in the browser’s page tab.

1. Create an SVG file
   ```sh
   touch app/icon.svg
   ```
2. Edit `app/icon.svg`
   ```svg
   <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32"><path d="M16 0C7.163 0 0 7.163 0 16s7.163 16 16 16 16-7.163 16-16S24.837 0 16 0zm0 30c-1.967 0-3.84-.407-5.538-1.139l7.286-8.197a.998.998 0 0 0 .253-.664v-3a1 1 0 0 0-1-1c-3.531 0-7.256-3.671-7.293-3.707A1 1 0 0 0 9.001 12h-4a1 1 0 0 0-1 1v6c0 .379.214.725.553.894l3.447 1.724v5.871c-3.627-2.53-6-6.732-6-11.489 0-2.147.484-4.181 1.348-6h3.652c.265 0 .52-.105.707-.293l4-4A1 1 0 0 0 12.001 5V2.581a14.013 14.013 0 0 1 4-.581c2.2 0 4.281.508 6.134 1.412A5.961 5.961 0 0 0 20.002 8c0 1.603.624 3.109 1.757 4.243a5.985 5.985 0 0 0 4.536 1.751c.432 1.619 1.211 5.833-.263 11.635a.936.936 0 0 0-.026.163A13.956 13.956 0 0 1 16.002 30z"/></svg>
   ```
3. Upload the `app/icon.svg` file into the [Favicon Generator](https://favicon.io/favicon-converter/)
4. Download the `favicon_io.zip` file
5. Unzip the `favicon_io.zip` file
6. Move the `favicon.ico` file into the `app` directory, e.g. `app/favicon.ico`

## The home stretch

Still with me? We’re almost home, just a few more steps...

1. Create a [CSS Module](https://www.sitepoint.com/understanding-css-modules-methodology/) for the Home page
   ```sh
   touch app/page.module.scss
   ```
2. Edit `app/page.module.scss`
   ```scss
   // STRUCTURAL RULES

   .section {
     padding: 3rem 1.5rem;
   }

   .container {
     margin: 0 auto;
     max-width: 768px;
   }

   // TYPOGRAPHIC RULES

   .heading {
     margin-top: 0;
     margin-bottom: 1rem;
   }

   .graph {
     font-size: 1.26rem;
     margin-top: 1rem;
     margin-bottom: 0;
     &:first-child {
       margin-top: 0;
     }
   }
   ```
3. Edit `app/page.tsx`
   ```tsx
   import { Metadata } from 'next'
   import styles from './page.module.scss'

   export const metadata: Metadata = {
     title: 'Welcome Home',
   }

   const Home = () => {
     return (
       <main>
         <section className={styles.section}>
           <div className={styles.container}>
             <h1 className={styles.heading}>Your dogs must be barking 🐶</h1>
             <p className={styles.graph}>Why don’t you come in and sit a spell?</p>
           </div>
         </section>
       </main>
     )
   }

   export default Home
   ```

## You did it!

Nice work bud, let’s see the final product.

1. Install all of the dependencies defined in the `package.json` file
   ```sh
   yarn install
   ```
2. Run the development environment
   ```sh
   yarn dev
   ```
3. Navigate to http://localhost:3000

## What’s next

Pat yourself on the back, you deserve a break. Hit <kbd>Ctrl</kbd> + <kbd>c</kbd> to stop the development environment, and stay tuned for our next expisode when we go [international](i18n.md).

## Digging into it

Plenty more to learn

- [Project Organization and File Colocation](https://nextjs.org/docs/app/building-your-application/routing/colocation)
- [Building Your Application: Styling](https://nextjs.org/docs/app/building-your-application/styling)
- [Metadata Object and generateMetadata Options](https://nextjs.org/docs/app/api-reference/functions/generate-metadata)
- [Metadata Files API Reference](https://nextjs.org/docs/app/api-reference/file-conventions/metadata)
