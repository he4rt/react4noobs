<p align="center">
<a href="https://github.com/he4rt/4noobs" target="_blank">
<img src="../../assets/global/header-4noobs.svg">
</a>
</p>

# O Que é Compound Components?

Compound Components é um padrão em React.
Tem como objetivo criar um design mais flexível compartilhando o estado e lógica entre um grupo de componentes, onde a comunicação entre o componente pai e os componentes filhos devem ser feitas de maneira flexível. Os componentes devem trabalhar juntos para realizarem algum comportamento sem criar árvores de props embaraçosas ou uma lógica complexa demais para ser refatorado ou compreendido futuramente.

Esse padrão nos ajuda a eliminar inflamações de props, onde temos que passar uma árvore de props entre os componentes. Essa inflamação é um problema, porque pode causar vários re-renders desnecessários a cada estado que for atualizado, já que cada estado irá atualizar todos os componentes filho.

Temos um exemplo de Compound Components na estrutura do `select` e `option` das tags em HTML:

```
<select>
  <option value="Danielhe4rt">Danielhe4rt</option>
  <option value="Gabriel">Gabriel</option>
  <option value="Marcelo">Marcelo</option>
</select>
```

<select>
  <option value="Danielhe4rt">Danielhe4rt</option>
  <option value="Gabriel">Gabriel</option>
  <option value="Marcelo">Marcelo</option>
</select>

<br/>

O `select` funciona como um gerenciador de estados da inferface, enquanto o `option` são configurados em como o `select` deve funcionar.
