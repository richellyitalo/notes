- [Estilos](#estilos)
  - [Estilos globais (styled-components)](#estilos-globais)

# Estilos
## Estilos globais
Pré-requisitos:\
 - Instalar o pacote: `yarn add styled-components`\

Arquivo **'styles/global.js'**
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

Arquivo **'App.js'**
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