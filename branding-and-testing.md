# Branding and Testing

Adding [Jest](https://jestjs.io/) to a [Next.js](https://nextjs.org/) project. Also adding `<header>` and `<footer>` branding. These changes build upon [up-next](README.md).

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

## Add Footer

1. Create the `footer` files in the `components/common` directory
   ```sh
   touch components/common/footer.module.scss && touch components/common/footer.test.tsx && touch components/common/footer.tsx
   ```
2. Edit `components/common/footer.module.scss`
   ```scss
   @use "/styles/variables" as var;

   .footer {
     padding: var.$fluid-gutter-padding;
   }

   .copyright {
     font-size: var.$fluid-legal-font-size;
   }
   ```
3. Edit `components/common/footer.tsx`
   ```ts
   import styles from "./footer.module.scss"

   export const Footer = () => {
     const today = new Date();
     return (
       <footer className={styles.footer}>
         <div className={styles.container}>
           <div className={styles.copyright}>
             &copy; <span data-testid="copyright-year">
               {today.getFullYear()}
             </span> Powered by Next.js
           </div>
         </div>
       </footer>
     )
   }
   ```
4. Edit `components/common/footer.test.tsx`
   ```ts
   import React from "react"
   import { render } from "@testing-library/react"
   import { Footer } from "./footer"

   const copyrightYear = "1969"

   describe("Footer component", () => {
     it("matches snapshot", () => {
       const { asFragment } = render(<Footer />, {})
       expect(asFragment()).toMatchSnapshot()
     })

     it("has the correct copyright year", () => {
       const { getByTestId } = render(<Footer />, {})
       expect(getByTestId("copyright-year").textContent).toBe(copyrightYear)
     })
   })
   ```

## Add Header

1. Create the `header` files in the `components/common` directory
   ```sh
   touch components/common/header.module.scss && touch components/common/header.tsx
   ```
2. Edit `components/common/header.module.scss`
   ```scss
   @use "/styles/variables" as var;

   .header {
     background-color: var.$dark-gray;
     padding: 0 9px;
   }

   .logo {
     display: flex;
     align-items: center;
     background: transparent url(/favicon.svg) no-repeat center left / cover;
     width: 54px;
     height: 54px;
   }
   ```
3. Edit `components/common/header.tsx`
   ```ts
   import styles from "./header.module.scss"

   export const Header = () => (
     <header className={styles.header}>
       <div className={styles.container}>
         <div className={styles.brand}>
           <div className={styles.logo}>
             <span className="visually-hidden">Moonbeam</span>
           </div>
         </div>
       </div>
     </header>
   )
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
3. Run tests (and maybe fix broken tests after running)
   ```sh
   yarn test
   ```
4. Run the development environment
   ```sh
   yarn dev
   ```
5. Navigate to http://localhost:3000
