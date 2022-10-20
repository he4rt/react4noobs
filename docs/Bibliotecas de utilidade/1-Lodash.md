[![4noobs](../../assets/global/header-4noobs.svg)](https://github.com/he4rt/4noobs)

# _Lodash

## O que é o Lodash

Por mais que seja divertido implementar do zero aquela função cheia de malabarismos
que demonstram todo seu conhecimento em ciência da computação, às vezes a gente
precisa de rapidez, eficiência, performance e modularidade o mais rápido possível.
Para resolver este problema, eu lhes apresento: [Lodash](https://lodash.com).

Lodash é uma biblioteca Javascript que possui várias funções que são frequentemente
utilizadas por quem desenvolve software com JS.

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
utiliza o lodash.  Você pode utilizar o nome que preferir.

## Categorias

O Lodash tem 13 categorias de funções:

- Array
- Collection
- Date
- Function
- Lang
- Math;
- Number;
- Object;
- Seq;
- String;
- Util;
- Properties;
- Methods.

## Algumas funções

Utilizar o lodash é super simples, pois funciona como qualquer outro objeto em
javascript. Nesse artigo, utilizaremos as funções mais conhecidas, mas você pode
checar a [documentação](https://lodash.com/docs/4.17.15) para mais exemplos.

---

### Contexto

Vamos supor que você acaba de ser contratado e ainda está conhecendo o sistema no
qual vai trabalhar. As pessoas estão te passando algumas pequenas tasks.

Existe uma tabela na interface da aplicação que está sendo desenvolvida, e enviado
para esta tabela, nós temos o seguinte [array de
objetos](https://www.freecodecamp.org/portuguese/news/tutorial-de-arrays-de-objetos-em-javascript-como-criar-atualizar-e-percorrer-objetos-em-lacos-usando-metodos-de-array-do-js/):

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

Te passaram algumas tasks para manipular apenas o array enquanto fazem seu onboarding.

Agora chega de papinho e vamos botar a mão na massa!

### capitalize

Como você pode notar, todos os nomes estão com a primeira letra minúscula. É legal
fazer isso para fins de normalização da informação, mas não queremos mostrar assim
para o usuário.

Então sua primeira task é deixar a primeira letra de todos os nomes em maiúsculo.

Felizmente, com o lodash, isso ficar mais simples do que já é:

```js
const capitalizedDevDepartment = devDepartment.map((worker) => ({
  ...worker,
  firstName: _.capitalize(worker.firstName),
  lastName: _.capitalize(worker.lastName)
}));
```

No trecho de código acima nós usamos o map para gerar uma nova lista! Aqui
[iteramos](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Guide/Loops_and_iteration)
sobre os elementos da lista `devDepartment`, e para cada elemento, nós adicionamos a
informação já existente do funcionário usando o [spread
operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
e sobrescrevemos o primeiro e segundo nome pelo retorno da função `capitalize()`
aplicada aos valores antigos.

Pareceu complicado na explicação, mas se você não entendeu, olhe o código novamente
e pense em cada operação que ele está executando.

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

Pode mover o card dessa task e enviar o pull request. Vamos para a próxima!

---

### orderBy

Agora você precisa implementar um filtro de ordenação na lista de funcionários. O
usuário deve ser capaz de **ordenar os funcionários pelo salário.**

A lodash nos oferece o `orderBy` para resolver esse problema:

```js
const workersOrderedBySalary = _.orderBy(capitalizedDevDepartment, 'salary', 'desc')
```

No snippet acima, nós estamos ordenando a lista `capitalizedDevDepartment` de forma
decrescente, utilizando a chave `salary` como parêmetro de ordenação. Então nós
armazenamos o [retorno da função](https://developer.mozilla.org/pt-BR/docs/Learn/JavaScript/Building_blocks/Return_values) na constante workersOrderedBySalary.

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

Já pode rodar a pipeline de produção, galera. Essa aqui foi fácil!

---

### uniqWith & isEqual

Ao subir o código para produção, o cliente nota um problema: ele só tem 7 funcionários
nesse departamento, mas estão aparecento 8. Você já deve ter notado o problema, certo?
O funcionário de ID 4 e firstName "Cardi", está duplicado!

Esse é um problema simples de resolver, mas com o lodash fica ainda mais fácil. **Você
vai combinar duas funções do lodash: `uniqWith` e `isEqual`**.

```js
const normalizedWorkersList = _.uniqWith(workersOrderedBySalary, _.isEqual)
```

Nessa curtia linha de código o Lodash está trabalhando bastante. Em resumo, a função
`uniqWith` faz a comparação entre dois elementos de cada vez, utilizando um
**comparador**, que no nosso caso é a função `isEqual()`. A função `isEqual` será
invocada com dois itens como argumento, o elemento da vez (othVal), e os outros
elementos que serão comparados(arrVal). Assim, todos os valores são comparados com
todos os outros valores, livrando a lista de toda duplicação.

Tá vendo como o Lodash abstrai bastante a complexidade dessas operações?

Foi tão fácil que nem parece que a gente tá trabalhando. Agora nosso array de objetos
está assim:

```js
[
  { id: 6, firstName: "Chico", lastName: "Science", salary: 15000, age: 46, level: "sr" },
  { id: 2, firstName: "Ada", lastName: "Lovelace", salary: 12000, age: 59, level: "sr" },
  { id: 5, firstName: "David", lastName: "Glover", salary: 10000, age: 31, level: "pl" },
  { id: 4, firstName: "Cardi", lastName: "B", salary: 9700, age: 32, level: "pl" },
  { id: 3, firstName: "Childish", lastName: "Gambino", salary: 4800, age: 49, level: "jr" },
  { id: 1, firstName: "Kendrick", lastName: "Lamar", salary: 4500, age: 22, level: "jr" },
  { id: 7, firstName: "Leonardo", lastName: "DaVinci", salary: 1200, age: 31, level: "jr" },
];
```

Existem formas até mais fáceis de resolver esse problema, como, por exemplo, utilizando
a função `uniqBy` do lodash. Mas eu quis mostrar esse exemplo para demonstrar que você
pode compor funções do lodash à vontade.

Que tal tentar resolver esse mesmo problema utilizando o uniqBy? Cheque a
[documentação](https://lodash.com/docs/4.17.15#uniqBy).

---

### groupBy

Outra feature que o cliente te pediu, é que o usuário possa agrupar os funcionários
pelo seu nível. Como sempre, a Lodash deixa essa tarefa mamão com açúcar. Vamos ao
exemplo:

```js
const workersGroupedByLevel = _.groupBy(normalizedWorkersList, 'level')
```

Aqui nós indicamos que queremos gerar um objeto a partir da lista `normalizedWorkersList`
e agrupar os elementos a partir da key `level`.

Com apenas uma linha, nós temos todos os funcionários agrupados pelo nível de senioridade.

Nosso array de funcionários agora é um objeto, e está assim:

```js
{
  sr: [
    { id: 6, firstName: "Chico", lastName: "Science", salary: 15000, age: 46, level: "sr" },
    { id: 2, firstName: "Ada", lastName: "Lovelace", salary: 12000, age: 59, level: "sr" },
  ],
  pl: [
    { id: 5, firstName: "David", lastName: "Glover", salary: 10000, age: 31, level: "pl" },
    { id: 4, firstName: "Cardi", lastName: "B", salary: 9700, age: 32, level: "pl" },
  ],
  jr: [
    { id: 3, firstName: "Childish", lastName: "Gambino", salary: 4800, age: 49, level: "jr" },
    { id: 1, firstName: "Kendrick", lastName: "Lamar", salary: 4500, age: 22, level: "jr" },
    { id: 7, firstName: "Leonardo", lastName: "DaVinci", salary: 1200, age: 31, level: "jr" },
  ],
}
```

Agora pode pedir um aumento!

---

## Conclusão

Se você chegou até aqui, você já tem ótimos exemplos e uma boa justificativa para utilizar
o Lodash. Muitas vezes as abstrações criadas pelo Lodash não serão o bastante para o caso
que você precisa tratar, mas certamente esses momentos serão raros. É uma biblioteca que
casa muito bem com o jeito funcional de pensar que o React trás enquanto framework.

Um exercício muito interessante de fazer é **tentar implementar todas essas funções
do zero**. Isso vai te dar uma boa ideia da complexidade que o lodash resolve.

Além disso, tentar ler o código que eles produzem é uma ótima forma de aprender
também, este é o link para o repositório open source deles:
[Lodash](https://github.com/lodash/lodash).

Bons estudos!

[![4noobs](../../assets/global/footer-4noobs.svg)](https://github.com/he4rt/4noobs)