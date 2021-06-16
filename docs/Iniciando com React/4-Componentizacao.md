<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

# Componentização

## O que é a componentização?

A componentização dentro do React é um conceito bastante utilizado. Um dos seus principais objetivos é maximizar o reuso em uma aplicação.

O **conceito de componentização** é uma das principais diferenças do React e de outras bibliotecas baseadas em componentes diante de bibliotecas como jQuery e Angular 1.

> Componentes são conjuntos isolados de lógica (javascript), visualização (JSX/HTML) e estilização (CSS).

A componentização funciona da seguinte forma, dividimos nossa interface/aplicação em pequenas partes (componentes) que sozinhas conseguem ter funcionalidades específicas.

Na imagem abaixo cada área separada com uma cor diferente é um componente, podemos ter componentes dentro de outros componentes. Aliás, nossa aplicação em si é um componente.

![Dividindo interface em componentes](https://camo.githubusercontent.com/c6c0539167806d8acd08abdfedd99cef216988f1/68747470733a2f2f69322e77702e636f6d2f7777772e71636f64652e696e2f77702d636f6e74656e742f75706c6f6164732f323031382f30372f72656163742d636f6d706f6e656e742d747265652e706e673f726573697a653d313032342532433537382673736c3d31)
_Fonte: [QCode](https://www.qcode.in/learn-react-by-creating-a-comment-app/)_

## Exemplos

### Exemplo 1 - Simples

Para que não fiquemos só na parte teórica, podemos exemplificar um componente simples em React. Um componente chamado `Button` que pode ser reutilizado na sua aplicação.

```js
import React from "react";

export default function Button() {
  return <button onClick={() => alert("Botão clicado")}>Clique aqui</button>;
}
```

Você deve ter percebido que o componente pode ser simplesmente uma função. O componente acima é um botão que mostra um _alert_ para o usuário quando é clicado.

### Exemplo 2 - Avançado

Podemos ter diversos tipos de componentes e cada componente com sua complexidade.

Na [imagem](#Dividindo-interface-em-componentes) que mostramos como podemos dividir uma aplicação em componentes, podemos mostrar de como ficaria o componente `Comment`, bora lá?

```js
import React from "react";

export default function Comment() {
  return (
    <div>
      <img src="usuario.png" alt="Fulano" />
      <section>
        <strong>Mike</strong>
        <p>Yew, it gives you total control over how you structure your app and date flow.</p>
      </section>
    </div>
  );
}
```

Nesse componente utilizamos algumas tags HTML, `img` para imagem do usuário do comentário, `section` envolvendo o `strong` que é o nome do usuário e `p` que é o comentário do usuário. Criando este componente, se pode reutiliza-lo por toda a aplicação, bastando apenas importá-lo.

### Exemplo 3 - Reuso

Como dito no inicio, um dos principais objetivos da componentização é o `reuso`, dito isto podemos declarar componentes para serem utilizados dentro de outros.
Para demonstrar, utilizaremos os componentes de Button e Comments já criados nos outros exemplos e um novo componente chamado `ComposedComponent`(Componente composto), que utilizará tanto o Button quanto o Comment.

```js
import React from "react";

function Button() {
  return <button onClick={() => alert("Botão clicado")}>Clique aqui</button>;
}

function Comment() {
  return (
    <div>
      <img src="usuario.png" alt="Fulano" />
      <section>
        <strong>Mike</strong>
        <p>Yew, it gives you total control over how you structure your app and date flow.</p>
      </section>
    </div>
  );
}

function ComposedComponent() {
  return (
    <div>
      <h1>Meus comentários</h1>
      <Comment />
      <Comment />
      <Comment />
      <Comment />
      <Comment />
      <Button />
    </div>
  );
}
```

Como podem ver, podemos reutilizar quantas vezes quisermos um componente criado no React, a unica diferença será que a primeira letra sempre será maiuscula.

Podemos concluir desse capítulo que tudo em React é componente, o quanto antes você entender as utilidades deles e como eles 'conversam' entre si (_spoiler_ dos próximos capítulos) mais rápido será seu aprendizado em React.

[Ir para Próxima Seção](./4.1-FormasDeDeclarar.md)

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>
