<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="./.github/images/header_4noobs.svg">
  </a>
</p>

Aviso:

Esta documentação tem como intenção ser o seu pontapé inicial para começar o desenvolvimento de um projeto React dentro de um ambiente preparado para o Typescript.

Se você quiser se aprofundar ainda mais sobre cada um desses temas e sobre o funcionamento do Typescript em si através de vários exemplos sinta-se livre para visitar o [Typescript4noobs!](https://github.com/Carolis/typescript4noobs)


# O que é o Typescript?

Typescript é considerado um **superset** da linguagem Javascript, dito isso, se você já sabe Javascript é muito fácil de começar a usá-lo já sabendo um pouco.
Ele tem como  principal funcionalidade a capacidade de adicionar **tipagens estáticas** ao código.
Um dos pontos positivos que vale a pena ser citado é a possibilidade de termos arquivos Typescript convivendo no mesmo projeto com arquivos Javascript já que no final das contas o Typescript é compilado para Javascript, ou seja, é uma ferramenta de **desenvolvimento**. Isso também permite que você adicione Typescript em qualquer momento do seu projeto, conforme necessidade e gosto pessoal.

### Por que usar Typescript?

O uso de Typescript traz segurança principalmente na detecção de **erros inesperados**. Um exemplo clássico seria o problema do operador `+` do Javascript que, dada uma soma com tipagens erradas poderia retornar erroneamente uma **concatenação** ao invés da soma propriamente dita.

```ts
function soma(x, y) {
    return x + y;
}
```

Chamando a função `soma(2,2)` o retorno seria `4`;

Chamando a função `soma('2','2')` o retorno seria `22`;

Esse problema seria facilmente evitado ao tiparmos as variáveis corretamente como números.

---

Outra grande vantagem de usar o Typescript é o aumento da inteligência dentro do seu editor ou IDE, o famoso **[IntelliSense](https://code.visualstudio.com/docs/editor/intellisense)** e a possibilidade de usar **parâmetros opcionais**. Além disso, as tipagens podem funcionar como uma mini documentação dentro do seu arquivo, facilitando futuras manutenções e fazendo com que todos esses fatores tragam uma camada a mais de segurança para o código.

# Instalando o Typescript ao lado do React

É possível inicializar um projeto react com um template para typescript de várias formas, uma delas se utilizando do create-react-app específico para o typescript, usando os seguintes comandos:

PS: antes de seguir com a instalação do typescript é importante ter o **node** previamente instalado.

`yarn create react-app my-app --template typescript` ou `npx create-react-app my-app --template typescript` 

Após isso, toda a estrutura de arquivos virá inicializada em torno de um ambiente preparado para o Typescript.

Ainda vale lembrar que você não precisa necessariamente usar um template através do create-react-app, sendo possível inicializar toda sua estrutura de arquivos do zero conforme gosto e necessidade.

# Tipos

Tipar variáveis é bem simples, como demonstrado no exemplo abaixo basta que você adicione `:tipo` depois de uma variável.

Exemplos:

```ts
let numero: number
numero = 3

let isTrue: boolean
isTrue = true
```

O Typescript desfruta de alguns tipos primitivos mais comuns, sendo eles:

`:number` 

`:string` 

`:boolean` 

`:bigInt` 

`:symbol` 

`:null` 

`:undefined` 

Você pode conferir ainda mais tipos e conferir exemplos para cada um deles consultando o repositório [Typescript4noobs](https://github.com/Carolis/typescript4noobs).

Abaixo seguem alguns exemplos de como ficaria a estrutura de um componente React num ambiente que faz uso de Typescript.

Componente **funcional** com Typescript: 

```ts
import React, { FunctionComponent, useState } from 'react'

interface Props {
  message: string
}

const App: FunctionComponent<Props> = props => {
  const [hasMessage, setHasMessage] = useState<boolean>(false)
  return <p>{hasMessage ? props.message : 'Default Message'}</p>
}

export default App
```

Componente de **classe** com o Typescript:

```ts
import React, { Component } from 'react'

interface AppProps {
  text: string
}

interface AppState {
  value: number
}

export default class App extends Component<AppProps, AppState> {
  constructor(props: IAppProps) {
    super(props)

    this.state = {
      value: 0
    }
  }

  public render() {
    return (
      <div>
        <p>{this.props.text}</p>
        <p>{this.state.value}</p>
      </div>
    )
  }
}
```

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="./.github/images/footer_4noobs.svg" width="380">
  </a>
</p>