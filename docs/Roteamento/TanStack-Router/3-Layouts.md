<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank" title="Clique para visualizar mais informações sobre o projeto 4noobs">
    <img src="../../../assets/global/header-4noobs.svg" alt="Cabeçalho do repositório representado pelo logotipo da He4rt, simbolizado por um coração roxo, na esquerda e a tipografia '4 noobs by He4rt devs' na direita">
  </a>
</p>

# TanStack Router - Layouts

> 🔥 **Tá com pressa?** Se liga no sumário:
> 1. [Definição](#o-que-são-layouts-aplicado-no-contexto-de-rotas)
> 2. [Estrutura das páginas](#construindo-a-estrutura-das-páginas)
> 3. [Estrutura do Layout](#construindo-a-estrutura-do-layout)
> 4. [Estruturando as rotas](#estruturando-rotas-com-o-tanstack-router)  

## O que são Layouts aplicado no contexto de rotas?

Os Layouts são elementos geralmente utilizados para definir a estrutura padrão numa aplicação, componentes nos quais são comuns em várias páginas do aplicativo, como por exemplo o cabeçalho e o rodapé, que são usados como um container para outros componentes que representam o conteúdo específico de cada página.

No **TanStack Router** isso é feito utilizando um truque o componente <Outlet /> dentro da renderização da Parent Route.Isso permite que você mantenha a estrutura básica de suas páginas consistente, enquanto ainda sendo capaz de renderizar conteúdo dinâmico baseado na rota atual.

## Construindo a estrutura das páginas

Abaixo foi criado uma estrutura de exemplo para essas páginas, onde cada uma possui um conteúdo específico para cada uma delas.

```TSX
import React from 'react';

// ARQUIVO: pages/Home.tsx
export function Home() {
  return (
    <h1>Bem-vindo ao react4noobs</h1>
  );
}

// ARQUIVO: pages/About.tsx
export function About() {
  return (
    <p>
      O projeto 4Noobs nasceu com o objetivo de ser um espaço onde as pessoas pudessem encontrar conteúdo de fácil entendimento em um primeiro encontro com determinado tema, promovendo uma melhor capacitação profissional. A intenção desse Open Source é que as pessoas de diferentes níveis de entendimento pudessem contribuir.
    </p>
  );
}
```

## Construindo a estrutura do Layout

Abaixo foi criado uma estrutura de exemplo para um Layout, que representa o cabeçalho replicado nas páginas.

```TSX
// ARQUIVO: layouts/RootLayout.tsx
export function RootLayout() {
  return (
    <>
      {/* Esse header será replicado para as sub rotas da Parent Route que você colocar o Layout */}
      <header>
        <Link to="/">Página inicial</Link> <Link to="/about">Sobre nós</Link>
      </header>
      <hr />
      <Outlet /> {/* O Outlet representa o conteúdo da sub rota */}
    </>
  )
}
```

## Estruturando rotas com o TanStack Router

Agora que já temos as páginas criadas, vamos criar as rotas para elas utilizando o <Outlet /> do **TanStack Router**.

```TSX
// ARQUIVO: router.tsx
// Note que a extensão mudou de .ts para .tsx porque iremos inserir componentes html em sua estrutura

// Importando funções do TanStack Router
import { ReactRouter, createRouteConfig, Link, Outlet } from '@tanstack/react-router';

// Importando o Layout
import { RootLayout } from './layouts/RootLayout';

// Importando as páginas da aplicação
import { Home } from './pages/Home';
import { About } from './pages/About';

// Criando o gerenciador de rota
const rootRoute = createRouteConfig({
  component: RootLayout // Layout construido para as rotas
});

// Criando a rota para a página inicial
const homeRoute = rootRoute.createRoute({
  path: '/', // Caminho da rota
  component: Home, // Componente da rota que será renderizado
});

// Criando a rota para a página sobre nós
const aboutRoute = rootRoute.createRoute({
  path: '/about', // Caminho da rota
  component: About, // Componente da rota que será renderizado
});

// Adicionando as rotas ao gerenciador
const routes = [homeRoute, aboutRoute];
const routeConfig = rootRoute.addChildren(routes);

// Criando a rota com o adapter para react
const router = new ReactRouter({
  routeConfig,
  defaultPreload: 'intent'
});

export default router;
```

Lembrando que o exemplo acima foi utilizado um layout de escopo global, pois foi criado no `rootRoute`, porém isso pode ser replicado para outras subrotas em seus Parent Routes, que você aprendeu a fazer no módulo de [Rotas Customizadas](./2-Rotas-customizadas.md).

E pronto! A partir de agora já é possível utilizar os Layouts em sua aplicação de maneira fácil utilizando o **TanStack Router**.

[Ir para Próxima Seção](./4-Caching.md)

<p align="center">Made with 💜</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../../assets/global/footer-4noobs.svg" width="380" alt="Tipografia com o título '4 noobs by He4rt devs' e o slogan 'Da comunidade para a comunidade 💜'">
  </a>
</p>
