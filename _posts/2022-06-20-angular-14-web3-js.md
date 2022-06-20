---
title: Angular 14 and Web3.js
published: true
---
How to setup Angular 14 app to use Web3.js lib
---

## Angular 14 and Web3.js

If you try to use web3.js in an Angular14 new app, it will fail.

Some errors looks like the following:

```sh
./node_modules/xhr2-cookies/dist/xml-http-request.js:39:12-28 - Error: Module not found: Error: Can't resolve 'https' in '/Users/agustinvinao/dev/blockchain-101/005-client-angular/smart-contract-client/node_modules/xhr2-cookies/dist
```

It may show different modules `https`, `http`, `stream`, `crypto` and/or `crypto-browserify`.

The issue is about web3.js trying to load some modules as if it's using node.

In order to fix this issue, we see the following information in the console:

```
BREAKING CHANGE: webpack < 5 used to include polyfills for node.js core modules by default.
This is no longer the case. Verify if you need this module and configure a polyfill for it.

If you want to include a polyfill, you need to:
        - add a fallback 'resolve.fallback: { "https": require.resolve("https-browserify") }'
        - install 'https-browserify'
If you don't want to include a polyfill, you can use an empty module like this:
        resolve.fallback: { "https": false }
```

To fix this issue, this is the steps to follow:

1. create a extra-webpack.config.js with all the fallback for the failing libs
2. install @angular-builders/custom-webpack
3. install dependencies 
4. update angular.json

### 1. Create a extra-webpack.config.js with all the fallback for the failing libs

filename: `extra-webpack.config.js`
```javascript
module.exports = {
  resolve: {
    fallback: {
      http: require.resolve("stream-http"),
      https: require.resolve("stream-http"),
      stream: require.resolve("stream-browserify"),
      crypto: require.resolve("crypto-browserify"),
      "crypto-browserify": require.resolve("crypto-browserify"),
    },
  },
};
```
### 2. install @angular-builders/custom-webpack

using yarn:
```bash
yarn add -D @angular-builders/custom-webpack
```

using npm:
```bash
npm i --save @angular-builders/custom-webpack
```

### 3. install dependencies 

The following dependencies are used by `web3.js`.

using yarn:

```bash
npm i browser crypto-browserify https-browserify os os-browserify stream-browserify stream-http url
```

```bash
yarn add browser crypto-browserify https-browserify os os-browserify stream-browserify stream-http url
```

### 4. update angular.json

This is how `angular.json` must be in order to use our webpack config:

```json
"architect": {
  "build": {
    "builder": "@angular-builders/custom-webpack:browser",
    "options": {
      "customWebpackConfig": {
        "path": "./custom-webpack.config.js",
        "replaceDuplicatePlugins": true
      },
      // ...
    },
    // ...
  },
  // ...
}
```
and (AngularCustomWebpackConfig is the name of the app you've created)
```json
"architect": {
  // ...
  "serve": {
    "builder": "@angular-builders/custom-webpack:dev-server",
    "options": {
      "browserTarget": "AngularCustomWebpackConfig:build"
    },
    "configurations": {
      "production": {
        "browserTarget": "AngularCustomWebpackConfig:build:production"
      }
    }
  },
  // ...
}
```