## O que é o Axios?

Axios é uma biblioteca que nos permite interagir com apis de maneira dinamica.



## Como instalar o Axios

Para instalar digite os comandos abaixo:

>  npm install axios

> yarn add axios

## Entendo como funciona uma api 

Antes de colocamos a mão no codigo devemos saber que uma api rest tem regras, ou seja dependendo da situação sera necessario usar um metodo **X** e em outro momento **Y**. Então que tal conhecer esse metodos.

`GET`: Com o metodo get nossa resposta so teremos dados
`POST`: Com o metodo Post poderemos realizar interações na Api
`DELETE`: Com esse metodo podemos apagar os dados da Api
`PUT`: Com esse metodo podemos alterar dados da api, no entanto ele funciona se já existir o dado, então ele apenas seria atualizado, mas caso não tenha ele é criado. 
`PATCH`: Esse metodo é parecido com o `PUT`, no entanto ele altera um dados especifico


Exemplos:

`GET`: Listar todos os usuarios registrados
`POST`: Registrar um novo usuario
`DELETE`: Apagar um usuario ou mais de um 
`PUT`: Alterar o dados de um usario, caso não encontra o usuario ele é criado.
`PATCH`: Alterar o dado do usuario,como por exemplo apenas a senha

Tambem existem outros metodos que não são usados tanto em uma api, no então caso queira dar uma conferida numa lista completa. [Clique aqui](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods)


Alem dos metodos apresentados temos os status da api que servem para informar para o desenvolvedor o que aconteceu com sua requisitação.

Por exemplo:
`201`: Seu pedido foi aceito e foi criado na api
`200`: Tudo certo com o seu pedido 
`400`: Sua função é dizer que não entendeu seu pedido, e que ha uma falha na estrutura do seu pedido
`404`: Muito famoso por dizer que não encontrou o que você pediu

Como são varios recomendo  o site **http cats** que ira te mostrar cada protocolo com um jeito divertido e muitos gatos.[Clique aqui](https://http.cat/)

### Como usar o Axios

Então chega de teoria, e vamos praticar o uso do axios?. Para esse exemplo criaremos um novo arquivo com o nome de `api.js` 

````js
import axios from 'axios';

const api = axios.create({
    baseURL: 'link da api'
})

export default api;
````

Nesse arquivo iremos criar nosso componente que ficara responsavel por interagir com a api

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
            const response = await api.post('users', data)
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
De maneira completamente simples utilizamos o hooks para receber os dados requisitados pelo formulario. Apos isso o metodo responsavel por se conectar api e executar ação `POST` e registrando o novo usuario
  






[Ir para Próxima Seção]()