<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank" title="Clique para visualizar mais informações sobre o projeto 4noobs">
    <img src="../../assets/global/header-4noobs.svg" alt="Cabeçalho do repositório representado pelo logotipo da He4rt, simbolizado por um coração roxo, na esquerda e a tipografia '4 noobs by He4rt devs' na direita">
  </a>
</p>


# **CUSTOM HOOKS: Compartilhando lógica entre componentes**

## O que é um Custom Hook?

Hook personalizado é uma função JavaScript na qual é possível reutilizar 
sua lógica em diversos componentes da aplicação. Imagine que na sua 
aplicação você tem vários componentes que precisam fazer requisições a 
uma API, ou salvar algo no local storage. Se você tiver um hook 
personalizado que faça tais coisas, não será necessário repetir o mesmo 
código várias vezes, apenas chamar o hook.

Um hook personalizado não é um recurso separado do React, é apenas uma 
função comum que usa, por baixo dos panos, hooks nativas como **`useState`** 
e **`useEffect`**.

Hooks personalizados não compartilham estados entre os componentes: cada 
componente que utiliza o hook possui seu estado isolado, a função 
compartilha apenas a lógica. A função precisa, obrigatoriamente, começar 
com a palavra **`use`**, essa convenção avisa o React que aquela função pode 
chamar outras hooks internamente, permitindo que ferramentas como o 
ESLint verifiquem se as regras das hooks estão sendo seguidas corretamente.

## Vantagens dos Custom Hooks:

  - **Reutilização de lógica:** Evita duplicar o mesmo código (fetch de API, manipulação de formulário, localStorage, etc.) em vários componentes diferentes.

  - **Componentes mais limpos:** A lógica complexa fica isolada na hook, deixando o componente focado apenas na renderização.

  - **Facilidade de manutenção:** Se precisar corrigir um bug ou mudar uma regra de negócio, você altera em um único lugar (a hook), em vez de em cada componente que repete a lógica.

  - **Testabilidade:** Como a lógica fica separada da interface, fica mais fácil testar a hook isoladamente, sem precisar renderizar todo o componente.

  - **Não quebra a árvore de componentes:** Diferente de HOCs e render props, custom hooks não adicionam camadas extras de componentes na árvore, evitando o "wrapper hell".

  - **Compartilhamento sem acoplamento:** Vários componentes podem usar a mesma lógica sem precisar estar relacionados entre si (não é necessário passar props entre pai e filho).


## Exemplo Prático: useFetch

Este hook encapsula toda a lógica de requisição a uma API, controlando 
os estados de carregamento, erro e dados retornados.

### O código:

```javascript
  import { useState, useEffect } from 'react';

  export function useFetch(url){
      const [data, setData] = useState(null);
      const [loading, setLoading] = useState(true);
      const [error, setError] = useState(null);

      useEffect( () => {
          //Função que busca a API
          const fetchData = async () => {
              setLoading(true); //Ativa o Loading quando começa a busca
              setError(null); // Reseta erros anteriores

              try{
                  const response = await fetch(url);
                  if (!response.ok){
                      throw new Error("Erro ao buscar a API");
                  }
                  const json = await response.json();
                  setData(json); //Guarda os dados.
              }catch (err){
                  setError(err.message); //Guarda o erro, caso aconteça.
                  setData(null);
              }finally{
                  setLoading(false);
              }
          };

          if(!url){
              return;
          }else{
              fetchData(); //Se tiver URL ele chama a função
          }
      }, [url]); //UseEffect roda toda vez que a variável url muda.

      //Retorna os estados em forma de objetos, dessa maneira é possível pegar o qual quiser.
      return { data, loading, error }; 
  }

```

### Como funciona?

  - Recebe uma **`url`** como parâmetro.
  - Retorna um objeto com três valores: **`data`** (os dados retornados), 
  **`loading`** (se a requisição está em andamento) e **`error`** (mensagem de 
  erro, se houver).
  - O **`useEffect`** roda automaticamente sempre que a **`url`** mudar, disparando 
  uma nova requisição.


### Usando a hook em um componente:

```jsx
  import {useFetch} from 'caminho_da_funcao'

  function ListaPokemon() {
    const { data, loading, error } = useFetch('https://pokeapi.co/api/v2/pokemon');

    if (loading) return <p>Carregando...</p>;
    if (error) return <p>Erro: {error}</p>;

    return (
        <ul>
            {data.results.map((pokemon) => (
                <li key={pokemon.name}>{pokemon.name}</li>
            ))}
        </ul>
    );
  }

```

Perceba como o componente ficou mais limpo: Ele não sabe **como** a requisição é feita, apenas **usa** o resultado.

<center>Made with 💜</center>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380" alt="Tipografia com o título '4 noobs by He4rt devs' e o slogan 'Da comunidade para a comunidade 💜'">
  </a>
</p>
