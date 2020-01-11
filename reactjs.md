- [Styles](#styles)
  - [Global styles (styled-components)](#global-styles)

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