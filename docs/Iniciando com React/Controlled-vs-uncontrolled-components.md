<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

# Controlled Components vs Uncontrolled Components

## Controlled Components

Os Controlled Components (componentes controlados) tem o React como responsável por controlar seus valores. O componente se torna controlado quando sobreescrevemos o valor da DOM, por exemplo, ao colocar a propriedade `value` em um componente de `input`. Com isso, nossa fonte de dado confiável é o estado, pois está controlando o componente, logo, se não atualizarmos o estado, a DOM não será atualizada.

A cada vez que o usuário digita algo, o estado é atualizado e por consequência o componente rerenderiza novamente. Por conta disso, validações em tempo real são utilizadas neste tipo de componente. 

```jsx
const Component = () => {
  const [name, setName] = useState("")

  return (
    <input
      value={name}
      onChange={event => setName(event.target.value)}
    />
  )
}
```

Para passar um valor padrão, basta colocar um valor inicial no estado que está controlando o componente.

```diff
const Component = () => {
- const [name, setName] = useState("")
+ const [name, setName] = useState("4noobs")

  return (
    <input
      value={name}
      onChange={event => setName(event.target.value)}
    />
  )
}
```

## Uncontrolled Components

Os Uncontrolled Components (componentes não controlados) tem a DOM como responsável por controlar seus valores, ou seja, quando precisamos de seus valores, precisamos pegar diretamente da DOM. Podemos fazer isso com o uso do hook [useRef](./8.4-useRef.md), que utiliza a referência do elemento da DOM para que seja possível acessar seus valores.

```jsx
const Component = () => {
  const emailInput = useRef(null)

  const handleClick = () => {
    console.log(emailInput.target.value)
  }

  return (
    <>
      <button onClick={handleClick}>Ver valor do email</button>
      <input
        ref={emailInput}
      />
    </>
  )
}
```

Para passar um valor padrão, basta colocar a propriedade `defaultValue` com um valor inicial para o componente.

```diff
const Component = () => {
  const emailInput = useRef(null)

  const handleClick = () => {
    console.log(emailInput.target.value)
  }

  return (
    <>
      <button onClick={handleClick}>Ver valor do email</button>
      <input
        ref={emailInput}
+       defaultValue="he4rt@4noobs.com"
      />
    </>
  )
}
```

[Ir para a próxima seção](./Listas-no-react.md)

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>