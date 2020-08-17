# PreProcessadores CSS

## O que é um pré processador

Basicamente é como se você programasse em uma linguagem de programação compilada. Você escreve na sintaxe definida (Less/Sass/etc), o pré processador transforma para CSS e então você acrescenta o arquivo CSS a sua página normalmente.

### ⚠ Aviso:

> Algo importante a frisar é que usar esses Pré processadores é bem simples independente da sintaxe... Porém, é muitíssimo importante que você já tenha uma boa base de CSS, caso você ainda não se sinta confotável com essa tecnologia [pode clicar aqui para aprender mais no Css4noobs](https://github.com/mathh95/css4noobs).

---

## qual os mais utilizados?

São muitos nomes no mercado, porém os mais poderosos e badalados são [Less](https://lesscss.org/), [Sass](https://sass-lang.com/), [Stylus](https://learnboost.github.io/stylus/).

## Afinal, Qual devo usar?

Recomendamos que você acesse o site de cada um dos pré processadores, veja o que mais te interessa ou agrada conforme sua experiência e o que te atenderia caso queira usar determinado Framework. Por exemplo: quer usar o Compass, aprenda Sass.

> Na próxima seção vamos tratar de Framework CSS, aguardo você.

De início vamos usar o Sass, porque desde 2018 o React já traz uma ótima compatibilidade com ele.

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

> No entanto, observe que isso instalará a implementação JavaScript pura do Sass

Se você usa o gerenciador de pacotes Homebrew para Mac OS X, pode instalar o Dart Sass executando

```
brew install sass / sass / sass
```
### ⚠ Observação:
Agora todos os seus arquivos CSS devem usar a extensão .scss, Por exemplo, ao invés de usar "App.css" use "App.scss".
## O básico de Sass:

> Vamos seguir o padrão mostrando primeiro como é feito em Sass e em seguida como seria em CSS puro (ou como o próprio Sass iria compilar para CSS)

## Variáveis

Pense nas variáveis ​​como uma forma de armazenar informações que você deseja reutilizar em sua folha de estilo. Você pode armazenar coisas como cores, fontes ou qualquer valor CSS que deseja reutilizar. **Sass usa o \$** para tornar algo uma variável.

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

> Quando o Sass é processado, ele leva as variáveis que definiu ($font-stack e $primary-color) para arquivos CSS com os nossos valores de variáveis colocados no CSS. Isso pode ser extremamente poderoso ao trabalhar com cores e mantê-las consistentes em todo o site.


## Nesting(Escopos)

Lembra do aninhamento em HTML? Algo que fazemos o tempo todo quando colocamos um < p > em um < div > e um < span > no < p > como este?
```
<body>
      <div>
          <p>
              <span></span>
          </p>
      <div>
</body>
```

O SCSS nos permite aninhar seletores CSS de maneira semelhante. O Nesting é um atalho para a criação de regras CSS. Portanto, em vez de escrever tantas linhas de CSS apenas para ser específico sobre o estilo que queremos aplicar a um elemento.

Então podemos escrever:
#### Sass:
```
#sidebar {
        position: fixed;
        height: 100%;

        ul {
            list-style-type: none;
            padding: 0;

            li {
                background-color: #F2F2F2;
                color: #404040;
            }
        }
    } 
```
#### CSS:
```
#sidebar {
        position: fixed;
        height: 100%; }
    #sidebar ul {
        list-style-type: none;
        padding: 0; }
    #sidebar ul li {
        background-color: #F2F2F2;
        color: #404040; }
```
> Esse foi um exemplo simples para demonstrar o poder do Sass, podendo transformar um código complexo para um de fácil entendimento, para uma futura manutenção

### Poderá usar Media query ou qualquer propriedade CSS normalmente, por exemplo:

#### Sass:
```
 #sidebar {
        position: fixed;
        height: 100%;

        @media (max-width:768px) {
            left: -9999;
        }

        ul {
            list-style-type: none;
            padding: 0;
        }
    } 
```

#### CSS:
```
  #sidebar {
        position: fixed;
        height: 100%; }
    @media (max-width: 768px) {
        #sidebar {
            left: -9999; } }
    #sidebar ul {
        list-style-type: none;
        padding: 0; }
```
### Propriedades CSS:

#### Sass:
```
 li {
       background: {
           image: url("image.png");
           position: fixed;
           }
       margin : {
           top: 1rem;
           left: 2rem;
           right: 1rem;
           }
      }
```
#### CSS:
```
  li {
        background-image: url("image.png");
        background-position: fixed;
        margin-top: 1rem;
        margin-left: 2rem;
        margin-right: 1rem; }
```

## Parciais
Você pode criar arquivos Sass parciais que contêm pequenos trechos de CSS  que podem ser incluídos em outros arquivos Sass. Esta é uma ótima maneira de modularizar seu CSS e ajudar a manter as coisas mais fáceis de manter. Um parcial é um arquivo Sass nomeado com um sublinhado à esquerda. Você pode chamá-lo de algo como **_arquivo.scss** (É obrigatório o uso do _ ). O sublinhado permite que o Sass saiba que o arquivo é apenas um arquivo parcial e que não deve ser gerado em um arquivo CSS . Parciais de Sass são usados ​​com a @use regra.

### Podemos importar esse arquivos parciais através da seguinte sintaxe:
```
@import "diretorio/_arquivo.scss";
```

## Mixins
Algumas coisas em CSS são um pouco tediosas de escrever, especialmente com CSS3  e as muitas propriedades que existem. Um mixin permite que você faça grupos de  declarações CSS que deseja reutilizar em todo o seu site. Você pode até mesmo passar valores para tornar seu mixin mais flexível. Um bom uso de um mixin é para prefixos de propriedades. Aqui está um exemplo para  transform.
```
@mixin he4rtDev($property) {
  -webkit-transform: $property;
  -ms-transform: $property;
  transform: $property;
}
.box { @include he4rtDev(rotate(30deg)); }
```
Para criar um mixin você usa o **@mixin** e dá um nome a ele. Nós nomeamos nosso mixin **he4rtDev**. 
Também estamos usando a variável  **$property** entre parênteses para que possamos passar uma transformação do que quisermos. Depois de criar seu mixin, você pode usá-lo como uma  declaração CSS começando com **@include** seguido pelo nome do seu mixin.