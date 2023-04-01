# Up Next

Start a [Next.js](https://nextjs.org) project on a Mac.

## Install Homebrew

[Homebrew](https://brew.sh) is a software package management system for macOS.

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

[Yarn](https://yarnpkg.com) is a package manager for JavaScript.

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

1. Create the project directory, e.g.
   ```sh
   mkdir mundo
   ```
2. Navigate into the project directory, e.g.
   ```sh
   cd mundo
   ```
3. Create a Next.js application
   ```sh
   yarn create next-app --typescript .
   ```

## Add Sass and Normalize.css

[Sass](https://sass-lang.com) is a CSS extension language, while [Normalize.css](https://necolas.github.io/normalize.css/) provides cross-browser consistency for styling HTML elements.

1. Add `sass` and `normalize.css` to the project
   ```sh
   yarn add --dev sass && yarn add normalize.css
   ```
2. Edit `next.config.js`
   ```js
   const path = require('path')

   /** @type {import('next').NextConfig} */
   const nextConfig = {
     reactStrictMode: true,
     sassOptions: {
       includePaths: [path.join(__dirname, 'styles')],
     },
   }

   module.exports = nextConfig
   ```
3. Create a website application stylesheet
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
5. Edit `pages/_app.tsx`
   ```tsx
   import 'normalize.css'
   import '@/styles/app.scss'
   import type { AppProps } from 'next/app'

   export default function App({ Component, pageProps }: AppProps) {
     return <Component {...pageProps} />
   }
   ```

## Update your favorite icon

A [favicon](https://developer.mozilla.org/en-US/docs/Glossary/Favicon) is the tiny icon displayed in the browser’s page tab.

1. Create an SVG file
   ```sh
   touch public/favicon.svg
   ```
2. Edit `public/favicon.svg`
   ```svg
   <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32"><path d="M16 0C7.163 0 0 7.163 0 16s7.163 16 16 16 16-7.163 16-16S24.837 0 16 0zm0 30c-1.967 0-3.84-.407-5.538-1.139l7.286-8.197a.998.998 0 0 0 .253-.664v-3a1 1 0 0 0-1-1c-3.531 0-7.256-3.671-7.293-3.707A1 1 0 0 0 9.001 12h-4a1 1 0 0 0-1 1v6c0 .379.214.725.553.894l3.447 1.724v5.871c-3.627-2.53-6-6.732-6-11.489 0-2.147.484-4.181 1.348-6h3.652c.265 0 .52-.105.707-.293l4-4A1 1 0 0 0 12.001 5V2.581a14.013 14.013 0 0 1 4-.581c2.2 0 4.281.508 6.134 1.412A5.961 5.961 0 0 0 20.002 8c0 1.603.624 3.109 1.757 4.243a5.985 5.985 0 0 0 4.536 1.751c.432 1.619 1.211 5.833-.263 11.635a.936.936 0 0 0-.026.163A13.956 13.956 0 0 1 16.002 30z"/></svg>
   ```
3. Edit `pages/index.tsx`
   ```tsx
   import Head from 'next/head'

   const Home = () => {
     return (
       <>
         <Head>
           <title>Welcome home</title>
           <meta name="viewport" content="width=device-width, initial-scale=1" />
           <link rel="icon" href="/favicon.svg" />
         </Head>
         <main>
           <h1>Your dogs must be barking 🐶</h1>
           <p>Why don’t you come sit a spell and tell us all about it.</p>
         </main>
       </>
     )
   }

   export default Home
   ```

## You did it!

Nice work bud, let’s check out your work.

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

Pat yourself on the back, you deserve a break. Hit <kbd>Ctrl</kbd> + <kbd>c</kbd> to stop the development environment. In our next expisode we go [international](https://nextjs.org/docs/advanced-features/i18n-routing).
