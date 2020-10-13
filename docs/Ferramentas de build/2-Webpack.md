<p align="center">
<a href="https://github.com/he4rt/4noobs" target="_blank">
<img src="../../assets/global/header-4noobs.svg">
</a>
</p>

# O que é WebPack?

O Webpack é um empacotador de módulos para projetos web que utilizam html, css, javascript e imagens, sendo uma das principais ferramentas utilizadas no core do React.

Primeiramente podemos dizer que a função do Webpack é variada entre muitas possibilidades que permitem facilitar o nosso ambiente de desenvolvimento. Um pequeno exemplo disso é uma função inclusa que permite converter códigos escritos em Typescript para nosso js puro. Pois, navegadores mais antigos não conseguem realizar a leitura do javascript moderno.

Outra de sua principal função é capacidade de ler arquivos separados de nossa aplicação. Imagine que você precise separar seu config.js para outro arquivo fora da index.js.

Bem, como podemos ver o Webpack é uma ótima ferramenta e totalmente completa por permitir enumeras funções de desenvolvimento onde o próprio desenvolvedor define suas próprias regras e plugins que usará em seu projeto.

# O que é Babel?

Bem, vamos falar um pouco de seu companheiro o **Babel JS**, como dito anteriormente o Webpack pode transformar o Typescript em Javascript, entretanto o Webpack não faz isso sozinho ele precisa da ajuda do Babel, que faz todo o processo de transformação do código, enquanto o Webpack faz a leitura e renderiza na pagina.

Caso você tenha curiosidade recomendo dar uma olhada na documentação oficial, basta [clicar aqui](https://babeljs.io/docs/en/)

# Como utilizar o Webpack no React?

De maneira simples, já estamos usando ele. Ao criar uma aplicação com o create-react-app, o webpack já é instalado e configurado. Sendo assim, não são necessárias configurações adicionais. Tudo é feito e configurado automaticamente.

# Bora praticar como usar o Webpack?

Então, chega de teoria e bora ver na prática como isso será aplicado no ecossistema do React.

Bem, para entender o conceito de Webpack e React iremos criar um Hello World.

Primeiramente iremos criar uma nova pasta para o nosso projeto, onde iremos iniciar já o nosso 'npm init', e logo após iremos instalar as bibliotecas que vamos usar nesse tutorial.

```
npm install --save react react-dom

npm install --save-dev webpack babel-core babel-loader babel-preset-react babel-preset-es2015
```

Agora podemos criar nosso index.html, o arquivo principal que importará todo o Javascript e carregará a aplicação:

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Webpack React Example</title>
</head>
<body>

<div id="app"></div>

<script src="bundle.js"></script>

</body>
</html>
```

Veja que temos uma parte que importa o arquivo 'bundle.js' ele será todo o javascript da nossa aplicação;

Para que esse arquivo seja criado, precisaremos do Webpack. Portanto, vamos criar o arquivo webpack.config.js, que será o arquivo de configuração do Webpack:

```js

module.exports = {

entry: './app.js',
output: {
filename: 'bundle.js',

  },
};
```

Feito já temos as configurações mínimas para uma aplicação com Webpack sendo necessário um arquivo de entrada (entry) e um de saída (output).

No caso nosso app.js sera o responsável pelo nosso javascript e por todo o resto ligado a nossa aplicação. Já o bundle.js será gerado automaticamente.


Após esses passos, podemos alterar o 'package.json' para que possamos rodar o webpack e gerar o build:

```json
{
"name": "webpack-react-example",
"version": "1.0.0",
"description": "",
"main": "index.js",
"scripts": {
"start": "webpack"
},
"author": "",
"license": "ISC",
"dependencies": {
"react": "^15.4.1",
"react-dom": "^15.4.1"
},
"devDependencies": {
"babel-core": "^6.18.2",
"babel-loader": "^6.2.8",
"babel-preset-es2015": "^6.18.0",
"babel-preset-react": "^6.16.0",
"webpack": "^1.13.3"
}
}

```

Nossa alteração foi adicionar o script `start`. Com ele, podemos rodar nossa aplicação com o comando:

```
npm start
```

Agora vamos criar o arquivo que falta, o app.js, que terá o Hello World em React:

```js
import React from 'react';
import ReactDOM from 'react-dom';

ReactDOM.render(<h1>Hello World</h1>, document.getElementById('app'));

```

Porém, apesar desse código ser muito simples, possui duas limitações que nossos browsers não conseguem interpretar:


- Código em React
- Código em ES2015

Por isso precisamos voltar em nosso arquivo de configuração do Webpack para usar loaders que transformem esse código em JavaScript puro que é entendido pelos browsers:

```js
module.exports = {
    entry: "./app.js",
    output: {
        filename: "bundle.js"
    },
    module: {
        loaders: [
    {
        test: /\.js$/,
        exclude: /node_modules/,
        loader: 'babel',
        query: {
            presets: ['react', 'es2015']
        }
       }
      ]
     }
}

```
Pode ter ficado complicado agora, mas vamos passo a passo.

Primeiro, vamos pegar todos os arquivos que terminem com .js:

```test: /\.js$/ ```

Depois, vamos excluir todos os arquivos que vem da pasta node_modules, porque não faz sentido tocarmos em libs externas:

```exclude: /node_modules/ ```

Agora, basta informarmos que vamos usar o Babel como loader principal:

```loader: 'babel```

E para fechar, vamos definir os dois loaders que precisamos, o babel-preset-es2015, e o babel-preset-react:

```
query: {
presets: ['react', 'es2015']
}

```
Pronto. Agora basta digitar o comando para rodar o Webpack:

```npm start```

Feito isso, temos um bom exemplo de como o webpack funciona. Caso quiser se aprofundar na ferramenta e melhorar essa aplicação, é recomendado ler o post original desse tutorial [clicando aqui](https://medium.com/tableless/webpack-para-react-o-guia-final-cb8a95b369ed).

Bem tudo isso foi um tutorial para explicar como o webpack funciona, e de certo modo é o que acontece por trás dos panos com o nosso index.html e nosso index.js, veja abaixo como fica os arquivos.

```js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(
<React.StrictMode>
<App />
</React.StrictMode>,
document.getElementById('root')
);
```


```html

<body>
<noscript>You need to enable JavaScript to run this app.</noscript>
<div id="root"></div>
<!--
This HTML file is a template.
If you open it directly in the browser, you will see an empty page.

You can add webfonts, meta tags, or analytics to this file.
The build step will place the bundled scripts into the <body> tag.

To begin the development, run 'npm start' or 'yarn start'.
To create a production bundle, use 'npm run build' or 'yarn build'.
-->
</body>
</html>

```

Apenas um pedaço do código original do index.html


##  Referências:

[Webpack para React: o Guia Final](https://medium.com/tableless/webpack-para-react-o-guia-final-cb8a95b369ed)

<br>
<p align="center">Made with :purple_heart:</p>

<p align="center">
<a href="https://github.com/he4rt/4noobs" target="_blank">
<img src="../../assets/global/footer-4noobs.svg" width="380">
</a>
</p>