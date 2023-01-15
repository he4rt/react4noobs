<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

# React Hooks

## O que são Hooks

Hooks são funções utilizadas para ter acesso recursos de **estado** e **ciclo de vida**, em **componentes funcionais**. Eles não podem ser utilizados em componentes de classe. Os Hooks no React são nomeados com o prefixo 'use'.

### ⚠ Aviso:

> Não use Hooks dentro de loops, regras condicionais ou funções aninhadas (funções dentro de funções). Em vez disso, sempre use Hooks no nível superior de sua função React. Seguindo essas regras, você **garante que os Hooks serão chamados na mesma ordem** a cada vez que o componente renderizar.

---

## useState

O _useState_ é um dos Hooks utilizados para criar estado dentro de um componente em React. O estado criado pelo _useState_ nada mais é que uma variável que o componente consegue reagir quando seu valor é atualizado.

O _useState_ recebe como parâmetro o valor inicial do estado. E retorna um _array_ onde o primeiro valor é o estado atual, e o segundo valor é uma função usada para alterar o valor do estado.

### Exemplo:

```jsx
import React, { useState } from 'react';

function Counter() {
  // Cria estado 'clicks' com valor inicial 0
  // Um jeito fácil de separar o retorno do useState é fazendo desestruturação de array
  const [clicks, setClicks] = useState(0);

  return (
    <div>
      <h1>{clicks}</h1>
      {/* A função 'setClicks' é usada para mudar valor de 'clicks' */}
      <button onClick={() => setClicks(oldState => oldState + 1)}>
        Clique Aqui!
      </button>
    </div>
  );
}
```

---

## useEffect

O _useEffect_ é um Hook utilizado para realizar efeitos colaterais. Esse Hook recebe respectivamente como parâmetros: uma função de _callback_ e um _array_ de dependências. Quando uma das variáveis do _array_ de dependências muda de valor, a função passada como primeiro parâmetro é executada.

### Exemplo:

```jsx
import React, { useState, useEffect } from 'react';

function Counter() {
  const [clicks, setClicks] = useState(0);

  // Atualiza o título da página toda vez que 'clicks' muda de valor
  useEffect(() => {
    document.title = `Você clicou ${clicks} vezes`;
  }, [clicks]);

  return (
    <div>
      <h1>{clicks}</h1>
      <button onClick={() => setClicks(oldState => oldState + 1)}>
        Clique Aqui!
      </button>
    </div>
  );
}
```

Caso o _array_ de dependências seja declarado vazio (`[]`), a função de _callback_ vai ser executada apenas no momento em que o componente é montado.

```jsx
useEffect(() => {
  // Essa função vai ser executada apenas quando o componente é montado
}, []);
```

Caso você queira que uma função seja executada quando o componente é desmontado, basta retornar essa função dentro do _callback_.

```jsx
useEffect(() => {
  // A função retornada pelo callback vai ser executada apenas quando o componente for desmontado
  return () => {
    console.log('Componente Desmontado');
  };
}, []);
```

Também é possível fazer com que o _callback_ seja executado todas as vezes que o componente renderizar novamente. Para isso, basta não passar nada como segundo parâmetro do _useEffect_. Porém, essa prática não é recomendada por questões de performance.

```jsx
useEffect(() => {
  // Essa função vai ser executada toda vez que o componente renderizar
});
```

---

## useRef

O _useRef_ é um Hook utlizado para acessar a referência valor sem que ele seja associado ao estado do componente para evitar que o elemento renderize novamente quando a refência mudar seu valor, esse hook recebe como parâmetro um valor inicial e retorna um objeto com uma referência mutável ao valor inserido, para acessar esse valor usamos a propriedade `.current` que é a referência do elemento.

Com isso podemos salvar tambem elementos HTML para que consigamos efeitos que se assemelham aos métodos _Finding HTML Elements_ do JavaScript nos Browsers.
Ex.: `document.getElementById()`, `document.getElementsByClassName()` e etc.

Para que façamos isso, passamos essa Ref como propriedades para o componente que queremos referenciar. Assim guardamos uma referência do elemento DOM como valor da nossa Ref.

### Exemplo:

```jsx
import React, { useRef } from 'react';

function ContactForm() {
  // Criamos uma const que recebe o useRef passando null como parâmetro inicial
  // Quando o elemento for renderizado em tela a variável inputRef será atualizada
  // A partir da primeira renderização, o valor será o elemento <input/>
  const inputRef = useRef(null);

  const handleContinue = () => {
    // Podemos acessar as informações do elemento
    // Nesse if verifico se o input possui algum valor, e se não, chamo a função focus
    if (!inputRef.current.value) {
      inputRef.current.focus();
    }
  };

  return (
    <div>
      {/* Quando esse elemento for renderizado atualizará a variável com a sua referência */}
      <input ref={inputRef} placeholder='Digite seu Email' />

      <button onClick={handleContinue}>Continuar</button>
    </div>
  );
}
```

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>
