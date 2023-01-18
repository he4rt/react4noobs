<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank" title="Clique para visualizar mais informações sobre o projeto 4noobs">
    <img src="../../../assets/global/header-4noobs.svg" alt="Cabeçalho do repositório representado pelo logotipo da He4rt, simbolizado por um coração roxo, na esquerda e a tipografia '4 noobs by He4rt devs' na direita">
  </a>
</p>

# React Router - Introdução

> 🔥 **Tá com pressa?** Se liga no sumário:
> 1. [O que é](#o-que-é-o-react-router)
> 2. [Vantagens](#algumas-vantagens-da-utilização-do-react-router)
> 3. [Instalação](#como-instalar-o-react-router)
> 4. [Mão no código](#iniciando-com-o-react-router)  
> 4.1 [Estrutura das páginas](#construindo-a-estrutura-das-páginas)  
> 4.2 [Estruturando as rotas](#estruturando-rotas-com-o-react-router)  
> 4.3 [Utilizando na aplicação](#utilizando-o-react-router-na-aplicação)

## O que é o React Router?

Atualmente mantido pelo mesmo grupo de criadores do famoso framework web [Remix](https://remix.run/), o **React Router** é uma biblioteca para criação de rotas em aplicações React. Ele permite que você defina rotas para diferentes URLs em seu aplicativo e gerencie como os componentes são exibidos de acordo com essas rotas. Isso é essencial em diferentes tipos de aplicações devido à capacidade de criar e gerenciar as rotas da aplicação de maneira marcante e simples.

Ele foi um dos principais pioneiros do ramo de roteamento de aplicativos de página única (SPAs) e é amplamente utilizado na comunidade do React devido a sua facilidade de uso e flexibilidade. Ele permite que você defina rotas aninhadas, gerencie parâmetros de URL e proteja rotas com autenticação e autorização. Além disso também fornece recursos como navegação programática, gerenciamento de histórico e geração de rotas dinâmicas. 

Ele também possui uma grande compatibilidade com bibliotecas e ferramentas externas, como [Redux](../../Controle%20de%20estado/2-Redux.md), para ajudar a gerenciar o estado global do aplicativo. Em resumo, o React Router é uma ferramenta poderosa para gerenciar a navegação em aplicativos React.

## Algumas vantagens da utilização do React Router

- [x] Possui uma impecável [documentação](https://reactrouter.com/)
- [x] É vastamente utilizado, entretanto obter ajuda/informações é muito fácil
- [x] Possui inúmeros hooks para carregamento e gerenciamento de dados internos e externos, navegação entre páginas, obtenção de parâmetros, dentre outros

## Como instalar o React Router

Para instalar o **React Router** em sua aplicação, basta utilizar algum dos comandos abaixo de acordo com o seu gerenciador de pacotes:

```BASH
# Utilizando npm
npm install react-router-dom
# Utilizando Yarn
yarn add react-router-dom
# Utilizando pnpm
pnpm add react-router-dom
```

## Iniciando com o React Router

Partindo para prática, no exemplo a seguir será criado uma aplicação com duas rotas, uma "Página inicial" e a página de "Sobre nós". Lembrando que a estrutura de pastas e arquivos foram apenas para uma simples exemplificação, podendo ser alterada de acordo com a necessidade/desejo do desenvolvedor.

## Construindo a estrutura das páginas

Abaixo foi criado uma estrutura de exemplo para essas páginas, onde cada uma possui um header com links para as outras páginas, e um conteúdo específico para cada uma delas.

```TSX
import React from 'react';
// importação do componente de âncora do React Router
import { Link } from 'react-router-dom';

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

## Estruturando rotas com o React Router

Agora que já temos as páginas criadas, vamos criar as rotas para elas utilizando o **React Router**.

```TSX
// ARQUIVO: router.ts

// Importando funções do React Router
import { createBrowserRouter } from 'react-router-dom';

// Importando as páginas da aplicação
import { Home } from './pages/Home';
import { About } from './pages/About';

// Criando a rota para a página inicial
const homeRoute = {
  path: '/' // Caminho da rota
  element: <Home /> // Componente que será renderizado
}

// Criando a rota para a página sobre nós
const aboutRoute = {
  path: '/about', // Caminho da rota
  element: About, // Componente que será renderizado
};

// Adicionando as rotas ao gerenciador
const routes = [homeRoute, aboutRoute];

// Criando o gerenciador de rotas com o adapter para navegadores
const router = createBrowserRouter([routes]);

export default router;
```

### Qual a função do `createBrowserRouter`?
O `createBrowserRouter` é uma função responsável por armazenar as rotas da aplicação web. Além de utilizar do DOM History API para fazer a alteração da rota e cuidar de toda o histórico de navegação da página. Dentro dela é possível ter um Array (Lista) de objetos, onde cada um deles é uma rota da aplicação, seguindo a seguinte estrutura:
  - **path**: Responsável por identificar o caminho da rota, como por exemplo `'/signin'` e `'/signup'`.
  - **element**: Responsável por renderizar o componente que será exibido na rota.

## Utilizando o React Router na aplicação

A partir do momento que já temos as rotas criadas com o **React Router**, basta utilizá-las na aplicação aplicando o Provider do próprio **React Router**, como mostra o exemplo a seguir:

```TSX
// ARQUIVO: main.tsx *ou inicializador da aplicação e semelhantes*

import React from 'react';
import ReactDOM from 'react-dom/client';

// Importando o provider das rotas
import { RouterProvider } from 'react-router-dom';

// Importando as rotas
import router from './router';

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <RouterProvider router={router} />
  </React.StrictMode>
);
```

E pronto! A partir de agora já é possível navegar entre as páginas da aplicação utilizando o **React Router**.

[Ir para Próxima Seção](./2-Rotas-customizadas.md)

<p align="center">Made with 💜</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../../assets/global/footer-4noobs.svg" width="380" alt="Tipografia com o título '4 noobs by He4rt devs' e o slogan 'Da comunidade para a comunidade 💜'">
  </a>
</p>
