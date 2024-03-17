# What is React

```
- 1. A JavaScript Library made by Facebook to build Web Pages and Mobile Applications
- 2. React has multiple libraries and all of them live on the Node JS Repository called npm
- 3. Example react (core) , react-dom (for Browsers) , react-native (for Mobiles)
- 4. React has primary two parts 
- 5. The first part : UI Related Business Logic is written using either JavaScript or TypeScript in .js or .ts files
- 6. The Second Part actual UI is written is a language called JavaScript XML or JSX in .jsx files
- 7. Both .jsx and .ts files are either transformed in JavaScript dynamically during Development or they can be statically build (using npm run build command) to generate JavaScript bundles and HTML/CSS to be deployed in WebServers
- 8. Angular has separate files for logic (.ts) and UI (.html) but React has a single file for UI which is .jsx files.
```

# What is TypeScript

```
- 1. A Strongly Typed language developed by Microsoft.
- 2. Native JavaScript does not support strong typing resulting in no checks for errors during Development time
- 3. TypeScript adds Strong Types, Classes and a lot of other bells and whitsles for developers
- 4. Both Angular and React now can use TypeScript.
- 5. All TypeScript files (.ts ) are compiled into native JavaScrit before the Web Browsers can execute them.
- 6. It is a standard pattern to develop in TypeScript and when done, generate build which transforms TypeScript into JAvaScript files to be deployed into WebServers, CDNs that serves the bundles (JS,CSS,HTML, Images) to Web Browsers
```

# What is WebPack

```
- 1. The Maven, Gradle, ANT or Unix Make Utility
```
# How to build a React App using WebPack

## Challenges

```
- 1. Setting up a React and TypeScript project is tricky because both JSX and TypeScript code needs to be transpiled into JavaScript.
```

## Introducing webpack

```
- 1. Webpack is a tool that bundles JavaScript source code files together.
- 2. It can also bundle CSS and images.
- 3. It can run other tools such as Babel to transpile React and the TypeScript type checker as it scans the files
- 4. Webpack is incredibly flexible but, unfortunately, it requires a lot of configuration.
```

## Creating the folder structure

```
- 1. Open Visual Studio Code in the folder where you want the project to be.
- 2. In the Explorer panel, create a folder called src. A folder can be created by right-clicking in the Explorer panel and choosing New Folder. Note that src is short for source code.
```

## Creating package.json : Create a package.json file at the root of the project with the following content:

```
{
  "name": "my-app",
  "description": "My React and TypeScript app",
  "version": "0.0.1"
}
```

## Reference : https://docs.npmjs.com/cli/v8/configuring-npm/package-json

## Adding a web page

## An HTML page is going to host the app. In the src folder, create a file called index.html with the following content:

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>My app</title>
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
```

## Adding TypeScript

```
npm install --save-dev typescript

```

## Verify the package.json

## Next, we will create a TypeScript configuration file. Note that we aren’t going to configure TypeScript to do any transpilation – we will use Babel for that, which is covered later. So, the TypeScript configuration will be focused on type checking.

```
{
  "compilerOptions": {
    "noEmit": true,
    "lib": [
      "dom",
      "dom.iterable",
      "esnext"
    ],
    "moduleResolution": "node",
    "allowSyntheticDefaultImports": true,
    "esModuleInterop": true,
    "jsx": "react",
    "forceConsistentCasingInFileNames": true,
    "strict": true
  },
  "include": ["src"],
  "exclude": ["node_modules", "dist"]
}
```

## Setting noEmit to true suppresses the TypeScript compiler from doing any transpilation.

## Setting allowSyntheticDefaultImports and esModuleInterop to true allows React to be imported as a default import, like the following:

```
import React from 'react'

```

## instead of

```
import * as React from 'react'

```

## Setting forceConsistentCasingInFileNames to true enables the type-checking process to check the casing of referenced filenames in import statements are consistent.

## Adding React

```
npm install react react-dom

```

## The core library is called react, which is used in all variants of React.

## The specific React variant, which is the variant used to build web apps, is called react-dom. An example of a different variant would be the React Native variant used to build mobile apps.

## React doesn’t include TypeScript types – instead, they are in a separate npm package. Let’s install these now:

```
npm install --save-dev @types/react @types/react-dom

```

## The root component will be in a file called index.tsx in the src folder

```
import React, { StrictMode } from 'react';
import { createRoot } from 'react-dom/client';

const root = createRoot(document.getElementById('root') as HTMLElement);

function App() {
  return <h1>My Super React and TypeScript App! {new Date().toString()}</h1>;
}

root.render(
  <StrictMode>
    <App />
  </StrictMode>,
);

```

## The structure of this file is similar to the index.js file in the alert component project from the first chapter. It injects the React app into a DOM element with an id of 'root'. The app is straightforward – it displays a heading called My React and TypeScript App!.

## Notice that the file extension for index is .tsx rather than .js. This allows Babel and TypeScript to detect TypeScript files containing JSX in the transpilation and type-checking processes. A .ts extension can be used for TypeScript code that doesn’t contain any JSX.

## Adding Babel

## As mentioned earlier, Babel will transpile both React and TypeScript code into JavaScript in this project. Carry out the following steps to install and configure Babel:

```
npm install --save-dev @babel/core

or

npm i -D @babel/core

then

npm i -D @babel/preset-env
npm i -D @babel/preset-react
npm i -D @babel/preset-typescript
npm i -D @babel/plugin-transform-runtime @babel/runtime

```

## Next, install a Babel plugin called @babel/preset-env that allows the latest JavaScript features to be used:

## Now, install a Babel plugin called @babel/preset-react that enables React code to be transformed into JavaScript:

## Similarly, install a Babel plugin called @babel/preset-typescript that enables TypeScript code to be transformed into JavaScript:

## The last two plugins to install allow the use of the async and await features in JavaScript:

#3 Verify package.json

```
{
  "name": "my-app",
  "description": "My React and TypeScript app",
  "version": "0.0.1",
  "devDependencies": {
    "@babel/core": "^7.19.3",
    "@babel/plugin-transform-runtime": "^7.19.1",
    "@babel/preset-env": "^7.19.4",
    "@babel/preset-react": "^7.18.6",
    "@babel/preset-typescript": "^7.18.6",
    "@babel/runtime": "^7.19.4",
    "@types/react": "^18.0.21",
    "@types/react-dom": "^18.0.6",
    "babel-loader": "^8.2.5",
    "html-webpack-plugin": "^5.5.0",
    "ts-node": "^10.9.1",
    "typescript": "^4.8.4",
    "webpack": "^5.74.0",
    "webpack-cli": "^4.10.0",
    "webpack-dev-server": "^4.11.1"
  },
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0"
  },
  "scripts": {
    "start": "webpack serve --config webpack.dev.config.ts"
  }

}

```

## Babel can be configured in a file called .babelrc.json. Create this file at the root of the project with the following content:

```
{
    "presets": [
      "@babel/preset-env",
      "@babel/preset-react",
      "@babel/preset-typescript"
    ],
    "plugins": [
      [
        "@babel/plugin-transform-runtime",
        {
          "regenerator": true
        }
      ]
    ]
  }

```

## Adding webpack

## Webpack is a popular tool that primarily bundles JavaScript source code files together. It can run other tools, such as Babel, as it scans the files. So, we will use webpack to scan all the source files and transpile them into JavaScript. The output from the webpack process will be a single JavaScript bundle that is referenced in index.html.

## Installing webpack

```
npm i -D webpack webpack-cli
npm i -D webpack-dev-server

```

## A webpack plugin is required to allow Babel to transpile the React and TypeScript code into JavaScript. This plugin is called babel-loader. Install this using the following command:

```
npm i -D babel-loader

```

## Webpack can create the index.html file that hosts the React app. We want webpack to use the index.html file in the src folder as a template and add the React app’s bundle to it. A plugin called html-webpack-plugin is capable of doing this. Install this plugin using the following command:

```
npm i -D html-webpack-plugin

```

## Configuring webpack

## Next, we will configure webpack to do everything we need. Separate configurations for development and production can be created because the requirements are slightly different. However, we will focus on a configuration for development in this chapter. Carry out the following steps to configure webpack:

```
npm i -D ts-node
```

## Now, we can add the development configuration file. Create a file called webpack.dev.config.ts in the project root.

## The path node library will tell webpack where to place the bundle.

## HtmlWebpackPlugin will be used to create index.html.

## The webpack configuration TypeScript types come from both the webpack and webpack-dev-server packages. So, we combine them using an intersect type, creating a type called Configuration.

## The mode property tells webpack the configuration is for development, meaning that the React development tools are included in the bundle

## The output.publicPath property is the root path in the app, which is important for deep linking in the dev server to work correctly

## The entry property tells webpack where the React app’s entry point is, which is index.tsx in our project

## Webpack expects the configuration object to be a default export, so we export the config object as a default export

## The module property informs webpack how different modules should be processed. We need to tell webpack to use babel-loader for files with .js, .ts, and .tsx extensions.

## The resolve.extensions property tells webpack to look for TypeScript files and JavaScript files during module resolution.

## As mentioned earlier, HtmlWebpackPlugin creates the HTML file. It has been configured to use index.html in the src folder as a template.

## HotModuleReplacementPlugin allows modules to be updated while an application is running, without a full reload.

## The devtool property tells webpack to use full inline source maps, which allow the original source code to be debugged before transpilation.

## The devServer property configures the webpack development server. It configures the web server root to be the dist folder and to serve files on port 4000. Now, historyApiFallback is required for deep links to work, and we have also specified to open the browser after the server has been started.

```
import path from 'path';
import HtmlWebpackPlugin from 'html-webpack-plugin';
import {
  Configuration as WebpackConfig,
  HotModuleReplacementPlugin,
} from 'webpack';
import {
  Configuration as WebpackDevServerConfig
} from 'webpack-dev-server';

type Configuration = WebpackConfig & {
  devServer?: WebpackDevServerConfig;
}

const config: Configuration = {
  mode: 'development',
  output: {
    publicPath: '/',
  },
  entry: './src/index.tsx',
  module: {
    rules: [
      {
        test: /\.(ts|js)x?$/i,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env', '@babel/preset-react', '@babel/preset-typescript'],
          },
        },
      },
    ],
  },
  resolve: {
    extensions: ['.tsx', '.ts', '.js'],
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: 'src/index.html',
    }),
    new HotModuleReplacementPlugin(),
  ],
  devtool: 'inline-source-map',
  devServer: {
    static: path.join(__dirname, 'dist'),
    historyApiFallback: true,
    port: 4000,
    open: true,
    hot: true,
  }
};

export default config;

```

## First, open package.json and add a scripts section with a start script:

```
 "scripts": {
    "start": "webpack serve --config webpack.dev.config.ts"
  }
```

## Run

```
npm run start
npm start
```

## Leave the app running and open the index.tsx file. Change the content of the h1 element to something slightly different:

## Summary of Webpack

```
- 1. An HTML file is required to host the React app
- 2. Webpack transpiles the app’s React and TypeScript code into JavaScript with the help of Babel and then references it in the HTML file
- 3. Webpack has a development server that automatically refreshes the app as we write code
```
