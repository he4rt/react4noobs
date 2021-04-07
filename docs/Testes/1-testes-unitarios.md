<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

# Testes Unitários

<p align="center">
  <img src="../../assets/unittest_faucet.gif">
</p>

## O que são Testes Unitários ?

Testes unitários podem ser definidos como porções de códigos responsáveis por validar o comportamento de unidades funcionais de código, sendo unidades funcionais qualquer componente que através de sua invocação possa gerar o resultado esperado. Podemos, então, pensar incilamnete em testes unitários no contexto de funções puras, que por sua vez são funções as quais não alteram o estado da nossa aplicação, tais como funções de soma de dois números. Segue um exemplo:

```js
function sum(a, b) {
  return a + b;
}
```

Porém, podemos expandir o conceito de teste unitários para coisas mais complexas, como por exemplo, no contexto do React, a renderização de um componente e verificar se o mesmo é renderizado, se é renderizado com o comportamento esperado e até mesmo lidando com eventos do próprio componente tais como cliques.

## A importância e o ciclo do TDD

TDD, ou Test-Driven Development (Desenvolvimento Orientado a Testes) é uma técnica de desenvolvimento de software fundamental para a validação de uma aplicação, muito utilizada pelas empresas e cobrada dos seus desenvolvedores. Essa prática minimiza os erros da aplicação, garantindo que em ambiente de produção ela ocorra da forma esperada.

O Ciclo de TDD pode ser definido em três etapas: Criação, Falha, Refatoração. No primeiro, criamos o teste do qual queremos validar, em seguida passamos para a segunda etapa, onde forçamos o teste a falhar e assim temos certeza do funcionamento do teste, por fim passamos para a Refatoração, na qual refatoramos o teste, agora otimizando-o e fazendo-o passar.

## Ferramentas utilizadas em testes de integração

Para aplicações escritas em javascript, é muito comum o uso do _framework_ de teste chamado [Jest](https://jestjs.io/). Ele é responsável pela estrutura do arquivo de teste, e nos permite criar conjuntos e cenários para que possamos criar as asserções que queremos.

Já para manipulação do DOM, podemos utilizar a biblioteca [React Testing Library](https://testing-library.com/docs/react-testing-library/intro). Ela nos permite renderizar e fazer _queries_ no nosso DOM para criarmos nossas asserções.

Além disso, temos outro _framework_ famoso no mercado, [Enzyme](https://enzymejs.github.io/enzyme/) utilizado principalmente no contexto de componentes funcionais React e teste de frontend graças à sua compatibilidade com outros frameworks de testes tais como o Jest,facilitando assim a criação de _Mocks_ para testes.

## Exemplos de Teste de Integração

> Configurações

No caso, usaremos a React Testing Library, a qual já vem com configurações pré-setadas, para isso, basta que criemos uma pasta com o nome " ** tests ** " dentro do nosso diretório "src" e então nomearemos nossos arquivos de testes com a seguinte extensão: .test.js .

No exemplo a seguir testaremos uma função pura de soma, então vamos nomeá-lo de: "sum.test.js"

> Vamos pensar no caso de uma função de soma

Queremos apenas testar a funcionalidade de uma função de soma certo? Nesse caso, um teste unitário será o mais adequado para ela.

```js
function sum(a, b) {
  return a + b;
}

it('Should sum 3,2 and return 5', () => {
  const sum = sum(3, 2);
  expect(sum).toBe(5);
});
```

Nesse teste, estamos usando os métodos "it,expect e toBe". As constatações, através do método it() devem informar o que o teste propôe, e no segundo parâmetro, através de uma _callback_ criar o teste. O expect() é o que guardará o objeto a ser validado, sendo que deverá ser ligado a um método de validação. No exemplo usamos o "toBe", ou seja, esperamos que sum seja 5. "Expect sum toBe 5". Então, teriamos nosso teste validado e ele passaria já que esperamos que ao somar 3 e 2 teriamos como resultado 5.

Seguindo o ciclo de TDD.

```js
it('Should sum 3,2 and return 5', () => {
  const sum = sum(3, 3);
  expect(sum).toBe(5);
});
```

Nesse caso o teste não passaria, pois esperamos que o resultado seja 5, porém os números somados (3,3) tem como soma o valor 6 e não cinco. Com isso, sabemos que a nossa função de soma está correta e agora podemos refatorar nosso código de uma forma genérica.

```js
it('Should sum two numbers an return its correct sum', () => {
  const first_sum = sum(3, 3);
  const second_sum = sum(4, 5);

  expect(first_sum).toBe(6);
  expect(second_sum).toBe(9);
});
```

Nosso teste passaria pois as duas expectativas são cumpridas e logo a constatação é válida.

## Testes Unitários no contexto do React

Abstraindo mais um pouco, podemos chegar ao contexto dos componentes e do React, seguindo o mesmo princípio, veja o exemplo a seguir:

```jsx
import React from 'react';
import {
  render,
  screen,
  getByLabelText,
  getByTestId,
  toHaveTextContent,
  toHaveAttribute,
} from '@testing-library/react';

export const LabelInput = () => {
  return (
    <div>
      <label data-testid="label1">Teste</label>
      <input data-testid="input1" placeholder="Input de teste" />
    </div>
  );
};

describe('LabelInput testing', () => {
  it('Should render LabelInput correctly', () => {
    render(<LabelInput />);

    const labelText = screen.getByLabelText('Teste');
    const input = screen.findByTestId('input1');

    expect(labelText).toHaveTextContent('Teste');
    expect(input).not.toHaveAttribute('readonly');
  });
});
```

Repare que nesse exemplo criamos um componente LabelInput o qual renderiza um Label e seu input. Para o teste, precisamos renderizar o componente primeiro e depois verificamos e ele possui o texto e se possui o atributo. Lembrando que nessa etapa estamos no ciclo de Refatoração do TDD.

Mais funcionalidades da React Library Testing podem ser vistas através desse [link](https://testing-library.com/docs/react-testing-library/api).

O mundo dos testes é bem amplo e necesário, portanto compensa muito gastarmos um tempo amais estudante este assunto.

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>
