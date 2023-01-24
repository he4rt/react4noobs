<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank" title="Clique para visualizar mais informações sobre o projeto 4noobs">
    <img src="../../../assets/global/header-4noobs.svg" alt="Cabeçalho do repositório representado pelo logotipo da He4rt, simbolizado por um coração roxo, na esquerda e a tipografia '4 noobs by He4rt devs' na direita">
  </a>
</p>

# TanStack Router - Rotas Customizadas

> 🔥 **Tá com pressa?** Se liga no sumário:
> 1. [Children Routes](#criando-children-routes-subrotas)
> 2. [Rotas com parâmetros](#criando-rotas-com-parâmetros)
> 3. [Consumindo parâmetros](#consumindo-parâmetros-de-uma-rota)
> 4. [Navegando entre rotas](#navegando-entre-rotas)  
> 4.1 [Hook useNavigation](#utilizando-o-hook-usenavigation)  
> 4.2 [Componente Link](#utilizando-o-componente-link)  
> 5. [Navegando para rotas anteriores](#navegando-para-uma-rota-anterior)  

## Criando Children Routes (subrotas)

Children routes são rotas que são aninhadas dentro de outra rota. Elas são usadas para criar hierarquias de rotas, ou seja, criar uma estrutura de rotas para a sua aplicação.

Por exemplo, imagine que você tem uma aplicação com uma página "Perfil Logado" e essa página possui as seguintes opções de navegação: "Editar perfil" e "Alterar senha". Em vez de ter duas rotas diferentes para cada opção, você pode criar uma rota "Perfil" e aninhar as três opções de navegação dentro dela como children routes.

Dessa forma, a rota "Perfil" seria o parent route e as outras três seriam as children routes, e ao acessar a rota "perfil", a aplicação saberia que as opções de navegação estão contidas nela, e renderizaria os componentes da rota filho correspondente.

Em resumo Children routes são uma forma de organizar suas rotas de maneira hierarquica, ou seja, criando um parent route para seus componentes filho. Para criar uma children route no **TanStack Router** basta utilizar o método `createRoute` do parent route, como no exemplo abaixo:

```TSX
// ARQUIVO: routes.ts

// Importando funções do TanStack Router
import { ReactRouter, createRouteConfig } from '@tanstack/react-router';

// ... Importação das páginas

let rootRoute = createRouteConfig();

// Criando a Parent Route
const profileRoute = rootRoute.createRoute({
  path: '/profile', // Caminho da rota
});

// Criando as Children Routes
const editProfileRoute = profileRoute.createRoute({
  path: '/edit', // Caminho da rota
  component: EditProfile, // Componente que será renderizado
});
const changePasswordRoute = profileRoute.createRoute({
  path: '/change-password', // Caminho da rota
  component: ChangePassword, // Componente que será renderizado
});

// Adicionando as Children Routes ao Parent
const profileRoutes = [editProfileRoute, changePasswordRoute];
const profileRouteConfig = profileRoute.addChildren(profileRoutes);

// Adicionando as rotas ao gerenciador
const routes = [profileRouteConfig];
const routeConfig = rootRoute.addChildren(routes);

// ... Criação do Router
```

## Criando rotas com parâmetros

As rotas com parâmetros são aquelas que permitem passar dados dinâmicos através de sua URL. Isso é muito útil quando se deseja passar informações específicas, tal como o ID do usuário afim de exibir seu perfil e suas informações relacionadas.

Imagine que você é o desenvolvedor da funcionalidade de perfil público no website da He4rt e deseja exibir a página de perfil de um usuário específico quando o usuário clicar em um nome de usuário na lista de usuários. Em vez de criar uma rota para cada usuário manualmente, você pode criar uma rota única para a página de perfil e passar o ID do usuário como um parâmetro na URL.

A sintaxe para criar uma rota com parâmetros é similar a criar uma rota normal, porém o nome do parâmetro é incluído um cifrão em seu início. Por exemplo:

```TSX
// ARQUIVO: routes.ts

// Importando funções do TanStack Router
import { ReactRouter, createRouteConfig } from '@tanstack/react-router';

// ... Importação das páginas

let rootRoute = createRouteConfig();

// Criando a rota com parâmetro
const viewProfileRoute = rootRoute.createRoute({
  path: '/profile/$id',
  component: ViewProfile,
});

// Adicionando a rota ao gerenciador
const routes = [viewProfileRoute];
const routeConfig = rootRoute.addChildren(routes);

// ... Criação do Router
```

## Consumindo parâmetros de uma rota

Para consumir os parâmetros de uma rota, você pode utilizar a função `useMatch` do **TanStack Router**. Essa função retorna um objeto que inclui parâmetros da rota, e você pode desestruturar esse objeto para obter os parâmetros que deseja. Veja o exemplo abaixo:

```TSX
// ARQUIVO: ViewProfile.tsx

// Importando a função useMatch do TanStack Router
import { useMatch } from '@tanstack/react-router';

export function ViewProfile() {
  // Obtendo os parâmetros da rota
  const { params } = useMatch({
    from: "/profile/$id", // Caminho da rota, note que se você habilitou o Type-Safe, já irá se auto-completar
  });

  // Desestruturando os parâmetros
  const { id } = params;

  return (
    // Renderizando o ID do perfil
    <h1>O ID do Perfil Informado é: {id}</h1>
  )
}
```

Ao acessar a rota `/profile/1234`, o resultado esperado é que o ID do perfil seja exibido na tela como "O ID do Perfil Informado é: 1234".

## Navegando entre rotas

Para navegar entre rotas, há duas formas de fazer isso: utilizando o hook `useNavigation` ou utilizando o componente `Link`.

### Utilizando o hook `useNavigation`

O hook `useNavigation` retorna uma função que permite navegar para uma rota específica. Para utilizá-lo, basta importar a função `useNavigation` do **TanStack Router** e chamar a função retornada por ela. Veja o exemplo abaixo:

```TSX
// Importando a função useNavigation do TanStack Router
import { useNavigation } from '@tanstack/react-router';

export function ExampleRoute() {
  // Obtendo a função de navegação
  const navigate = useNavigation();

  function handleNavigateToOtherUser(id: string) {
    return navigate({
      to: "/profile/$id",
      params: { id },
    })
  }

  return (
    // Renderizando o botão de navegação
    <button onClick={() => handleNavigateToOtherUser("1234")}>
      Navegar para usuário 1234
    </button>
  )
}
```

### Utilizando o componente `Link`

O componente `Link` é um componente que permite navegar para uma rota específica. Para utilizá-lo, basta importar o componente `Link` do **TanStack Router** e passar o caminho da rota para qual você deseja navegar. Veja o exemplo abaixo:

```TSX
// Importando o componente Link do TanStack Router
import { Link } from '@tanstack/react-router';

export function ExampleRoute() {
  return (
    // Renderizando o botão de navegação
    <Link to="/profile/$id" params={{ id: "1234" }}>
      Navegar para usuário 1234
    </Link>
  )
}
```

## Navegando para uma rota anterior

Para navegar para a rota anterior, você pode utilizar a variável history desestruturada do hook `useRouter` do **TanStack Router**. Essa variável contém é um objeto que contém a função `back` que permite navegar para a rota anterior. Veja o exemplo abaixo:

```TSX
// Importando a função useRouter do TanStack Router
import { useRouter } from '@tanstack/react-router';

export function ExampleRoute() {
  // Obtendo a variável history
  const { history } = useRouter();

  function handleNavigateToPreviousRoute() {
    return history.back();
  }

  return (
    // Renderizando o botão de navegação
    <button onClick={handleNavigateToPreviousRoute}>
      Navegar para a rota anterior
    </button>
  )
}
```

E pronto! A partir de agora já é possível criar rotas dinâmicas e navegar na aplicação utilizando o **TanStack Router**.

[Ir para Próxima Seção](./3-Layouts.md)

<p align="center">Made with 💜</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../../assets/global/footer-4noobs.svg" width="380" alt="Tipografia com o título '4 noobs by He4rt devs' e o slogan 'Da comunidade para a comunidade 💜'">
  </a>
</p>
