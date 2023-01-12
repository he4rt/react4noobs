<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../../assets/global/header-4noobs.svg">
  </a>
</p>

## O que é o TanStack Router?

Criada pelos mesmos criadores do famoso [TanStack Query](https://tanstack.com/query/latest) (antigamente chamado de `React Query`), o **TanStack Router** é um novo framework agnóstico de bibliotecas para criação de rotas de forma simples e escalável em aplicações de diversos níveis com foco em revolucionar a maneira de como são gerenciadas as rotas nessas aplicações.

Uma das principais vantagens ao se utilizar essa biblioteca é o fato de possuir um poderoso gerenciamento de cache embutido em seu núcleo, assim como o [TanStack Query](https://tanstack.com/query/latest), melhorando muito mais a experiência do usuário ao navegar em sua aplicação, que por sua vez se torna mais fluida.

Além disso, ela também é baseada em grandes ferramentas já conhecidas, tais como [React Router](https://reactrouter.com/), [Next.js](https://nextjs.org/) e [Remix](https://remix.run/), porém com uma base de código 100% reformulada visando performance, segurança e utilização de boas práticas do [TypeScript](https://www.typescriptlang.org/) e seu [Type-Safety](./1.1-Type-Safety.md), melhorando assim também a experiência do desenvolvedor, principalmente em aplicações grandes com diversas pessoas trabalhando ao mesmo tempo.

Vale ressaltar que no momento no qual este conteúdo foi produzido (jan/2023), o framework ainda está em fase beta, entretanto novas atualizações ainda serão implementadas até a versão final, que deve ser lançada em breve.

## Algumas vantagens da utilização do TanStack Router

- [x] Suporte completo ao TypeScript seguindo boas práticas com Type-Safe
- [x] Cacheamento automático (ou manual caso preferir)
- [x] Agnóstico de Frameworks (Por enquanto disponível apenas para React, mas sinta-se a vontade para [contribuir com novas implementações para o projeto](https://github.com/tanstack/router))
- [x] Pré-carregamento automática de rotas
- [x] DevTools própria para depuração
- [x] Elementos de rotas assíncronos
- [x] Validação, formatação, serialização e processamento de dados com a Search Param API

## Como instalar o TanStack Router

Para instalar o **TanStack Router** em sua aplicação, basta utilizar algum dos comandos abaixo de acordo com o seu gerenciador de pacotes:

```BASH
# Utilizando npm
npm install @tanstack/react-router@beta --save
# Utilizando Yarn
yarn add @tanstack/react-router@beta
# Utilizando pnpm
pnpm add @tanstack/react-router@beta
```

## Iniciando com o TanStack Router

Partindo para prática, no exemplo a seguir será criado uma aplicação com duas rotas, uma "Página inicial" e a página de "Sobre nós". Lembrando que a estrutura de pastas e arquivos foram apenas para uma simples exemplificação, podendo ser alterada de acordo com a necessidade/desejo do desenvolvedor.

## Construindo a estrutura das páginas

Abaixo foi criado uma estrutura de exemplo para essas páginas, onde cada uma possui um header com links para as outras páginas, e um conteúdo específico para cada uma delas.

```TSX
import React from 'react';
// importação do componente de âncora do TanStack Router
import { Link } from '@tanstack/react-router';

// ARQUIVO: pages/Home.tsx
export function Home() {
  return (
    <div>
      <header>
        <Link to="/">Página inicial</Link> <Link to="/about">Sobre nós</Link>
      </header>
      <h1>Bem-vindo ao react4noobs</h1>
    </div>
  );
}

// ARQUIVO: pages/About.tsx
export function About() {
  return (
    <div>
      <header>
        <Link to="/">Página inicial</Link> <Link to="/about">Sobre nós</Link>
      </header>
      <p>
        O projeto 4Noobs nasceu com o objetivo de ser um espaço onde as pessoas pudessem encontrar conteúdo de fácil entendimento em um primeiro encontro com determinado tema, promovendo uma melhor capacitação profissional. A intenção desse Open Source é que as pessoas de diferentes níveis de entendimento pudessem contribuir.
      </p>
    </div>
  );
}
```

## Estruturando rotas com o TanStack Router

Agora que já temos as páginas criadas, vamos criar as rotas para elas utilizando o **TanStack Router**.

```TSX
// ARQUIVO: router.ts

// Importando funções do TanStack Router
import { createReactRouter, createRouteConfig } from '@tanstack/react-router';

// Importando as páginas da aplicação
import { Home } from './pages/Home';
import { About } from './pages/About';

// Criando o gerenciador de rota
const rootRoute = createRouteConfig();

// Criando a rota para a página inicial
const homeRoute = rootRoute.createRoute({
  path: '/', // Caminho da rota
  component: Home, // Componente que será renderizado
});

// Criando a rota para a página sobre nós
const aboutRoute = rootRoute.createRoute({
  path: '/about', // Caminho da rota
  component: About, // Componente que será renderizado
});

// Adicionando as rotas ao gerenciador
const routes = [homeRoute, aboutRoute];
const routeConfig = rootRoute.addChildren(routes);

// Criando a rota com o adapter para react
const router = createReactRouter({ routeConfig });

export default router;
```
### ⭐ Habilitando o [Type-Safety](./1.1-Type-Safety.md) em aplicações com o Typescript

```TSX
declare module '@tanstack/react-router' {
  interface RegisterRouter {
    router: typeof router
  }
}
```

## Utilizando o TanStack Router na aplicação

A partir do momento que já temos as rotas criadas com o **TanStack Router**, basta utilizá-las na aplicação.

```TSX
// ARQUIVO: App.ts *ou inicializador da aplicação e semelhantes*

import React from 'react';

// Importando o provider das rotas
import { RouterProvider } from '@tanstack/react-router';

// Importando as rotas
import router from './router';

function App() {
  // Utilizando as rotas na aplicação
  return <RouterProvider router={router} />;
}

export default App;
```

E pronto! A partir de agora já é possível navegar entre as páginas da aplicação utilizando o **TanStack Router**.

[Ir para Próxima Seção](./2-Rotas-customizadas.md)

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>
