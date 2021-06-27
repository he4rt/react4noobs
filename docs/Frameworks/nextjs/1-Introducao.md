<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

Aviso:
Esta seção tem como objetivo ser um início para que você consiga começar a desenvolver aplicações Next.js

Se você quiser se aprofundar ainda mais sobre cada um desses temas e sobre o funcionamento do Next.js em si, sinta-se livre para visitar o [NextJs4noobs](https://github.com/caioreix/NextJs4noobs)!

# Next.js

> Vá ponto a ponto ou vá direto ao que você está buscando! :
>
1. Conceitos
    1. [O que é o Next.JS?](#nextjs-o-que-e)
    2. [Por quê usar Next.JS?](#nextjs-porque)
    3. [Somente o NextJS faz SSR?](#nextjs-tem-outros)
    4. [Se é framework, logo é difícil?](#framework)
    5. [Modelos de Renderização](#renderizacao)
        1. [Single Page Application - SPA](#funcionalidades-spa)
        2. [Server Side Rendering - SSR](#funcionalidades-ssr)
        3. [Static Site Generation - SSG](#funcionalidades-ssg)
        4. [Incremental Static Regeneration - ISR](#funcionalidades-ssg-isr)
2. Projeto
    1. [Hora do código, vamos a prática com um projeto!](#codigo-next-js)
    2. [Formas de criar um projeto Next.JS](#create-app)
    3. [Usando o create-next-app](#create-next-app)
    4. [Limpando estrutura do projeto](#clean-app)
    5. [Utilizando o File System Routing](#fsr)
    6. [Implementando navegação SPA](#spa)
    7. [Criando componentes](#componentization)
    8. [Estilização global e adicionando fontes](#styles)
    9. [Renderizando dados com CSR](#csr)
    10. [Recurso de SSR](#ssr)
    11. [A dádiva do SSG](#ssg)
3. [Extras](#extras)
    1. [Tipagem estática com Typescript](#integracao-typescript)
6. [Conclusão](#conclusao)
7. [Referências](#referências)

<a href="#">Próximo -></a>

## O que é Next.JS?

O Next.JS é um framework popular de desenvolvimento front-end baseado em React e "pronto para produção", que visa acelerar o processo de construção de uma interface.

Atualmente ele é mantido pela Vercel e em seu core há como principal proposta elevar a produtividade de um desenvolvedor com setup de zero configuração e implementações simplificadas de internacionalização, endpoints, suporte ao roteamento, Typescript, renderização ao lado do servidor, hybrid static e entre outras que podem melhorar a experiência de desenvolvimento como utilizar uma única tecnologia para desenvolver um web app completo.

### Por quê utilizá-lo?

- *Setup zero config* -> Quando iniciamos um projeto React.JS ou um projeto front-end qualquer, nós precisamos configurar um esquema de roteamento para navegação entre páginas, normalmente no contexto do React.JS utiliza-se [react-router-dom](inserir-link-roteamento-react4noobs), configurar o webpack, se for prefirível, configurar o Typescript e o Babel e entre outras muitas opções dependendo do web app que vcoê está produzindo. Mas, no Next.JS, como a parte da configuração é abstraída, o desenvolvedor pode focar inteiramente no desenvolvimento de novas funcionalidades.

- *Diversos modelos de renderização* -> Permite um fluxo de trabalho produtivo e de zero configuração para utilização de diversos modelos de renderização como o Cliente-side rendering, Server-side rendering, Static Site Generation e Incremental Static Regeneration, que serão explicados ao longo desse artigo.

- *File System Routing* -> A estrutura de pastas e arquivos da sua aplicação definirá as rotas dela.

- *API endpoints* -> Uma estrutura de desenvolvimento Serverless intuitiva.

- *Suporte ao Typescript* -> Permite que você adicione facilmente tipagem estática ao seu código.

### Somente o Next.JS faz SSR?

Não, existem diversas ferramentas como frameworks e bibliotecas como o Angular, o Nuxt.JS (baseado em Vue.JS), Gatsby (também é baseado em React.JS como o Next.JS) e muitas outras tecnologias que te permitem implementar esse modelo de renderização.

### Frameworks são complexos em sua construção, mas e em seu uso?

A dificuldade que você enfrentará nas tecnologias que for aprender será sempre relativa ao seu tempo de experiência em determinado ecossistema, a sua facilidade de aprender coisas novas e dentre outros fatores, mas normalmente, corre um equívoco sobre frameworks serem majoritariamente mais difíceis.

Isso não se demonstra necessariamente sempre uma verdade, pois no mundo da programação usamos muito a palavra **abstração**, que consiste em você isolar num conceito um elemento à exclusão dos demais. Na prática, isso significa omitir/encapsular alguns conceitos.

Nesse contexto, todas configurações complexas ou não, trabalhosas ou não que você teria que fazer sem a utilização de um framework, são omitidos com a utilização de um e você acaba não tendo que se preocupar com essas questões.

Normalmente, costuma ser em torno disso a proposta de frameworks opinados, visam automatizar rotinas juntamente de aglutinar boas críticas da experiência de outros desenvolvedores para que possamos entregar um produto de melhor qualidade com maior produtividade.

> ⚠️ **Ainda sim, recomendo que evite pular etapas!** Faça como quiser, mas se você quer dominar Next.JS e sequer conhece React.JS ou até mesmo Javascript, entenda que você vai ter inúmeras dificuldades de lidar de uma vez só, a dificuldade de aprender uma linguagem de programação, entender o funcionamento da biblioteca React.JS e compreender as possiblidades que o framework Next.JS te oferece. Isso pode desanimar e atrapalhar sua trilha. Embora algumas coisas levem tempo, é importante não dar um passo maior que a perna querendo economizar tempo pois assim vai acabar gastando mais ainda.

## Funcionalidades relacionadas a renderização

Muito do que popularizou o Next.JS foi a possibilidade de você adotar diferentes modelos de renderização numa mesma ferramenta com uma facilidade delicinha, tentarei fazer uma síntese desses modelos. Todos são funcionalidades que pretendo demonstrar na prática com Next.JS no decorrer desse texto, mas não se limite a esse artigo para entendê-los.

### Single Page Application e Client Side Rendering

Hoje, a maior parte das web apps que são desenvolvidas estão no formato Single Page Application (SPA, ou Aplicação de uma Única Página). Provalvemente, você já conhece e implementa esse formato em [React.JS](inserir-link-roteamento-react4noobs), mas afinal, o que é isso?

O mais relevante da SPA é o seu comportamento, do qual ao navegagar **não há recarregamento do site** que proporciona uma sensação de feedback instantâneo da página para o usuário.

O modelo de SPA surgiu como uma solução de melhoria da usabilidade e dinamismo de alguns nichos de formatos de aplicações, como dashboards. Pois, nesse modelo costuma ser feito o CSR (Client Side Rendering), isto é, quando o usuário acessa um domínio, ele recebe em seu navegador uma única página que tem seu Javascript baixado pelo navegador (provido por um CDN - Content Delivery Network, um servidor de arquivos estáticos), e **é gerada pela execução do navegador** a aplicação Javascript contida nessa página que controla todas as interações, de forma a carregar dinâmicamente os pedaços dos conteúdos que são acessados conforme o usuário interage com tal app sem recarregar a página.

Um dos principais tradeoffs desse modelo que utiliza CSR é uma depreciação no SEO (Search Engine Optimization, Otimização para Mecanismos de Busca), i.e. práticas que tem como objetivo alcançar bons rankings em mecanismos de buscas para obter maior tráfego. O SEO acaba sendo menos eficiente com CSR por causa que alguns robôs de indexação de conteúdo nos mecanismo de busca, como crawlers, não conseguem indexar tão bem por dificuldades relacionadas a baixar o Javascript.

Tal como no React, pode ser feito com o uso de useState, useEffect e uma função assíncrona, como no seguinte componente funcional:

```javascript
export default function AnyComponent() {
  const [anythings, setAnythings] = useState(null);

  const handleGetAnythings = async () => {
    const response = await fetch('https://anyapi');
    const data = await response.json();
     setAnythings(data);
  };

  useEffect(() => {
    handleGetAnythings();
  }, []);

return (
    <div>
      {anythings && (<div>anythings</div>)}
    </div>
}
```

<!-- -criar ilustração para demonstrar o fluxo do CSR -->

### Server Side Rendering

O formato Server Side Rendering (SSR - Renderização no lado do servidor), consiste num processo diferente do CSR, que ao invés de o Javascript e CSS de uma página serem carregados no client-side (navegador), são renderizados como arquivos estáticos do lado do servidor.

Nesse modelo, ao usuário acessar um domínio, é disparada uma requisição para um servidor e o dados da página **em tempo de execução** são gerados no lado do server-side, que envia o HTML completo e pronto com todos dados de navegação necessários para o client-side. E por fim, o navegador só tem o trabalho de baixar e exibir essa página.

No uso do Next.JS, com o uso do `getServerSideProps` (que demonstraremos na prática com um projeto), é possível implementar facilmente essa renderização no lado do servidor. Assim, elevando SEO, performance e segurança da sua aplicação.

Nessa função recebemos o contexto, que é um objeto contedo uma chave de parâmetros chamada params (podemos injetar algum id nesses params), também contém outras chaves relacionadas a configuração de preview (preview, previewData) e internacionalização (locale, locales, defaultLocale). E podemos retornar props para o componente do arquivo no qual ela foi declarada, uma opção de revalidate e outra de notFound.

```javascript

export async function getStaticProps(context) {
  // Algum código no Server-side
  return {
    props: {
      he4rt: 'react4noobs' // valor que poderá ser utilizado nas props do componente.
    },
  }
}
```

<!-- -criar ilustração para demonstrar o fluxo do SSR -->

### Static Site Generation

O modelo de Static Site Generation (SSG - Geração de Site Estático), apresenta um formato em que páginas estáticas são geradas no momento **em que a aplicação está sendo construída (build)**. Então, diferentemente do SSR, em que a todo momento, a cada page refresh, a página estática com os dados dinâmicos é gerada. Nesse modelo, essas informações serão geradas uma vez a cada build.

Nesse formato, ao usuário acessar um domínio, é disparada uma requisição para um servidor CDN, pois as páginas já foram geradas por um servidor **em tempo de build**, após isso o navegador recebe a página estática, baixa e constrói ela para o usuário visualizar as informações contidas nela.

Esse recurso também é de simples uso com `getStaticProps/getStaticPaths` no Next.JS. Com isso, é possível otimizar a renderização contínua de páginas que possuem informações que não mudam constantemente.

#### Incremental Static Regeneration

Esse modelo Incremental Static Regeneration (ISR - Regeneração Estática Incremental), possui a mesma ideia do SSG, com alguns benéficios adicionais, Como o re-rendering de páginas existentes em background, ou seja possibilita a geração de páginas estáticas **em tempo de execução**.

## Hora do código

Agora que entendemos um pouco sobre o que é o Next.JS na aba de conceitos. como para que ele serve, quais são os principais modelos de renderização presentes Next.JS. Finalmente, vamos ver tudo isso na prática e vou cobrir cada conceito em seu momento adequado, começando com como fazer o Setup do projeto.

Caso tenha dúvidas sobre sua implementação e queira comparar com o projeto original, ele está disponível nessa [branch](https://github.com/joaobispo2077/pokedex/tree/contrib/he4rt-react4noobs).

### Formas de criar um projeto Next.JS

- Utilizando create-next-app semelhante ao create-react-app

```
npx create-next-app nome-do-seu-app
# or
yarn create next-app nome-do-seu-app
```

Após isso, entre no diretório do seu App com `cd nome-do-seu-app`.

- Manual
  - 1º Instale os pacotes necessários:

  ```
  npm install next react react-dom
  # or
  yarn add next react react-dom
  ```  

  - 2º  Prepare os scripts necessários no arquivo `package.json`:

    ```json

  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start"
  }

  ```  
  - 3º Crie um arquivo dentro da pasta pages com uma função que retorne JSX.

------------------

### Criando um projeto e inicializando app

Com o intuito de explorar os modelos de renderização e outras funcionalidades do Next.JS eu arbitrariamente vou rodar: `yarn create next-app pokedex` e vou abrir o projeto no editor de código que eu uso.

Após o comando `yarn create next-app` ou `npx create-next-app` finalizarem a sua execução,teremos nossa pasta de projeto `pokedex` criada, entrarei nela via terminal com o comando `cd pokedex`.

Então, você verá que terá uma estrutura de pastas e arquivos semelhantes com a seguinte:

```
├───.git
│   │
│   └───(configurações do versionamento do projeto)
├───.next
│   │
│   └───(configurações do Next)
│
├───node_modules
│   │
│   └───(várias dependências)
│
├───pages
│   │   index.js
│   │   _app.js
│   │
│   └───api
│           hello.js
│
├───public
│       favicon.ico
│       vercel.svg
│
├───styles
│       globals.css
│       Home.module.css
│
├───.gitignore
│
├───package.json
│
├───README.md
│
└───yarn.lock


```

Salvo execeção de que se você utilizou o comando `npx create-next-app pokedex`, invés de um `yarn.lock`, você possuirá um `package-lock.json`, ambos para o registro/histórico dos pacotes.

Podemos perceber que de pastas temos uma chamda styles para guardarmos o CSS dos projetos temos um README.md com instruções de manuseio do projeto em inglês, também .gitignore com template pronto para ignorar arquivos e pastas que não serão interessantes versionar.

Ao observar o arquivo `package.json`, você possuirá algo semelhante a isso:

```json
{
  "name": "pokedex",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start"
  },
  "dependencies": {
    "next": "10.1.3",
    "react": "17.0.2",
    "react-dom": "17.0.2"
  }
}
```

Note que o `create next app`, que diferentemente de um `create react app` instalou a dependência next além do react e do react-dom e forneceu alguns scripts para trabalharmos com nosso app. Com isso, podemos rodar o comando o seguinte comando para inicializar nossa aplicação:

```
yarn dev
# or
npm run dev
```

Ao utilizar esse comando, se a porta 3000 do seu dispositivo estiver disponível, o app estará disponível em `http://localhost:3000` com a página de demonstração que o create next app criou em seu `./pages/index.js` com fast-refresh/hot-reload, que é o recarregamento da tela ao alterar arquivos do seu projeto Next.JS.

### Limpando estrutura de arquivos

Agora que temos nosso app rodando, vamos apagar tudo que não utilizaremos. Primeiramente, vou remover os seguintes **arquivos**:

```
├───public
│       favicon.ico
│       vercel.svg
│
├───styles
│       globals.css
│       Home.module.css
```

Ao remover esses arquivos, se o seu app estiver rodando, vão ocorrer erros de compilação por esses arquivos estarem sendo referenciados em alguns locais, então agora vamos remover a referência a esses arquivos.

Entrando em `./pages/index.js`, encontraremos um arquivo que exporta uma função chamada "Home" que retorna JSX, então no topo do arquivo removerei a seguinte importação:

```
import styles from '../styles/Home.module.css'
```

Também removerei todo o conteúdo do retorno dessa função Home para um Fragmento contendo o componente Head com o title do app tendo como "irmão" uma tag main e uma tag footer referenciando o criador do projeto, ficando o seguinte o resultado no arquivo `./pages/index.js`:

```jsx
import Head from 'next/head'

export default function Home() {
  return (
    <>
      <Head>
        <title>PokéHome</title>
      </Head>
      <main>
      </main>
      <footer>
        Projeto desenvolvido por seu-nome
      </footer>
    </>
  )
}
```

Vai notar que o projeto ainda vai falhar na compilação do código, pois precisamos remover mais uma referência que ainda não removemos. Então entraremos em `./pages/_app.js` e removeremos a importação do arquivo que não existe mais, ficando com o seguinte resultado nesse `_app.js`:

```
function MyApp({ Component, pageProps }) {
  return <Component {...pageProps} />
}

export default MyApp
```

vai notar que seu projeto voltou a compilar, e agora é exibido na tela "Projeto desenvolvido por seu-nome".

Agora que temos a estrutura do projeto mais limpa, facilita a visualização do que temos em cada pasta e arquivo.

---------

### Entendendo o básico e utilizando o File-System Router

Lembro que da primeira vez que ouvi "file-system router", eu imaginei que teria que fazer algum mapeamento das pastas e arquivos para algum tipo de função consumir esse mapeamento e gerar as rotas. Mas, na verdade, é muito mais simples que isso.

No Next.JS, esse File-system router já vem configurado e basta você utilizá-lo. E para usá-lo, basta criar um arquivo que retorna JSX dentro da pasta `./pages`.

Você também pode criar uma pasta com um arquivo index.js e isso se tornará uma rota também. Irei adicionar dentro da pasta pages, uma pasta chamada pokemon,s e dentro dessa pasta pokemons, um arquivo index.js (`./pages/pokemon/index.js`) com o seguinte JSX:

```jsx
import Head from 'next/head'

export default function Pokemons() {
  return (
    <>
      <Head>
        <title>Pokémons</title>
      </Head>
      <main>
        <section>
          <h1>Lista de pokémons</h1>

        </section>
      </main>
      <footer>
        Projeto desenvolvido por seu-nome
      </footer>
    </>
  )
}
```

Com essa página pronta, basta acessar no seu navegador o endereço `http://localhost:3000/pokemons`, assumindo que a sua porta 3000 não esteja sendo usada, se estiver, o Next.JS usará outra porta que encontrar livre e informará ela via terminal, que vai encontrar o seguinte conteúdo:

```
Lista de pokémons

Projeto desenvolvido por seu-nome
```

Por questões de organização da estrutura desse mini projeto, vou parar a execução do projeto e criar na raíz do projeto uma pasta chamada `src` e mover a pasta `pages`, `public` e `styles` para dentro da src.

Agora, basta utilizar do comando `yarn dev` ou `npm run dev` para executar novamente a aplicação e o Next.JS encontrará automaticamente a pasta "pages" e construirá as páginas da sua aplicação.

-----

### Navegando entre páginas

Primeiro, podemos notar que, atualmente, está um pouco trabalhoso navegar, quando queremos acessar a página raíz da aplicação, temos que digitar no navegador `http://localhost:3000/` e quando queremos acessar a página de pokémons, temos que digitar `http://localhost:3000/pokemons`.

Agora, vamos mudar isso adicionando botões de navegação nessas duas páginas. Iniciando pela página que está em `./src/pages/index.js`, vamos importar o componente `NextLink`de dentro de `next/link` e passar a propridade **href** como sendo da rota que queremos acessar ('/pokemons') e criaremos um botão dentro desse componente com o texto "Ver pokémons". Ficando com o seguinte código:

```jsx
import Head from 'next/head'
import NextLink from 'next/link';

export default function Home() {
  return (
    <>
      <Head>
        <title>PokéHome</title>
      </Head>
      <main>
        <NextLink href="/pokemons">
            <button>Ver pokémons</button>
        </NextLink>
      </main>
      <footer>
        Projeto desenvolvido por seu-nome
      </footer>
    </>
  )
}

```

Ao salvar o arquivo e acessar `http://localhost:3000/`, poderá  clicar no botão para ir à página de pokémons, recomendo que esteja atento ao ícone da página. Pois, assim notará que a página não recarregou, então parabéns! Você acaba de implementar uma navegação entre páginas com o comportamento de SPA :D

Se não notou a diferença, tu pode acessar a página de pokémons pelo digitando o endereço dela em seu navegador (`http://localhost:3000/pokemons`) e após isso retornar à página raíz e utilizar do botão.

Para complementar essa navegação apenas de ida, podemos fazer a volta dela. Então, basta abrirmos o arquivo `./src/pages/pokemons/index.js` e importaremos o componente NextLink novamente, entretanto mudando a propriedade **href** para a rota raíz da aplicação, sendo `href="/"`, e adicionando um botão dentro do componente NextLink com o texto "Ir para a Pokéhome". Assim, ficando com o seguinte código:

```jsx
import Head from 'next/head'
import NextLink from 'next/link';

export default function Pokemons() {
  return (
    <>
      <Head>
        <title>Pokémons</title>
      </Head>
      <main>
        <header>
          <NextLink href="/">
            <button>Ir para a Pokéhome</button>
          </NextLink>
        </header>
        <section>
          <h1>Lista de pokémons</h1>
        </section>
      </main>
      <footer>
        Projeto desenvolvido por seu-nome
      </footer>
    </>
  )
}
```

Agora, temos uma navegação com comportamento de SPA entre essas duas páginas!

-------------------

### Vamos criar um componente

Não podemos esquecer a essência de frameworks frontend, além de terem a motivação da navegação SPA muito forte, a ideia de componentização da interface também é um dos pilares.

Temos 1 excelente candidato para componentização, que é o footer, então vamos colocar a mão na massa!

Primeiro vou criar um arquivo para o componente de Footer e uma pasta, então em `./src/components/Footer.js` colocarei o seguinte conteúdo:

```javascript
export default function Footer() {
  return (
    <footer>
      Projeto desenvolvido por seu-nome
    </footer>
  )
}
```

E agora podemos importar o Footer e usar o mesmo compoennte tanto no nosso index quanto na página de pokemons. Ficando da seguinte forma index (`./src/pages/index.js`):

```javascript

import Head from 'next/head';
import NextLink from 'next/link';
import Footer from '../components/Footer';

export default function Home() {
  return (
    <>
      <Head>
        <title>PokéHome</title>
      </Head>
      <main>
        <NextLink href="/pokemons">
          <button>Ver pokémons</button>
        </NextLink>
      </main>
      <Footer />
    </>
  )
}
```

Já a página de pokémons ficará assim com a substituição do footer pelo componente de Footer:

```javascript
import Head from 'next/head';
import NextLink from 'next/link';
import Footer from '../../components/Footer';

export default function Pokemons() {
  return (
    <>
      <Head>
        <title>Pokémons</title>
      </Head>
      <main>
        <header>
          <NextLink href="/">
            <button>Ir para a Pokéhome</button>
          </NextLink>
        </header>
        <section>
          <h1>Lista de pokémons</h1>
        </section>
      </main>
      <Footer />
    </>
  )
}

```

Com isso, parabéns você acaba de criar um componente reutilizável!

-------------------------------------------------------------------

### Carregando estilos e fontes em um app Next.JS

Hora do CSS! Mas não tanto, pois não vamos aplicar grandes estilizações, e o foco não será o CSS em sim e sim te mostrar uma das várias formas de carregar estilos **globais** em uma aplicação Next.JS.

Então, vamos fazer um reset de estilos. Criarei o arquivo `./src/styles/global.css` com o seguinte conteúdo:

```css
:root {
  --main-background: #ecf1f8;
  --main-font-color:#333;
}

* {
  margin: 0;
  padding: 0;
  outline: 0;
  box-sizing:  border-box;
}

html, body, #__next {
  height: 100%;
}

body {
  font: 14px 'Bebas Neue', sans-serif;
  background: var(--main-background);
  color: var(--main-font-color);
  -webkit-font-smoothing: antialiased !important;
}

ul {
  list-style: none;
}
```

Nesse arquivo, eu declaro 2 variáveis css com cores, tendo o intuito de utilizar uma no background e outra na cor da fonte. Após isso, elimino margin, padding e outline de todos elementos, também mudo o box-sizing para border-box para caso elementos internos não "estourem para fora" de elementos que estão contidos. Também coloco uma altura de 100% no html, no  body e na div que o next criará.

Por fim, adiciono que a cor do background do body será a variável CSS de background declarada, a fonte será Bebas Neue, a cor do texto sendo a variável declarada para cor e adiciono também um antialised e desativo o estilo de listas da tag ul.

Temos que fazer uma última modificação para carregar a fonte, irei alterar o _app.js (`./src/pages/_app.js`) para:

```javascript
import Head from 'next/head';
import '../styles/global.css';

function MyApp({ Component, pageProps }) {
  return (
    <>
      <Head>
        <link rel="preconnect" href="https://fonts.gstatic.com" />
        <link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Roboto:wght@500&display=swap" rel="stylesheet" />
      </Head>
      <Component {...pageProps} />
    </>)
}

export default MyApp;

```

Peguei essa fonte no google fonts, e utilizei da tag Head para fazer o carregamento dela em todo App.

Caso queira aprofundar nas variadas formas de se utilizar CSS no Next.JS, recomendo essa [seção de NextJS4noobs](https://github.com/caioreix/NextJs4noobs/blob/master/learn/basic/assets-metadata-css/1.md#recursos-metadados-e-css)

Parabéns por ter carregado seus primeiros estilos globais no Next.js.

------------------------

### Renderização na prática com Client-side-rendering

Finalmente, alcançamos a nossa primeira renderização com cliente-side-rendering, mas não é muito diferente do que você provavelmente já conheceu no React.JS.

No arquivo `./src/pages/pokemons/index.js` vamos importar o useState e o useEffect, para no useState criarmos nosso estado de pokémons e no useEffect quando o componente renderizar pela primeira vez chamaremos uma função que dispara uma requisição HTTP para API de pokémons.

```javascript
import { useState, useEffect } from 'react';
// Ao final da explicação mostrarei como ficou o arquivo inteiro.

```

E então criremos o estado onde guardaremos esses pokémons:

```javascript
  const [pokemons, setPokemons] = useState([]);

```

E após isso escreveremos uma função assíncrona que usará a fetch API para fazer uma requisição de tipo GET na API "pokeapi" e esperaremos pelo resultado, quando obtermos a resposta, iremos converte-lá para json e por fim usaremos o setPokemons para armazenar os dados da lista de pokémons:

```javascript
  const handleLoadPokemons = async () => {
    const response = await fetch('https://pokeapi.co/api/v2/pokemon');
    const data = await response.json();
    console.log(data.results);
    setPokemons(data.results);
  };

  useEffect(() => {
    handleLoadPokemons();
  }, []);

```

E a última alteração será modificar o nosso JSX, para exibir os 20 pokémons que a API retornará, basicamente vou criar uma lista não ordenada no mesmo nível do título "Lista de pokémons" e abrirei a síntaxe de javascript colocando uma condicional de que se o estado de pokemons não é um valor falsy (valor falso) então deverá ocorrer uma iteração sobre os pokémons e para cada pokémon retornará uma li com um parágrafo escrito "Poke: " e o nome do pokémon. Da seguinte forma:

```javascript
  <ul>
    {pokemons && pokemons.map(pokemon => <li key={pokemon.name}><p>Poke: {pokemon.name}</p></li>)}
  </ul>

```

E agora, ficamos com o arquivo `./src/pages/pokemons/index.js` da seguinte forma:

```javascript
import { useState, useEffect } from 'react';
import Head from 'next/head';
import NextLink from 'next/link';
import Footer from '../../components/Footer';

export default function Pokemons() {
  const [pokemons, setPokemons] = useState([]);

  const handleLoadPokemons = async () => {
    const response = await fetch('https://pokeapi.co/api/v2/pokemon');
    const data = await response.json();
    console.log(data.results);
    setPokemons(data.results);
  };

  useEffect(() => {
    handleLoadPokemons();
  }, []);

  return (
    <>
      <Head>
        <title>Pokémons</title>
      </Head>
      <main>
        <header>
          <NextLink href="/">
            <button>Ir para a Pokéhome</button>
          </NextLink>
        </header>
        <section>
          <h1>Lista de pokémons</h1>
          <ul>
            {pokemons && pokemons.map(pokemon => <li key={pokemon.name}><p>Poke: {pokemon.name}</p></li>)}
          </ul>
        </section>
      </main>
      <Footer />
    </>
  )
}

```

Para efeitos de comparação com o próximo capítulo, vale a pena dar uma olhada na origem da página do seu navegador! No Chrome,
Firefox e Opera ao pressionar o atalho `CTRL+U` você abrirá a origem da página e
poderá constatar que é uma renderização client-side pois embora os nomes dos pokémons
estarão dispostos VISUALMENTE na página, você não vai encontrá-los no HTML da origem da página.

Você acaba de fazer a sua primeira renderização dinâmica no client-side, parabéns.

-------------------------------------------------------

### Melhorando o SEO com o poderoso Server-side rendering (SSR)

Agora você verá como é simples fazer diferentes renderizações no Next.JS, pois vamos
refatorar a renderização Client-side dos pokémons para uma renderização Server-side.

Caso não conheça o conceito de Server-side rendering, nos explicamos [aqui](link-do-futuro).

Primeiramente, apagaremos o state, o useEffect e a função que carrega os pokémons, mas também colocaremos que o componente recebe a props "pokemons".

Nosso componente da página pokemons ficará da seguinte forma:

```javascript
import Head from 'next/head';
import NextLink from 'next/link';
import Footer from '../../components/Footer';

export default function Pokemons({ pokemons }) {

  return (
    <>
      <Head>
        <title>Pokémons</title>
      </Head>
      <main>
        <header>
          <NextLink href="/">
            <button>Ir para a Pokéhome</button>
          </NextLink>
        </header>
        <section>
          <h1>Lista de pokémons</h1>
          <ul>
            {pokemons && pokemons.map(pokemon => <li key={pokemon.name}><p>Poke: {pokemon.name}</p></li>)}
          </ul>
        </section>
      </main>
      <Footer />
    </>
  )
}

```

E para fechar com chave de ouro exportaremos uma função com o nome de `getServerSideProps`,
pois o Next.JS vai detectar que essa função foi exportada e vai possibilitar
a página utilizar um mecanismo de Server-side rendering no código por causa que essa função executará
no lado do servidor.

No corpo dela, faremos um fetch para a API de pokémons, converteremos a resposta em json e retornaremos
a props "pokemons" contendo o valor dos resultados da API. Ficando dessa forma a função:

```javascript
export async function getServerSideProps(context) {
  const response = await fetch('https://pokeapi.co/api/v2/pokemon');
  const data = await response.json();

  return {
    props: {
      pokemons: data.results
    },
  }
}

```

Após essa modificações, o arquivo inteiro da página de pokemons deve estar assim:

```javascript
import Head from 'next/head';
import NextLink from 'next/link';
import Footer from '../../components/Footer';

export default function Pokemons({ pokemons }) {

  return (
    <>
      <Head>
        <title>Pokémons</title>
      </Head>
      <main>
        <header>
          <NextLink href="/">
            <button>Ir para a Pokéhome</button>
          </NextLink>
        </header>
        <section>
          <h1>Lista de pokémons</h1>
          <ul>
            {pokemons && pokemons.map(pokemon => <li key={pokemon.name}><p>Poke: {pokemon.name}</p></li>)}
          </ul>
        </section>
      </main>
      <Footer />
    </>
  )
}

export async function getServerSideProps(context) {
  const response = await fetch('https://pokeapi.co/api/v2/pokemon');
  const data = await response.json();

  return {
    props: {
      pokemons: data.results
    },
  }
}

```

Para efeitos de comparação com a renderização no client-side, vale a pena dar
uma olhada na origem da página do seu navegador! No Chrome, Firefox e Opera ao
pressionar o atalho `CTRL+U` você abrirá a origem da página.

Assim, poderá constatar que é uma renderização Server-side pois todos seus pokemons
já vão estar no HTML da origem da página.

Parabéns por concluir sua primeira renderização no server-side com Next.js.

--------------------------------------------------------------------------------------------------------------------------

### Implementando a geração de páginas estáticas (SSG)

#### Geração estática de páginas estáticas

Como sabemos que nossa página de listagem dos 20 primeiros pokémons dificilmente mudará, abre chance
de implementarmos a geração dessa página no momento de Build da aplicação ao invés do formato atual em que cada vez que
a página é acessada essa informação é processada pelo servidor. Para saber mais sobre SSG, clique [aqui](link-do-futuro).

Para mudar, basta trocar o nome da nossa função de `getServerSideProps` para `getStaticProps` no arquivo `./src/pages/pokemons/index.js`.
Apenas com essa mudança está finalizada a implementação de geração de páginas estáticas. Ficará da seguinte forma:

```javascript
export async function getStaticProps(context) {
  const response = await fetch('https://pokeapi.co/api/v2/pokemon');
  const data = await response.json();

  return {
    props: {
      pokemons: data.results
    },
  }
}

```

Agora você acaba de implementar a geração estática de páginas estáticas, mas vamos aprofundar na geração dinâmica também!

#### Geração dinâmica de páginas estáticas

Antes de fazermos geração dinâmica de páginas estáticas vamos criar uma página dinâmica,
mas antes disso vamos alterar a página de listagem de pokemons para que ela tenha um botão com um Link do Next para uma
página de detalhes de cada pokemon!

```javascript
import Head from 'next/head';
import NextLink from 'next/link';
import Footer from '../../components/Footer';

export default function Pokemons({ pokemons }) {

  return (
    <>
      <Head>
        <title>Pokémons</title>
      </Head>
      <main>
        <header>
          <NextLink href="/">
            <button>Ir para a Pokéhome</button>
          </NextLink>
        </header>
        <section>
          <h1>Lista de pokémons</h1>
          <ul>
            {pokemons && pokemons.map(pokemon => (
              <li key={pokemon.name}>
                <p>Poke: {pokemon.name}</p>
                <NextLink
                  href="/pokemons/[name]"
                  as={`/pokemons/${pokemon.name}`}
                >
                  Ver detalhes
                </NextLink>
              </li>
            ))}
          </ul>
        </section>
      </main>
      <Footer />
    </>
  )
}

export async function getStaticProps(context) {
  const response = await fetch('https://pokeapi.co/api/v2/pokemon');
  const data = await response.json();

  return {
    props: {
      pokemons: data.results
    },
  }
}

```

Repare que passamos o href com uma sinalização de "[name]", para indicar que
será referente a rota dinâmica que criaremos, também passei uma propriedade "as"
para o componente de Link do Next indicando que queremos ir ao Path referente ao nome do pokemon.

Depois dessa etapa, precisamos criar essa página dinâma com roteamento dinâmico, e a forma que faremos
será criando um arquivo chamado `[name].js` em `./src/pages/pokemons/[name].js`.

Nesse arquivo retornaremos a função Pokemon que retornará o JSX que será disposto nessa página de detalhes
do pokemon:

```javascript
import Head from "next/head";
import NextLink from 'next/link';

export default function Pokemon({ pokemon }) {
  return (
    <div>
      {pokemon && (
        <>
          <Head>
            <title>{pokemon.name.toUpperCase()}</title>
          </Head>
          <NextLink href="/pokemons">
            <button>Ir para a lista de Pokemon</button>
          </NextLink>
          <h1>Nome: {pokemon.name}</h1>
          <p>Ordem: {pokemon.order}</p>
          <p>Experiência base: {pokemon.base_experience}</p>
          <h4>Formas</h4>
          <ul>
            {pokemon.forms.length && pokemon
              .forms.map(form => <li key={form.name}>{form.name}</li>)}
          </ul>
        </>
      )}
    </div>
  )
}

```

Repare que colocamos o operador de curto-circuito para definir ques se a propriedade pokemon existir então
será renderizado os detalhes do pokemon. E logo abaixo adicionaremos duas funções sendo o `getStaticProps` e o `getStaticPaths`.

No `getStaticProps` pegaremos o nome do pokémon que estará nos parâmetros do contexto da página, e então disparemos uma requisição para API de pokemon
para termos os dados do detalhe desse pokemon, convertemos para JSON e retornamos com propriedade do componente:

```javascript
export async function getStaticProps(context) {
  const { name } = context.params;
  const response = await fetch(`https://pokeapi.co/api/v2/pokemon/${name}`);
  const pokemon = await response.json();

  return {
    props: {
      pokemon
    },
  }
}

```

Já no `getStaticPaths` retornaremos os caminhos das páginas dinâmicas que queremos renderizar no momento do Build e também passamos
definimos como `true` o valor da chave fallback, que se estiver como `false` todas páginas dinâmicas que tentarmos acessar que não estiverem nos paths teremos
como resposta "not found", pois o Next.JS não fara nada a respeito delas. Agora se colocarmos o valor de  `true`
o Next.JS vai tentar gerar essa página, segue a função do getStaticPaths:

```javascript
export async function getStaticPaths(context) {
  // É possível inserir uma lógica que obtém esses caminhos de um banco de dados, API ou até arquivo.
  return {
    paths: [
      { params: { name: 'charmander' } },
      { params: { name: 'bulbasaur' } },
      { params: { name: 'squirtle' } },
    ],
    fallback: true
  }
}

```

Ao fim disso, teremos o seguinte conteúdo no arquivo de `./src/pages/pokemons/[name].js`:

```javascript
import Head from "next/head";
import NextLink from 'next/link';

export default function Pokemon({ pokemon }) {

  return (
    <div>
      {pokemon && (
        <>
          <Head>
            <title>{pokemon.name.toUpperCase()}</title>
          </Head>
          <NextLink href="/pokemons">
            <button>Ir para a lista de Pokemon</button>
          </NextLink>
          <h1>Nome: {pokemon.name}</h1>
          <p>Ordem: {pokemon.order}</p>
          <p>Experiência base: {pokemon.base_experience}</p>
          <h4>Formas</h4>
          <ul>
            {pokemon.forms.length && pokemon
              .forms.map(form => <li key={form.name}>{form.name}</li>)}
          </ul>
        </>
      )}
    </div>
  )
}

export async function getStaticProps(context) {
  const { name } = context.params;
  const response = await fetch(`https://pokeapi.co/api/v2/pokemon/${name}`);
  const pokemon = await response.json();

  return {
    props: {
      pokemon
    },
  }
}

export async function getStaticPaths(context) {
  return {
    paths: [
      { params: { name: 'charmander' } },
      { params: { name: 'bulbasaur' } },
      { params: { name: 'squirtle' } },
    ],
    fallback: true
  }
}
```

### Regeneração incremental de páginas estáticas (ISR)

 Em nosso último modelo de renderização, veremos que caso exista chance da nossa listagem dos primeiros 20 pokemons mudar antes do próximo Build, significa que se não atualizarmos nossa aplicação, teremos dados desatualizados!

 Então, para isso não ocorrer, vamos definir um intervalo em segundos que para após a primeira solicitação daquela página a cada vez que aquele tempo decorrer a página em questão será gerada novamente em tempo de execução da aplicação e em background com o benefício de que se 2 usuários acessarem o mesmo conteúdo, ele será gerado novamente apenas 1 única vez.

 Para fazer isso basta retornamos a propriedade revalidate no `getStaticProps` com o intervalo de tempo que queremos que a página será gerada novamente, então nosso arquivo `./src/pages/pokemons/index.js` ficará da seguinte forma (repare na função getStaticProps retornando um revalidate de 15 segundos):

 ```javascript
 import Head from 'next/head';
import NextLink from 'next/link';
import Footer from '../../components/Footer';

export default function Pokemons({ pokemons }) {

  return (
    <>
      <Head>
        <title>Pokémons</title>
      </Head>
      <main>
        <header>
          <NextLink href="/">
            <button>Ir para a Pokéhome</button>
          </NextLink>
        </header>
        <section>
          <h1>Lista de pokémons</h1>
          <ul>
            {pokemons && pokemons.map(pokemon => (
              <li key={pokemon.name}>
                <p>Poke: {pokemon.name}</p>
                <NextLink
                  href="/pokemons/[name]"
                  as={`/pokemons/${pokemon.name}`}
                >
                  Ver detalhes
                </NextLink>
              </li>
            ))}
          </ul>
        </section>
      </main>
      <Footer />
    </>
  )
}

export async function getStaticProps(context) {
  const response = await fetch('https://pokeapi.co/api/v2/pokemon');
  const data = await response.json();

  return {
    props: {
      pokemons: data.results
    },
    revalidate: 15
  }
}

 ```

 Parabéns, você mandou bem, acaba de explorar os principais modelos de renderização do Next.JS, se mantenha estudando, incremente seu projeto e poste nas redes sociais marcando os canais de comunicação da he4rt!

## Tipagem estática com Next.JS

Para começar um projet Next.JS com TypeScript basta utilizar um dos seguintes comandos:

```
npx create-next-app --ts
# ou
yarn create next-app --typescript
```

Agora para adicionar TypeScript a um projeto Next.JS existente acredito que uma boa forma dde se fazer é instalando o typescript e as tipagens do React como dependência de desenvolvimento:

```
npm install --dev typescript @types/react
# ou
yarn add --dev typescript @types/react

```

Após isso, crie um arquivo .ts ou .tsx na pasta pages, pode ser um "teste.ts" ou "teste.tsx" que na próxima vez que você rodar o script de "dev":

```
npm run dev
# ou
yarn dev
```

O Next.JS irá criar um tsconfig.json e um next.d.ts.

E pronto já poderá adicionar tipagem estática a sua base de código Javascript.

---------------------------------------------------------------

## Conclusão

Nesse artigo fomos do absoluto início, que seria da definição do Next.js e passamos tanto por conceitos quanto por implementações com essa ferramenta, parabéns por ter chegado até aqui e espero que tenhamos contribuído com o seu conhecimento.

Continue compartilhando conhecimento participando da comunidade da he4rt! Saiba que sempre tem alguém que você poderá ajudar.

Caso tenha ficado alguma dúvida em relação ao projeto final, fica de referência a [branch](https://github.com/joaobispo2077/pokedex/tree/contrib/he4rt-react4noobs) do projeto com cada commit em que foi criado.

## Referências utilizadas

- [Documentação oficial do Next.JS](https://nextjs.org/docs/getting-started)
- [Documentação oficial do Next.JS traduzida para português pelo integrante Caio da he4rt](https://github.com/caioreix/NextJs4noobs)

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>
