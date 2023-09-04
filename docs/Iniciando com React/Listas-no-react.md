<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

# Listas

> Sumário:
>
> - [Como renderizar uma lista](#como-renderizar-uma-lista)
> - [Oque são Keys e por que precisamos delas](#o-que-são-keys-e-por-que-precisamos-delas)
> - [Posso utilizar Fragments ao renderizar uma lista?](#posso-utilizar-fragments-ao-renderizar-uma-lista)
> - [Conclusão](#conclusão)

# Como renderizar uma lista

Durante o desenvolvimento de um aplicativo, é muito comum que, em algum momento, você precise mostrar uma lista de itens na tela, independentemente de quais sejam esses itens. Obviamente, você não vai pegar e inserir cada um deles no código, pois não seria prático e seria quase impossível de mantê-los atualizados. <br/>
No React, graças ao JSX, conseguimos renderizar listas de forma bastante simples, utilizando uma função existente nos arrays chamada map. Com isso, podemos iterar sobre uma lista e retornar componentes React de acordo com ela.

```jsx
const lista = ['item1', 'item2', 'item3'];

function Componente() {
  return (
    <ul>
      {lista.map((item) => {
        return <li>{item}</li>;
      })}
    </ul>
  );
}
```

<p align="center">
<img src="../../assets/lists/lists-examples-1.png" alt="resultado do código acima"/>

</p>

Como podemos ver no código acima, realizamos um mapeamento (map) literal da nossa lista para que ele retorne um componente/tag para cada item.

Ah, vale lembrar que também podemos utilizar o `retorno explícito` para deixar o código mais conciso. Utilizamos essa forma principalmente quando precisamos apenas renderizar o componente sem nenhum tipo de processamento, cálculo, etc. Por exemplo, criar uma variável para renderizar algum tipo de dado, dependendo do conteúdo do item. <br/>

Vale ressaltar que só é permitido retornar `um` componente por vez, ou seja, caso seja necessário retornar mais de um, é preciso envolvê-los com um `fragment,` uma `div` ou alguma outra tag.

```jsx
const lista = ['item1', 'item2', 'item3'];

function Componente() {
  return (
    <ul>
      {lista.map((item) => (<li>{item}</li>)}
    </ul>
  );
}
```

Você sabia que os exemplos acima têm um problema? Então, se rodar os exemplos e abrir o `inspetor` do seu navegador, irá se deparar com a seguinte mensagem de erro:

<p align="center">
<img src="../../assets/lists/lists-examples-2.png" alt="resultado do código acima"/>
</p>

Percebe-se que o erro basicamente nos diz: `Cada item de uma lista precisa ter uma chave (key) única`.

# O que são Keys e por que precisamos delas

Neste ponto, a pergunta principal deve ser: "Certo, mas o que são essas tais `keys`?" Basicamente, o atributo `key` é um identificador único que pode ser uma `string ou um número`, para que o React possa encontrar nosso elemento na `DOM (Document Object Model)` e realizar as atualizações corretas (adicionar na tela, remover da tela, alterar valores, etc.).

```jsx
const lista = ['item1', 'item2', 'item3'];

function Componente() {
  return (
    <ul>
      {lista.map((item) => (<li key={item}>{item}</li>)}
    </ul>
  );
}
```

Você sempre deve selecionar uma informação única para atribuir a uma `key`. Além disso, essas keys não podem mudar, caso contrário, elas perdem o seu propósito.

`!!Nota importante -> Evite utilizar` <br/>

- A posição (index) do elemento na lista não é uma boa escolha como key, pois dentro de um array podem ocorrer diversas alterações, como reordenação, e isso pode levar a problemas de renderização.

- O uso de Math.random() não é apropriado para gerar keys, pois ele gera números aleatórios a cada renderização, o que pode causar instabilidade no comportamento do React.

- Lembre-se de que as keys são propriedades específicas que o React utiliza para otimizar a renderização, e elas existem apenas para o propósito interno da biblioteca. Se você precisar que uma informação seja passada para o componente como propriedade para realizar alguma ação, é melhor criar uma nova propriedade e atribuir o valor a ela, em vez de usar a key para essa finalidade.

```jsx
<Componente key={name} name={name} />
```

# Posso utilizar Fragments ao renderizar uma lista?

Sim, podemos utilizar Fragments em uma lista, mas não da forma com a qual estamos acostumados. Os Fragments são basicamente uma forma de agrupar diversos elementos sem a necessidade de usar uma tag HTML específica. Quando renderizados, eles essencialmente desaparecem e renderizam apenas o seu conteúdo na nossa árvore de elementos. Portanto, quando usamos Fragments em listas, onde precisamos sempre declarar a key, é necessário importar o componente Fragment do React para utilizá-lo.

Normalmente, utilizamos o componente Fragment por meio da famosa abreviação

```jsx
<>
  <div />
  <div />
  <div />
</>
```

Mas, para listas precisa ser assim:

```jsx
import { Fragment } from 'react';

const lista = [
  {
    id: 1,
    name: 'Fulano',
    idade: 15,
  },
  {
    id: 2,
    name: 'Fulano2',
    idade: 15,
  },
];

function Componente() {
  return (
    <div>
      {lista.map((item) => {
        return (
          <Fragment key={item.id}>
            // Geralmente por Id`s serem propriedades únicas, é muito utilizado
            como keys.
            <span>{item.name}</span>
            <span>{item.idade}</span>
          </Fragment>
        );
      })}
    </div>
  );
}
```

# Conclusão

Até aqui vimos como renderizar as listas no react e o motivo para algumas especificidades.
A renderização de listas é algo que você com certeza irá utilizar no dia a dia e é muito importante saber as regras. <br/>

Esperamos que este conteudo tenha te ajudado a entender melhor a respeito das listas. Também deixo aqui o [link da documentação](https://react.dev/learn/rendering-lists#challenges) do React para caso queira ver direto da fonte.
Nos vemos no próximo capitulo, seeyaa!

[Ir para a próxima seção](./7-Manipulando%20Eventos.md)

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>

``
