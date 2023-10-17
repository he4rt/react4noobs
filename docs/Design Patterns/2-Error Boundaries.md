<p align="center">
<a href="https://github.com/he4rt/4noobs" target="_blank">
<img src="../../assets/global/header-4noobs.svg">
</a>
</p>

# O que é Error Boundaries?

Antes do React 16 as aplicações costumavam crashar quando ocorria algum erro de javascript, como por exemplo erro de tipagem. Os componentes corrompiam o estado interno e retornavam erros imcompreensíveis, erros esses causados por erros anteriores no código da aplicação, mas não tinhamos como trata-los, então as aplicações acabavam crashando e o usuário era forçado a recarregar a página.

A partir do React 16, temos o conceito de Error boundaries que é basicamente um trycatch em forma de componente, utilizados para capturar e tratar erros de javascript. Os componentes de error boundaries são necessariamente componentes de classe, porque devem acessar ao método `componentDidCatch(error, info)`, que é o método responsável por capturar o erro em tempo de execução. Também podemos usar o hook `react-error-boundary` caso opite por componentes funcionais, mas não temos nenhum hook equivalente ao `componentDidCatch()`.

É ideal usar um Error Boundary para evitar crashs na aplicação, como tratamento de erros e para exibir uma interface alternativa para o usuário.

Em certos tipos de erro não conseguimos usar o Error Boundary:

- Manipuladores de evento
- Código assíncrono (ex. callbacks de setTimeout ou requestAnimationFrame)
- Renderização no servidor
- Erros lançados na própria error boundary (ao invés de em seus filhos)

# Utilização

Nesse componente estamos usando o try catch para tratar um erro no componente `<Counter />`, e isso de fato funciona, a tag `h1` é exibida no tratamento do erro.

```jsx
import React from 'react'

const Counter = (props) => {
  try {
    users?.map((user) => {
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

Mesmo dando erro, ele compila a aplicação:
![Alt text](../../assets/error-boundaries-1.png)

![Alt text](image-3.png)

Mas se passarmos o trycatch para um contexto superior, ele não irá conseguir tratar o erro

![Alt text](image-4.png)

![Alt text](image-5.png)

E isso traria problemas caso quiséssemos tratar o erro de uma renderização de páginas por exemplo, e quiséssemos usar a mesma tratativa para todas as páginas.

Utilizando o `react-error-boundary`

![Alt text](image-6.png)

![Alt text](image-7.png)

Veja que criamos um componente fallback para exibir caso ocorra algum erro em qualquer componente que está encapsulado no `<ErrorBoundary />`, onde diferente do `trycatch`, conseguimos fazer uma tratativa de erro global.

### Método `onError`

![Alt text](image-8.png)
![Alt text](image-9.png)

Com o `onError` conseguimos retornar no `arg1` o erro que causado na aplicação e no `arg2` temos informações do source map. Com isso podemos utilizar alguns servicos para monitorar os erros da aplicação, como sentry, kibana, etc...

![Alt text](image-10.png)

## Referências

- [Doc antiga do react](https://pt-br.legacy.reactjs.org/docs/error-boundaries.html)
- [Error Boundaries no ReactJS - Tratamento de Erros #014](https://www.youtube.com/watch?v=6FRzHRoZmG8&ab_channel=Jo%C3%A3oBibiano)
- [A FORMA CORRETA DE TRATAR ERROS NO REACT](https://youtu.be/cV4JswN3L24)
- [Trate erros de JavaScript no React com Error Boundaries](https://youtu.be/vfwbOgpSvQA)
