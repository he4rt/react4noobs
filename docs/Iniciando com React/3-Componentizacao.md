# Componentização

## O que é a componentização?

A componentização dentro do React é um conceito bastante utilizado. Um dos objetivos para a utilização é aumentar o máximo do reuso em uma aplicação.

O **conceito de componentização** é uma das principais diferenças do React e de outras bibliotecas baseadas em componentes diante de bibliotecas como jQuery e Angular 1.

> Componentes são conjuntos isolados de lógica (javascript), visualização (JSX/HTML) e possível estilização (CSS).

A componentização funciona da seguinte forma, dividimos nossa interface/aplicação em pequenas partes(componentes) que sozinhas conseguem ter funcionalidades específicas.

Na imagem abaixo cada área separada com uma cor diferente é um componente, podemos ter componentes dentro de outros componentes. Aliás, nossa aplicação em si é um componente.

<img name = "Dividindo-interface-em-componentes" src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/150d7991-e7ed-427e-98cc-0fc4a5fa8d64/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20200610%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20200610T083421Z&X-Amz-Expires=86400&X-Amz-Signature=9fc9d8075760178bb1f3a57178317d05f9c2e884afe740013dba5b41f68a8ce8&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22" alt="Dividindo interface em componentes" />

## Exemplos

### Exemplo 1 - Simples

Para que não fiquemos só na parte teórica, podemos exemplicar um componente simples em React. Um componente chamado `Button` que pode ser reutilizado na sua aplicação.

```js
import React from "react";

export default function Button() {
  return <button onClick={() => alert("Botão clicado")}>Clique aqui</button>;
}
```

Você deve ter percebido que o componente pode ser simplesmente uma função. Então, o componente acima é um botão que mostra um _alert_ para o usuário quando é clicado.

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
        <p>
          Yew, it gives you total control over how you structure your app and
          date flow.
        </p>
      </section>
    </div>
  );
}
```

Nesse componente utilizamos algumas tags HTML, `img` para imagem do usuário do comentário, `section` envolvendo o `strong` que é o nome do usuário e `p` que é o comentário do usuário. Criando este componente, se pode reutiliza-lo por toda a aplicação, bastando apenas importa-lo.

Podemos concluir desse capítulo é que tudo em React é componente, o quanto antes você entender as utilidades deles e como eles 'conversam' entre si(_spoiler_ dos próximos capitulos) mais rápido será seu aprendizado em React.
