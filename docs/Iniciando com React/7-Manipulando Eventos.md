<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

# Manipulando Eventos

## Qual a diferença dos eventos do HTML para o React?
Bom, de certa forma a manipulação de eventos no React é bem parecida com o padrão do HTML porém existem algumas diferenças.
* Eventos são nomeados utilizando camelCase, ou seja ao invez de um espaço, barra ou traço entre as palavras, simplesmente usa letra maiuscula. (Ex: manipulandoEventos).
* Graças ao JSX você passa uma função na propriedade do evento e não um texto.
* No HTML podemos evitar o comportamento padrão de alguns elementos enviando false porém no React precisamos fazer isso o **preventDefault**.

Exemplo 1:
```html
<!-- Exemplo HTML -->
<button onclick="searchUsers()">
  Pesquisar usuários
</button>

<!-- Exemplo REACT -->
<button onClick={searchUsers}>
  Pesquisar usuários
</button>

```

Exemplo 2:
```html
<!-- HTML -->
<form onsubmit="handleSubmit(); return false">
  <input type="text" name="nome" id="nome" placeholder="Digite seu nome"/>
  <button type="submit">Enviar </button>
</form>
```

```jsx
// React

function Form(){
  function handleSubmit(event){
    event.preventDefault();
    console.log("funfo");
  }

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" name="nome" id="nome" placeholder="Digite seu nome"/>
      <button type="submit">Enviar </button>
    </form>
  )
  // ou
  return (
    <form onSubmit={(event) => handleSubmit(event)}>
      <input type="text" name="nome" id="nome" placeholder="Digite seu nome"/>
      <button type="submit">Enviar </button>
    </form>
  )
}
```

Vale lembrar que toda função alocada a um evento recebe como parametro o evento, portando é possivel manipular da forma que deseja seu comportamento. Por exemplo: As vezes você nem quer pegar o objeto **event** inteiro, apenas o valor pra realizar sua função... A depender do componente, tudo que precisa é uma arrow function *(event) => function(event.target.value)* ou algo do tipo.


## Consigo passar mais de um parâmetro
A resposta é sim! Como disse no tópico anterior, podemos utilizar arrow functions para passar como argumento, portando tudo que precisamos fazer é utiliza-las de forma correta!

Ex:
```jsx

function Form(){
  function handleSubmit(event, id){
    event.preventDefault();
    console.log("funfo", id);
  }

  return (
    <form onSubmit={(event) => handleSubmit(event, id)}>
      <input type="text" name="nome" id="nome" placeholder="Digite seu nome"/>
      <button type="submit">Enviar </button>
    </form>
  )
}
```


---


[Ir para Próxima Seção](../Ferramentas%20de%20build/1-npm-yarn.md)

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>
