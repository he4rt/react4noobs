<p align="center">
<a href="https://github.com/he4rt/4noobs" target="_blank">
<img src="../../assets/global/header-4noobs.svg">
</a>
</p>

<p align="center">
    <img src="../../assets/vite.png" style="width: 200px">
</p>

# O que é Vite?

O Vite.js é um servidor de desenvolvimento rápido e leve para projetos JavaScript e TypeScript. Ele usa o especificador de arquivo de configuração do Vite para detectar automaticamente as configurações de compilação e fornece recursos como transpilação em tempo real e recarregamento automático de página.

Ele também possui suporte a módulos ES modules nativos, o que significa que você pode começar a desenvolver imediatamente sem configurar um bundler como webpack. Vite é uma boa opção para projetos menores ou para prototipagem rápida.

# Por que usar o vite e não outras ferramentas de build?

o Vite foi projetado para ser rápido e eficiente, especialmente em comparação com outras ferramentas populares como webpack. Ele usa o ES modules nativo para carregar módulos sem precisar passar por um processo de empacotamento, o que torna o desenvolvimento mais rápido.

Além disso, ele não requer configurações complexas, ele usa o arquivo vite.config.js para detectar automaticamente configurações de compilação.

E para aqueles que são fã do typescript o vite tem suporte nativo para TypeScript, o que significa que você pode começar a escrever códigos TypeScript sem ter que fazer uma configuração adicional.

Caso você tenha curiosidade recomendo dar uma olhada na documentação oficial, basta [clicar aqui](https://vitejs.dev/guide/)

# Como utilizar o Vite no React?

De maneira simples, o vite disponibiliza comandos para iniciar um projeto React, Angular, Vue, Svelte e Lit. Para iniciar um projeto React basta rodar o comando:

```bash
npm create vite@latest my-react-app --template react

ou

npm create vite@latest my-react-app --template react-ts

```

Após isso, basta você codar e o vite irá fazer o resto. Ele irá criar um servidor de desenvolvimento e irá atualizar a página automaticamente quando você salvar um arquivo.

## Referências:

[Site oficial do ViteJS](https://vitejs.dev)

[Ir para Próxima Seção](../Estilizacao/1.Preprocessadores%20CSS.md)

<br>
<p align="center">Made with :purple_heart:</p>

<p align="center">
<a href="https://github.com/he4rt/4noobs" target="_blank">
<img src="../../assets/global/footer-4noobs.svg" width="380">
</a>
</p>
