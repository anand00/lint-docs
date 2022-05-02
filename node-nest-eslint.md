# Introduction

At Osmosys all Node.js applications will be developed using [NestJs](https://nestjs.com/) framework.

# Prerequisite

- [NestJs v8.2.5](https://docs.nestjs.com/first-steps)

An existing application or new application developed using NestJs framework.


**Install Nest CLI**

```sh
npm i -g @nestjs/cli@8.2.5
```

**Create new project**

```sh
nest new project-name
```

- [Node.js v16.14.2](https://nodejs.org/en/)

[Node.js](https://nodejs.org/en/) (`v16.14.2`) built with SSL support. (If you are using an official Node.js distribution, SSL is always built in.)

# Installation

ESLint comes preinstalled with NestJs. Right now we don't plan to add any more extensions or plugins.

# Configuration

Copy below configuration to `.eslintrc.js` file in the root directory of your project.


```js
module.exports = {
  parser: '@typescript-eslint/parser',
  parserOptions: {
    project: 'tsconfig.json',
    tsconfigRootDir: __dirname, 
    sourceType: 'module',
  },
  plugins: ['@typescript-eslint/eslint-plugin'],
  extends: [
    'plugin:@typescript-eslint/recommended',
    'plugin:prettier/recommended',
  ],
  root: true,
  env: {
    node: true,
    jest: true,
  },
  ignorePatterns: ['.eslintrc.js'],
  rules: {},
};
```

> For now the default rules are good enough. We will add new rules as we encounter issues when using this framework.

# Usage

With NestJs you get a predefined script to run lint checks.

```sh
"lint": "eslint \"{src,apps,libs,test}/**/*.ts\" --fix",
```

**`npm run lint`**

This command will run ESLint and display all the warnings and errors in your code and it will even fix the issues if they are fixable by ESLint.