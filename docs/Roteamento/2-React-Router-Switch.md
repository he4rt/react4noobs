<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

# Outras Rotas

Além da rota padrão (o "/") podemos ter outras rotas como  "/posts", para isso precisaremos utilizar outro componente do React Router, o Switch.

## Como funciona o Switch

O Switch irá pegar e renderizar a primeira rota o seu path (caminho) que corresponder a URL. Observando que o arquivo 'router.js', construido no capítulo anterior, sem o switch temos apenas uma rota e no caso a nossa rota padrão:

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

Mas agora queremos alterar o nosso 'router.js' para utilizar o Switch, com isso precisamos importar o Switch do 'react-router-dom' e envolver os nosso Router com o Switch:

```js
import React from 'react';
import { Route, BrowserRouter, Switch } from 'react-router-dom';

import Home from './Routes/Home';

function Routes() {
  return (
    <BrowserRouter>
      <Switch>
        <Route path="/" exact component={Home} />
      </Switch>
    </BrowserRouter>
  );
}

export default Routes;
```

## Construindo a rota About

Dentro da pasta **src/Routes** do projeto vamos criar uma nova pasta, agora com nome 'About' e dentro dela um arquivo **index.js**. O nosso **index.js** ficará assim:

```js
import React from 'react';
import './style.css';

export default function About() {
  return (
    <div>
      <h1>Olá, estamos na página About!</h1>
    </div>
  );
}
```

Vamos agora importar esse componente no arquivo 'router.js', para criar uma nova rota para esse componente precisamos adicionar um novo Route com *path="/about*" e utilizaremos a propriedade *exact* já que só devemos renderizar o componente About quando visitarmos a sua rota:

```js
import React from 'react';
import { Route, BrowserRouter, Switch } from 'react-router-dom';

import Home from './Routes/Home';
import About from './Routes/About';

function Routes() {
  return (
    <BrowserRouter>
      <Switch>
        <Route path="/" exact component={Home} />
        <Route path="/about" exact component={About} />
      </Switch>
    </BrowserRouter>
  );
}

export default Routes;
```

Com isso podemos agora criar exibir componentes diferentes com base na URL.

[Ir para Próxima Seção](../Cliente%20REST/1-Fetch.md)

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>
