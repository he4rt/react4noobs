# PreProcessadores CSS

## O que é um pré processador

Basicamente é como se você programasse em uma linguagem de programação compilada. Você escreve na sintaxe definida (Less/Sass/etc) e o pré processador compila para CSS e então você acrescenta o arquivo CSS a sua página normalmente.

### ⚠ Aviso:
> Algo importante a frisar é que usar esses Pré processadores é bem simples independente da sintaxe... Porém, é muitíssimo importante que você já tenha uma boa base de [CSS](https://www.w3schools.com/css/).
---
## Qual os mais utilizados?
São muitos nomes no mercado, porém os mais poderosos e badalados são  [Less](https://lesscss.org/), [Sass](https://sass-lang.com/), [Stylus](https://learnboost.github.io/stylus/). 

## Afinal, Qual devo usar?

Recomendamos que você acesse o site de cada um dos pré processadores e veja o que mais te interessa ou agrada conforme sua experiência e o que te atenderia caso queira usar determinado Framework. Por exemplo: quer usar o Compass, aprenda Sass.
> Vamos tratar de Framework CSS futuramente aqui no React4noobs, fique atento.

De início vamos usar o Sass porque desde 2018 o React já traz uma ótima compatibilidade com ele. 

<img align="center" src="/assets/estilizacao/SassReact.png" width="70%"> 

## Por que usar o Sass?
CSS por si só pode ser divertido, mas as folhas de estilo estão ficando maiores, mais complexas e mais difíceis de manter. É aqui que um pré-processador pode ajudar. O Sass permite que você use recursos que ainda não existem no CSS, como variáveis, aninhamento, mixins, herança e outros recursos interessantes que tornam a escrita CSS divertida novamente.

Palavras da equipe Sass.

## Agora podemos instalar o Sass, utilizando o Node.js, com o npm execute:
```
npm install -g sass
```
Ou se você prefere Yarn:
```
yarn add lib.sass
```
>No entanto, observe que isso instalará a implementação JavaScript pura do Sass

Se você usa o gerenciador de pacotes Homebrew para Mac OS X, pode instalar o Dart Sass executando
```
brew install sass / sass / sass
```

## O básico de Sass:

> Vamos seguir o padrão mostrando primeiro como é feito em Sass e em seguida como seria em CSS puro(ou como o próprio Sass iria compilar para CSS)

### Variáveis
Pense nas variáveis ​​como uma forma de armazenar informações que você deseja reutilizar em sua folha de estilo. Você pode armazenar coisas como cores, fontes ou qualquer valor CSS que achar que deseja reutilizar. **Sass usa o $ símbolo** para tornar algo uma variável.

#### Sass:
```
$font-stack:    Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```
#### CSS:
```
body {
  font: 100% Helvetica, sans-serif;
  color: #333;
}
```
>Quando o Sass é processado, ele leva as variáveis que definiu como "$font-stack e $primary-color" para saídas normais CSS com os nossos valores de variáveis colocados no CSS. Isso pode ser extremamente poderoso ao trabalhar com cores e mantê-las consistentes em todo o site.
