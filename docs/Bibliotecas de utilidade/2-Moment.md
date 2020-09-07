<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

<p align="center">
  <h2 align="center">React4Noobs</h2>

  <h1 align="center">
  <img src="../../assets/logo.png" alt="Imagem do Reactjs" width="220">
</h1>
  
  <p align="center">
    <br />
    <a href="../README.md">Explore a documentação »</a>
    <br />
    <br />
    <a href="https://github.com/he4rt/react4noobs/issues">Report Bug</a>
    ·
    <a href="https://github.com/he4rt/react4noobs/issues">Request Feature</a>
  </p>
</p>

# Moment.js

<p align="center">
    <img src="../../assets/moment-logo.png">
</p>

## O que é o Moment?

Moment (Ou [Moment.js](https://momentjs.com/)) é uma biblioteca leve e super inteligente que traz diversos recursos de manipulação de data/hora.

### Instalando o Moment

Para instalar o Moment é necessário de qualquer um dos comandos abaixo

```
npm install moment --save   # npm
yarn add moment             # Yarn

// Os acima são os principais, mas também está disponível em outros gerenciadores de pacote
Install-Package Moment.js   # NuGet
spm install moment --save   # spm
meteor add momentjs:moment  # meteor
```

Para mais informações, consulte a documentação do {Moment}(https://momentjs.com/docs/).

## Iniciando com Moment

Importe o moment.

```js
import moment from 'moment';
```

Isto lhe disponibilizará uma interface para as manipulações do moment.

> ### DICA: Você pode usar [esta sandbox](http://jsfiddle.net/brandonscript/rLjQx/) para testar o moment mais rapidamente!

### Interpretação de data/hora

O moment possui um interpretador que tenta descobrir o formato da sua data e realizar a sua interpretação adequadamente. Portanto, podemos realizar as seguintes ações:

```js
moment() // Sat Aug 08 2020 15:06:09 GMT-0300
moment("05/05/1998"); // Tue May 05 1998 00:00:00 GMT-0300
moment("06/05/2004 15:40"); // Sat Jun 05 2004 15:40:00 GMT-0300
moment("06/05/2004 3:00 PM"); // Sat Jun 05 2004 15:00:00 GMT-0300

// Também são aceitos objetos Date
moment(new Date()); // Sat Aug 08 2020 15:09:22 GMT-0300

// E UNIX timestamps
moment(1596910256); // Mon Jan 19 1970 08:35:10 GMT-0300

// O moment também aceita objetos moment.Moment
moment(moment())
```

> ### DICA: O UNIX timestamp representa os segundos desde a meia-noite do dia 1970 (Em UTC) sem considerar segundos bissextos. Leitura recomendada: [Clique aqui para acessar](https://pt.stackoverflow.com/a/70604/126413)

### Locales (Linguagem)

O moment define diversos locales para uso nas datas. No exemplo acima notamos que o moment levou como base o inglês.

```js
moment.locale();         // en
```

Podemos alterar o locale com o uso da função `locale()`, passando como parâmetro o locale que necessitamos.

```js
moment.locale('pt-br'); // Locale alterado para Português - Brasil
```

### Funções de utilidade 

Conforme apresentado anteriormente, o moment tem diversas funções utilitárias para manipulação de datas

```js
// Datas "desde agora" (tempo relativo)
moment("20111031", "YYYYMMDD").fromNow(); // há 9 anos
moment("20120620", "YYYYMMDD").fromNow(); // há 8 anos
moment().startOf('day').fromNow();        // há 15 horas
moment().endOf('day').fromNow();          // em 9 horas
moment().startOf('hour').fromNow();       // há 24 minutos

// Subtração/Adição de datas. Formatação com base no calendário
moment().subtract(10, 'days').calendar(); // 29/07/2020
moment().subtract(6, 'days').calendar();  // Último domingo às 15:24
moment().subtract(3, 'days').calendar();  // Última quarta-feira às 15:24
moment().subtract(1, 'days').calendar();  // Ontem às 15:24
moment().calendar();                      // Hoje às 15:24
moment().add(1, 'days').calendar();       // Amanhã às 15:24
moment().add(3, 'days').calendar();       // terça-feira às 15:24
moment().add(10, 'days').calendar();      // 18/08/2020
```

O moment também disponibilizaa diversas opções para formatação de datas em strings, muito utilizado para apresentação de dados.

```js
moment().format('MMMM Do YYYY, h:mm:ss a'); // agosto 8º 2020, 3:27:04 pm
moment().format('dddd');                    // sábado
moment().format("MMM Do YY");               // ago 8º 20
moment().format("YYYY [exemplo] YYYY");     // 2020 exemplo 2020
moment().format();                          // 2020-08-08T15:27:16-03:00
```

Esta função `format` toma como base o locale fornecido, portanto, você pode utilizar como o código abaixo, para caso sejam necessárias línguas diferentes.

```js
var marco = moment('2020-03')
marco.format('MMMM') // Março

moment.locale('de')  // Toma 'de' como base de locale
marco.format('MMMM') // 'March', pois a instância foi criada antes do locale ser definido.

var novoMarco = moment('2020-03')
novoMarco.format('MMMM') // 'März', conforme o 'de'

// O mesmo não acontece caso você altere o locale do momento que já foi definido
marco.locale('pt-br')
marco.format('MMMM') // 'Marzo'
```

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>