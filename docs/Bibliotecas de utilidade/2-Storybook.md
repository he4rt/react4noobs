[![4noobs](../../assets/global/header-4noobs.svg)](https://github.com/he4rt/4noobs)

# Storybook

## O que é o Storybook

[**Storybook**](https://storybook.js.org/) é uma ferramenta de desenvolvimento que permite criar e testar componentes de interface de usuário (UI) de forma isolada. É amplamente utilizada em projetos de desenvolvimento front-end para criar bibliotecas de componentes reutilizáveis e garantir a consistência visual e funcionalidade dos componentes antes de integrá-los em um projeto maior.

## Instalando o Storybook

```js
npx storybook@latest init
```

O comando acima fará as seguintes alterações em seu ambiente local:

📦 Instalará as dependências necessárias.<br>
🛠 Configurará os scripts necessários para executar e construir o Storybook.<br>
🛠 Adicionará a configuração padrão do Storybook.<br>
📝 Adicionará alguns exemplos de histórias para você começar.

## Iniciar o Storybook

O Storybook inclui um servidor de desenvolvimento integrado. Ao executar o comando do Storybook, ele inicia o servidor local, exibe o endereço e abre automaticamente uma nova aba no navegador com uma tela de boas-vindas.

```js
npm run storybook
```

## Renderizar estilos de componentes

O Storybook não impõe uma maneira específica de gerar ou carregar CSS e renderiza os elementos DOM fornecidos. No entanto, pode ser necessário configurar suas ferramentas de CSS para que os componentes sejam exibidos corretamente. Existem guias de configuração disponíveis para ferramentas populares na comunidade.

- [Tailwind](https://storybook.js.org/recipes/tailwindcss/)
- [Material UI](https://storybook.js.org/recipes/@mui/material/)
- [Vuetify](https://storybook.js.org/recipes/vuetify/)
- [Styled Components](https://storybook.js.org/recipes/styled-components/)
- [Emotion](https://storybook.js.org/recipes/@emotion/styled/)
- [Sass](https://storybook.js.org/recipes/sass/)
- [Bootstrap](https://storybook.js.org/recipes/bootstrap/)
- [Less](https://storybook.js.org/recipes/less/)
- [Vanilla-extract](https://storybook.js.org/recipes/@vanilla-extract/css/)
