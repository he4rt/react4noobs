<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

# NPM e Yarn

O npm e o yarn são um gerenciador de pacotes, com ele é possível criar bibliotecas js e disponibilizá-las para a comunidade, além de poder incluir outras bibliotecas externas na sua aplicação.

Não iremos nos aprofundar muito no npm nesta seção, apenas explicar o básico sobre como instalar o React com a utilização do mesmo.

Se quiser um estudo mais profundo sobre npm, cheque a seção npm no [node4noobs](https://github.com/anabastos/node4noobs/blob/master/contents/1-primeiros-passos/npm.md).

# Create-react-app

O Create React App é uma ferramenta para criar projetos em React com o intuito de facilitar a configuração da aplicação.

## Instalação

Com o npx do npm iremos executar o seguinte comando para criar a aplicação. Ou podemos utilizar o Yarn para fazermos o mesmo processo.

```cmd
npx create-react-app react4noobs

-- ou --
 
yarn create react-app react4noobs
```

Aguarde alguns minutos para que o npm baixe as dependências.

O create react app irá gerar todo o projeto em modo padrão, não é necessário configurar **ferramentas** como Babel ou Webpack, eles estarão pré-configurados por debaixo dos panos.

Ao abrir seu package-lock.json você encontrará três scripts, para :


| Comando | Rodando com NPM | Rodando com Yarn |
| ------- | --------------- | ---------------- |
| start   | npm start       | yarn start       |
| build   | npm run build   | yarn build       |
| eject   | npm run eject   | yarn eject       |

O **start** iniciará a aplicação de acordo com os componentes desenvolvidos no */src*.

E uma tela no navegador irá se abrir:

<img align="center" src="/assets/npm-start-react.jpeg" alt="" width="50%">

Quando você alterar qualquer arquivo e salvar, eles serão recompilados e a janela do navegador será atualizada. Caso algum erro ocorra, ele aparecerá em vermelho no console.

<img align="center" src="/assets/error-npm.jpg" alt="" width="50%">

O **build** é utilizado para enviar a aplicação para "produção".

Como isso acontece? Ao executá-lo o babel transpila a aplicação automaticamente e todo o app será mandado para uma pasta */build* fora da */src* em arquivos estáticos, e então seu arquivo estará pronto para ser colocado em produção.

O **eject** é interessante, inicialmente o create-react-app empacota e esconde os módulos do npm que ele está usando por debaixo dos panos, para que o *package.json* seja mais limpo e simples. Porém se você quiser começar a adicionar configurações mais complexas e instalar outros módulos, seus módulos atuais precisam saber quais são os módulos existentes. Então ao executar o **eject** ele não esconderá mais esses módulos, e eles estarão disponíveis no seu *package.json*.

Por fim, não é sempre necessário utilizar o create-react-app para criar o seu projeto, você também pode criar o seu projeto na mão, do zero. Porém como o curso tem o foco para inciantes, isso seria um assunto para conversarmos no futuro.

---

Vamos olhar agora um pouco sobre  [dependências](./1.1.1-O-que-são-dependências.md).

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>