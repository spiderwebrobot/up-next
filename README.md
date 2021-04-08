# Up Next

A [Next.js](https://nextjs.org/) project with [TypeScript](https://www.typescriptlang.org/), [Sass](https://sass-lang.com/) and [Jest](https://jestjs.io/).

* [Prerequisites](#prerequisites)
* [Start a Next.js project](#start-a-nextjs-project)
* [Add TypeScript](#add-typescript)
* [Add Sass](#add-sass)
* [Add Jest](#add-jest)
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
   mkdir over-the-moon
   ```
2. Navigate into the project directory, e.g.
   ```sh
   cd over-the-moon
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

## Add Jest

1. Add `jest` to the project
   ```sh
   yarn add --dev babel-jest identity-obj-proxy jest @testing-library/react @types/jest
   ```
2. Create Babel and Jest configuration files
   ```sh
   touch .babelrc && touch jest.config.js
   ```
3. Edit `.babelrc`
   ```json
   {
     "presets": ["next/babel"]
   }
   ```
4. Edit `jest.config.js`
   ```js
   module.exports = {
     roots: ["<rootDir>"],
     moduleFileExtensions: ["ts", "tsx", "js", "json", "jsx"],
     testPathIgnorePatterns: ["<rootDir>[/\\\\](node_modules|.next)[/\\\\]"],
     transformIgnorePatterns: ["[/\\\\]node_modules[/\\\\].+\\.(ts|tsx)$"],
     transform: {"^.+\\.(ts|tsx)$": "babel-jest"},
     moduleNameMapper: {"\\.(css|less|sass|scss)$": "identity-obj-proxy"},
   }
   ```

## Organize the project files

### Housekeeping

1. Remove the `pages`, `public` and `styles` directories
   ```sh
   rm -rf pages && rm -rf public && rm -rf styles
   ```

### Public files

1. Create the `public` directories and files
   ```sh
   mkdir -p public/fonts && mkdir -p public/images && touch public/favicon.svg && touch public/fonts/PoiretOne-Regular.woff2 && touch public/images/enamorada.jpg
   ```
2. Download the [full moon](https://upload.wikimedia.org/wikipedia/commons/e/ee/Weather_icon_-_full_moon.svg) to `public/favicon.svg`
3. Download [Poiret One](https://fonts.gstatic.com/s/poiretone/v9/UqyVK80NJXN4zfRgbdfbo55cV-UyZKA.woff2) to `public/fonts/PoiretOne-Regular.woff2`
4. Download the [hero](https://m.media-amazon.com/images/M/MV5BMGVhMmE2ZGQtOTc0Yy00MTdjLTljNmUtMWM1NWVmZGM5YWJjXkEyXkFqcGdeQXVyMDc2NTEzMw@@._V1_UY1536_CR18,108,2048,1080_AL_.jpg) to `public/images/enamorada.jpg`

### Application styles

1. Create the `styles` directory and files
   ```sh
   mkdir styles && touch styles/_mixins.scss && touch styles/_variables.scss && touch styles/app.scss
   ```
2. Edit `styles/_mixins.scss`
   ```scss
   // Media queries

   @mixin media-landscape {
     @media (min-aspect-ratio: 4/3) {
       @content;
     }
   }
   ```
3. Edit `styles/_variables.scss`
   ```scss
   // Colors

   $dark-gray: #333333;
   $light-gray: #E5E5E5;

   // Layout

   $gutter-height: 1.44rem;
   $gutter-width: clamp(1.44rem, 3vw, 2.7rem);
   $container-width: 1024px;

   // Text

   $fluid-heading: clamp(27px, 3vw, 36px);
   $fluid-caption: clamp(100%, 3vw, 1.26rem);

   // Formulas...
   // The default browser font-size is usually 16 pixels.
   // Pixels / 16 = REMs
   // REMs * 16 = Pixels
   // (Pixels / Viewport Width) * 100 = Viewport Percentage
   ```
4. Edit `styles/app.scss`
   ```scss
   @import "normalize.css"; // TODO: figure out how to `@use` normalize.css

   // Web fonts

   @font-face {
     font-family: "Poiret One";
     font-style: normal;
     font-weight: 400;
     font-display: swap;
     src: url("/fonts/poiret-one/PoiretOne-Regular.woff2") format("woff2");
     unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD;
   }

   // Utility styles

   .visually-hidden {
     position: absolute;
     overflow: hidden;
     clip: rect(0 0 0 0);
     height: 1px; width: 1px;
     margin: -1px; padding: 0; border: 0;
   }
   ```

### Components

1. Create the `components` directory and files
   ```sh
   mkdir components && touch components/brand.module.scss && touch components/brand.test.tsx && touch components/brand.tsx && touch components/hero.module.scss && touch components/hero.tsx && touch components/layout.module.scss && touch components/layout.tsx
   ```
2. Edit `components/brand.module.scss`
   ```scss
   @use "/styles/variables" as var;

   .header {
     background-color: var.$dark-gray;
   }

   .footer {
     border-top: solid 1px var.$light-gray;
     padding: 0 var.$gutter-width;
   }

   .container {
     max-width: var.$container-width;
     margin: 0 auto;
   }

   .logo {
     display: flex;
     align-items: center;
     height: 2.7rem;
     font-family: "Poiret One", fantasy;
     background: transparent url(/favicon.svg) no-repeat center left / contain;
     color: white;
     padding-left: 2.7rem;
     font-size: clamp(100%, 2vw, 27px);
   }

   .copyright {
     font-family: "Franklin ITC", sans-serif;
     font-weight: 400;
     font-style: normal;
     font-size: clamp(12px, 2vw, 100%);
     padding: var.$gutter-height 0;
   }
   ```
3. Edit `components/brand.tsx`
   ```ts
   import styles from "./brand.module.scss"

   const Header = () => (
     <header className={styles.header}>
       <div className={styles.container}>
         <div className={styles.logo}>
           <span className="visually-hidden">O</span>ver the Moon
         </div>
       </div>
     </header>
   )

   const Footer = () => {
     const today = new Date();
     return (
       <footer className={styles.footer}>
         <div className={styles.container}>
           <div className={styles.copyright}>
             &copy; <span data-testid="copyright-year">
               {today.getFullYear()}
             </span> Over the Moon | Powered by Next.js
           </div>
         </div>
       </footer>
     )
   }

   export { Footer, Header }
   ```
4. Edit `components/brand.test.tsx`
   ```ts
   import React from "react"
   import { render } from "@testing-library/react"
   import { Footer, Header } from "./brand"

   describe("Footer component", () => {
     it("matches snapshot", () => {
       const { asFragment } = render(<Footer />, {})
       expect(asFragment()).toMatchSnapshot()
     })

     it("has copyright year", () => {
       const { getByTestId } = render(<Footer />, {})
       expect(getByTestId("copyright-year").textContent).toBe("1969")
     })
   })

   describe("Header component", () => {
     it("matches snapshot", () => {
       const { asFragment } = render(<Header />, {})
       expect(asFragment()).toMatchSnapshot()
     })
   })
   ```

5. Edit `components/hero.module.scss`
   ```scss
   @use "/styles/variables" as var;
   @use "/styles/mixins" as mix;

   .figure {
     margin: 0;
   }

   .frame {
     max-width: var.$container-width;
     margin: 0 auto;
   }

   .caption {
     padding: 0 var.$gutter-width;
   }

   .container {
     max-width: var.$container-width;
     margin: 0 auto;
     padding: var.$gutter-height 0;
   }

   .heading {
     font-family: "Franklin ITC", sans-serif;
     font-weight: 700;
     font-size: var.$fluid-heading;
     margin: 0 0 0.9rem;
   }

   .blockquote {
     margin: 0;
     @include mix.media-landscape {
       margin-right: 5.4rem;
     }
   }

   .blurb {
     color: #222;
     font-family: Georgia, Times, "Times New Roman", serif;
     font-size: var.$fluid-caption;
     line-height: 1.8;
     margin: 0;
   }
   ```
6. Edit `components/hero.tsx`
   ```ts
   import styles from "./hero.module.scss"
   import Image from "next/image"

   const Hero = () => (
     <figure className={styles.figure}>
       <div className={styles.frame}>
         <Image
           src="/images/enamorada.jpg"
           alt="María Félix in Enamorada (1946)"
           width={1024}
           height={540}
           layout="responsive"
         />
       </div>
       <figcaption className={styles.caption}>
         <div className={styles.container}>
           <h1 className={styles.heading}>
             Enamorada (1946)
           </h1>
           <blockquote className={styles.blockquote} cite="https://www.imdb.com/title/tt0038510/">
             <p className={styles.blurb}>
               During the Mexican Revolution, a rebel general falls in love with the independent-minded daughter of an aristocrat in the town that he is occupying.
             </p>
           </blockquote>
         </div>
       </figcaption>
     </figure>
   )

   export { Hero }
   ```
7. Edit `components/layout.module.scss`
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
   import { Footer, Header } from "~/components/brand"

   type Props = {
     children: React.ReactNode
     footer?: React.ReactNode
     header?: React.ReactNode
   }

   const Layout = ({ children, footer=<Footer />, header=<Header /> }: Props) => (
     <div className={styles.page}>
       <Head>
         <title>Over the Moon</title>
         <link rel="preload" href="/fonts/PoiretOne-Regular.woff2" as="font" type="font/woff2" />
         <link rel="stylesheet" href="/styles/app.scss" />
         <link rel="icon" type="image/svg+xml" href="/favicon.svg" />
       </Head>
       {header}
       <main className={styles.main}>
         {children}
       </main>
       {footer}
     </div>
   )

   export { Layout }
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
   import { Hero } from "~/components/hero"

   const HomePage = () => (
     <Layout>
       <Head>
         <title>Welcome to Over the Moon</title>
       </Head>
       <Hero />
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
3. Run tests
   ```sh
   yarn test # please fix broken after running
   ```
4. Run the development environment
   ```sh
   yarn dev
   ```
5. Navigate to http://localhost:3000

## Resources

* [CSS Fluid Image Techniques for Responsive Site Design](https://thenewcode.com/586/CSS-Fluid-Image-Techniques-for-Responsive-Site-Design)
* [Getting Started](https://nextjs.org/docs/)
* [Hiding Content for Accessibility](https://snook.ca/archives/html_and_css/hiding-content-for-accessibility)
* [Introducing JSX](https://reactjs.org/docs/introducing-jsx.html)
* [NextJS Typescript Boilerplate](https://github.com/vercel/next.js/tree/canary/examples/with-typescript-eslint-jest)
* [Normalize.css](https://necolas.github.io/normalize.css/)
* [Poiret One](https://fonts.google.com/specimen/Poiret+One)
* [Sticky Footer](https://philipwalton.github.io/solved-by-flexbox/demos/sticky-footer/)
* [SVG, Favicons, and All the Fun Things We Can Do With Them](https://css-tricks.com/svg-favicons-and-all-the-fun-things-we-can-do-with-them/)
* [Weather Icon: Full Moon](https://commons.wikimedia.org/wiki/File:Weather_icon_-_full_moon.svg)
