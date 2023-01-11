<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

# Outras Rotas

Além da rota padrão (o "/") podemos ter outras rotas como "/posts", para isso precisaremos adicionar ao nosso arquivo 'routes/index.js' mais uma rota, mas como fazer isso?

## Como funciona o createBrowserRouter

O createBrowserRouter funciona como um objeto, onde você passa um array de objetos, cada objeto é uma rota, e cada rota tem um path e um componente. Veja o exemplo abaixo:

```js
const router = createBrowserRouter([
  {
    path: '/',
    element: <Home />,
  },
]);
```

Mas agora queremos alterar o nosso router para adicionar a rota de posts, e faremos da seguinte forma:

```js
const router = createBrowserRouter([
  {
    path: '/',
    element: <Home />,
  },
  {
    path: '/posts',
    element: <Posts />,
  },
]);
```

## Construindo a rota Posts

Dentro da pasta **src/pages** do projeto vamos criar uma nova pasta, agora com nome 'Posts' e dentro dela um arquivo **index.jsx**. O nosso **index.jsx** ficará assim:

```jsx
import React from 'react';
import './style.css';

export default function Posts() {
  return (
    <div>
      <p>Lorem ipsum</p>
      <span>Author - Data</span>
    </div>
  );
}
```

Vamos agora importar esse componente no arquivo 'routes/index.js', para criar uma nova rota para esse componente precisamos adicionar um novo Route com _path="/posts_"

```js
import { createBrowserRouter } from 'react-router-dom';

import Home from './pages/Home';
import About from './pages/Posts';

const router = createBrowserRouter([
  {
    path: '/',
    element: <Home />,
  },
  {
    path: '/posts',
    element: <Posts />,
  },
]);

export { router };
```

Com isso podemos agora criar exibir componentes diferentes com base na URL.

[Ir para Próxima Seção](../Cliente%20REST/1-Fetch.md)

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>
