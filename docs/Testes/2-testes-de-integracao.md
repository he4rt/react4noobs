<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

# Testes de integração

<p align="center">
  <img src="../../assets/integration-test.gif">
</p>

## O que é teste de integração?

Testes de integração são aqueles que testam os módulos da aplicação de forma conjunta. Eles garantem que módulos menores interajam entre si corretamente. Ao contrário dos testes unitários, os testes de integração evitam utilizar dados _mockados_ garantindo o comportamento real de módulos menores.

## Escreva testes. Não muitos, mas a maioria de integração

Essa é uma frase que foi _tweetada_ por [Guillermo Rauch](https://twitter.com/rauchg/status/807626710350839808) criador do [Vercel](https://vercel.com/) e [Socket.io](https://socket.io/).

Ele quer dizer que a grande maioria dos projetos devem ter testes automatizados, eles garantem que o produto faz o que tem que fazer, e nos dá confiança de que está fazendo da forma correta.

Em relação a quantidade, escreva o necessário para que suas funcionalidades principais estejam cobertas e o usuário não tenha problemas em usá-las quando algo novo for lançado.

Sobre a maioria dos seus testes, eles devem ser de integração. **Kent C. Dodds** fala sobre o real retorno dos esforços com sua teoria do [Troféu de teste](https://twitter.com/kentcdodds/status/960723172591992832). Essa teoria diz que os testes de integração criam o equilíbrio real entre confiança e esforço.

## Ferramentas utilizadas em testes de integração

Para aplicações escritas em javascript, é muito comum o uso do _framework_ de teste chamado [Jest](https://jestjs.io/). Ele é responsável pela estrutura do arquivo de teste, e nos permite criar conjuntos e cenários para que possamos criar as asserções que queremos.

Já para manipulação do DOM, podemos utilizar a biblioteca [React Testing Library](https://testing-library.com/docs/react-testing-library/intro). Ela nos permite renderizar e fazer _queries_ no nosso DOM para criarmos nossas asserções.

## Exemplo de um teste de integração

Imagine a seguinte jornada:

> Eu como usuário desejo ver um alerta ao clicar em um botão escrito "Exibir alerta"

Pensando nos testes unitários, poderíamos testar se o botão está invocando a função passada e poderíamos verificar se o alerta está visível baseado em uma variável de controle de exibição.

```js
// Button.spec.js
describe('Meu botão', () => {
  test('deve chamar a função onClick', () => {
    const onClickMock = jest.fn();

    render(<Button onClick={onClickMock}>Exibir alerta</Button>);

    userEvent.click(screen.getByRole('button', { name: 'Exibir alerta' }));

    expect(onClickMock).toHaveBeenCalled();
  });
});
```

```js
// Alert.spec.js
describe('Meu Alerta', () => {
  test('deve exibir o alerta', () => {
    render(<Alert isOpen>Aqui está seu alerta!</Alert>);

    expect(screen.getByRole('alert')).toBeInDocument();
  });

  test('não deve exibir o alerta', () => {
    render(<Alert isOpen={false}>Aqui está seu alerta!</Alert>);

    expect(
      screen.getByRole('alert', { name: 'Aqui está seu alerta!' })
    ).not.toBeInDocument();
  });
});
```

Os testes a cima são executados com sucesso, eles recebem os dados que precisam para simular seu funcionamento.

Agora vamos criar a integração entre esses componentes e o teste que garante que quando o botão for clicado, o alerta será exibido.

```js
// App,js
const App = () => (
  <>
    <Alert isOpen={isOpen}>Aqui está seu alerta!</Alert>
    <Button onClick={() => setIsOpen(true)}>Exibir alerta</Button>
  </>
);
```

```js
// App.spec.js
describe('Minha página inicial', () => {
  test('deve exibir o alerta quando clicar no botão "Exibir alerta"', () => {
    render(<App />);

    userEvent.click(screen.getByRole('button', { name: 'Exibir alerta' }));

    expect(
      screen.getByRole('alert', { name: 'Aqui está seu alerta!' })
    ).toBeInDocument();
  });
});
```

Note que desta vez não renderizamos cada componente isolado, mas sim o componente no qual está utilizando cada um deles.

Com isso, nós procuramos dentro do DOM a existência de um botão com o texto _Exibir alerta_ e clicamos nele, como consequência desta ação, esperamos ver um alerta com o texto _Aqui está seu alerta_.

Esse é um exemplo bem simples, mas mostra como nosso teste garante o comportamento de um alerta e um botão quando eles estão juntos, dois módulos pequenos que criam um contexto quando juntam suas forças!

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>
