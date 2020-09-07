<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

<p align="center">
  <h2 align="center">React4Noobs</h2>

  <h1 align="center">
  <img src="../../assets/logo.png" alt="Imagem do Reactjs" width="220">
</h1>
  
  <p align="center">
    <br />
    <a href="../README.md">Explore a documentação »</a>
    <br />
    <br />
    <a href="https://github.com/he4rt/react4noobs/issues">Report Bug</a>
    ·
    <a href="https://github.com/he4rt/react4noobs/issues">Request Feature</a>
  </p>
</p>

# O que é o React Router?

O React Router é uma biblioteca essencial em nossas aplicações devido à capacidade de criar e gerenciar as rotas da aplicação de maneira marcante e simples.

# Como instalar o React Router

Para instalar digite um dos comandos abaixo:

```cmd
npm install react-router-dom

yarn add react-router-dom
```

# Como usar o React Router

Então chega de teoria, e vamos praticar como usar o React Routes? Para esse exemplo criaremos uma pasta chamada 'Routes' é ela que ficara com nosso componente.

Nessa pasta criaremos o nome da nossa page como 'Home' e dentro dela dois arquivos um **index.js** e um **style.css**

## Estrutura do Index.js

```js

import React from 'react';
import './style.css';

export default function Home() {

return (
<div>
<h1>Ola sou a Home
</div>

);
```
A este ponto você deve notar que a estrutura de cada pagina segue o mesmo padrão da App.js.

E a partir disso podemos criar um arquivo na raiz do nosso projeto chamado 'router.js' ele que sera responsável por controlar as rotas e seus componentes. Veja o código abaixo:

```js
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
```
Abaixo você encontrará a explicação do routes.js
- BrowserRouter: Responsável por trocar nossa rota dependendo da URL;
- BrowserRouter: Responsável por observar a URL digitada e passar a informação para o **Route**;
- Route: Responsável por carregar na tela nosso componente, dependendo da URL que o BrowserRouter enviar;
-- **path**: seria o nosso caminho como, por exemplo ''/login'', ''/home''
-- **exact**: Responsável pela função de carregar determinada rota apenas se a URL for exatamente a pedida. Sendo ela em nosso exemplo apenas necessária na primeira pagina da nossa aplicação

E pronto e a partir deste  momento podemos para utilizar o routes em nosso App.js

```js
import React from 'react';
import Routes from './routes';

function App() {

return (
<Routes />
);

}

export default App;
```

E pronto a partir de agora nossas paginas são dinâmicas dependendo da URL.

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>