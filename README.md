# Up Next

* [Prerequisites](#prerequisites)
* [Project setup](#project-setup)
* [Public files](#public-files)
* [Website styles](#website-styles)
* [Brand components](#brand-components)
* [Hero component](#hero-component)
* [Pages](#pages)
* [Resources](#resources)

## Prerequisites

### Install or update `brew`

1. Check if `brew` is already installed
   ```sh
   which brew # e.g. /usr/local/bin/brew
   ```
2. If `brew` is already installed, then update it...
   ```sh
   brew update && brew upgrade && brew cleanup
   ```
3. Otherwise, follow the installation instructions at https://brew.sh/

### Install `yarn`

1. Check if `yarn` is already installed
   ```sh
   which yarn # e.g. /usr/local/bin/yarn
   ```
2. Otherwise, install `yarn`
   ```sh
   brew install yarn
   ```

## Project setup

### Start a Next.js project

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

### Install TypeScript

1. Create a TypeScript configuration file
   ```sh
   touch tsconfig.json
   ```
2. Add `typescript` to the project
   ```sh
   yarn add --dev typescript @types/react @types/node
   ```
3. Autopopulate the `tsconfig.json` file
   ```sh
   yarn dev
   ```

### Edit the `tsconfig.json` file

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

1. Add `sass` to the project
   ```sh
   yarn add --dev sass
   ```
2. Create a Next.js configuration file
   ```sh
   touch next.config.js
   ```
3. Edit the `next.config.js` file
   ```js
   const path = require('path')

   module.exports = {
     sassOptions: {
       includePaths: [path.join(__dirname, 'styles')],
     },
   }
   ```

### Install normalize

1. Add `normalize` to the project
   ```sh
   yarn add normalize.css
   ```

### Housekeeping

1. Remove the `pages`, `public` and `styles` directories
   ```sh
   rm -rf pages && rm -rf public && rm -rf styles
   ```

## Public files

1. Create the directories
   ```sh
   mkdir -p public/fonts/poiret-one && mkdir -p public/images/brand && mkdir -p public/images/heroes/maria-felix
   ```
2. Download the latin-version of [Poiret One](https://fonts.googleapis.com/css2?family=Poiret+One&display=swap) to `public/fonts/poiret-one/PoiretOne-Regular.woff2`
3. Download the [Full Moon](https://commons.wikimedia.org/wiki/File:Weather_icon_-_full_moon.svg) to `public/images/brand/full-moon.svg`
4. Download the [fallback hero image](https://m.media-amazon.com/images/M/MV5BMGVhMmE2ZGQtOTc0Yy00MTdjLTljNmUtMWM1NWVmZGM5YWJjXkEyXkFqcGdeQXVyMDc2NTEzMw@@._V1_UY414_CR18,0,414,414_AL_.jpg) to `public/images/heroes/maria-felix/enamorada.jpg`
5. Download the [landscape hero image](https://m.media-amazon.com/images/M/MV5BMGVhMmE2ZGQtOTc0Yy00MTdjLTljNmUtMWM1NWVmZGM5YWJjXkEyXkFqcGdeQXVyMDc2NTEzMw@@._V1_FMjpg_UX1024_.jpg) to `public/images/heroes/maria-felix/landscape.jpg`
6. Download the [portrait hero image](https://m.media-amazon.com/images/M/MV5BMGVhMmE2ZGQtOTc0Yy00MTdjLTljNmUtMWM1NWVmZGM5YWJjXkEyXkFqcGdeQXVyMDc2NTEzMw@@._V1_UY768_CR18,0,768,768_AL_.jpg) to `public/images/heroes/maria-felix/portrait.jpg`

## Website styles

1. Create the directory and files
   ```sh
   mkdir styles && touch styles/_mixins.scss && touch styles/_variables.scss && touch styles/brand.scss
   ```
2. Edit `styles/_mixins.scss`
   ```scss
   // Media Queries

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

   $text-heading: clamp(27px, 3vw, 36px);
   $text-lead: clamp(100%, 3vw, 1.26rem);
   ```
4. Edit `styles/brand.scss`
   ```scss
   @import "normalize.css"; // TODO: figure out how to `@use` normalize.css

   // Web Fonts

   @font-face {
     font-family: "Poiret One";
     font-style: normal;
     font-weight: 400;
     font-display: swap;
     src: url("/fonts/poiret-one/PoiretOne-Regular.woff2") format("woff2");
     unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD;
   }

   // Page Styles

   .page {
     display: flex;
     min-height: 100vh;
     flex-direction: column;
   }

   main {
     flex: 1;
   }

   // Utility Styles

   .fluid-image {
     width: 100%;
     height: auto;
     image-rendering: -webkit-optimize-contrast;
   }

   .visually-hidden {
     position: absolute;
     overflow: hidden;
     clip: rect(0 0 0 0);
     height: 1px; width: 1px;
     margin: -1px; padding: 0; border: 0;
   }
   ```

## Brand components

### Footer component

1. Create the directories and files
   ```sh
   mkdir -p components/brand && touch components/brand/Footer.module.scss && touch components/brand/Footer.tsx
   ```
2. Edit `components/brand/Footer.module.scss`
   ```scss
   @use "/styles/variables" as var;

   .footer {
     border-top: solid 1px var.$light-gray;
     padding: 0 var.$gutter-width;
   }

   .container {
     padding: var.$gutter-height 0;
     max-width: var.$container-width;
     margin: 0 auto;
   }

   .copyright {
     font-family: "Franklin ITC", sans-serif;
     font-weight: 400;
     font-style: normal;
     font-size: clamp(12px, 2vw, 100%);
   }
   ```
3. Edit `components/brand/Footer.tsx`
   ```ts
   import styles from "./Footer.module.scss"

   const Footer = () => {
     const today = new Date();
     return (
       <footer className={styles.footer}>
         <div className={styles.container}>
           <div className={styles.copyright}>
             &copy; {today.getFullYear()} Over the Moon | Powered by Next.js
           </div>
         </div>
       </footer>
     )
   }

   export { Footer }
   ```

### Header component

1. Create the files
   ```sh
   touch components/brand/Header.module.scss && touch components/brand/Header.tsx
   ```
2. Edit `components/brand/Header.module.scss`
   ```scss
   @use "/styles/variables" as var;

   .header {
     background-color: var.$dark-gray;
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
     background: transparent url(/images/brand/full-moon.svg) no-repeat center left / contain;
     color: white;
     padding-left: 2.7rem;
     font-size: clamp(100%, 2vw, 27px);
   }
   ```
3. Edit `components/brand/Header.tsx`
   ```ts
   import styles from "./Header.module.scss"

   const Header = () => (
     <header className={styles.header}>
       <div className={styles.container}>
         <div className={styles.logo}>
           <span className="visually-hidden">O</span>ver the Moon
         </div>
       </div>
     </header>
   )

   export { Header }
   ```

## Hero component

1. Create the directory and files
   ```sh
   mkdir components/heroes && touch components/heroes/MariaFelix.module.scss && touch components/heroes/MariaFelix.tsx
   ```
2. Edit `components/heroes/MariaFelix.module.scss`
   ```scss
   @use "/styles/variables" as var;
   @use "/styles/mixins" as mix;

   .figure {
     margin: 0;
   }

   .picture {
     display: flex;
     justify-content: center;
     max-width: var.$container-width;
     margin: 0 auto;
   }

   .caption {
     padding: 0 var.$gutter-width;
   }

   .container {
     max-width: var.$max-width;
     margin: 0 auto;
     padding: var.$gutter-height 0;
   }

   .heading {
     font-family: "Franklin ITC", sans-serif;
     font-weight: 700;
     font-size: var.$text-heading;
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
     font-size: var.$text-lead;
     line-height: 1.8;
     margin: 0;
   }
   ```
3. Edit `components/heroes/MariaFelix.tsx`
   ```ts
   import styles from "./MariaFelix.module.scss"

   const MariaFelix = () => {
     return (
       <figure className={styles.figure}>
         <picture className={styles.picture}>
           <source
             srcSet="/images/heroes/maria-felix/landscape.jpg"
             media="(min-aspect-ratio: 4/3), (orientation: landscape)"
           />
           <source
             srcSet="/images/heroes/maria-felix/portrait.jpg"
             media="(max-aspect-ratio: 4/3), (orientation: portrait)"
           />
           <img
             className="fluid-image"
             src="/images/heroes/maria-felix/enamorada.jpg"
             alt="María Félix in Enamorada (1946)"
           />
         </picture>
         <figcaption className={styles.caption}>
           <div className={styles.container}>
             <h1 className={styles.heading}>
               Enamorada
             </h1>
             <blockquote className={styles.blockquote} cite="https://www.imdb.com/title/tt0038510/">
               <p className={styles.blurb}>
                 In Mexican Revolution times, a guerrilla general (Armendáriz) and his troops take the conservative town of Cholula, near by Mexico City. As the revolutionaries mistreat the town's riches, Armendáriz falls for beautiful and wild Beatriz Peñafiel (María Félix), the daughter of one of the town's richest men.
               </p>
             </blockquote>
           </div>
         </figcaption>
       </figure>
     )
   }

   export { MariaFelix }
   ```

## Pages

1. Create the directory and files
   ```sh
   mkdir pages && touch pages/_app.tsx && touch pages/index.tsx
   ```
2. Edit `pages/_app.tsx`
   ```ts
   import { AppProps } from 'next/app'
   import '../styles/brand.scss'

   const MyApp = ({ Component, pageProps }: AppProps) => {
     return <Component {...pageProps} />
   }

   export default MyApp
   ```
3. Edit `pages/index.tsx`
   ```ts
   import Head from 'next/head'
   import { Footer } from "~/components/brand/Footer"
   import { Header } from "~/components/brand/Header"
   import { MariaFelix } from "~/components/heroes/MariaFelix"

   const HomePage = (props) => {
     return (
       <div className="page">
         <Head>
           <title>Welcome to Over the Moon</title>
           <link rel="preload" href="/fonts/poiret-one/PoiretOne-Regular.woff2" as="font" type="font/woff2" />
         </Head>
         <Header />
         <main>
           <MariaFelix />
         </main>
         <Footer />
       </div>
     )
   }

   export default HomePage
   ```

## Resources

* [Absolute Imports and Module path aliases](https://nextjs.org/docs/advanced-features/module-path-aliases)
* [About normalize.css](http://nicolasgallagher.com/about-normalize-css/)
* [Built-In CSS Support](https://nextjs.org/docs/basic-features/built-in-css-support)
* [CSS Fluid Image Techniques for Responsive Site Design](https://thenewcode.com/586/CSS-Fluid-Image-Techniques-for-Responsive-Site-Design)
* [File:Weather icon - full moon.svg](https://commons.wikimedia.org/wiki/File:Weather_icon_-_full_moon.svg)
* [Hiding Content for Accessibility](https://snook.ca/archives/html_and_css/hiding-content-for-accessibility)
* [Introducing JSX](https://reactjs.org/docs/introducing-jsx.html)
* [Poiret One](https://fonts.google.com/specimen/Poiret+One)
* [Sticky Footer -- Solved by Flexbox --- Cleaner, hack-free CSS](https://philipwalton.github.io/solved-by-flexbox/demos/sticky-footer/)
