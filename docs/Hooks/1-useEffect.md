<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

# useEffect

Com o _useEffect_ te permite executar efeitos colaterais nos componentes, que basicamente é semelhante com os métodos do ciclo de vida do React como `componentDidMount`, `componentDidUpdate`, e `componentWillUnmount` combinados

## Quando usar?

Quando necessitar lidar com efeitos colaterais (_side-effects_) como chamados à API, tarefas assíncronas, modificações na DOM, etc.

## Como usar

Declaramos da seguinte forma o _useEffect_:

```jsx
  useEffect(() => {
    console.log(contagem);
  }, [contagem]);
```

Primeiro parâmetro é uma função, que pode assíncrona ou não, que é executada após inicialização e atualização do componente.

O segundo parâmetro `[contagem]` indica em quais situações esse efeito deve executar, nesse exemplo ele só executará caso o valor de `contagem` sofra alguma ateração. Podemos também não definir nenhum parâmetro, deixando o array vazio `[]`, para que hook execute somente na inicialização e em todas atualizações do componente, independente de seus valores sofra alguma alteração.

Passando no segundo parâmetro do _useEffect_ um array vazio ele só executara **uma vez e na inicilização**:

```jsx
  useEffect(() => {
    console.log('Component montado');
  }, []);
```

## Usando

Recebemos o desafio de atualizar o título de página toda vez que a informação da variável `contagem` sofrer alguma alteração, tal alteração será feita através do evento de um botão.

Vamos começar preparando nosso component com os hooks.

```jsx
import React, { useEffect, useState } from 'react';

export default function Contador() {
  const [contagem, setContagem] = useState(0);

  useEffect(() => {
    document.title = `${contagem} vezes`
  }, [contagem]);

  return <div />
}
```

Foi definido a variável de estado `contagem` inicializando com o valor **0**, no qual utilizaremos para fazer incrementação.

No _useEffect_ como primeiro parâmetro que é uma função, foi declarado o comando para mudar título da página, já no segundo parâmetro, defini a váriavel `contagem` para que toda vez que ela sofrer uma mudança, executar o efeito.

```jsx
import React, { useEffect, useState } from 'react';

export default function Contador() {
  const [contagem, setContagem] = useState(0);

  useEffect(() => {
    document.title = `${contagem} vezes`
  }, [contagem]);

  function incrementar() {
    setContagem(contagem + 1);
  }

  return (
    <>
      <h1>
        Botão foi clicado <strong>{contagem}</strong> vezes.
      </h1>
      <button type="button" onClick={incrementar}>Incrementar contagem</button>
    </>
  )
}
```

Na renderização do component foi declarado um botão que possui o evento `onClick` que chama a função `incrementar`, toda vez que botão é clicado. Nesta função ele incrementa o valor da `contagem` com mais um.

Com isso, nós concluímos o nosso desafio!

## Considerações adicionais

Com _useEffect_ combinando com outros hooks, pode ter um controle excelente de todos efeitos em seu componente, como por exemplo, armazenar em uma váriavel estado a informação de identificação algo, e utilizar para fazer requisições a API para obter os dados, assim atualizando as informações contidas na tela sem precisar atualizar a página.


```jsx
useEffect(() => {
  async function loadUser() {
    const response = await axios.get(`https://api.heartdevs.com/user/${userId}`);
    const { data } = response;

    setUser(data);
  }
  
  loadUser();
}, [userId]);
```

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>
