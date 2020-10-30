<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

## O que é o Axios?

Axios é uma biblioteca criada com o intuito de realizar conexões HTTP de maneira dinâmica.


## Como instalar o Axios

Para instalar, digite um dos comandos abaixo:

> npm install axios

> yarn add axios

## O conceito de API para o Axios

Primeiramente, devemos compreender que o termo API é muito amplo e tem inúmeras funções. O axios faz uma ponte entre a sua aplicação e uma API. Você pode pensar nele como um garçom entre você e a cozinha, levando o seu pedido e trazendo o seu prato de comida.

## Regras de uma API HTTP

Antes de colocamos a mão no código devemos saber que uma API HTTP tem regras. Dependendo da situação será necessário usar um método **X** e em outro momento **Y**. Então, que tal conhecer esses métodos?

`GET`: Com o método GET solicitamos dados de um recurso específico
`POST`: Com o método POST podemos realizar interações na API
`DELETE`: Com esse método podemos apagar dados via API
`PUT`: Com esse método podemos alterar dados da API. Ele atualiza recursos já existentes ou pode criar um recurso inexistente
`PATCH`: Esse método é parecido com o `PUT`. No entanto, ele altera dados específicos

Exemplos:

`GET`: Listar todos os usuários registrados
`POST`: Registrar um novo usuário
`DELETE`: Apagar um ou mais usuários
`PUT`: Alterar os dados de um usuário, caso não encontre o usuário ele é criado.
`PATCH`: Alterar um dado do usuário, como por exemplo a senha

Tambem existem outros métodos que não são usados tanto em uma API. Caso queira dar uma conferida numa lista completa, [clique aqui](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods).


Alem dos métodos apresentados, temos os status da API. Eles servem para informar para o desenvolvedor o que aconteceu com sua requisição.

Por exemplo:
`201`: Seu pedido foi aceito e foi criado na API
`200`: Tudo certo com o seu pedido
`400`: Não deu para entender seu pedido, pode ser que há uma falha na estrutura nele
`404`: Muito famoso por dizer que não encontrou o que você pediu

Como são vários, recomendamos o site **http cats**. Lá você pode ver o título de cada status de um jeito divertido e com muitos gatos. [Clique aqui](https://http.cat/)

### Como usar o Axios

Então chega de teoria, e vamos praticar o uso do axios?. Para esse exemplo criaremos um novo arquivo com o nome de `api.js`

````js
import axios from 'axios';

const API = axios.create({
    baseURL: 'link da API'
})

export default API;
````

Nesse arquivo iremos criar nosso componente que ficará responsável por interagir com a API.

Feito isso, podemos ir para o arquivo que queremos que tenha uma interação entre o front-end e o back-end.

```js
import React, { useState } from 'react';


import api from 'api';

export default function Register() {
    const [name, setName] = useState('');
    const [email, setEmail] = useState('');
    const [password, setPassword] = useState('');

   async function handleRegister(e){
        e.preventDefault();

        const data = {
            name,
            email,
            password,
        };

        try {
            const response = await API.post('users', data)
            console.log('Registrado com sucesso ');

        } catch (error) {
            alert(`Erro ao Registrar`);
            console.log(error);
        }

    };

    return (
        <div className="register-container">
            <form onSubmit={handleRegister}>
                <input placeholder="Nome" value={name} onChange={e => setName(e.target.value)}></input>
                <input placeholder="Email" type="email" value={email} onChange={e => setEmail(e.target.value)}></input>
                <input placeholder="Password" value={password} onChange={e => setPassword(e.target.value)}></input>
                <button className="button" type="submit">Cadastrar</button>
            </form>
        </div>
    )
}
```
De maneira completamente simples utilizamos os hooks para receber os dados requisitados pelo formulário. Após isso, chamamos o método responsável por se conectar a API e executar a ação `POST`. Com isso, um novo usuário é registrado!


[Ir para Próxima Seção]()

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>
