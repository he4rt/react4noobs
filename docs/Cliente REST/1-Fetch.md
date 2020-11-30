<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

## O que é o Fetch?

[Fetch][1] é uma biblioteca nativa dos *browsers* para executar requisições HTTP. Usamos *Fetch* para requerer dados de um servidor na Web, que pode servir desde páginas HTML, arquivos CSS, JS, PDF, entre outros, até informações por meio de uma [*API*][2]. Quando a requisição é atendida, a aplicação decide o que faz com o que recebeu, sendo erro ou não.

O Fetch é o sucessor do [*XMLHTTPRequest*][3], que também é nativo nos navegadores e, assim como o *Fetch*, provê ao código da aplicação uma forma de transferir dados entre o *browser* (cliente) e um servidor. *XMLHttpRequest* era usado constantemente na programação de [*AJAX*][4].

Como estamos falando do *ReactJS*, que é executado nos navegadores, *Fetch* não precisa ser instalada, por ser nativa. É importante dizer que, no ambiente [*nodejs*][5], isso não é verdade, e para poder usar a mesma ideia do *Fetch*, é necessário importar a biblioteca [*node-fetch*][6].

## Requisições HTTP

### Recurso

Uma requisição HTTP possui regras bem definidas para que possamos executá-las, e assim usar os dados da resposta à essa requisição. Para poder fazer uma requisição com a biblioteca *Fetch*, devemos informar pelo menos o **recurso** que queremos acessar e coletar dados. Esse recurso é, normalmente, a URL de algum serviço exposto na Web. Se a sua requisição tiver apenas a URL, *Fetch* subentende que o **método** `GET` deve ser usado para a requisição, assim como toda chamada que fazemos de um navegador. Ou seja, quando você faz uma pesquisa no Google, você está fazendo uma requisição HTTP com método `GET`. :wink:

## Método

Como dissemos, precisamos informar o método na requisição para coletar dados desse recurso. Existem vários métodos e [aqui][7] vai a lista completa deles. Vamos nos concentrar nos mais usados e suas respectivas funções:

- `GET`: solicitar dados de um determinado recurso, por exemplo a página do Google;
- `POST`: assim com o `GET`, mas podemos passar dados no corpo na requisição;
- `DELETE`: apagar dados ou arquivos do serviço.
- `PUT`: alterar recursos já existentes ou criar um recurso inexistente no serviço Web;
- `PATCH`: parecido com o `PUT`, mas altera dados específicos.

Normalmente os serviços Web executam verificações (autorização, permissão, etc.) nas requisições que recebem, ou seja, elas são tratadas quando chegam. Portanto, é necessário que o serviço implemente o método, para que seja possível usá-lo. Por exemplo, o Google retorna erro quando tentamos executar uma requisição o método `DELETE`.
```shell
foo@bar:~$ curl -X DELETE google.com
<!DOCTYPE html>
<html lang=en>
  <meta charset=utf-8>
  <meta name=viewport content="initial-scale=1, minimum-scale=1, width=device-width">
  <title>Error 405 (Method Not Allowed)!!1</title>
  <style> ... </style>
  <a href=//www.google.com/><span id=logo aria-label=Google></span></a>
  <p><b>405.</b> <ins>That’s an error.</ins>
  <p>The request method <code>DELETE</code> is inappropriate for the URL <code>/</code>.
  <ins>That’s all we know.</ins>
foo@bar:~$
```

### Status Codes

Quando fazemos uma requisição, recebemos a resposta da mesma, que também contém muita informação, e uma delas é o *status code*, que serve para informar para a aplicação o que aconteceu com sua requisição. Alguns [exemplos][12]:

- `200`: "Tudo certo com o seu pedido";
- `201`: "Seu pedido foi aceito e foi criado na API";
- `400`: "Não deu para entender seu pedido, pode ser que há uma falha na ;estrutura nele";
- `404`: Muito famoso por dizer que não encontrou o que você pediu.

A lista completa dos *status codes* HTTP você vê [aqui][8]. Recomendamos tornar a experiência mais divertida e, para isso o site [*http cats*][9] pode ajudar. Lá você pode ver o título de cada status com gatos.

![418 HTTP Status Code](https://http.cat/418)

## Como usar o Fetch

Como dissemos, a requisição HTTP a ser executada pelo navegador precisa de algumas informações para sua execução. A estrutura básica de uma requisição usando *Fetch* é a seguinte:

```js
const fetchResponsePromise = fetch(resource [, init])
```

- `resource`: a url que a requisição vai chamar. Por exemplo: http://www.example.com
- `init`: um objeto **opcional**, no qual configuramos de forma mais detalhada a requisição. Todos os detalhes sobre esse objeto [aqui][10].

Como o *Fetch* já é carregado por padrão no browser, usar o *Fetch* fica fácil. Você pode executar as chamadas diretamente no seu código:

````js
  ...

  fetch("https://swapi.dev/api/people/1/")
    .then(res => res.json())
    .then(
      (result) => {
        console.log(result);
      },
      (error) => {
        console.error(error);
      }
    )
  ...
````

O *Fetch* também pode estar em algum dos métodos do seu componente React:

````js
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      error: null,
      isLoaded: false,
      items: []
    };
  }

  componentDidMount() {
    fetch("https://api.example.com/items")
      .then(res => res.json())
      .then(
        (result) => {
          this.setState({
            isLoaded: true,
            items: result.items
          });
        },
        (error) => {
          this.setState({
            isLoaded: true,
            error
          });
        }
      )
  }

  render() {
    const { error, isLoaded, items } = this.state;
    if (error) {
      return <div>Error: {error.message}</div>;
    } else if (!isLoaded) {
      return <div>Loading...</div>;
    } else {
      return (
        <ul>
          {items.map(item => (
            <li key={item.id}>
              {item.name} {item.price}
            </li>
          ))}
        </ul>
      );
    }
  }
}
````

No exemplo acima, o componente trata a requisição assim que é montado pelo React. Depois, o componente itera pelos items e os dispõe em tela.

### Mais informações
- [ReactJS Docs - AJAX e APIs][11]

[Ir para Próxima Seção](./2-Axios.md)

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>

[1]: https://developer.mozilla.org/pt-BR/docs/Web/API/Fetch_API/Using_Fetch
[2]: https://pt.wikipedia.org/wiki/Interface_de_programa%C3%A7%C3%A3o_de_aplica%C3%A7%C3%B5es
[3]: https://developer.mozilla.org/pt-BR/docs/Web/API/XMLHttpRequest
[4]: https://developer.mozilla.org/pt-BR/docs/Web/Guide/AJAX
[5]: https://nodejs.org
[6]: https://github.com/node-fetch/node-fetch
[7]: https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods
[8]: https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Status
[9]: https://http.cat/
[10]: https://developer.mozilla.org/pt-BR/docs/Web/API/WindowOrWorkerGlobalScope/fetch
[11]: https://pt-br.reactjs.org/docs/faq-ajax.html
[12]: https://external-preview.redd.it/VIIvCoTbkXb32niAD-rxG8Yt4UEi1Hx9RXhdHHIagYo.jpg?width=960&crop=smart&auto=webp&s=5d890e52d9f9a0ed647b3ff217cf226536a1f651