<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

## O que é o GraphQL?

GraphQL é uma linguagem de consulta de dados desenvolvida e usada pelo Facebook desde 2012, ele substitui o REST como um novo conceito de paradigma de API.

## O conceito do GraphQL

Primeiramente, para a melhor compreensão do GraphQL, já que ele é muito amplo, vou dar alguns exemplos. Em um Instagram, precisamos exibir os dados especifico de um usuário. Nessa página temos, username, posts, bio, stories... Como podemos fazer solução com REST e GraphQL?

### Rest

- **GET** `/user/<id>`

- **GET** `/post/<id>/stories`

- **GET** `/post/<id>/posts`

_Exemplo de consulta em REST_

### GraphQL

De outra forma, no GraphQL você envia apenas uma consulta que inclui todos os dados requisitados e o servidor responde com um objeto JSON com os dados requisitados.

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

## Benefício da tipagem

Ao usar o GraphQL é uma forma forte para definir recursos da API. Todos os _schemas_ da API são definidos pelo back-end, a partir disso temos queries validadas que definem quais dados o cliente pode fazer buscas no servidor.

Assim, tanto o back-end, quanto o front-end estão ciente da estrutura de dados definidas envidas nas comunicações.

## Vantagens

- Rápido.
- Sem problemas de over-fetching e under-fetching.
- Fortemente tipada.
- Entrega somente dos dados requisitados, barato para o cliente e servidor. (Menor e rápido)
- Única versão, rota e dados totalmente desacoplados.
- Documentação automática.

## Desvantagens

- Consultas na API.
- Curva de aprendizado, pois você terá que aprender um novo conceito.
- Armazenamento em cache.
- Solicitações com status code `200`. 🤣
- Rate Limiting

De maneira simples, utilizamos os hooks para receber os dados requisitados pelo formulário. Após isso, chamamos o método responsável por se conectar a API e executar a ação `POST`. Com isso, um novo usuário é registrado!

## Conclusão

_Como utilizo o GraphQL?_ Nas próximas seções veremos como utilizar o GraphQL mais afundo com algumas bibliotecas dentro do React. Caso já queira ir dando uma olhada no GraphQL, o GitHub possui um **[playground do GraphQL público](https://docs.github.com/en/graphql/overview/explorer)**!

[Ir para Próxima Seção]()

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
