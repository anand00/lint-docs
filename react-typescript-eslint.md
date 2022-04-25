# Introduction

ESLint is a tool to identify and report on patterns found in ECMAScript/JavaScript code, with the goal to make code more consistent and avoid bugs.

This repository will document different technology specific linting rules for ESLint.

At [Osmosys Software Solutions Pvt Ltd](https://osmosys.co/) we standardize the ESLint configuration, which will be used across multiple projects.

# Prerequisite

- React app with TypeScript

Any existing React app with TypeScript. If you don't have one then you can create a basic React app using the following command.

```sh
npx create-react-app my-app --template typescript
```

- Node.js

[Node.js](https://nodejs.org/en/) (`^12.22.0`, `^14.17.0`, or `>=16.0.0`) built with SSL support. (If you are using an official Node.js distribution, SSL is always built in.)

# Installation

Install the following packages:

- [eslint@7.32.0](https://github.com/eslint/eslint)
- [@typescript-eslint/eslint-plugin@4.33.0](https://github.com/typescript-eslint/typescript-eslint/tree/main/packages/eslint-plugin)
- [eslint-config-standard-with-typescript@21.0.1](https://github.com/standard/eslint-config-standard-with-typescript)
- [eslint-plugin-import@2.25.3](https://github.com/import-js/eslint-plugin-import)
- [eslint-plugin-promise@5.1.1](https://github.com/xjamundx/eslint-plugin-promise)
- [eslint-plugin-react@7.27.0](https://github.com/jsx-eslint/eslint-plugin-react)


```sh
npm i -D eslint@7.32.0 @typescript-eslint/eslint-plugin@4.33.0 eslint-config-standard-with-typescript@21.0.1 eslint-plugin-import@2.25.3 eslint-plugin-promise@5.1.1 eslint-plugin-react@7.27.0
```

> **Note**: for now assuming we will use `npm` over `yarn`

# Configuration

Create `.eslintrc.js` file in the root directory of your project.

Then add the below configuration in this file.

```js
module.exports = {
  root: true,
  parser: '@typescript-eslint/parser',
  plugins: [
    '@typescript-eslint',
    'react'
  ],
  parserOptions: {
    project: './tsconfig.json',
    ecmaFeatures: {
      jsx: true
    }
  },
  extends: [
    'eslint:recommended',
    'plugin:@typescript-eslint/recommended',
    'standard-with-typescript',
    'plugin:react/recommended'
  ],
  settings: {
    // https://github.com/yannickcr/eslint-plugin-react#configuration
    react: {
      'version': 'detect'
    }
  },
  rules: {
    "@typescript-eslint/semi": ["error", "always"]
  }
};
```

# Usage

Add couple of script commands to run ESLint.

```
"scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject",
    "lint": "eslint src --ext .js,.jsx,.ts,.tsx --max-warnings=0",
    "lint-fix": "eslint src --ext .js,.jsx,.ts,.tsx --fix"
  },
```

**`npm run lint`**

This command will run ESLint and display all the warnings and errors in your code.

**`npm run lint-fix`**

This command will run ESLint, display all the warnings and errors and it will even fix the issues if they are fixable by ESLint.