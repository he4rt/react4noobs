<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

# Introdução

> Caso prefira, também escrevi esse artigo no meu [Blog](https://gabrielduete.com/pt-br/blog/art-of-lazy-loading) e no [DEV](https://dev.to/gabrielduete/the-art-of-lazy-loading-how-to-improve-your-frontend-app-performance-nextjsreact-4h5l).

Lazy Loading é uma estratégia de otimização de desempenho. Com essa estratégia,
garantimos que alguns recursos sejam carregados **somente quando realmente
necessários**, ou seja, quando estão prestes a entrar na **área visível da
página (viewport)**.

## Visão geral

Por padrão, podemos usar Lazy Loading em JavaScript, CSS, fontes, imagens e
iframes.

Podemos definir o atributo `loading` em elementos `img` ou `iframe`, assim:

![example-attribute_loading.html](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/71u1kqx5sncswurvi1uo.png)

Com isso, conseguimos instruir o navegador a **adiar o carregamento** desse
elemento até que ele esteja prestes a ser exibido na tela.

# Lazy Loading no Next.js

No Next.js, as coisas funcionam de forma um pouco diferente. Temos **duas
estratégias nativas principais** para criar componentes com lazy loading, e vou
adicionar mais uma que pode facilitar ainda mais nossa vida:

- [Dynamic Imports (Next.js)](https://nextjs.org/docs/pages/building-your-application/optimizing/lazy-loading#nextdynamic)
- [React Lazy (React)](https://react.dev/reference/react/lazy)
- [react-lazyload (biblioteca externa)](https://www.npmjs.com/package/react-lazyload)

# 1. Dynamic Imports

Com os **Dynamic Imports** do Next.js, podemos importar componentes
dinamicamente, algo muito útil para componentes que **não são necessários no
carregamento inicial da página**.

Um bom exemplo de uso é com componentes de feedback, como modais ou alertas, que
só são exibidos após alguma ação do usuário. Então, por que carregá-los logo no
início?

Podemos importar apenas quando for realmente necessário!

Veja um exemplo onde temos um botão e um componente `Snackbar` do Material UI.
Após o clique, o Snackbar deve ser exibido com um aviso:

![code](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/mny2gzxqeek3itovxdr4.png)

Resultado:

![Resultado no navegador](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/vgf51ji9vr6fj00w6qyc.gif)

Podemos ver que o `Snackbar` e o `Alert` são carregados inicialmente, mas só são
utilizados **se** o usuário clicar no botão. E se ele **não** clicar? O
carregamento desses dois componentes se torna inútil.

Vamos olhar para o tamanho do Build, especialmente o "First Load JS":

![Imagem do build](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/uwhnnhg46rn2thj1xnqj.png)

Agora, o mesmo exemplo usando **Dynamic Imports** para `Snackbar` e `Alert`:

![Exemplo com dynamic imports](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/q73g9cu49o3ujejs22xp.png)

Resultado idêntico:

![Resultado no navegador](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3jee9bnacpc9idqfm01l.gif)

Build:

![Imagem do build](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/6kn8w0dslvp44uq6hayl.png)

Podemos ver que o tamanho do **First Load JS** caiu significativamente!

- De `43 KB` para `35.6 KB`
- E de `148 KB` para `141 KB`

Você pode pensar: “Mas foi pouco!”. Estamos falando de **apenas uma página**,
com uma funcionalidade simples. Agora imagine isso em **todo o seu site**?

### Vamos calcular o ganho total para 10 páginas:

1. **Antes da otimização:**

   - Tamanho por página: **43 KB**
   - Total: **43 KB × 10 = 430 KB**

2. **Depois da otimização:**
   - Tamanho por página: **35.6 KB**
   - Total: **35.6 KB × 10 = 356 KB**

### **Economia total**

- Redução: **430 KB - 356 KB = 74 KB**
- Porcentagem: **(74 ÷ 430) × 100 ≈ 17,2%**

Isso mostra que, em um site com muitas páginas, pequenas otimizações podem gerar
uma **grande diferença** no consumo de recursos e no tempo de carregamento.

# 2. React Lazy

Também podemos usar o `React.lazy`, que é uma funcionalidade nativa do React
para importar componentes dinamicamente — bem parecido com os dynamic imports do
Next.js.

A diferença é que aqui, **precisamos usar o `Suspense`** para envolver o
componente, e passar um componente no `fallback`, que será exibido **enquanto o
componente está sendo carregado**.

Esse carregamento ocorre **apenas na primeira vez** que o componente é usado. Se
o usuário recarregar a página, será carregado novamente — mas se ele continuar
navegando, não haverá novo carregamento.

Exemplo:

![Código com React.lazy](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/dyi8m0yt6lje5cev6dv7.png)

Resultado:

![Resultado no navegador](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/udehn5nfq9kxtq055yf4.gif)

Note que no primeiro clique no botão, apareceu "loading...", que é o componente
definido no fallback.

Build:

![Imagem do build](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/vmrqapbfiaibdpk23t6e.png)

Houve uma **redução ainda maior** do que com os Dynamic Imports do Next.js.
Porém, há um **componente de loading adicional**, o que pode impactar na
experiência do usuário (UX).

Por isso, **essa abordagem deve ser alinhada com o time de design e produto** —
pois exibir um loading pode não ser uma boa ideia em alguns casos. É
recomendável usar apenas quando o componente for **realmente pesado** ou a
página estiver **muito lenta**.

# 3. React-Lazyload

O `react-lazyload` funciona de forma um pouco diferente. Ele **não afeta
diretamente o carregamento inicial** da página, mas sim monitora **a posição dos
elementos** em relação ao viewport.

Quando um elemento estiver **próximo da tela**, ele será renderizado.

Ou seja, podemos usá-lo para renderizar **componentes pesados à medida que o
usuário rola a página**.

Exemplo:

![Código com react-lazyload](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/sbeoxao9npd352j2anyz.png)

Esse código gera 15 imagens. Imagine como seria pesado carregar todas de uma vez
só? Com o Lazyload, as imagens são carregadas **aos poucos**, conforme o usuário
rola a página.

Resultado:

![Resultado no navegador](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/xmex10qd2o3008sh9lw0.gif)

Na aba “Network” do navegador, vemos que as imagens são carregadas **à medida
que são exibidas** na tela.

Isso traz um **grande ganho de performance**, garantindo que a internet do
usuário não fique sobrecarregada.

# Conclusão

Vimos práticas valiosas para melhorar a performance da sua aplicação usando Lazy
Loading com Next.js e React. Aprendemos que é possível **carregar componentes,
imagens e iframes apenas quando necessário**, reduzindo consumo de recursos e
acelerando o carregamento das páginas.

Espero que as explicações tenham sido claras. Qualquer dúvida, é só me chamar
para conversar.

**Fique com Deus e bons estudos!**

[Caso queira, explore também seção de Design Patterns.](../Design%20Patterns/1-Compound%20Components.md)

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>
