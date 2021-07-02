<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

# Estados

Neste capítulo você entenderá o que são **Estados** no React.

## O que é?

Estados são dados que podem variar, sendo que essa variação pode ser causada pela ação do usuário em sua aplicação. Normalmente já trabalhamos com isso, sabe quando você faz um contador em javascript e o valor fica toda hora alterando de 0, 1, 2, 3 , 4, etc... Isso são estados. No caso do React os estados também são uma forma de verificação para a renderização, então quando esse valor(estado) é alterado causa uma nova renderização.

<p>**Esse também é um dos motivos do React ser one way databinding**(Significa que ele observa as mudanças por apenas um caminho para então atualizar a arvore de elementos(DOM)).</p>

Vamos pra mais um exemplo:

<p>Suponha que tu faça uma aplicação de contador, quando tu apertar start ele sairá do 0 e ficará mudando. Vemos aqui que o estado inicial da aplicação é 0 e conforme ele vai sendo alterado o valor em tela também é.</p>

## Como fazer no React?

Bom no React temos algumas formas de lidar com isso, seja pelos hooks ou pelos componentes de classe.
Como não falamos sobre hooks ainda, trabalharemos apenas com componentes de classe.

Nesse exemplo vamos trabalhar apenas com um estado, porém é possivel por quantos quiser no objeto.

```js
import React from 'react';

class Counter extends React.Component {
  // No contrutor de classe, criamos nossos estados através do this.state
  constructor(props){
    super(props);
    this.state = {
      counter: 0,
    }
  }

 // É possivel acessar o estado com this.state.nome do estado
  render(){
    return (
      <div>
        <h1> Contador: {this.state.counter}</h1>
        <span>
      </div>
    )
  }
}
```

Agora o React trabalha com conceitos de imutabilidade, portantdo você nunca poderá alterar um dado diretamente. Como por exemplo: this.state.counter = 10; Ele não permite isso.

Com o conceito de imutabilidade, sempre iremos definir novos dados ao invez de modificar o dado.
Para isso o React usa uma função chamada setState que adiciona um novo valor a variavel.

```js
  // No contrutor de classe, criamos nossos estados através do this.state
  constructor(props){
    super(props);
    this.state = {
      counter: 0,
    }
  }

  function handlePlusCounter(){
    // Através da função setState, podemos definir novos valores.
    this.setState({
      counter: this.state.counter + 1;
    })
  }

  function handleMinusCounter(){
    this.setState({
      counter: this.state.counter - 1;
    })
  }

 // É possivel acessar o estado com this.state.nome do estado
  render(){
    return (
      <div>
        <h1> Contador: {this.state.counter}</h1>
        <button onClick={handlePlusCounter}>+</button>
        <button onClick={handleMinusCounter}>-</button>
        <span>
      </div>
    )
  }
}
```

Então o que acontece no exemplo acima? Se tu clicar em "+", o estado terá um novo valor "1" e terá uma nova renderização, onde em tela o valor será atualizado também. E se tu apertar "-", o atual valor 1 voltará a ser 0 e causará uma nova renderização fazendo com que tu veja 0 em tela.

O conceito de estado e seu uso no React é bem simples porém conforme a aplicação cresce a complexidade aumenta.

Nos próximos capítulos vocês aprenderão sobre **Ciclo de vida de um componente** e **Hooks**.

[Ir para Próxima Seção](./6-React%20Hooks.md)

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>
