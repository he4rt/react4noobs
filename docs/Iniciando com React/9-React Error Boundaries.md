<p align="center">
<a href="https://github.com/he4rt/4noobs" target="_blank">
<img src="../../assets/global/header-4noobs.svg">
</a>
</p>

# O que é Error Boundaries?

Antes do React 16 as aplicações costumavam quebrar quando ocorria algum erro de javascript, como por exemplo erro de tipagem. Os componentes corrompiam o estado interno e retornavam erros imcompreensíveis, os quais eram causados por algum problema em outra parte do código, mas não tinhamos como trata-los, então as aplicações acabavam crashando e o usuário era forçado a recarregar a página. Além de corromper o estado interno, quando acontece um erro que não é tratado, o React desmonta toda a arvore de componentes.

A partir do React 16, temos o conceito de Error boundaries que é basicamente um trycatch em forma de componente, utilizados para capturar e tratar erros de javascript. Os componentes de error boundaries são necessariamente componentes de classe, porque devem acessar ao método `componentDidCatch(error, info)`, que é o método responsável por capturar o erro em tempo de execução. Também podemos usar o hook `react-error-boundary` caso opite por componentes funcionais, mas não temos nenhum hook equivalente ao `componentDidCatch()`.

É ideal usar um Error Boundary para evitar crashs na aplicação, como tratamento de erros e para exibir uma interface alternativa para o usuário.

Em certos tipos de erro não conseguimos usar o Error Boundary:

- Manipuladores de evento
- Código assíncrono (ex. callbacks de setTimeout ou requestAnimationFrame)
- Renderização no servidor
- Erros lançados na própria error boundary (ao invés de em seus filhos)

# Utilização

Nesse componente estamos usando o try...catch para tratar um erro no componente `<Counter />`, e isso de fato funciona, a tag `h1` é exibida no tratamento do erro.

```jsx
import React from 'react'

const Counter = () => {
  try {
    users?.map(({ user }) => {
      return <h1>He4rt User: {user}</h1>
    })
  } catch {
    return <h1>Deu ruim</h1>
  }
}

const App = () => {
  return <Counter />
}

export default App
```

![Aviso de aplicação compliada com o seguinte erro: 'users' is not defined](../../assets/error-boundaries-1.png)

Mesmo dando erro, ele compila a aplicação:

![Aplicação rodando com o título 'Deu ruim'](../../assets/error-boundaries-2.png)

---

Porém, se não queremos usar o `try...catch` dentro do `Counter` e passar ele para um contexto superior, o `App` não irá conseguir tratar o erro, vejamos:

```jsx
import React from 'react'

const Counter = () => {
  users?.map(({user}) => {
    return <h1>He4rt User: {user}</h1>
  })
}

const App = () => {
  try{
    return <Counter />
  } catch(){
    return <h1>Deu ruim</h1>
  }
}

export default App
```

Erro:
![Crash na aplicação por conta do seguinte erro: 'users' is not defined](../../assets/error-boundaries-3.png)

E isso traria problemas caso quiséssemos tratar o erro de uma renderização de páginas por exemplo, e quiséssemos usar a mesma tratativa para todas as páginas.

# Criando um componente Error Boundaries

Vamos criar um componente Error Boundaries usando um componente de classe, é importante lembrar que componentes de classes estão defasados, mas é importante entender caso se depare com algum na sua jornada.

```jsx
import React, { Component } from 'react'

class ErrorBoundary extends Component {
  constructor(props) {
    super(props)
    this.state = { hasError: false }
  }

  // Este método é chamado quando ocorre um erro em qualquer componente filho
  componentDidCatch(error, info) {
    this.setState({ hasError: true })
    // Você pode registrar o erro ou realizar ações específicas aqui
    console.error('Erro capturado:', error)
    console.error('Informações do erro:', info)
  }

  render() {
    // Se ocorreu um erro, você pode renderizar uma mensagem de erro personalizada
    if (this.state.hasError) {
      return <p>Desculpe, algo deu errado.</p>
    }

    // Se não houve erro, renderiza normalmente os componentes filhos
    return this.props.children
  }
}

// Exemplo de componente que pode gerar um erro
class ComponenteComErro extends Component {
  render() {
    // Simulando um erro (isso seria geralmente uma operação que pode falhar)
    throw new Error('Erro simulado!')
    return <div>Conteúdo do componente com erro</div>
  }
}

// Componente pai usando o ErrorBoundary
class App extends Component {
  render() {
    return (
      <ErrorBoundary>
        <div>
          <h1>Minha Aplicação</h1>
          <ComponenteComErro />
        </div>
      </ErrorBoundary>
    )
  }
}

export default App
```

Podemos ver nesse exemplo aspectos importantes do Error Boundaries. Criamos nosso método que vai ser chamado sempre que ocorrer um erro não tratado em QUALQUER componente filho. Em seguida criamos um componente que pode gerar um erro e envolvmentos o componente de Error Boundary na aplicação, onde será gerado um erro em um dos componentes filhos e exibir a mensagem ''Desculpe, algo deu errado.'' na tela.

# Utilizando o `react-error-boundary`

Como visto anteriormente, necessariamente componentes de Error Boundary são criados como componentes de classe, mas componentes de classe já estão depreciados. Então podemos usar o [react-error-boundary](https://github.com/bvaughn/react-error-boundary) para utilizar Error Boundaries como componentes funcionais que está mais próximo aos códigos React que vemos no dia a dia.

Vejamos como implementar o `react-error-boundary` seguindo o mesmo exemplo anterior:

```jsx
import React from 'react'

import { ErrorBoundary } from 'react-error-boundary'

const Counter = () => {
  users?.map(({ user }) => {
    return <h1>He4rt User: {user}</h1>
  })
}

const ErrorHandler = () => {
  return <h1>Eita, deu ruim! D:</h1>
}

const App = () => {
  return (
    <ErrorBoundary FallbackComponent={ErrorHandler}>
      <Counter />
    </ErrorBoundary>
  )
}

export default App
```

Resultado:

![Resultado do código anterior compilado, com o título: 'Eita, deu ruim! D:' sendo exibido](../../assets/error-boundaries-4.png)

Terminal:

![Resultado do terminal com o aviso de erro: 'users is not defined' sendo exibido](../../assets/error-boundaries-5.png)

Veja que criamos um componente fallback para exibir caso ocorra algum erro em qualquer componente que está encapsulado no `<ErrorBoundary />`, onde diferente do `try...catch`, conseguimos fazer uma tratativa de erro global. Então se tivessemos vários componentes encapsulados no `<ErrorBoundary />` e algum deles ocorresse algum erro que não foi tratado localmente, seria exibido o componente da fallback

# Método `onError`

Usando o exemplo anterior, podemos adicionar o método `onError`:

```jsx
import React from 'react'

import { ErrorBoundary } from 'react-error-boundary'

const Counter = () => {
  users?.map(({ user }) => {
    return <h1>He4rt User: {user}</h1>
  })
}

const ErrorHandler = () => {
  return <h1>Eita, deu ruim! D:</h1>
}

const App = () => {
  return (
    <ErrorBoundary
      FallbackComponent={ErrorHandler}
      onError={(arg1, arg2) => {
        console.log({ arg1, arg2 })
      }}
    >
      <Counter />
    </ErrorBoundary>
  )
}

export default App
```

Perceba que adicionamos uma `prop` `onError` no `<ErrorBoundary />`, se vermos o resultado `console.log` do `onError`:

![Resultado do console.log do onError do código anterior](../../assets/error-boundaries-6.png)

Com o `onError` conseguimos retornar no `arg1` o erro que causado na aplicação e no `arg2` temos informações do source map. Com isso podemos utilizar alguns serviços para monitorar os erros da aplicação, como sentry, kibana, etc...

Veja como ficaria o código se quiséssemos usar o onError para disparar algum evento em algum serviço:

```jsx
import React from 'react'

import { ErrorBoundary } from 'react-error-boundary'

const Counter = () => {
  users?.map(({ user }) => {
    return <h1>He4rt User: {user}</h1>
  })
}

const ErrorHandler = () => {
  return <h1>Eita, deu ruim! D:</h1>
}

const notifyError = () => {
  // func para mandar notificação de erro para o sentry ou alguma outra plataforma de monitoramento
}

const App = () => {
  return (
    <ErrorBoundary
      FallbackComponent={ErrorHandler}
      onError={(arg1, arg2) => {
        // Quando ocorre um erro não tratado, o React desmonta toda a tela.
        console.log({ arg1, arg2 })
      }}
    >
      <Counter />
    </ErrorBoundary>
  )
}

export default App
```

Em situações de erro não tratado, o React adota uma abordagem mais drástica, desmontando a árvore de componentes para manter a estabilidade e prevenir efeitos colaterais indesejados. Por isso é importante enfatizar o uso de componentes Error Boundaries para capturar e lidar com erros de forma controlada.

---

Podemos também registrar o erro para observabilidade. Veja o exemplo:

```jsx
import React from 'react'
import { ErrorBoundary } from 'react-error-boundary'

// Simulando um erro
const Counter = () => {
  throw new Error('Erro simulado!')
  return <h1>He4rt User: {user}</h1>
}

const ErrorFallback = ({ error, resetErrorBoundary }) => {
  // Aqui, podemos registrar o erro para observabilidade
  registrarErroParaObservabilidade(error)

  return (
    <div role="alert">
      <p>Algo deu errado. Estamos trabalhando para resolver o problema!</p>
      <button onClick={resetErrorBoundary}>Tentar novamente</button>
    </div>
  )
}

const registrarErroParaObservabilidade = (error) => {
  // Simulando o envio do erro para um serviço de observabilidade (por exemplo, Sentry)
  console.error('Erro enviado para observabilidade:', error)
  // Lógica adicional para enviar o erro para um serviço externo
  // Exemplo: Sentry.captureException(error);
}

const App = () => {
  return (
    <ErrorBoundary
      FallbackComponent={ErrorFallback}
      onError={(error, info) => {
        // Aqui você pode enviar o erro para um serviço de monitoramento
        // ou realizar outras ações de tratamento.
        console.error('Erro:', error)
        console.error('Informações do erro:', info)
      }}
    >
      <Counter />
    </ErrorBoundary>
  )
}

export default App
```

Podemos ver que a função `registrarErroParaObservabilidade` é chamada dentro do componente `ErrorFallback` com o objetivo de simular o envio do erro para um serviço de observabilidade, como o Sentry. Essa lógica pode ser adaptada para se integrar com o serviço de observabilidade escolhido em sua aplicação. Importante lembrar de personalizar a função de acordo com as necessidades específicas de cada aplicação e do serviço de observabilidade que a mesma esta utilizando.

# Error Boundary com StackTrace

Também podemos utilizar o error boundaries para exibir informações detalhadas de erro de forma mais amigável e sem desmontar toda a tela.
Vejamos o exemplo a seguir:

```jsx
import React from 'react'
import { ErrorBoundary } from 'react-error-boundary'

// Simulando o erro
const Counter = () => {
  throw new Error('Erro simulado!')
  return <h1>He4rt User: {user}</h1>
}

const ErrorFallback = ({ error, resetErrorBoundary }) => {
  return (
    <div role="alert">
      <p>Algo deu errado:</p>
      <pre style={{ whiteSpace: 'normal' }}>{error.message}</pre>
      <button onClick={resetErrorBoundary}>Tentar novamente</button>
    </div>
  )
}

const App = () => {
  return (
    <ErrorBoundary
      FallbackComponent={ErrorFallback}
      onError={(error, info) => {
        // Aqui podemos enviar o erro para um serviço de monitoramento
        // ou realizar outras ações de tratamento.
        console.error('Erro:', error)
        console.error('Informações do erro:', info)
      }}
    >
      <Counter />
    </ErrorBoundary>
  )
}

export default App
```

Nesse exemplo, podemos ver que `ErrorFallback` é chamada quando ocorre um erro dentro do componente `Counter`. O componente `ErrorBoundary` fornece um objeto `error` contendo informações sobre o erro, incluindo a mensagem de erro. Esse objeto pode ser usado para exibir o `stack trace` de maneira mais simplificada.

Lembrando que devemos adaptar esse exemplo de acordo com as necessidades específicas para cada aplicação. Onde o componente ErrorFallback deve ser construído para exibir informações de erro de acordo com as especificidades que varia de cada aplicação.

# Conclusão

Vimos como encapsular e tratar erro genericos de maneira global usando Error Boundaries com componentes de classe, também vimos na prática como utilizar usando o `react-error-boundary`.

Fica a dica de praticar um pouco em projetos pessoais. Não é algo que você vai usar com frequência no dia a dia, mas é importante entender esse conceito para ter mais uma carta na manga na hora de tratar erros em React.

# Referências

- [Doc antiga do react](https://pt-br.legacy.reactjs.org/docs/error-boundaries.html)
- [Error Boundaries no ReactJS - Tratamento de Erros #014](https://www.youtube.com/watch?v=6FRzHRoZmG8&ab_channel=Jo%C3%A3oBibiano)
- [A FORMA CORRETA DE TRATAR ERROS NO REACT](https://youtu.be/cV4JswN3L24)
- [Trate erros de JavaScript no React com Error Boundaries](https://youtu.be/vfwbOgpSvQA)

[Ir para a próxima seção](./Controlled-vs-uncontrolled-components.md)

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>
