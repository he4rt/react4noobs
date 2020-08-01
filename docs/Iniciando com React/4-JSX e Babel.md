# JSX

O JSX é uma extensão de sintaxe para Javascript, basicamente é uma sintaxe semelhante ao XML, onde você consegue compreender de uma melhor forma como será montado o seu componente UI.

O React não obriga o uso do JSX, mas geralmente utilizamos por achar prático e por ele ajudar bastante na parte visual.

## Exemplo

```js
const elemento = <h1>Olá, membro He4rt!!</h1>;
```

Este código acima é o JSX propriamente dito, não é uma string e nem HTML, legal né?

Em JSX, como acabamos misturando sintaxe HTML com Javascript, em atributos do HTML como `class` devemos substituir para `className` no JSX.

Se pode utilizar JSX dentro de `if` e laços `for`, para mostrar um elemento, vamos ver os detalhes mais adiante.

# Babel

O Babel é um transpilador utilizado para transformar o JSX em outras versões Javascript, mas agora vem a dúvida, por quê?

Atualmente nem todos os navegadores entendem o Javascript moderno, mas com o Babel, a compatibilidade entre todos se torna possível.

<img align="center" src="/assets/tirinha-babel.jpg" width="100%"> 