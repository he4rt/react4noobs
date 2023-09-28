<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

# Renderização Condicional

Hoje falaremos sobre renderização condicional no React! O que é? Como utlizar?

> Sumário:
>
> - [O que é a renderização condicional](#o-que-é-a-renderização-condicional)
> - [Condicionando o retorno dos nossos componentes](#condicionando-o-retorno-dos-nossos-componentes)
> - [Condicionando no JSX](#condicionando-no-jsx)
> - [Condicionando com operador ternário](#condicionando-com-operador-ternário)
> - [Condicionando com operador AND(&&)](#condicionando-com-operador-and)
> - [Aumentando a complexidade com o OR(||)](#aumentando-a-complexidade-com-o-or)
> - [Conclusão](#conclusão)

# O que é a renderização condicional

A renderização condicional é basicamente uma forma de alterar o que é mostrado em tela a partir de uma condição. Algo como utilizar um `if else` para algo, porém no JSX. Podemos ter diversas lógicas e alterar a visualização dos componentes, como por exemplo: `Um modal que só ira abrir quando o estado isOpen for true` ou `Um texto que quando o estado for true será "batata" e quando for false será "ok"`.
Bem simples, não? Agora vamos ver um pouco a respeito das formas de utilização.

# Condicionando o retorno dos nossos componentes

Como nós já sabemos, no final de todo componente sempre irá existir um `return` com o nosso HTML, certo? Então, podemos condicionar ele, adicionando alguma condição junto de um `segundo retorno`.
Segue o exemplo abaixo:

```jsx
const Componente = ({ data }) => {
  if (!data) {
    return (
      <div>
        <h1>Dados não encontrados</h1>
      </div>
    );
  }

  return (
    <div>
      <h1>{data.nome}</h1>
      <h1>{data.idade}</h1>
    </div>
  );
};
```

Neste exemplo, nosso `Componente` recebe a propriedade `data` e renderiza `nome` e `idade`. Caso o componente não receba a propriedade, normalmente iria estourar um erro ou renderizaria `undefined` ou `null` em tela. Dito isto, podemos colocar uma condição antes do nosso `retorno padrão do componente`, neste caso adicionamos para caso o `componente não receba a propriedade data`, ele renderize uma div com o texto `Dados não encontrados`. Quando ele receber o valor, ele irá partir para a renderização padrão.

`Nota: Isso é o mesmo que utilizar IF ELSE. Se acontecer algo faça tal, se não, faça isso.`

# Condicionando no JSX

Graças ao JSX, assim como virmos nos estados, podemos colocar variaveis dentro do nosso HTML, até mesmo fazer listas com 'map'. Ou seja, `podemos utilizar código javascript dentro do HTML`. Com isso também podemos fazer algumas condições dentro deles, utilizando alguns operadores como o `ternário e o AND(&&)`.

# Condicionando com operador ternário

Vamos direto ao exemplo:

```jsx
import { useState, useEffect } from 'react';

const Componente = () => {
  const [isLoading, setIsLoading] = useState(true);

  useEffect(() => {
    setTimeout(() => setIsLoading(false), 3000);
  }, []);

  return (
    <div>
      {isLoading ? (
        <p>Loading...</p>
      ) : (
        <div>
          <h1>Nome</h1>
          <h1>Idade</h1>
        </div>
      )}
    </div>
  );
};
```

No exemplo acima, temos um componente com o estado de `isLoading`
que quando for `true`, deve aparecer um texto escrito `loading` em tela. E quando for `false` deve aparecer os outros componentes. E isso tudo utilizando o ternário dentro do HTML.

# Condicionando com operador AND(&&)

```jsx
import { useState, useEffect } from 'react';

const Componente = () => {
  const [isLoading, setIsLoading] = useState(true);

  useEffect(() => {
    setTimeout(() => setIsLoading(false), 3000);
  }, []);

  return (
    <div>
      <h1>Nome</h1>
      <h1>Idade</h1>
      {isLoading && <p>Loading...</p>}
    </div>
  );
};
```

Neste exemplo, alteramos o exemplo com `ternários` para mostrar o `AND operator, mais conhecido como &&`. Nesta situação, o elemento com o texto `loading...` só irá aparece quando o `isLoading` for `true`, quando for `false` será removido da tela. Como vocês podem ver, neste caso é `se for true renderize, se não, não renderize`.

É muito bom utilizar quando temos elementos que só podem aparecer em tela sob alguma condição e não afeta os outros elementos.

# Aumentando a complexidade com o OR(||)

O operador OR(||) também conhecido como `OU` pode trazer uma complexidade maior e é muito util a depender do que você precisa na sua aplicação.

Exemplo misto com o operador ternário.

```jsx
import { useState, useEffect } from 'react';

const Componente = () => {
  const [isLoading, setIsLoading] = useState(true);
  const [hasError, setHasError] = useState(false);

  useEffect(() => {
    setTimeout(() => {
      setIsLoading(false);
      setHasError(true);
    }, 3000);
  }, []);

  return (
    <div>
      {isLoading || hasError ? (
        <p>Loading...</p>
      ) : (
        <div>
          <h1>Nome</h1>
          <h1>Idade</h1>
        </div>
      )}
    </div>
  );
};
```

Neste exemplo, temos um novo estado chamado `hasError` que iniciará como `false` e ao terminar os três segundos do `setTimeout` irá ter seu valor alterado para `true`. Podemos ver uma leve diferença na condição do ternário, agora caso `isLoading ou hasError forem true` irá renderizar o texto "Loading...". Neste caso, se qualquer um dos dois estados for true, não irá renderizar as informações.

Exemplo com AND(&&):

```jsx
import { useState, useEffect } from 'react';

const Componente = () => {
  const [isLoading, setIsLoading] = useState(true);
  const [hasError, setHasError] = useState(false);

  useEffect(() => {
    setTimeout(() => {
      setIsLoading(false);
      setHasError(true);
    }, 3000);
  }, []);

  return (
    <div>
      <h1>Nome</h1>
      <h1>Idade</h1>
      {(isLoading || hasError) && <p>Loading...</p>}
    </div>
  );
};
```

Neste exemplo, basicamente `se isLoading ou hasError for true, renderiza o <p>Loading...</p>`

# Conclusão

Neste tópico você aprendeu sobre `Renderização condicional` no React, tenha certeza que irá utiliza-la com frequencia em seu dia a dia.

Caso queira saber mais, segue o link da documentação do [React](https://react.dev/learn/conditional-rendering#conditionally-assigning-jsx-to-a-variable)

Espero que tenham gostado do conteúdo, aso surja alguma duvida, sinta-se livre para entrar em contato! Então é isso, até a proxima! Seeyaaaa.

[Ir para a próxima seção](./8-React%20Hooks.md)

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>
```
