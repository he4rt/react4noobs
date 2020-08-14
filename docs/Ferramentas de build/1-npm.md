# NPM

O npm é um gerenciador de pacotes, com ele é possível criar bibliotecas js e disponibiliza-las para a comunidade, além de poder incluir outras bibliotecas externas na sua aplicação.

Não iremos nos aprofundar muito no npm nessa sessão, apenas explicar o básico de como instalar o React com a utilização do mesmo.

Se quiser um estudo profundo sobre, cheque a sessão npm no [node4noobs](https://github.com/anabastos/node4noobs/blob/master/contents/1-primeiros-passos/npm.md).

# Create-react-app

O Create React App é uma ferramenta para criar projetos em React com o intuito de facilitar a configuração da aplicação.

## Instalação

```cmd
    npm install -g create-react-app
```

Agora para criar sua aplicação, iremos digitar duas coisas na linha de comando, uma sendo o create-react-app e o nome do projeto.

```cmd
    create-react-app react4noobs
```

Aguarde alguns minutos para que o npm baixe as dependências.

*insira aqui um gif da criação*

O create react app irá gerar todo o projeto em modo padrão, não é necessário configurar ferramentas como Babel ou Webpack, eles estarão pré-configurados por debaixo dos panos.

Ao abrir seu package-lock.json você encontrará três scripts:

- start
- build
- eject

O **start** iniciará a aplicação de acordo com os componentes desenvolvidos no */src*.

E uma tela no navegador irá se abrir:

*insira aqui uma imagem do localhost*

Quando você alterar qualquer arquivo e salvar, eles são recompilados e a janela do navegador será atualizada, caso algum erro ocorra, ele aparecerá em vermelho no console.

*insira imagem de erro aqui*