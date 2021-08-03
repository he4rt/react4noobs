<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

# Manipulando Eventos

## Qual a diferença dos eventos do HTML para o React?

Bom, de certa forma a manipulação de eventos no React é bem parecida com o padrão do HTML porém existem algumas diferenças.

- Eventos são nomeados utilizando camelCase, ou seja ao invez de um espaço, barra ou traço entre as palavras, simplesmente usa letra maiuscula. (Ex: manipulandoEventos).
- Graças ao JSX você passa uma função na propriedade do evento e não um texto.
- No HTML podemos evitar o comportamento padrão de alguns elementos enviando false porém no React precisamos fazer isso o **preventDefault**.

Exemplo 1:

```html
<!-- Exemplo HTML -->
<button onclick="searchUsers()">Pesquisar usuários</button>

<!-- Exemplo REACT -->
<button onClick="{searchUsers}">Pesquisar usuários</button>
```

Exemplo 2:

```html
<!-- HTML -->
<form onsubmit="handleSubmit(); return false">
  <input type="text" name="nome" id="nome" placeholder="Digite seu nome" />
  <button type="submit">Enviar</button>
</form>
```

```jsx
// React

function Form() {
  function handleSubmit(event) {
    event.preventDefault();
    console.log("funfo");
  }

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" name="nome" id="nome" placeholder="Digite seu nome" />
      <button type="submit">Enviar </button>
    </form>
  );
  // ou
  return (
    <form onSubmit={(event) => handleSubmit(event)}>
      <input type="text" name="nome" id="nome" placeholder="Digite seu nome" />
      <button type="submit">Enviar </button>
    </form>
  );
}
```

Vale lembrar que toda função alocada a um evento recebe como parametro o evento, portando é possivel manipular da forma que deseja seu comportamento. Por exemplo: As vezes você nem quer pegar o objeto **event** inteiro, apenas o valor pra realizar sua função... A depender do componente, tudo que precisa é uma arrow function _(event) => function(event.target.value)_ ou algo do tipo.

## Consigo passar mais de um parâmetro

A resposta é sim! Como disse no tópico anterior, podemos utilizar arrow functions para passar como argumento, portando tudo que precisamos fazer é utiliza-las de forma correta!

Ex:

```jsx
function Form() {
  function handleSubmit(event) {
    event.preventDefault();
    console.log("funfo", id);
  }

  return (
    <form onSubmit={(event) => handleSubmit(event)}>
      <input type="text" name="nome" id="nome" placeholder="Digite seu nome" />
      <button type="submit">Enviar </button>
    </form>
  );
}
```

Lembra de como é feito para lidar com eventos no JS puro?
Um comportamento padrão é que esses eventos ficam disponibilizados para as funções, ela passa o evento. Por exemplo, tu cria a função `handleChange()` e coloca em um `onchange` que no `React` é `onChange`. Essa função irá receber como parametro `SEMPRE` o `event`, ou seja os dados do evento.
Esse comportamento é melhor de explicar com Javascript puro da seguinte forma.

```js
// Pegamos o botão
cont btnSave = document.querySelect('#saving');

// Adicionamos um evento para ele através do addEventListner
// 1º Parametro: nome do evento
// 2º Parametro: Função de callback, lembrando que sempre irá receber um event como parametro.
btnSave.addEventListener('click', (event) => {

})

// Tu também pode fazer o seguinte
function handleClick(event){
  //algo aqui dentro
}

btnSave.addEventListener('click', handleClick)

// Outra forma é ir direto pra uma propriedade do componente.

btnSave.click = handleClick;
```

Enfim, por que isso foi explicado? Lembra que o React não permite que utilizemos os mesmos nomes do HTML padrão? Apenas por camel case(ex: onchange = onChange). Porém o comportamento é o mesmo, todo onChange irá passar como `primeiro parametro` das funções o `event`.

```js
import {useState} from 'react'

function inputChangeComponent(){
  const [text, setText] = useState('');

  // Recebemos o evento
  // Vale lembrar que após o primeiro parametro, podemos simplesmente por qualquer parametro que quisermos.
  function handleChange(event){
    setText(event.target.value)
  }

  return(
    <>
      <input type="text" name="text" value={text} onChange={handleChange}>
      </input>
  )
}
```

Outro ponto importante de destacar é: se apenas colocarmos nossa função no onchange/onChange, assim como no javascript puro irá passar o `event` como primeiro parametro. Porém também é possivel passar como segundo ou terceiro a depender da sua escolha.
Vamos utilizar o exemplo do form que fizemos lá em cima.

```jsx
function Form() {
  // Essa forma de fazer com o ID é meramente para mostrar a possibilidade.
  // Lembre-se que a depender do contexto, pode ser resolvido de muitas outras formas.
  const id = 847875211221;

  function handleSubmit(event, id) {
    event.preventDefault();
    console.log("funfo", id);
  }

  return (
    // Com uso das arrow functions, fazemos uma função anônima tendo como parametro o event e em sequida chamamos nosso handleSubmit passando tanto o event quanto o id.
    // Lembre-se que a ordemn nesse caso fica a sua escolha, se eu definisse na função que iria receber primeiro o id e o segundo seria o event daria o mesmo resultado.
    <form onSubmit={(event) => handleSubmit(event, id)}>
      <input type="text" name="nome" id="nome" placeholder="Digite seu nome" />
      <button type="submit">Enviar </button>
    </form>
  );
}
```

Nesse tópico você aprendeu sobre manipulação de eventos no React. Agora é praticar e estudar para poder melhorar cada vez mais.
Deixo também o link da [documentação do React](https://pt-br.reactjs.org/docs/handling-events.html), para poderem ver direto da fonte.

---

[Ir para Próxima Seção](../Ferramentas%20de%20build/1-npm-yarn.md)

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>
