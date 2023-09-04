<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

# O que é o GraphQL?

[GraphQL](2) é um padrão de API conceitualizada e usada pelo time de engenharia do Facebook desde 2012 e da por uma grande comunidade que inclui [empresas](8) e [membros ativos](9), o intuito do graphql não é substituir o [_REST_](5) como um novo conceito de paradigma de [_API_](6), mas sim entender a análise de dados de uma perspectiva diferente, é possível utilizar REST e Graphql ao mesmo tempo, tudo depende das necessidades do software a ser desenvolvido.

# O conceito do GraphQL

## História

Por que foi criado?

- Uma forma diferente de entender e manipular os dados.

  Para explicar isso, vamos tentar entender a cor azul.
  Imagina que você tem uma tabela "cores" com a cor azul, vermelha, amarela, etc.
  Agora imagina que está tentando entender o que ela significa no seu conjunto de dados.

  Se você tem um database sobre carros, a cor azul simboliza a cor do carro.
  Mas se você tem uma database sobre psicologia, a cor azul pode simbolizar que o paciente está deprimido, ou chateado [(pacientes da lingua inglesa)](10), ou que ele está feliz [(pacientes brasileiros)](11).

  Isso significa que se você quiser entender o que a cor azul representa no seu conjunto de dados, terá que ter em mão muito mais do que somente o recurso da tabela cores.

  Será necessário ter mais dados juntos com a cor azul para ser capaz de entender o que ela significa.

- Qual o problema que o facebook queria resolver?

  O problema do facebook era a necessidade em ter uma API e um sistema de dados que fossem faceis de entender e que pudessem ser usados por muitos ao mesmo tempo.

  Era necessario entender por exemplo, pessoas que gostam da cor preta, também gostam de heavy metal?

  Eu posso oferecer uma propaganda de chinelo para uma pessoa que estar saindo de férias para florianópolis?

  Mas como fazer isso quando você usa um padrão de API que isola os dados do seu sistema?

  Como fazer isso quando você tem muitos dados?

  Como fazer isso em pequenas requisições?

Vamos agora tentar melhorar a compreensão do [GraphQL](2), já que ele é muito amplo, vou lhe apresentar alguns exemplos.

## Exemplos

Em um Instagram, precisamos exibir os dados especifico de um usuário. Nessa página temos, username, posts, bio, stories... Como podemos fazer solução com [_REST_](5) e [GraphQL](2)?

### Rest

- **GET** `/user/<id>`

- **GET** `/post/<id>/stories`

- **GET** `/post/<id>/posts`

_Exemplo de consulta em REST_

### GraphQL

Agora vamos ver como o [GraphQL](2) faria a manipulação dos mesmos dados.
Você envia apenas uma consulta que inclui todos os dados requisitados e o servidor responde com um objeto JSON com eles.

```graphql
query {
  User(id: 1234) {
    name
    posts {
      title
      media {
        url
      }
      likes {
        totalCount
      }
    }
    stories {
      media {
        url
      }
    }
  }
}
```

_Exemplo de consulta em GraphQL_

## Benefício da modelagem de dados distribuída

Ao usar o [GraphQL](2) ele permite que você defina o significado de um único dado [_API_](6). Todos os _schemas_ da [_API_](6) são definidos pela modelagem definida, **na maioria das vezes**,no back-end e a partir disso temos queries que tem a capacidade de entender que o dados que será retornado e garantir que tem a mesma característica dos dados buscados pelo cliente ao realizar queries no servidor.

Assim, tanto o back-end, quanto o front-end estão ciente da estrutura de dados definidas envidas nas comunicações.

Vamos exemplificar para entender melhor esse conceito.

### Modelando o usuário

```graphql
type User {
  id: ID!
  name: String!
  posts: [Post]
  stories: [Story]
}
```

Oq significa esse modelo acima definido?

Temos uma fonte de dados chamada User, ao ser acessada ela permite que você receba como resposta id, name, posts, stories.
Vamos tentar entender agora o campo name.

O tipo do campo `name` é string?

- `Não!` string é aquilo que este campo vai responder ao ser acessado pelo cliente. Os campos no graphql são recursos que abrem as portas para a ligação ou não com outros recursos.

Para entender melhor precisamos olhar agora para o compo `posts`.

O tipo do campo `posts` é um array? Ou um `Post`? Mas que tipo é `Post`? string? int? boolean?

Não há um tipo definido para `posts` no GraphQL. O que existe de fato é um acordo no modelo de dados que a resposta será um array de Post. Que pode ainda ser muitas coisas, por isso vamos definir o tipo de Post.

```graphql
type Post {
  id: ID!
  title: String!
  media: Media
}
```

Agora com o tipo Post definido, sabemos que ao consultar um usuário no sistema e requisitarmos o campo `Post` ele vai retornar um array de Post. Que por sua vez tem seus próprios campos definidos.

A todas essas definições de dados, a todas essas modelagens, chamamos `typedefs` definições de tipos.

ATENÇÃO! _Os tipos no graphql nada tem que ver com "tipagem de dados"_

### Definindo resolução de tipos

Os `resolvers` no graphql são os responsáveis por, dado um modelo de dados, analisar o que o cliente quer e responder com o modelo de dados que esta definido.

É normalmente definido por um objeto que nele tem suas funções que ao serem executadas retornam o modelo de dados que o cliente quer.

- Exemplo:

```javascript
const resolvers = {
  User: {
    id: () => '1'
    name: () => 'User',
    posts: () => [],
    stories: () => []
  },
  Post: {
    id: () => '1',
    title: () => 'Post',
    media: () => {}
  }
}
```

Este é um exemplo `aceitável` de resolvers para um graphql, mas não é o ideal.

O que quero com esse exemplo é fazer você entender que o campo `name` do tipo `User` é um resolver que retorna uma string, mas ele não é uma string por si.

Para fazermos algo mais interessante, vamos fazer um resolver um user por uma querie.

Primeiro precisamos modelar essa query!

```graphql
type Query {
  User(id: ID): User
}
```

Criamos no nosso modelo que é uma query User que recebe um id como parametro e retorna um User, mas agora precisamos criar o resolver que retorna esse user:

```javascript
const resolvers = {
  Query: {
    User: () => ({
      id: '1',
      name: 'User',
      posts: [{ title: 'Post1' }, { title: 'Post2' }],
      stories: [],
    }),
  },
};
```

Temos aqui um objeto resolver, que resolve Query, temos um item User que é uma função que retorna um objeto User.

Com isso podemos realizar no cliente uma query como:

```graphql
query {
  User(id: 1) {
    id
    name
    posts {
      title
    }
  }
}
```

E com isso podemos ter como resposta:

```json
{
  "data": {
    "User": {
      "id": 1,
      "name": "User",
      "posts": [{ "title": "Post1" }, { "title": "Post2" }]
    }
  }
}
```

## Vantagens

- Rápido.
- Sem problemas de over-fetching e under-fetching.
- Fortemente tipada.
- Entrega somente dos dados requisitados, barato para o cliente e servidor. (Menor e rápido)
- Única versão, rota e dados totalmente desacoplados.
- Documentação automática.

## Desvantagens

- Curva de aprendizado, pois você terá que aprender um novo conceito.
- Armazenamento em cache, mas pode ser desligado.
- Rate Limiting

De maneira simples, utilizamos os hooks para receber os dados requisitados pelo formulário. Após isso, chamamos o método responsável por se conectar a [_API_](6) e executar a ação `POST`. Com isso, um novo usuário é registrado!

## Conclusão

_Como utilizo o GraphQL?_ Nas próximas seções veremos como utilizar o [GraphQL](2) mais afundo com algumas bibliotecas dentro do React. Caso já queira ir dando uma olhada no [GraphQL](2), o [_GitHub_](7) possui um **[playground do GitHub público](https://docs.github.com/en/graphql/overview/explorer)**!

<p align="center">Made with 💜</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>

[1]: https://www.howtographql.com/
[2]: https://docs.github.com/en/graphql/overview/explorer
[3]: https://graphql.org/
[4]: https://www.redhat.com/pt-br/topics/api/what-is-graphql
[5]: https://developer.mozilla.org/pt-BR/docs/Glossary/REST
[6]: https://developer.mozilla.org/pt-BR/docs/Glossary/API
[7]: https://github.com
[8]: https://graphql.org/foundation/members/
[9]: https://github.com/orgs/graphql/people
[10]: https://lindnercenterofhope.org/blog/feeling-blue-vs-being-depressed-what-is-the-difference/
[11]: https://diariodovale.com.br/colunas/qual-a-cor-da-felicidade/
