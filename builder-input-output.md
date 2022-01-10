# Builder.io

Adding [Builder](https://www.builder.io/) to a [Next.js](https://nextjs.org/) project. These changes build upon [up-next](README.md).

## Add Builder

1. Add `builder.io` to the project
   ```sh
   yarn add @builder.io/react @builder.io/sdk
   ```
2. Create Builder environment and configuration files
   ```sh
   touch .env.development .env.production builder.config.ts
   ```
3. Edit `.env.development` (see the "Public API Key" in the [Builder.io dashboard](https://builder.io/account/space))
   ```
   BUILDER_PUBLIC_KEY=seeThePublicAPIKeyInTheBuilderIODashboard
   FORCE_RUNTIME_TAG=canary
   ```
4. Edit `builder.config.ts`
   ```ts
   if (!process.env.BUILDER_PUBLIC_KEY) {
     throw new Error('Missing env varialbe BUILDER_PUBLIC_KEY')
   }

   const config = {
     apiKey: process.env.BUILDER_PUBLIC_KEY,
   }

   export default config
   ```

## Edit Home page

1. Edit `pages/index.tsx`
   ```ts
   import { BuilderComponent, Builder, builder } from '@builder.io/react'
   import { builder as sdk } from '@builder.io/sdk'
   import builderConfig from '~/builder.config'
   // import { Heading } from '~/components/heading'
   import { Layout } from "~/components/layout"

   const HomePage = (props) => {
     console.log('HomePage', props)
     return (
       <Layout>
         <BuilderComponent content={props.content} model="section" />
         <h1>Welcome to Moonbeam</h1>
         <p>{props.yep.data.message}</p>
       </Layout>
     )
   }

   export default HomePage

   export const getStaticProps: GetStaticProps = async (context) => {
     const content = (await builder.get('main-ad', {
       apiKey: builderConfig.apiKey,
       // url: context.resolvedUrl,
       userAttributes: { urlPath: '/' },
       cachebust: true,
     }).toPromise()) || null

     const yep = (await sdk.get('announcement', {
       apiKey: builderConfig.apiKey,
       // url: context.resolvedUrl,
       userAttributes: { urlPath: '/' },
       cachebust: true,
     }).toPromise()) || null

     return { 
       props: { content, yep },
       revalidate: 5, // at most once every 5 seconds
     }
   }
   ```

## Run it

1. Install all of the dependencies defined in the `package.json` file
   ```sh
   yarn install
   ```
2. Run tests (and maybe fix broken tests after running)
   ```sh
   yarn test
   ```
3. Run the development environment
   ```sh
   yarn dev
   ```
4. Navigate to http://localhost:3000
