# Up Next

* [Prerequisites](#prerequisites)
* [Project setup](#application-setup)
* [Deployment](#deployment)
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
   brew update && brew upgrade && brew cleanup #
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
2. Create and name your project
   ```sh
   yarn create next-app
   ```
3. Navigate to project directory
   ```sh
   cd [your-project-name] # e.g. cd up-next
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

## Deployment

## Resources
