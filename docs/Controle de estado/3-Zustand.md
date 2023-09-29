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

Primeiramente criamos a nossa `store`: 
```js
import { create } from 'zustand'

const useStore = create((set) => ({
  bears: 0,
  increasePopulation: () => set((state) => ({ bears: state.bears + 1 })),
  removeAllBears: () => set({ bears: 0 }),
}))
```

Como podemos ver no código acima, a nossa `store` é um `hook`
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

Perceba que pode-se utilizar o "hook" `useStore` em qualquer lugar e sem a necessidade de `providers` como acontece no Redux.


## Atualizando estado

Para atualizar o estado basta utilizar a função que realiza esta ação (`action`).
Pegando o exemplo da "store" anterior e adcionando o estado `bearName` e a respectiva `action` `updateBearName` temos a seguinte configuração da nossa `store`:

```js
const useStore = create((set) => ({
  bears: 0,
  bearName: '',
  updateBearName: (bearName) => set(() => ({ bearName: bearName}))
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

Observação: `shallow` se trata de uma função comparadora utilizada para verificar se arrays e objetos tem os mesmos elementos aos anteriores. Se você verificar `{name: 'zustand'} === {name: 'zustand'}` esta sentença no javascript a resposta será sempre `false` pois são instâncias distintas, são dois objetos diferentes que contém os mesmos valores, então se faz necessário o uso da função comparadora para não gerar excessivas renderizações em sua aplicação.

## Fatiando sua store

A medida que for construindo, a sua `store` pode ficar cada vez maior e mais difícil de dar manutenção, por isso pode ser interessante criar `slices` da sua `store` que são pequenas e específicas `stores`.

Abaixo vemos uma pequena store com um `state` chamado `fishes` e uma `action` para adcionar o valor de 1 a cada vez que é acionado:

```js
export const createFishSlice = (set) => ({
  fishes: 0,
  addFish: () => set((state) => ({ fishes: state.fishes + 1 })),
})
```

Já nesta outra, temos um `state` chamado de `bears` e duas `actions`, a primeira adciona mais 1 ao estado de `bears` e a segunda subtrai do estado `fishes` o valor de 1:

```js
export const createBearSlice = (set) => ({
  bears: 0,
  addBear: () => set((state) => ({ bears: state.bears + 1 })),
  eatFish: () => set((state) => ({ fishes: state.fishes - 1 })),
})
```

Agora podemos juntar essas duas stores em uma só `useBoundStore`.

```js
import { create } from 'zustand'
import { createBearSlice } from './bearSlice'
import { createFishSlice } from './fishSlice'

export const useBoundStore = create((...a) => ({
  ...createBearSlice(...a),
  ...createFishSlice(...a),
}))
```

E por fim podemos utilizar normalmente em nosso componente React:

```jsx
import { useBoundStore } from './stores/useBoundStore'

function App() {
  const bears = useBoundStore((state) => state.bears)
  const fishes = useBoundStore((state) => state.fishes)
  const addBear = useBoundStore((state) => state.addBear)
  return (
    <div>
      <h2>Number of bears: {bears}</h2>
      <h2>Number of fishes: {fishes}</h2>
      <button onClick={() => addBear()}>Add a bear</button>
    </div>
  )
}

export default App
```

## Conclusão

Usar Zustand é realmente simples e fácil como você pôde perceber lendo este material, e essa é a proposta desta solução para gerenciamento de estados no React. Na sua documentação oficial há alguns outros detalhes para caso você precise dar uma conferida como a sua utilização com typescript e outros guias interessantes.

[Documentação Oficial](https://docs.pmnd.rs/zustand/getting-started/introduction)

Achou algo de errado? Algo que possa melhorar? Fique a vontade para [abrir uma issue](https://github.com/he4rt/react4noobs/issues). Vejo você na próximo seção!

[Ir para Próxima Seção](../Estilizacao/1.Preprocessadores%20CSS.md)

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>