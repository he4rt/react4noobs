<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

# API de Contexto

Quando estamos trabalhando em um projeto React, aprendemos que os dados trafegam sempre de pai para filho (via props).

Em algumas situações, replicar essa passagem de props em vários níveis acaba se tornando repetitivo e extremamente verboso.

A API de Contexto (Context API) serve exatamente nesse caso. Ela fornece uma forma de compartilhamento de dados entre todos os componentes dentro de sua árvore, sem que o desenvolvedor precise escrever a passagem de props entre os níveis.

## Quando usar?

Você gostaria de personalizar as cores do seu sistema baseado em uma escolha do usuário.

Para isso, você escreve um componente para o usuário escolher a cor e o coloca na sua aplicação.

```jsx
function App() {
  const [userColor, setUserColor] = React.useState('#3DB7F4');

  return <div>
    <SeletorDeCores onChange={setUserColor} />
    <p style={{ color: userColor }}>Olá mundo colorido</p>
  </div>
}
```

Você cria um novo componente e precisa usar as cores do usuário. Vamos criar esse componente:

```jsx
function ListaColorida({ items, color }) {
  return <ul>
    {
      items.map((item) => <li key={item} style={{ color }}>{item}</li>)
    }
  </ul>
}
```

Além da lista, você desenvolve outros componentes e coloca-os em uma parte da sua aplicação:

```jsx
function Dashboard({ color }) {
  return <main>
    <MenuDeNavegacao color={color} />
    <ListaColorida color={color} items={itemsVindosDeUmaApi} />
  </main>
}
```

E a nossa aplicação, que precisa também passar essa propriedade adiante:

```jsx
function App() {
  const [userColor, setUserColor] = React.useState('#3DB7F4');

  return <div>
    <SeletorDeCores onChange={setUserColor} />
    <TextoColorido color={userColor}>Olá mundo colorido</TextoColorido>
    <Dashboard color={userColor} />
  </div>
}
```

Quando a sua aplicação cresce, a propriedade `color` será passada em 4, 5, 6 níveis de hierarquia, incluindo componentes que só terão a responsabilidade de delegar a propriedade para seus componentes filhos.

Não seria legal se apenas os componentes que vão lidar com a cor do usuário tenham conhecimento desse dado? É exatamente nesse tipo de situação em que a `ContextAPI` pode ser usada.

## Como usar

Para iniciar, é necessário criar um Contexto. Este será o objeto que vai representar o dado que será trafegado entre os componentes.

```javascript
const ContextoCorUsuario = React.createContext();
```

Depois, vamos colocar um provedor do contexto. Este provedor deve ficar no nível mais alto da hierarquia dos componentes.

```jsx
function App() {
  const [userColor, setUserColor] = React.useState('#3DB7F4');

  return <ContextoCorUsuario.Provider value={userColor}>
    <div>
      ...
    </div>
  </ContextoCorUsuario.Provider>
}
```

Agora, todo componente dentro dessa árvore pode receber a cor escolhida pelo usuário através desse contexto. Por exemplo, nossa lista colorida.

```jsx
function ListaColorida({ items }) {
  return <ContextoCorUsuario.Consumer>
    { (color) => (
      <ul>
        {
          items.map((item) => <li key={item} style={{ color }}>{item}</li>)
        }
      </ul>
    ) }
  </ContextoCorUsuario.Consumer>
}
```

Com isso, os componentes não precisam receber a cor do usuário através dos seus pais. Eles pró-ativamente consomem a cor vinda do contexto.

Nosso App e nosso Dashboard ficam mais simples também:

```jsx
function Dashboard() {
  return <main>
    <MenuDeNavegacao />
    <ListaColorida items={itemsVindosDeUmaApi} />
  </main>
}
```

```jsx
function App() {
  const [userColor, setUserColor] = React.useState('#3DB7F4');

  return <ContextoCorUsuario.Provider value={userColor}>
    <SeletorDeCores onChange={setUserColor} />
    <TextoColorido>Olá mundo colorido</TextoColorido>
    <Dashboard />
  </ContextoCorUsuario.Provider>
}
```

## Usando useContext

Na implementação anterior, usamos o `ContextoCorUsuario.Consumer` para obter a cor vinda do contexto. Nós podemos simplificar a escrita desse componente usando o `useContext`.

```jsx
function ListaColorida({ items }) {
  const color = useContext(ContextoCorUsuario)

  return <ul>
    {
      items.map((item) => <li key={item} style={{ color }}>{item}</li>)
    }
  </ul>
}
```

Na prática, o comportamento do componente permanece igual. A vantagem é que seu código fica mais limpo e a leitura do JSX fica mais clara.

## Considerações adicionais

Você pode construir quantos contextos forem necessários. Você pode criar um contexto diferente para cada tipo de dado, colocar os provedores hierarquizados no topo da árvore e cada componente apenas com os contextos relevantes para a própria montagem.

```jsx
function App() {
  return <ContextoCorUsuario.Provider value={userColor}>
    <ContextoLocalizacaoUsuario.Provider value={userGPS}>
      <ContextoInternacionalizacao.Provider value={translations}>
        ...
      </ContextoInternacionalizacao.Provider>
    </ContextoLocalizacaoUsuario.Provider>
  </ContextoCorUsuario.Provider>
}
```

```jsx
function BarraDeNavegacao() {
  const localizacao = useContext(ContextoLocalizacaoUsuario)
  const corUsuario = useContext(ContextoCorUsuario)

  return <ul>
    <li>{localizacao.latitude} {localizacao.longitude}</li>
    <li style={{ color: corUsuario }}>{corUsuario}</li>
  </ul>
}
```

## Agora que você já sabe

A Context API é simples e poderosa, e você pode usá-la em várias circunstâncias (como internacionalização, temas, localização do usuário, controle de estado global). Mas é importante avaliar se o seu componente deveria absorver a responsabilidade de obter suas propriedades.

Você aprendeu na sua jornada de React até aqui que as props dão poder para que seus componentes sejam reutilizáveis. Isso continua valendo, e muito.

Seus componentes mais reutilizáveis devem continuar recebendo os dados via props. Você pode consumir dados do Contexto em componentes menos especializados e mais focados. A beleza do React está no poder de combinar várias técnicas para que seus dados fluam como você preferir com o melhor design de código possível. Conhecer cada técnica e quando usá-la vai te ajudar a construir aplicações robustas e consistentes.

Achou algo de errado? Algo que possa melhorar? Fique a vontade para [abrir uma issue](https://github.com/he4rt/react4noobs/issues). Vejo você na próximo seção!

[Ir para Próxima Seção](../Verificadores%20de%20Tipo/Typescript.md)

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>
