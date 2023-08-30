<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

# Zustand
O Zustand é um dos menores gerenciadores de estado para React encontrado atualmente. Ele possui um tamanho de 1.17kB, sendo assim menor do que o Redux (2kB) e o Jotai (2.73kB) por exemplo.

É de fácil utilização por se prover de conceitos da arquitetura flux, utilizada pelo Redux, de maneira mais simplificada.

# Instalação
Você pode instalar o zustand através do npm ou yarn:

```bash
# NPM
npm install zustand

# Yarn
yarn add zustand
```

# Como ele funciona
Assim como no Redux, o Zustand funciona com uma única "store" onde serão armazenados os estados necessários a sua aplicação.

Primeiramente criamos a nossa "store": 
```js
import { create } from 'zustand'

const useStore = create((set) => ({
  bears: 0,
  increasePopulation: () => set((state) => ({ bears: state.bears + 1 })),
  removeAllBears: () => set({ bears: 0 }),
}))
```

Como podemos ver no código acima, a nossa "store" é um "hook"
onde temos:
1. O estado e o seu valor inicial -> `bears: 0`
2. Função para acrescentar 1 ao valor do estado atual -> `increasePopulation`
3. Função onde é zerado o valor do estado -> `removeAllBears`

Agora com a "store" criada e suas "actions" podemos utilizá-la nos respectivos componentes: 

```jsx
function BearCounter() {
  const bears = useStore((state) => state.bears)
  return <h1>{bears} around here...</h1>
}

function Controls() {
  const increasePopulation = useStore((state) => state.increasePopulation)
  return <button onClick={increasePopulation}>one up</button>
}
```

Perceba que pode-se utilizar o "hook" `useStore` em qualquer lugar e sem a necessidade de "providers" como acontece no Redux.


## Atualizando estado

Para atualizar o estado basta utilizar a função que realiza esta ação ("action").
Pegando o exemplo da "store" anterior e adcionando o estado `bearName` e a respectiva "action" `updateBearName` temos a seguinte configuração da nossa "store":

```js
const useStore = create((set) => ({
  bears: 0,
  bearName: '',
  updateBearName: () => set((bearName) => ({ bearName: bearName}))
  increasePopulation: () => set((state) => ({ bears: state.bears + 1 })),
  removeAllBears: () => set({ bears: 0 }),
}))
```

Com isso no código do nosso app podemos atualizá-lo da seguinte forma:

```js
function App() {
	const [bearName, updateBearName] = useStore(
		(state) => [state.bearName, state.updateBearName]
		shallow
	)

	return (
		<main>
			<label>
				Bear Name
				<input
				onChange={(e) => updateBearName(e.target.value)}
				value={bearName}
				/>
			</label>
		</main>
	)
}
```
