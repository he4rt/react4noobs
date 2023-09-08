<p align="center">
<a href="https://github.com/he4rt/4noobs" target="_blank">
<img src="../../assets/global/header-4noobs.svg">
</a>
</p>

# O Que é Compound Components?

O Compound Components é um padrão avançado em React.
Tem como objetivo criar um design mais flexível, permitindo o compartilhamento de estado e lógica entre um grupo de componentes. Onde a comunicação entre o componente pai e os componentes filhos devem ser feitas de maneira flexível. Os componentes devem trabalhar juntos para realizarem algum comportamento sem criar árvores de props embaraçosas ou uma lógica complexa demais para ser refatorado ou compreendido futuramente.

Esse padrão nos ajuda a eliminar inflamações de props, onde temos que passar uma árvore de props entre os componentes. Essa injeção de props é um problema, pois pode causar vários re-renders desnecessários a cada estado que for atualizado, já que cada estado irá atualizar todos os componentes filho.

Temos um exemplo de Compound Components na estrutura do `select` e `option` das tags em HTML:

```jsx
<select>
  <option value="Danielhe4rt">Danielhe4rt</option>
  <option value="Gabriel">Gabriel</option>
  <option value="Marcelo">Marcelo</option>
</select>
```

![Demonstração de como é utilizado Compound Components nas tags HTML select e option](/assets/example-select-compound-components.png)

O `select` funciona como um gerenciador de estados da inferface, enquanto o `option` são configurados em como o `select` deve funcionar.

# Exemplo utilizando Compound Components

Neste exemplo, vamos criar um `Modal`, que é dividida em dois componentes compostos: `Toggle` e `Content`. Onde vão compartilhar o estado de abrir e fechar o modal entre eles.

Vamos ver como seria criar esse componente passo a passo:

1. Podemos começar criando a context responsável por gerênciar o state de abrir e fechar o modal

```jsx
import { createContext, useState } from 'react'

export const ModalContext = createContext()

export const ModalStorage = ({ children }) => {
  const [isOpen, setIsOpen] = useState(false)

  return (
    <ModalContext.Provider value={{ isOpen, setIsOpen }}>
      {children}
    </ModalContext.Provider>
  )
}
```

2. Criando a base do componente Modal

```jsx
import { ModalStorage } from './context'

const Modal = ({ children }) => {
  return <ModalStorage>{children}</ModalStorage>
}

export default Modal
```

Perceba que estamos usando `children`, para pegar os componentes que serão inseridos dentro do Modal, vamos querer usa-lo assim:

```
<Modal>
  <Modal.Toggle>...</Modal.Toggle>
  <Modal.Content>
    <p>conteúdo do modal</p>
  </Modal.Content>
</Modal>
```

3. Agora precisamos criar o componente toggle, que vai ser responsável por abrir o Modal

```jsx
import { useContext } from 'react'

import { ModalContext } from '../context'

const Toggle = ({ children }) => {
  const { setIsOpen } = useContext(ModalContext)

  return <button onClick={() => setIsOpen(true)}>{children}</button>
}

export default Toggle
```

4. Também precisamos do componente content que vai ser responsável por exibir o conteúdo do Modal

```jsx
import { createContext, useState } from 'react'

export const ModalContext = createContext()

export const ModalStorage = ({ children }) => {
  const [isOpen, setIsOpen] = useState(false)

  return (
    <ModalContext.Provider value={{ isOpen, setIsOpen }}>
      {children}
    </ModalContext.Provider>
  )
}
```

5. Por fim, podemos atribuir os dois ao nosso componente Modal e já ta no jeito (:

```jsx
import Toggle from './Toggle'
import Content from './Content'

import { ModalStorage } from './context'

const Modal = ({ children }) => {
  return <ModalStorage>{children}</ModalStorage>
}

Modal.Toggle = Toggle

Modal.Content = Content

export default Modal
```

6. Utilizando

```jsx
import Modal from './components/Modal'

const App = () => {
  return (
    <Modal>
      <Modal.Toggle>Abrir Modal</Modal.Toggle>
      <Modal.Content>
        <h2>React4Noobs</h2>
        <p>Compound Components é dahora! /o/</p>
      </Modal.Content>
    </Modal>
  )
}

export default App
```

7. Resultado

Assim, a gente torna a criação e o uso de modais extremamente flexíveis e reutilizáveis. `Modal.Toggle` é responsável por ativar a exibição do modal, enquanto `Modal.Content` deve exibir o conteúdo do nosso modal.

Essa estrutura permite que os desenvolvedores personalizem facilmente o comportamento e o conteúdo dos modais de acordo com as necessidades específicas de suas aplicações, tornando o código mais limpo e organizado.

# Outros exemplos

Também podemos utilizar Compound Components em outros contextos, por exemplo:

Componentes de Accordion

```jsx
<Accordion>
  <Accordion.Title>Titulo</Accordion.Title>
  <Accordion.Section>Seção 1</Accordion.Section>
  <Accordion.Section>Seção 2</Accordion.Section>
  <Accordion.Section>Seção 3</Accordion.Section>
  <Accordion.Button>Botão</Accordion.Button>
</Accordion>
```

Componentes de Menu

```jsx
<Menu>
  <Menu.Logo>Image Logo</Menu.Logo>
  <Menu.Item>Home</Menu.Item>
  <Menu.Item>About</Menu.Item>
  <Menu.Item>Services</Menu.Item>
  <Menu.Item>Contact</Menu.Item>
  <Menu.Login>Login</Menu.Login>
</Menu>
```

Todos são flexivéis e adptavéis, facilitando o desenvolvimento, escalabilidade e uso do componente.

# Conclusão

Vimos o quanto escrever componentes no padrão Compound Components pode ser útil em nossas aplicações, vimos também como utilizar e alguns exemplos em que esse padrão pode encaixar.

Fique à vontade para explorar e brincar criando componentes com Compoud Components, use com sabedória e veja se realmente faz sentido aplicar no seu contexto, as vezes, se não for bem aplicado, ele pode mais atrapalhar doque ajudar.

<p align="center">Made with 💜</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>
