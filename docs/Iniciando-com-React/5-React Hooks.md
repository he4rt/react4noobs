# React Hooks

## O que são Hooks
Hooks são funções utilizadas para ter acesso recursos de **estado** e **ciclo de vida**, em **componentes funcionais**. Eles não podem ser utilizados em componentes de classe. Os Hooks no React são nomeados com o prefixo 'use'.

### ⚠ Aviso:
> Não use Hooks dentro de loops, regras condicionais ou funções aninhadas (funções dentro de funções). Em vez disso, sempre use Hooks no nível superior de sua função React. Seguindo essas regras, você **garante que os Hooks serão chamados na mesma ordem** a cada vez que o componente renderizar.

---

## useState
O *useState* é um dos Hooks utilizados para criar estado dentro de um componente em React. O estado criado pelo *useState* nada mais é que uma variável que o componente consegue reagir quando seu valor é atualizado.

O *useState* recebe como parâmetro o valor inicial do estado. E retorna um *array* onde o primeiro valor é o estado atual, e o segundo valor é uma função usada para alterar o valor do estado.

### Exemplo:
```jsx
import React, { useState } from 'react';

function Counter () {
  // Cria estado 'clicks' com valor inicial 0
  // Um jeito fácil de separar o retorno do useState é fazendo desestruturação de array
  const [clicks, setClicks] = useState(0);
  
  return(
    <div>
      <h1>{clicks}</h1>
      {/* A função 'setClicks' é usada para mudar valor de 'clicks' */}
      <button onClick={() => setClicks(clicks + 1)}>
        Clique Aqui!
      </button>
    </div>
  );
}
```

---

## useEffect
O *useEffect* é um Hook utilizado para realizar efeitos colaterais. Esse Hook recebe respectivamente como parâmetros: uma função de *callback* e um *array* de dependências. Quando uma das variáveis do *array* de dependências muda de valor, a função passada como primeiro parâmetro é executada.

### Exemplo:
```jsx
import React, { useState, useEffect } from 'react'

function Counter() {
  const [clicks, setClicks] = useState(0);

  // Atualiza o título da página toda vez que 'clicks' muda de valor
  useEffect(() => {
    document.title = `Você clicou ${clicks} vezes`;
  }, [clicks]);

  return(
    <div>
      <h1>{clicks}</h1>
      <button onClick={() => setClicks(clicks + 1)}>
        Clique Aqui!
      </button>
    </div>
  );
}
```

Caso o *array* de dependências seja declarado vazio (`[]`), a função de *callback* vai ser executada apenas no momento em que o componente é montado.
```jsx
useEffect(() => {
  // Essa função vai ser executada apenas quando o componente é montado
}, []);
```

Caso você queira que uma função seja executada quando o componente é desmontado, basta retornar essa função dentro do *callback*.
```jsx
useEffect(() => {
  // A função returnada pelo callback vai ser executada apenas quando o componente for desmontado
  return () => { console.log('Componente Desmontado') }
}, []);
```

Também é possível fazer com que o *callback* seja executado todas as vezes que o componente renderizar novamente. Para isso, basta não passar nada como segundo parâmetro do *useEffect*. Porém, essa prática não é recomendada por questões de performance.
```jsx
useEffect(() => {
  // Essa função vai ser executada toda vez que o componente renderizar
});
```
