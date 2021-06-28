<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../../assets/global/header-4noobs.svg">
  </a>
</p>

## Tipagem estática com Next.JS

Para começar um projet Next.JS com TypeScript basta utilizar um dos seguintes comandos:

```
npx create-next-app --ts
# ou
yarn create next-app --typescript
```

Agora para adicionar TypeScript a um projeto Next.JS existente acredito que uma boa forma dde se fazer é instalando o typescript e as tipagens do React como dependência de desenvolvimento:

```
npm install --dev typescript @types/react
# ou
yarn add --dev typescript @types/react

```

Após isso, crie um arquivo .ts ou .tsx na pasta pages, pode ser um "teste.ts" ou "teste.tsx" que na próxima vez que você rodar o script de "dev":

```
npm run dev
# ou
yarn dev
```

O Next.JS irá criar um tsconfig.json e um next.d.ts.

E pronto já poderá adicionar tipagem estática a sua base de código Javascript.

----------------

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>
