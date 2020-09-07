<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

## O que é o Axios?

Axios é uma biblioteca criada com o intuito de realizar conexões HTTP de maneira dinamica.


## Como instalar o Axios

Para instalar digite os comandos abaixo:

>  npm install axios

> yarn add axios

## O conceito de API para o Axios

Primeiramente devemos comprender que o termo API é muito amplo e tem inúmeras funcões. Sendo assim uma explicação mais simples para o axios seria que ele faz uma ponte entre API, ou seja, em um exemplo mais claro ele se torna um garçom  que deve trazer seu pedido de comida.

## Regras de uma API HTTP

Antes de colocamos a mão no código devemos saber que uma API HTTP tem regras, ou seja dependendo da situação sera necessario usar um método **X** e em outro momento **Y**. Então que tal conhecer esse metodos.

`GET`: Com o método GET solicitamos dados de um recurso especifico  
`POST`: Com o método POST poderemos realizar interações na API
`DELETE`: Com esse método podemos apagar os dados da API
`PUT`: Com esse método podemos alterar dados da API, no entanto ele funciona se já existir o dados, então ele apenas seria atualizado, mas caso não tenha ele é criado. 
`PATCH`: Esse método é parecido com o `PUT`, no entanto ele altera um dados especifico


Exemplos:

`GET`: Listar todos os usuários registrados
`POST`: Registrar um novo usuário
`DELETE`: Apagar um usuário ou mais de um 
`PUT`: Alterar os dados de um usuário, caso não encontre o usuario ele é criado.
`PATCH`: Alterar o dado do usuário, como por exemplo apenas a senha

Tambem existem outros metodos que não são usados tanto em uma API, no então caso queira dar uma conferida numa lista completa. [Clique aqui](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods)


Alem dos metodos apresentados temos os status da API que servem para informar para o desenvolvedor o que aconteceu com sua requisição.

Por exemplo:
`201`: Seu pedido foi aceito e foi criado na API
`200`: Tudo certo com o seu pedido 
`400`: Sua função é dizer que não entendeu seu pedido, e que há uma falha na estrutura do seu pedido
`404`: Muito famoso por dizer que não encontrou o que você pediu

Como são varios recomendo  o site **http cats** que ira te mostrar cada protocolo com um jeito divertido e muitos gatos.[Clique aqui](https://http.cat/)

### Como usar o Axios

Então chega de teoria, e vamos praticar o uso do axios?. Para esse exemplo criaremos um novo arquivo com o nome de `api.js` 

````js
import axios from 'axios';

const API = axios.create({
    baseURL: 'link da API'
})

export default API;
````

Nesse arquivo iremos criar nosso componente que ficará responsável por interagir com a API

Feito isso podemos ir para o arquivo que queremos que tenha uma interação entre o front-end e o back-end.

```js
import React, {  useState } from 'react';


import api from 'api';

export default function Register() {
    const [name, setName] = useState('');
    const [email, setEmail] = useState('');
    const [password, SetPassword] = useState('');

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
                    <input placeholder="Password" value={password} onChange={e => SetPassword(e.target.value)}></input>
                    </div>
                    <button className="button" type="submit">Cadastrar</button>
                </form>
            </div>
        </div>
    )
}
```   
De maneira completamente simples utilizamos o hooks para receber os dados requisitados pelo formulário. Apos isso o metodo responsável por se conectar API e executar ação `POST` e registrando o novo usuário
  






[Ir para Próxima Seção]()

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>