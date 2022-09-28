# _Lodash

## O que é o Lodash

Por mais que seja divertido implementar do zero aquela função cheia de malabarismos
que demonstram todo seu conhecimento em ciência da computação, às vezes a gente
precisa de rapidez, eficiência, performance e modularidade o mais rápido possível.
Para resolver este problema, eu lhes apresento: [Lodash](https://lodash.com).

Lodash é uma biblioteca Javascript que possui várias funções que são frequentemente
utilizadas por quem desenvolve software com JS. São funções utilitárias para manipular
arrays, strings, matrizes, objetos, datas, collections, etc.

## Instalando o Lodash

A melhor forma instalar o Lodash é usando um gerenciador de pacotes.

Na pasta do seu projeto, utilize um dos dois comandos (conforme o gerenciador de
pacotes que você está utilizando):

```bash
npm install --save lodash
# ou
yarn add lodash 
```

No seu código, dentro do arquivo desejado, você pode importar o lodash:

```js
import _ from "lodash"
```

**Nota**: usar `_` para nomear o pacote é apenas uma convenção da comunidade que
*utiliza o lodash.  Você pode utilizar o nome que preferir.

## Categorias

O Lodash tem 13 categorias de funções:

- Array

## Algumas funções

Utilizar o lodash é super simples, pois funciona como qualquer outro objeto em
javascript. Nesse artigo, utilizaremos as funções mais conhecidas, mas você pode
checar a [documentação](https://lodash.com/docs/4.17.15) para mais exemplos.

Chega de papinho. Vamos botar a mão na massa!

### Capitalize

Vamos supor que seu sistema lista todos os funcionários de um determinado departamento
numa tabela. Sua task é criar uma funcionalidade na qual, ao clicar em uma das linhas da
tabela, **você consiga ver algumas as informações do funcionário da linha.** O clique na
linha já envia o ID do funcionário.

O objeto que está sendo enviado para a tabela é esse:

```js
const devDepartment = [
  { id: 1, firstName: "kendrick", lastName: "lamar", salary: 4500, age: 22, level: "jr" },
  { id: 2, firstName: "ada", lastName: "lovelace", salary: 12000, age: 59, level: "sr" },
  { id: 3, firstName: "childish", lastName: "gambino", salary: 4800, age: 49, level: "jr" },
  { id: 4, firstName: "cardi", lastName: "b", salary: 9700, age: 32, level: "pl" },
  { id: 5, firstName: "david", lastName: "glover", salary: 10000, age: 31, level: "pl" },
  { id: 7, firstName: "leonardo", lastName: "daVinci", salary: 1200, age: 31, level: "jr" },
  { id: 4, firstName: "cardi", lastName: "b", salary: 5700, age: 32, level: "jr" },
  { id: 6, firstName: "chico", lastName: "science", salary: 15000, age: 46, level: "sr" },
];
```

O primeiro problema que você precisa resolver é deixar a primeira letra de cada nome
maiúscula.

Felizmente, com o lodash, isso ficar mais fácil do que já é:

```js
const capitalizedDevDepartment = funcionarios.map((funcionario) => ({
  ...funcionario,
  firstName: _.capitalize(funcionario.firstName),
  lastName: _.capitalize(funcionario.lastName)
}));

```

Pronto! Resolvido. Temos todos os nomes começando com letra maiúscula. Nosso lista está
assim:

```js
[
  { id: 2, firstName: "Ada", lastName: "Lovelace", salary: 12000, age: 59, level: "sr" },
  { id: 5, firstName: "David", lastName: "Glover", salary: 10000, age: 31, level: "pl" },
  { id: 4, firstName: "Cardi", lastName: "B", salary: 9700, age: 32, level: "pl" },
  { id: 4, firstName: "Cardi", lastName: "B", salary: 9700, age: 32, level: "pl" },
  { id: 3, firstName: "Childish", lastName: "Gambino", salary: 4800, age: 49, level: "jr" },
  { id: 7, firstName: "Leonardo", lastName: "DaVinci", salary: 1200, age: 31, level: "jr" },
  { id: 1, firstName: "Kendrick", lastName: "Lamar", salary: 4500, age: 22, level: "jr" },
  { id: 6, firstName: "Chico", lastName: "Science", salary: 15000, age: 46, level: "sr" },
];
```

### OrderBy

Agora você precisa implementar um filtro de ordenação na lista de funcionário. O
usuário deve ser capaz de ordenar os funcionários pelo salário. 

A lodash nos oferece o `orderBy`:

```js
const workersOrderedBySalary = _.orderBy(capitalizedDevDepartment, 'salary', 'desc')
```

E dessa forma você consegue a lista anterior ordenada do maior salário para o menor:

```js
[
  { id: 6, firstName: "Chico", lastName: "Science", salary: 15000, age: 46, level: "sr" },
  { id: 2, firstName: "Ada", lastName: "Lovelace", salary: 12000, age: 59, level: "sr" },
  { id: 5, firstName: "David", lastName: "Glover", salary: 10000, age: 31, level: "pl" },
  { id: 4, firstName: "Cardi", lastName: "B", salary: 9700, age: 32, level: "pl" },
  { id: 4, firstName: "Cardi", lastName: "B", salary: 9700, age: 32, level: "pl" },
  { id: 3, firstName: "Childish", lastName: "Gambino", salary: 4800, age: 49, level: "jr" },
  { id: 1, firstName: "Kendrick", lastName: "Lamar", salary: 4500, age: 22, level: "jr" },
  { id: 7, firstName: "Leonardo", lastName: "DaVinci", salary: 1200, age: 31, level: "jr" },
];
```

### GroupBy

Outra feature que o cliente te pediu, é que o usuário possa agrupar os funcionários
pelo seu nível. Como sempre, a Lodash deixa essa tarefa mamão com açúcar. Vamos ao
exemplo:

```js

```
