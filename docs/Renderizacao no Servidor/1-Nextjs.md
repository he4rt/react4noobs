<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

# O que é

Usando do Next.js podemos renderizar (de modo simplificado, o processo de transformar os componentes React escritos em JSX para HTML) o conteúdo da página de diferentes formas, no lado do cliente, padrão do React, chamado de _Client-Side Rendering_ (CSR), e no lado do servidor com múltiplas abordagens que serão tratadas abaixo. Por padrão o Next.js irá renderizar o máximo das páginas do projeto no lado do servidor.

# Por que devemos preferir renderizar no servidor?

As vantagens da renderização no servidor se dão de duas formas, (1) performance e (2) SEO. A performance se beneficia porque podemos "guardar" o HTML da página já pronto em servidores espalhados pelo mundo (CDN), isso também pode ocorrer com arquivos JavaScript porém além de serem maiores suas contrapartes em HTML, eles teriam de ser pegos pelo navegador do usuário e transformados em HTML, assim ganhamos velocidade no carregamento da página, lembrando que **quanto menos JavaScript for enviado para o cliente melhor**. Já para o SEO (Search Engine Optimization) a melhora vem do fato dos mecanismos de busca terem dificuldade em categorizar corretamente páginas que o conteúdo é gerado dinamicamente via JavaScript, então ao enviarmos HTML "preenchido" para o cliente facilitamos a indexação do nosso site em serviços como Google. Outra vantagem é por exemplo no caso do usuário ter uma conexão ruim, assim carregar pelo servidor é mais rápido que no cliente.

# No lado do servidor (Server-Side Rendering - SSR)

Podemos carregar dados dinamicamente, a cada request, com a função `getServerSideProps`, que deve ser exportada de uma página, dentro de um arquivo na pasta `pages`, o retorno da função é usado na população das props da página. Por exemplo, em uma rede social podemos carregar os 10 primeiros posts do feed de um usuário no lado do servidor e deixar apenas as postagens subsequentes para o navegador buscar. O SSR é, na maior parte dos casos, preferível comparado ao CSR mas ainda apresenta problemas, visto que caso alguma chamada realizada na função `getServerSideProps` leve muito tempo, o navegador irá ficar "pendurado" no request, aguardando sua resposta para mostrar o conteúdo da página

```ts
// /pages/feed/index.tsx

export default function Posts ({posts}) {
    ...
    // Logica da página
}

// Essa função será executada a cada request pela página /feed
export const getServerSideProps: GetServerSideProps = async (context) => {
    const firstPosts = await fetchPosts()

return {
    props: {
        posts: firstPosts
    },
};
```

# Geração estática (Static Site Generation - SSG)

Caso os dados apresentados na página não mudem, podemos carregá-los apenas uma vez, no build do projeto, e deixar o HTML completamente pronto, para isso usamos a função `getStaticProps`. Essa funcionalidade pode ser útil quando construindo, por exemplo, um blog, já que os dados não serão mudados constantemente. Essa abordagem é a mais performática, sempre que possível tente usá-la.

```ts
// /pages/articles/index.tsx

export default function ArticlesList ({ articles }) {
    ...
    // Logica da página
}

// Essa função será executada apenas uma vez, no build do projeto
export const getStaticProps: GetStaticProps = async (context) => {
    const articles = await getArticles()

    return {
        props: {
            // Como a propriedade e a variável tem o mesmo nome, não precisamos
            // explicitar qual propriedade deve ser assimilada, equivalente a
            // fazermos `articles: articles`
            articles
        },

}


```

# Geração estática incremental (Incremental Static Regeneration - ISR)

Caso sua página possa ser gerada em _build time_ porém o conteúdo se altera com alguma frequência podemos usar da abordagem de site estático porém que se "recarrega" em um certo intervalo de tempo, para isso passamos a propriedade `revalidate` no retorno da função `getStaticProps`, com o intervalo em segundos que a página será buildada novamente. Isso pode ser útil no caso de um e-commerce em que a página inicial tem uma sessão de itens "quentes" que mostram os itens mais vendidos nas últimas 24 horas, uma informação assim, pode facilmente ser atualizada a cada 10 minutos. Para maioria dos casos o ISR apresenta o melhor dos dois mundos, conteúdo gerado dinamicamente e alta performance, se possível seu uso é recomendado junto ao SSG.

```ts
// /pages/index.tsx

export default function Home ({ hotItems }) {
    ...
    // Logica da página
}

// Essa função será executada no build do projeto e também a cada 10 minutos
export const getStaticProps: GetStaticProps = async (context) => {
    const trendingItems = await getTrending()

    return {
        props: {
            hotItems: trendingItems
        },
        revalidate: 600 // 10 (minutos) * 60 (segundos)
}
```
