<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../../assets/global/header-4noobs.svg">
  </a>
</p>

1. Conceitos
    1. [O que é o Next.JS?](#o-que-é-nextjs)
    2. [Por quê usar Next.JS?](#por-quê-utilizá-lo)
    3. [Somente o NextJS faz SSR?](#somente-o-nextjs-faz-ssr)
    4. [Se é framework, logo é difícil?](#frameworks-são-complexos-em-sua-construção-mas-e-em-seu-uso)
    5. [Modelos de Renderização](#funcionalidades-relacionadas-a-renderização)
        1. [Single Page Application - SPA](#single-page-application-e-client-side-rendering)
        2. [Server Side Rendering - SSR](#server-side-rendering)
        3. [Static Site Generation - SSG](#static-site-generation)
        4. [Incremental Static Regeneration - ISR](#incremental-static-regeneration)
    6. [Referências](#referências-utilizadas)

## O que é Next.JS?

O Next.JS é um framework popular de desenvolvimento front-end baseado em React e "pronto para produção", que visa acelerar o processo de construção de uma interface.

Atualmente, ele é mantido pela Vercel e em seu core há como principal proposta elevar a produtividade de um desenvolvedor com setup de zero configuração e implementações simplificadas de internacionalização, endpoints, suporte ao roteamento, Typescript, renderização ao lado do servidor, hybrid static e entre outras que podem melhorar a experiência de desenvolvimento como utilizar uma única tecnologia para desenvolver um web app completo.

### Por quê utilizá-lo?

- *Setup zero config* -> Quando iniciamos um projeto React.JS ou um projeto front-end qualquer, nós precisamos configurar um esquema de roteamento para navegação entre páginas, normalmente no contexto do React.JS utiliza-se [react-router-dom](https://github.com/he4rt/react4noobs/blob/master/docs/Roteamento/1-React-Router.md), configurar o webpack, se for prefirível, configurar o Typescript e o Babel e entre outras muitas opções dependendo do web app que vcoê está produzindo. Mas, no Next.JS, como a parte da configuração é abstraída, o desenvolvedor pode focar inteiramente no desenvolvimento de novas funcionalidades.

- *Diversos modelos de renderização* -> Permite um fluxo de trabalho produtivo e de zero configuração para utilização de diversos modelos de renderização como o Cliente-side rendering, Server-side rendering, Static Site Generation e Incremental Static Regeneration, que serão explicados ao longo desse artigo.

- *File System Routing* -> A estrutura de pastas e arquivos da sua aplicação definirá as rotas dela.

- *API endpoints* -> Uma estrutura de desenvolvimento Serverless intuitiva.

- *Suporte ao Typescript* -> Permite que você adicione facilmente tipagem estática ao seu código.

### Somente o Next.JS faz SSR?

Não, existem diversas ferramentas de bibliotecas a frameworks como o Angular, o Nuxt.JS (baseado em Vue.JS), Gatsby (também é baseado em React.JS como o Next.JS) e muitas outras tecnologias que te permitem implementar esse modelo de renderização.

### Frameworks são complexos em sua construção, mas e em seu uso?

A dificuldade que você enfrentará nas tecnologias que for aprender será sempre relativa ao seu tempo de experiência em determinado ecossistema, a sua facilidade de aprender coisas novas e dentre outros fatores, mas normalmente, corre um equívoco sobre frameworks serem majoritariamente mais difíceis.

Isso não se demonstra necessariamente sempre uma verdade, pois no mundo da programação usamos muito a palavra **abstração**, que consiste em você isolar num conceito um elemento à exclusão dos demais. Na prática, isso significa omitir/encapsular alguns conceitos.

Nesse contexto, todas configurações complexas ou não, trabalhosas ou não que você teria que fazer sem a utilização de um framework, são omitidos com a utilização de um e você acaba não tendo que se preocupar com essas questões.

Normalmente, costuma ser em torno disso a proposta de frameworks opinados, visam automatizar rotinas juntamente de aglutinar boas críticas da experiência de outros desenvolvedores para que possamos entregar um produto de melhor qualidade com maior produtividade.

> ⚠️ **Ainda sim, recomendo que evite pular etapas!** Faça como quiser, mas se você quer dominar Next.JS e sequer conhece React.JS ou até mesmo Javascript, entenda que você vai ter inúmeras dificuldades de lidar de uma vez só, a dificuldade de aprender uma linguagem de programação, entender o funcionamento da biblioteca React.JS e compreender as possiblidades que o framework Next.JS te oferece. Isso pode desanimar e atrapalhar sua trilha. Embora algumas coisas levem tempo, é importante não dar um passo maior que a perna querendo economizar tempo pois assim vai acabar gastando mais.

## Funcionalidades relacionadas a renderização

Muito do que popularizou o Next.JS foi a possibilidade de você adotar diferentes modelos de renderização numa mesma ferramenta com uma facilidade delicinha, tentarei fazer uma síntese desses modelos. Todos são funcionalidades que pretendo demonstrar na prática com Next.JS no decorrer desse texto, mas não se limite a esse artigo para entendê-los.

### Single Page Application e Client Side Rendering

Hoje, a maior parte das web apps que são desenvolvidas estão no formato Single Page Application (SPA, ou Aplicação de uma Única Página). Provalvemente, você já conhece e implementa esse formato em [React.JS](https://github.com/he4rt/react4noobs/blob/master/docs/Iniciando%20com%20React/1-Introducao.md), mas afinal, o que é isso?

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

### Incremental Static Regeneration

Esse modelo Incremental Static Regeneration (ISR - Regeneração Estática Incremental), possui a mesma ideia do SSG, com alguns benéficios adicionais, Como o re-rendering de páginas existentes em background, ou seja possibilita a geração de páginas estáticas **em tempo de execução**.

----------------

## Referências utilizadas

- [Documentação oficial do Next.JS](https://nextjs.org/docs/getting-started)
- [Documentação oficial do Next.JS traduzida para português pelo integrante Caio da he4rt](https://github.com/caioreix/NextJs4noobs)

<a href="#">Próximo -></a>

----------------

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>
