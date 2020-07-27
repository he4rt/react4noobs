## O que é o Axios?

É uma biblioteca que nos permite interagir com Api rest de maneira simplesmente e dinâmica.

## Como instalar o Axios

Para instalar digite os comandos abaixo:

>  npm install axios

> yarn add axios


## Entendo como funciona uma Api Rest

Antes de colocamos a mão no código devemos saber que uma api rest tem regras, ou seja dependendo da situação será necessário usar um método **X** e em outro momento **Y**. Então que tal conhecer esses métodos.

`GET`: Com o método get nossa resposta só teremos dados
`POST`: Com o método Post poderemos realizar interações na Api
`DELETE`: Com esse método podemos apagar os dados da Api
`PUT`: Com esse método podemos alterar dados da api.

Exemplos:

`GET`: Listar todos os usuários registrados
`POST`: Registrar um novo usuário
`DELETE`: Apagar um usuário ou mais de um 
`PUT`: Alterar a senha do usuário 

### Como usar o Axios

Então chega de teoria, e vamos pra praticar como podemos usar o axios. Para esse exemplo criaremos um novo arquivo com o nome de `api.js`


````js
import axios from 'axios';

const api = axios.create({
    baseURL: 'link da api'
})

export default api;
````


Nesse arquivo iremos criar nosso componente que ficara responsável por interagir com a api

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
  
