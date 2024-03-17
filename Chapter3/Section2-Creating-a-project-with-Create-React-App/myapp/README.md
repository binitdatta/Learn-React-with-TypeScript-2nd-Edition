# How to build a React Web App using Tools

## Using Create React App

```
npx create-react-app myapp --template typescript

```

## Adding linting to Visual Studio Code

## Linting is the process of checking code for potential problems. It is common practice to use linting tools to catch problems early in the development process as code is written. ESLint is a popular tool that can lint React and TypeScript code. Fortunately, Create React App has already installed and configured ESLint in our project.

## Open up the Extensions area in Visual Studio Code. The Extensions option is in the Preferences menu in the File menu on Windows or in the Preferences menu in the Code menu on a Mac.

## A list of extensions will appear on the left-hand side and the search box above the extensions list can be used to find a particular extension. Enter eslint into the extensions list search box.

## Click the Install button to install the extension.

## Now, we need to make sure the ESLint extension is configured to check React and TypeScript. So, open the ## Settings area in Visual Studio Code. The Settings option is in the Preferences menu in the File menu on Windows or in the Preferences menu in the Code menu on a Mac.

## Make sure that typescript and typescriptreact are on the list. If not, add them using the Add Item button.

The ESLint extension for Visual Studio Code is now installed and configured in the project.

## In the settings search box, enter eslint: probe and select the Workspace tab:

## Adding code formatting

## The next tool we will set up automatically formats code. Automatic code formatting ensures code is consistently formatted, which helps its readability. Having consistently formatted code also helps developers see the important changes in a code review – rather than differences in formatting.

## Prettier is a popular tool capable of formatting React and TypeScript code. Unfortunately, Create React App doesn’t install and configure it for us. Carry out the following steps to install and configure Prettier in the project:

```
npm i -D prettier
npm i -D eslint-config-prettier eslint-plugin-prettier
```

## eslint-config-prettier disables conflicting ESLint rules, and eslint-plugin-prettier is an ESLint rule that formats code using Prettier.

## The ESLint configuration needs to be updated to allow Prettier to manage the styling rules. Create React App allows ESLint configuration overrides in an eslintConfig section in package.json. Add the Prettier rules to the eslintConfig section in package.json as follows:

```
 "eslintConfig": {
    "extends": [
      "react-app",
      "react-app/jest",
      "plugin:prettier/recommended"
    ]
  },
```

## Prettier can be configured in a file called .prettierrc.json. Create this file with the following content in the root folder:

```
{
  "printWidth": 100,
  "singleQuote": true,
  "semi": true,
  "tabWidth": 2,
  "trailingComma": "all",
  "endOfLine": "auto"
}

```

## Open the Extensions area in Visual Studio Code and enter prettier into the extensions list search box. An extension called Prettier – Code formatter should appear at the top of the list:

## Click the Install button to install the extension.

## Next, open the Settings area in Visual Studio Code. Select the Workspace tab and make sure the Format On Save option is ticked:

## There is one more setting to set. This is the default formatter that Visual Studio Code should use to format code. Click the Workspace tab and make sure Default Formatter is set to Prettier - Code formatter:

## Starting the app in development mode

```
npm start
```

## Open App.tsx and change the Learn React link to Learn React and TypeScript:

```
import React from 'react';
import './App.css';
import { Alert } from './Alert';

function App() {
  return (
    <div className="App">
      <Alert heading="Success" closable>
        Everything is really good!
      </Alert>
    </div>
  );
}

export default App;

```

## Producing a production build

```
npm run build
```

## Open the build folder – it contains many files. The root file is index.html, which references the other JavaScript, CSS, and image files. All the files are optimized for production with whitespace removed and the JavaScript minified.

## Creating a React and TypeScript component

## Adding a props type

## Create a new file in the src folder called Alert.tsx.

```
import { useState } from 'react';

type Props = {
  type?: string;
  heading: string;
  children: React.ReactNode;
  closable?: boolean;
  onClose?: () => void;
};

export function Alert({ type = 'information', heading, children, closable, onClose }: Props) {
  const [visible, setVisible] = useState(true);
  if (!visible) {
    return null;
  }
  function handleCloseClick() {
    setVisible(false);
    if (onClose) {
      onClose();
    }
  }
  return (
    <div>
      <div>
        <span role="img" aria-label={type === 'warning' ? 'Warning' : 'Information'}>
          {type === 'warning' ? '⚠' : 'ℹ️'}
        </span>
        <span>{heading}</span>
      </div>
      {closable && (
        <button aria-label="Close" onClick={handleCloseClick}>
          <span role="img" aria-label="Close">
            ❌
          </span>
        </button>
      )}
      <div>{children}</div>
    </div>
  );
}

```

## Rest Of The Files

```
body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen',
    'Ubuntu', 'Cantarell', 'Fira Sans', 'Droid Sans', 'Helvetica Neue',
    sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

code {
  font-family: source-code-pro, Menlo, Monaco, Consolas, 'Courier New',
    monospace;
}

```

## App.css

```
.App {
  text-align: center;
}

.App-logo {
  height: 40vmin;
  pointer-events: none;
}

@media (prefers-reduced-motion: no-preference) {
  .App-logo {
    animation: App-logo-spin infinite 20s linear;
  }
}

.App-header {
  background-color: #282c34;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: calc(10px + 2vmin);
  color: white;
}

.App-link {
  color: #61dafb;
}

@keyframes App-logo-spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

```

## index.tsx

```
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';

const root = ReactDOM.createRoot(document.getElementById('root') as HTMLElement);
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();

```

# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.\
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).
