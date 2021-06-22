<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

# Roteamento

O roteamento é entrega de dados com base em algo, no nosso caso a nossa url. Quando você visita o **youtube.com** você está acessando a rota padrão do youtube, mas quando acessamos por exemplo **youtube.com/feed/explore** estamos acessando a rota "*feed/explore*", o explorar do youtube. Quando construimos um site podemos ter uma página home (representada normalmente pelo "/") que por padrão seria o nosso endereço, exemplo o **www.meusite.com** mas podemos ter também a rota "*/posts* "que teriam todos os posts do nosso site.

## Roteamento com react

O react em si não possui um gerenciamento próprio de rotas, mas podemos utilizar bibliotecas como o React Router ou ferramentas como Next.js ou Gatsby que veremos em breve para criarmos a nossas rotas. Nesse módulo veremos como utilizar o React Router

## O que é o React Router?

O React Router é uma biblioteca essencial em nossas aplicações devido à capacidade de criar e gerenciar as rotas da aplicação de maneira marcante e simples.

## Como instalar o React Router

Para instalar digite um dos comandos abaixo:

```cmd
npm install react-router-dom

yarn add react-router-dom
```

## Como usar o React Router

Então chega de teoria, e vamos praticar como usar o React Router? Para esse exemplo criaremos uma pasta chamada 'Routes', é ela que ficará com nosso componente.

Nessa pasta criaremos o nome da nossa page como 'Home' e dentro dela dois arquivos um **index.js** e um **style.css**

## Construindo a rota Home

```js
import React from 'react';
import './style.css';

export default function Home() {
  return (
    <div>
      <h1>Ola sou a Home</h1>
    </div>
  );
}
```

Neste ponto você deve notar que a estrutura de cada pagina segue o mesmo padrão da App.js.

E a partir disso podemos criar um arquivo na raíz do nosso projeto chamado 'router.js' que será responsável por controlar as rotas e seus componentes. Veja o código abaixo:

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
  - **path**: seria o nosso caminho como, por exemplo ''/login'', ''/home''
  - **exact**: Responsável pela função de carregar determinada rota apenas se a URL for exatamente a pedida. Sendo ela em nosso exemplo apenas necessária na primeira página da nossa aplicação

A partir deste momento podemos colocar o componente de rotas em nosso App.js

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

E pronto! A partir de agora temos a nossa rota Home, vamos ver como mudar o compomente com base na rota no próximo capítulo.

[Ir para Próxima Seção](./2-React-Router-Switch.md)

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>
