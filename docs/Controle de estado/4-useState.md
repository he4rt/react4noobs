<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

## useState

O `useState` é um Hook do React que permite adicionar **estado** a componentes funcionais.

Ele retorna um array com duas posições:
- o **valor atual do estado**
- uma **função para atualizar esse estado**

---

### Como se lê a sintaxe?

```
 const [estado, setEstado] = useState(valorInicial);
```


*estado*: valor atual do estado (por exemplo: count, nome, loading).

*setEstado*: função que você chama pra atualizar esse valor e disparar a re-renderização (por exemplo setCount, setName, etc).

Aqui o useState(valorInicial) é chamado apenas *na primeira renderização*; nas próximas, ele retorna o valor atual do estado.

---

### Exemplo simples

```
import { useState } from "react";

function Contador() {
  const [contador, setContador] = useState(0);

  return (
    <div>
      <p>Valor: {contador}</p>
      <button onClick={() => setContador(contador + 1)}>
        Incrementar
      </button>
    </div>
  );
}

export default Contador;


```

Nesse exemplo, o estado **contador** começa com valor **0** e é atualizado sempre que o botão é clicado.


---

### Erros comuns

- Esquecer de importar o *useState*
- Tentar alterar o estado diretamente (estado = novoValor)
- Esperar que o estado seja atualizado imediatamente


---

## Conclusão

O *useState* é um dos Hooks mais importantes do React e geralmente é o primeiro contato de quem está começando com gerenciamento de estado em componentes funcionais.


[Documentação Oficial do useState](https://react.dev/reference/react/useState)


Achou algo de errado? Algo que possa melhorar? Fique a vontade para [abrir uma issue](https://github.com/he4rt/react4noobs/issues). Vejo você na próxima seção!

[Ir para Próxima Seção](../Estilizacao/1.Preprocessadores%20CSS.md)

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>