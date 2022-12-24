# Vite template setup

Empty Vite template with basic setup

This is an example of basic setup of project based on Vite. By default, the template includes configured ESLint with Airbnb style guide and testing instruments like Vitest and Testing Library.

## Get started

    git clone https://github.com/OleksiiDvornik/vite-template.git
    cd vite-template
    npm i

## Manual setup

If you want to set up this template manually, there is a full step-by-step instruction:

### Step #1. Download and setup basic Vite template

    npm create vite@latest
    npm install  

### Step #2. Install and setup ESLint with Airbnb Style Guide

    npm install -D eslint
    npx eslint --init

### Step #3. Install Airbnb Style Guide

    npx install-peerdeps -D eslint-config-airbnb
    npm install -D eslint-config-airbnb-typescript

Configure ESLint:

    "extends": [
    - "eslint:recommended",
    + "airbnb",
    + "airbnb/hooks",
    + "airbnb-typescript"  
    ],
    ...
    "parserOptions": {
    + "project": "./tsconfig.json"
    }

Add ESLint rules:

    {
      "react/react-in-jsx-scope": "off",
      "linebreak-style": "off",
      "no-console": "off",
      "react/function-component-definition": [
          1, {"namedComponents": "arrow-function"}
        ],
      "arrow-body-style": "warn"
    }

### Step #4. Configure tsconfig.json

    "include": [
      "src",
    + "vite.config.ts",
    + ".eslintrc.json" 
    ]

### Step #5. Install and setup Vitest and Testing Library

    npm install -D vitest
    npm install -D @testing-library/react @testing-library/jest-dom

Edit vite.config.ts:

    + /* eslint-disable import/no-extraneous-dependencies */

    + /// <reference types="vitest" />
    + /// <reference types="vite/client" />

    import { defineConfig } from 'vite';
    import react from '@vitejs/plugin-react';

    // https://vitejs.dev/config/
    export default defineConfig({
      plugins: [react()],
    + test: {
    +   globals: true,
    +   environment: 'jsdom',
    +   setupFiles: ['./src/setupTests.ts'],
      },
    });

Create setupTests.ts file in ./src folder:

    /* eslint-disable import/no-extraneous-dependencies */

    import matchers from '@testing-library/jest-dom/matchers';
    import { expect } from 'vitest';

    expect.extend(matchers);

Add "test" script to package.json:

    "scripts": {
      ...
    + "test": "vitest"
    }
