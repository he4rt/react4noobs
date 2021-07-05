<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

# Ciclo de vida

Neste capítulo você entenderá o que é **Ciclo de vida** no React.

## Introdução

Quando estamos utilizando o React que tem por base a componentização, **é preciso entender como que tudo funciona para que possamos saber o que fazer e quando fazer algo.** Todos os componentes possuem um ciclo de vida que vai desde o momento em que ele aparece na tela até ele desaparecer da tela.

O objetivo desse ciclo é gerenciar os recursos da aplicação, ou seja, tudo que não está em tela é "destruido" ou apagado pra poder garantir recursos para os que estão em tela.

Ainda não entendeu? Vamos para um exemplo:

Tu tem dois componentes em tela, porém após alguma ação do usuário um dos componentes desaparece da tela. Nesse momento o React "destroi"/apaga ele da DOM para guardar recursos e garantindo que todo o resto continue funcionando.

Enfim, vamos ao que interessa!

O React permite que manipulemos o ciclo de vida e podemos dividir o mesmo em 3 momentos:

- Montagem (Quando aparece em tela)
- Atualização (Quando altera um dado em tela)
- Desmontagem (Quando desaparece da tela)

![lifecycle image](https://www.notion.so/Ciclo-de-Vida-9cfadd42ca05429a94795803c5ccd216#a68de13b879648e884c0c92ff8b3cf5d)

## Montagem

Nesta etapa ocorre quando **nosso componente aparece em tela da primeira vez**, quando ele é colocado na DOM. Então nosso componente é renderizado em tela com todas as props que passamos para ele, todas as requisições de dados e etc.

Temos três funções nesta etapa:

- **componentWillMount** → Essa etapa é executada antes mesmo da montagem do componente, aqui colocamos ações das quais queremos que execute no inicio do nosso componente. Como por exemplo chamadas na API, tratamento de dados recebidos e por ai vai.

  > O equivalente dele no React Hooks é ouseLayoutEffect.
  > Exemplo:
  > Para todos os exemplos utilizaremos umabiblioteca chamada Axios para lidar com asrequisições, ela possui algumas vantagens emrelação a fetch api nativa do JS mas vocêpode utilizar o que tu bem entender.

```jsx
import React from "react";
import axios from "axios";
class CardPerson extends React.Component {
  constructor() {
    super();
    this.state = {
      name: "",
      birthday: "",
    };
  }
  // Funcão para pegar os dados
  async loadData() {
    try {
      // Fazemos uma requisição para algumaapi
      const response = await axios.get("URLDE ALGUMA API");
      // Após pegar os dados setamos ele noestado
      this.setState({
        name: response.data.name,
        birthday: response.data.birthday,
      });
    } catch (error) {
      console.log("error");
    }
  }
  componentWillMount() {
    loadData();
  }
  render() {
    return (
      <div>
        <h1>{this.state.name}</h1>
        <h2>{this.state.birthday}</h2>
      </div>
    );
  }
}
```

Durante a construção do componente em tela,ele irá executar uma função que irá pegardados de alguma api nossa, para então pegaresses dados e coloca-los nos estados.
Vamos supor que nossa api retornou os dados:{name: "Heart", birthday:"13/13/2090"}.
_SE_ nossa requisição obter sucesso, apósrenderizar aparecerá em tela: Heart e 13/132020
_SE NÃO_ não irá aparecer nada pois iniciamoso estado como strings vazias.
ATENÇÃO!
Essa é uma parte do ciclo quase nãoutilizada, pois existem diversos problemas.Atualmente no React é recomendando o usar ocomponentDidMount.

<br/>

- **constructor** (No caso dos componentes de classe) → No caso dos componentes de classe, é nessa etapa que definimos as propriedades, estados e em alguns casos um bind para que o nosso _this_ faça referência ao componente.

<br/>

- **componentDidMount →** Basicamente ocorre após a montagem do componente na DOM, ou seja após o método **render.** Nessa etapa colocamos ações das quais queremos que execute no inicio do nosso componente. Como por exemplo chamadas na API, tratamento de dados recebidos e por ai vai.

> Seu equivalente no React Hooks é o useEffect.

```jsx
import React from "react";
import axios from "axios";
class CardPerson extends React.Component {
  constructor() {
    super();
    this.state = {
      name: "",
      birthday: "",
    };
  }
  // Funcão para pegar os dados
  async loadData() {
    try {
      // Fazemos uma requisição para algumaapi
      const response = await axios.get("URLDE ALGUMA API");
      // Após pegar os dados setamos ele noestado
      this.setState({
        name: response.data.name,
        birthday: response.data.birthday,
      });
    } catch (error) {
      console.log("error");
    }
  }
  componentDidMount() {
    loadData();
  }
  render() {
    return (
      <div>
        <h1>{this.state.name}</h1>
        <h2>{this.state.birthday}</h2>
      </div>
    );
  }
}
```

A diferença pode parecer que é apenas o nome mas tudo muda completamente. Agora só estamos fazendo a requisição após o componente estar na DOM e não antes.

## Atualização

Esta etapa está relacionada a qualquer atualização ou mudança de dados em tela. Sejaquando uma propriedade ou até mesmo um estado seja alterado.
Temos três funções nesta etapa:

  <br/>

- **shouldComponentUpdate** → Essa função será chamada sempre que um estado ou propriedade for chamada. Nela tu pode decidir se o componente irá renderizar novamente ounão, por padrão ele re-renderiza.
  Esse método existe apenas para questão de performance, confiar nele para evitar re-renderização pois pode ocasionar bugs indesejados.

```jsx
import React from "react";
import axios from "axios";

class CardPerson extends React.Component {
  constructor(props) {
    super();
    this.state = {
      name: props.name,
      birthday: props.birthday,
    };
  }
  // Essa função recebe as proximas propsestate
  shouldComponentUpdate(nextPropsnextState) {
    if (nextProps.name === this.statename) {
      return false;
    } else {
      return true;
    }
  }
  render() {
    return (
      <div>
        <h1>{this.state.name}</h1>
        <h2>{this.state.birthday}</h2>
      </div>
    );
  }
}
```

Ok, mas o que está acontecendo? Bom,estamosdizendo que quando ocorrer umaatualizaçãode dados, se o nome for igualao estado atual, ele não re-renderiz(false). Se não,ele renderiza novamente.

**Devo alertar novamente que essa funçãoéutilizada em casos muito raros e nãoérecomendado ficar mexendo nela sem um motivo concreto.**

<br/>

- **componentWillUpdate** → Essa função éexecutada no momento da atualização de dado(props ou estados) e assim como a anteriordefine se deve renderizar novamente ou não.Atualmente é um método marcado como inseguropela própria documentação do React erecomenda-se que seja substituído pelocomponentDidUpdate que falaremos a seguir.

<br/>

- **componentDidUpdate** → Esse metodo échamado logo após do componentDidMount,basicamente ele que tu irá utilizar parachecar se ocorreu alguma atualização dedados. Um bom exemplo é quando seu componenteprecisa fazer uma requisição para uma APIsempre que um dado muda.

> Seu equivalente no React Hooks é ouseEffect

```jsx
import React from "react";
import axios from "axios";
class CardPerson extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: props.name,
      birthday: "",
    };
  }
  // Funcão para pegar os dados
  async loadData() {
    try {
      // Fazemos uma requisição para alguma api
      const response = await axios.get("URL DE ALGUMA API");
      // Após pegar os dados setamos ele no estado
      this.setState({
        name: response.data.name,
        birthday: response.data.birthday,
      });
    } catch (error) {
      console.log("error");
    }
  }
  // Guarda as propriedades e estados anteriores
  componentDidUpdate(prevProps, prevState) {
    if (prevState.name !== this.state.name) {
      loadData();
    }
  }
  render() {
    return (
      <div>
        <h1>{this.state.name}</h1>
        <h2>{this.state.birthday}</h2>
      </div>
    );
  }
}
```

Aqui sempre que o name for alterado,faremos uma requisição nova na api parapegar os novos dados.

## Desmontagem

Esta é a ultima etapa, é quando ocomponente não é mais necessário em telae portando deve ser removido. Aqui temosapenas uma função, ela é chamada de**componentWillUnmount.**

- **componentWillUnmount** → Essa funçãoocorre sempre que um componente éremovido de tela para garantir que elenão permaneça na DOM. É uma parteimportante porém tu só mexe em casosmuito específicos, por exemplo: Limparalgum dado durante a desmontagem que tudefiniu durante a montage(**componentDidMount**).

## Conclusão

Podemos concluir que o ciclo de vida doscomponentes no React é algo muito bemtrabalhado e interessante. Podemos nãoapenas entender mas também manipula-lospara realizar diversas ações.
Bom, até então em todos os exemplosutilizamos a abordagem mais clássica doReact que são os componente de classe.Porém é algo não muito utilizado nos diasde hoje, com a vinda dos _React Hooks_ setornou muito melhor desenvolverutilizando componentes de função.
Nos próximos tópicos você aprenderá sobreoque são hooks, como utilizar e seusequivalentes em relação ao ciclo de vida!

[Ir para Próxima Seção](./7-React%20Hooks.md)

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>
