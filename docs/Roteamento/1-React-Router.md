# O que é o React Router?

O React Router é uma biblioteca essencial em nossas aplicações devido à capacidade de criar e gerenciar as rotas da aplicação de maneira marcante e simples.

# Como instalar o React Router

Para instalar digite os comandos abaixo:

```cmd
npm install react-router-dom

yarn add react-router-dom
```

# Como usar o React Router

Então chega de teoria, e vamos praticar como usar o React Routes? Para esse exemplo criaremos uma pasta chamada 'Routes' é ela que ficara com nosso componente.

Nessa pasta criaremos o nome da nossa page como, por exemplo 'Home' e dentro dela (dois) arquivos um **index.js** e um **style.css**

>Estrutura do Index.js

```js

import React, {useEffect, useState} from 'react';
import LogoImg from '../../assents/logo.svg'
import './style.css';
import { Link, useHistory } from 'react-router-dom';
import { FiPower, FiTrash2 } from 'react-icons/fi'
import api from '../../services/api';

export default function Home() {

return (
<div>
<h1>Ola sou a Home
</div>

);
```

Feito isso podemos criar um arquivo na raiz do nosso projeto chamado 'router.js' ele que sera responsável por controlar as rotas e seus componentes. Veja o código abaixo:

'''js
import React from 'react';
import { Route, BrowserRouter } from 'react-router-dom';

import Home from './Routes/Home';

function Routes() {
return (
<BrowserRouter>
<Route path="/" exact component={Home} />
</BrowserRouter>
);
}

export default Routes;
'''
Abaixo você encontrara a explicação do routes.js
- BrowserRouter: Responsável por trocar nossa rota dependendo da URL;
- Route: Responsável por trocar nossa rota dependendo da URL;
-- **path**: Seria o nosso caminho como, por exemplo ''/login'', ''/home''
-- **exact**: Necessário apenas na primeira pagina de nossa aplicação como o /

E pronto estamos pronto para utilizar o routes em nosso App.js

'''js
import React from 'react';
import Routes from './routes';

function App() {

return (
<Routes />
);

}

export default App;
'''

E pronto a partir de agora nossas paginas são dinâmicas dependendo da URL.