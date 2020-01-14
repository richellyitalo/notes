- [Styles](#styles)
  - [Global styles (styled-components)](#global-styles)
- [Dev dependencies](#dev-dependencies)
  - [Root Import (Absolute path to imports)](#root-import-absolute-path-to-imports)
- [Store](#store)
  - [Redux + Saga + Reactotron (DEBUG)](#redux--saga--reactotron-debug)

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
# Store
## Redux + Saga + Reactotron (DEBUG)
Pre requisites: 
  - `yarn add redux react-redux redux-saga reactotron-redux reactotron-redux-saga immer`

File **'store/modules/auth/reducer.js'**
```js
const INITIAL_STATE = {};
export default function auth(state = INITIAL_STATE, action) {
  switch (action.type) {
    default:
      return state;
  }
}
```

File **'store/modules/auth/actions.js'**
```js
// action functions
```

File **'store/modules/auth/sagas.js'**
```js
import { all } from 'redux-saga/effects';

export default all([])
```

File **'store/modules/rootReducer.js'**
```js
import { combineReducers } from 'redux';
import auth from './auth/reducer';

export default combinReducers({ auth });
```

File **'store/modules/rootSaga.js'**
```js
import { all } from 'redux-saga/effects';
import auth from './auth/reducers.js';

export default function* rootSaga() {
  return yield all([auth]);
}
```

File **'config/ReatotronConfig.js'**
```js
import Reactotron from 'reactotron-react-js';
import { reactotronRedux } from 'reactotron-redux';
import reactotronSagaPlugin from 'reactotron-redux-saga';

if (process.env.NODE_ENV === 'development') {
  const tron = Reactotron
    .configure()
    .use(reactotronRedux())
    .use(reactotronSagaPlugin())
    .connect();

    tron.clear();

    // hack tron in console :D
    console.tron = tron;
}
```

File **'store/createStore.js'**
```js
import { createStore, compose } from 'redux';

export default (reducers, middlewares) => {
  const enhancer = process.env.NODE_ENV === 'development'
    ? compose(console.tron.createEnhancer(), applyMiddleware(...middlewares))
    : applyMiddleware(...middlewares);

  return createStore(reducers, enhancer);
}
```

File **'store/index.js'**
```js
import createStore from './createStore';
import createSagaMiddleware from 'redux-saga';

import rootReducer from './modules/rootReducer';
import rootSaga from './modules/rootSaga';

const sagaMonitor = process.env.NODE_ENV === 'develpment'
  ? console.log.createSagaMonitor()
  : null;

const sagaMiddleware = createSagaMiddleware({ sagaMonitor });

const middlewares = [sagaMiddleware];

const store = createStore(rootReducer, middlewares);

sagaMiddleware.run(rootSaga);
```

File **'App.js'**
```js
import { Provider } from 'react-redux';

import './config/ReactotronConfig'; // before Store

import store from './store'; // after ReactotronConfig

// ...

function App() {
  return (
    <Provider store={store}>
      {/*components app*/}
    </Provider>
  )
}

// ...
```