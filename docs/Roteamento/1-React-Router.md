<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

# Roteamento

O roteamento é entrega de dados com base em algo, no nosso caso a nossa url. Quando você visita o **youtube.com** você está acessando a rota padrão do youtube, mas quando acessamos por exemplo **youtube.com/feed/explore** estamos acessando a rota "_feed/explore_", o explorar do youtube. Quando construimos um site podemos ter uma página home (representada normalmente pelo "/") que por padrão seria o nosso endereço, exemplo o **www.meusite.com** mas podemos ter também a rota "_/posts_ "que teriam todos os posts do nosso site.

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

Então chega de teoria, e vamos praticar como usar o React Router? Para esse exemplo criaremos uma pasta chamada 'pages', é ela que ficará com nossas páginas e seus respectivos componentes.

Nessa pasta criaremos o nome da nossa page como 'Home' e dentro dela dois arquivos um **index.jsx** e um **style.css**

## Construindo a rota Home

```jsx
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

Neste ponto você deve notar que a estrutura de cada pagina segue o mesmo padrão da App.jsx.

E a partir disso podemos criar um arquivo na pasta 'routes' chamado index.js que será responsável por controlar as rotas e seus componentes. Veja o código abaixo:

```js
import { createBrowserRouter } from 'react-router-dom';
import Home from '../pages/Home';

const router = createBrowserRouter([
  {
    path: '/',
    element: <Home />,
  },
]);

export { router };
```

Abaixo você encontrará a explicação do routes.js

- CreateBrowserRouter: é uma função responsável por armazenar as rotas da aplicação web. Além de utilizar do DOM History API para fazer a alteração da rota e cuidar de toda o histórico de navegação da página. Dentro dela é possível ter um Array (Lista) de objetos, onde cada um deles é uma rota da aplicação, seguindo a seguinte estrutura:
  - **path**: seria o nosso caminho como, por exemplo ''/login'', ''/home''.
  - **element**: Responsável por renderizar o componente que será exibido na rota.

A partir deste momento podemos colocar o objeto de rotas em nosso main.jsx, que é o nosso arquivo principal da aplicação. Utilizando o Provider do próprio react-router-dom, como no exemplo a seguir:

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import { RouterProvider } from 'react-router-dom';
import { router } from './routes';

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <RouterProvider router={router} />
  </React.StrictMode>
);
```

E pronto! A partir de agora temos a nossa rota Home, vamos ver como mudar o compomente com base na rota no próximo capítulo.

[Ir para Próxima Seção](./2-React-Router-More-Pages.md)

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>
