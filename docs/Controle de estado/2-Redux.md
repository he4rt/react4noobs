<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

# Redux

"Redux é um "container" de estado previsível para aplicativos JavaScript.

Ele ajuda a escrever aplicativos que se comportam de forma consistente, pode ser executado em ambientes diferentes (cliente, servidor e nativo) e fáceis de testar. Além disso, ele fornece uma ótima experiência para o desenvolvedor, como edição de código em tempo real combinado com um depurador em tempo de execução.

Você pode usar o Redux junto com o React ou com qualquer outra biblioteca/Framework Front-end. É compacto (2kB, incluindo dependências), mas tem um grande ecossistema de "add-ons" (componente de software que adiciona novas funcionalidades ou características) disponíveis." - definição traduzida do site https://redux.js.org/introduction/getting-started

## O que é o Flux?

Primeiramente precisamos entender como funciona a arquitetura do Redux, no caso entender primero o que é a arquitetura Flux.

Flux é uma arquitetura criada pelo Facebook como solução alternativa ao padrões de arquitetura usuais como por exemplo MVC, para solucionar problemas de controle de estados, na época um problema constante do Facebook era as notificações que não atualizavam o seu estado de forma correta.

Essa arquitetura tem como conceito o princípio do fluxo unidirecional tendo 4 (quatro) estados Action, Dispatcher, Store e View, dessa forma o usuário provoca algum evento que gera uma "Action" especifica, essa "Action" vai acionar um "Dispatcher" que comunica ao "Store" a necessecidade de mudar algum dado e por fim envia um evento para que seja mostrado na "View" a alteração realizada. veja abaixo no diagrama uma vizualização da arquitetura:

<img src="img/flux_exemplo_1.png" alt="Flux1-Facebook"> - créditos: https://facebook.github.io/flux/docs/in-depth-overview/

Perceba também que nessa estrutura a View também podem gerar novas "Actions" para os "Dispatchers" e retornar o fluxo do ínicio, veja abaixo no diagrama essa interação:

<img src="img/flux_exemplo_2.png" alt="Flux2-Facebook"> - créditos: https://facebook.github.io/flux/docs/in-depth-overview/

Apenas vou fazer algumas observações sobre características do Flux, os estados da aplicação são mutáveis, possuí apenas um único "Dispatcher" e possuí multiplos "Store".

## Como Funciona o Redux

Agora que entendemos a arquitetura do Flux, vamos entender como funciona o Redux, que é baseado no Flux, mas não é completamente igual a ele. Primeiro de tudo temos a "Action", "Reducers", "Store" e "React", essa é a estrutura do Redux, nela já observamos que temos de igual algumas coisa e outras não.

No geral tudo funciona bem parecido mas existem diferenças importantes, os "Reducers" são equivalente ao "Dispatcher" com uma diferença não existe um único "Reducers" e sim pode haver 1 (um) ou mais deles, a "Store" é igual com a diferença que só existe uma em vez de várias "Stores", o "React" é igual a "View" mas como estamos aplicando em React ela tem esse nome, e as "Actions" possuem a mesma função e da mesma forma que no Flux. Abaixo temos um diagrama comparando o funcionamento do Flux com o Redux:

<img src="img/redux-flux_exemplo.jpg" alt="Redux-Facebook"> - créditos: https://facebook.github.io/flux/docs/in-depth-overview/

## Como usar o Redux no React

Primeiramente para instalar os pacotes do Redux na sua aplicação React, use os seguintes comandos:
  - npm install redux
  - npm install react-redux
  - npm install --save-dev redux-devtools

Agora vamos entender como a estrutura funciona no código em si, começando pelas "Actions", elas basicamente vão ser as informações de estado que a aplicação vai enviar para o "Store" através dos "Reducers".

Nesse primeiro código vemos um exemplo de um "Action Creator", ele basicamente é um objeto que passara os nomes de estados a ser informado para a "Store".

```jsx
export const ActionsTypes = {
    SET_PRODUCTS: "SET_PRODUCTS",
    SELECTED_PRODUCTS: "SELECTED_PRODUCTS",
    REMOVE_SELECTED_PRODUCTS: "REMOVE_SELECTED_PRODUCTS",
};
```

### Action

Nesse código agora estou exportando minhas "Actions", que irão usar as "Action Creator" criadas anteriormente, para enfim passar os valores de estado da aplicação.

```jsx
import { ActionsTypes } from "../contants/action-types";

export const setProducts = (products) => {
    return {
        type: ActionsTypes.SET_PRODUCTS,
        payload: products,
    }
}

export const selectedProducts = (products) => {
    return {
        type: ActionsTypes.SELECTED_PRODUCTS,
        payload: products,
    }
}

export const removeSelectedProducts = () => {
    return {
        type: ActionsTypes.REMOVE_SELECTED_PRODUCTS,
    }
}
```

Agora veja no código a seguir como usar as "Actions" criadas para avisar ao "Reducers" que houve alguma mudança e é necessário avisar ao "Store".

```JSX
import React, { useEffect } from 'react';
import { useSelector, useDispatch } from 'react-redux';
import axios from 'axios';
import ProductComponent from './ProductComponent';
import { setProducts } from '../redux/actions/productActions';

const ProductListing = () => {

    const products = useSelector((state) => state);
    const dispatch = useDispatch();

    const fetchProducts = async () => {
        const response = await axios
            .get("https://fakestoreapi.com/products")
            .catch((err) => {
                console.log("error: ", err);
            });
        dispatch(setProducts(response.data));
    };

    useEffect(() => {
        fetchProducts()
    }, []);

    return(
        <div className="ui grid container">
            <ProductComponent />
        </div>
    );
}

export default ProductListing;
```

 Veja que crio uma constante "dispatch" para receber a função "useDispatch()" Dentro da constante "fetchProducts" crio uma "Arrow Function" e nela quando faço uma requisição a API passo o argumento a "dispatch" como "setProducts(response.data)", para assim avisar a necessidade de mundança no estado da aplicação e como argumento da função passo os dados retornados de minha API, onde serão armazenadas no "payload" de "setProducts()".

### Reducers



## Agora que você já sabe



Achou algo de errado? Algo que possa melhorar? Fique a vontade para [abrir uma issue](https://github.com/he4rt/react4noobs/issues). Vejo você na próximo seção!

[Ir para Próxima Seção](../Verificadores%20de%20Tipo/Typescript.md)

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>
