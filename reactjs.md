- [Styles](#styles)
  - [Global styles (styled-components)](#global-styles)
- [Dev dependencies](#dev-dependencies)
  - [Root Import (Absolute path to imports)](#root-import-(absolute-path-to-imports))

# Styles
## Global styles
Pre requisites:
 - Install the lib: `yarn add styled-components`

File **'styles/global.js'**
```js
import { createGlobalStyle } from 'styled-components';

import background from '../assets/images/background.svg';

export default createGlobalStyle`
  @import url('https://fonts.googleapis.com/css?family=Roboto&display=swap');

  * {
    margin: 0;
    padding: 0;
    outline: 0;
    box-sizing: border-box;
  }
  /* ... */
`;
```

File **'App.js'**
```js
// ..
import GlobalStyle from './styles/global';

function App() {
  
export default function App() {
  return (
    <BrowserRouter>
      <Routes />

      <GlobalStyle />
    </BrowserRouter>
  );
}
```

# Dev dependencies
## Root Import (Absolute path to imports)
Pre requisites:
 - Install the lib: `yarn add customize-cra react-app-rewired babel-plugin-root-import eslint-import-resolver-babel-plugin-root-import -D`

File **'config-overrides.js'** *(overriding configs react-app)*
```js
const { addBabelPlugin, override } = require('customize-cra');

module.exports = override(
  addBabelPlugin([
    'babel-plugin-root-import',
    {
      rootPathSuffix: 'src',
    },
  ])
);
```

File **'package.json'** *(changing start, buld and test app scripts)*
```json
{
  "name": "app",
  // ... 
  "scripts": {
    "start": "react-app-rewired start", // replace 'react-scripts' to 'react-app-rewired'
    "build": "react-app-rewired build",
    "test": "react-app-rewired test",
    "eject": "react-scripts eject"
  },
  // ...
}
```

File **'.eslintrc'** *(to eslint dont appear errors)*
```js
module.exports = {
  // ...
  settings: {
    'import/resolver': {
      'babel-plugin-root-import': {
        rootPathSuffix: 'src',
      },
    },
  },
};

```

File **'jsconfig.json'** *(to vscode recognize)*
```json
{
  "compilerOptions": {
    "baseUrl": "src",
    "paths": {
      "~/*": ["*"]
    }
  }
}
```