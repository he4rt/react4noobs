<div align="center">
  <h1>JSX & Babel</h1>
  <img align="center" src="../../assets/react.png" alt="" width="30%">
  <img align="center" src="../../assets/babel.svg" alt="" width="30%">
</div>
<hr />

# Explicando o **Babel**

Os browsers apenas entendem, a princípio, o JavaScript Vanilla (puro), mas nós utilizamos a sintaxe JSX no desenvolvimento React, e é aí que o **Babel** entra; Ele é o cara que transpila o código JSX para JS (Padrão ES6+), fazendo com que os browsers, novos ou antigos, possam compreender os scripts.

Estes exemplos são iguais:

**_• Exemplo 1_**

```jsx
const message = <p className="message">Hello He4rt</p>;
```

**_• Exemplo 2_**

```jsx
const message = React.createElement(
  "p",
  { className: "message" },
  "Hello He4rt"
);
```

O **_Exemplo 1_** está utilizando a sintaxe JSX padrão, e o **_Exemplo 2_** é como o Babel trabalha fazendo a compilação do trecho de código em questão.

O Babel compila JSX para chamadas `React.createElement()`.

O `React.createElement()` cria objetos, e nós podemos imaginá-los como descrições do que queremos ver na tela.

É assim que o Babel trabalha com JSX.

# **JSX** - Introdução

**JSX** (XML dentro do JS) é uma sintaxe extendida para JavaScript que facilita a criação e o entendimento de um componente na UI.

Um breve exemplo:

```jsx
const title = <h1>Hello He4rt</h1>;
```

_O JSX facilita a nossa vida enquanto utilizamos o React. O uso dessa sintaxe não é obrigatória, mas posso falar que a maior parte da comunidade React faz uso do mesmo. A diferença entre o uso e o desuso é ENORME, então prefira sempre utilizá-lo. Esse 4Noobs será feito em volta do JSX._

Usando o JSX podemos escrever estruturas que lembram o HTML, dentro do mesmo arquivo em que criamos os scripts. O **Babel** converterá tudo isso para JavaScript, fazendo com que o código seja entendido pelo browser.

Resumindo, _JSX é a sintaxe utilizada em projetos ReactJS/React Native para facilitar a criação/legibilidade de componentes e, posteriormente, a manutenção do código_.

## Utilizando **JSX**

O JSX hoje pode ser utilizado em arquivos com a extensão `.js` e `.tsx`, configurando manualmente o **Babel** ou criando um projeto rodando o comando `npx create-react-app 'NomeDoProjeto'` no terminal. Para incluir TypeScript no projeto (.tsx), ao final do comando adicione `--template=typescript`.

É permitido o uso de **qualquer expressão JavaScript válida** dentro do JSX utilizando as { }.

Por exemplo:

```jsx
const organization = "He4rt";
const message = <p>Hello {organization}</p>;
```

O retorno será `Hello He4rt`.

Isto significa que **podemos utilizar JSX dentro de condições `if` e laços `for`, atribuí-lo a variáveis, aceitá-lo como argumentos e retorná-los de funções**.

Depois da compilação, as expressões em JSX se transformam em chamadas normais de funções que retornam objetos JavaScript.

## Especificando Atributos com **JSX** (Vale a pena lembrar disso)

Para especificar atributos como uma string, você pode usar " ":

```jsx
const example = <h1 title="Hello World"></h1>;
```

Para especificar atributos com uma _expressão JavaScript_, você pode utilizar { }, como já introduzido anteriormente.

```jsx
const example = <img src={user.avatarImg}></img>;
```

## Especificando Elementos Filhos com **JSX**

Tags feitas em JSX podem ter elementos filhos utilizando os parênteses:

```jsx
const titles = (
  <div>
    <h1>Hello World</h1>
    <p>Hello He4rt</p>
  </div>
);
```

### **_O que foi falado até agora sobre JSX/Babel é apenas a ponta do iceberg!_** 💜
