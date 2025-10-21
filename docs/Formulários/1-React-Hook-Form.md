<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/header-4noobs.svg">
  </a>
</p>

# Formulários – React Hook Form

## O que é o React Hook Form?

O **React Hook Form (RHF)** é uma biblioteca leve e performática para manipulação de formulários em aplicações **React**.
Seu principal objetivo é simplificar a criação, validação e submissão de formulários, reduzindo a necessidade de *boilerplate* e melhorando a performance através do uso dos **React Hooks**.

Ao invés de controlar cada campo de formulário através de *states* e *handlers* (como em `onChange` e [`useState`](../Iniciando%20com%20React/8.1-useState.md)), o React Hook Form utiliza **referências diretas ([refs](../Iniciando%20com%20React/Refs.md))** para registrar e monitorar os campos, tornando o código mais limpo e eficiente.

---

## Por que usar o React Hook Form?

Criar formulários no React sem uma biblioteca pode rapidamente se tornar algo verboso e repetitivo.
Veja algumas vantagens do RHF:

* ✅ **Performance:** reduz renderizações desnecessárias;
* ✅ **Validação integrada:** suporte nativo a validações síncronas e assíncronas;
* ✅ **Integração fácil:** funciona com *Yup*, *Zod* e outros validadores;
* ✅ **Menos código:** elimina a necessidade de `onChange` e `setState`;
* ✅ **Controle fino:** acesso direto ao estado do formulário (erros, valores, *dirty*, *touched* etc).

---

## Instalação

Para começar, basta instalar a biblioteca:

```bash
npm install react-hook-form
# ou
yarn add react-hook-form
```

---

## Criando o primeiro formulário

Vamos criar um exemplo simples de formulário de login com os campos **email** e **senha**.

```jsx
import React from "react";
import { useForm } from "react-hook-form";

export function LoginForm() {
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm();

  const onSubmit = (data) => {
    console.log("Dados enviados:", data);
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <div>
        <label>Email:</label>
        <input
          type="email"
          {...register("email", { required: "O e-mail é obrigatório" })}
        />
        {errors.email && <span>{errors.email.message}</span>}
      </div>

      <div>
        <label>Senha:</label>
        <input
          type="password"
          {...register("password", { required: "A senha é obrigatória" })}
        />
        {errors.password && <span>{errors.password.message}</span>}
      </div>

      <button type="submit">Entrar</button>
    </form>
  );
}
```

### O que está acontecendo aqui?

* **`useForm()`** inicializa o controle do formulário.
* **`register()`** conecta os campos ao RHF.
* **`handleSubmit()`** lida com o evento `onSubmit` e fornece os dados validados.
* **`formState.errors`** exibe mensagens de erro automaticamente.

---

## Validação com *Yup*

Podemos integrar o React Hook Form com o *Yup* para validações mais robustas e reutilizáveis.

```bash
npm install @hookform/resolvers yup
```

```jsx
import React from "react";
import { useForm } from "react-hook-form";
import { yupResolver } from "@hookform/resolvers/yup";
import * as yup from "yup";

const schema = yup.object({
  email: yup.string().email("E-mail inválido").required("Campo obrigatório"),
  password: yup
    .string()
    .min(6, "Mínimo de 6 caracteres")
    .required("Campo obrigatório"),
});

export function LoginFormYup() {
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm({
    resolver: yupResolver(schema),
  });

  const onSubmit = (data) => console.log(data);

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input placeholder="Email" {...register("email")} />
      <p>{errors.email?.message}</p>

      <input placeholder="Senha" type="password" {...register("password")} />
      <p>{errors.password?.message}</p>

      <button type="submit">Enviar</button>
    </form>
  );
}
```

Agora as validações são controladas pelo *Yup*, e o formulário só é submetido se todos os campos forem válidos.

---

## Controle de estado e reset

O RHF fornece métodos úteis como `reset`, `watch` e `setValue` para lidar com o estado dos campos.

```jsx
const { register, handleSubmit, reset, watch } = useForm();

const onSubmit = (data) => {
  console.log(data);
  reset(); // limpa o formulário após o envio
};

const emailValue = watch("email"); // observa o valor em tempo real
```

Essas funções permitem criar formulários dinâmicos com comportamento avançado.

---

## Integração com componentes externos

O React Hook Form também permite integrar com bibliotecas de UI como **Ant Design**, **Material UI** ou **Chakra UI** utilizando o componente `Controller`.

```jsx
import { Controller, useForm } from "react-hook-form";
import { Input } from "antd";

export function ControlledInputExample() {
  const { control, handleSubmit } = useForm();

  const onSubmit = (data) => console.log(data);

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <Controller
        name="username"
        control={control}
        defaultValue=""
        render={({ field }) => <Input {...field} placeholder="Nome de usuário" />}
      />
      <button type="submit">Enviar</button>
    </form>
  );
}
```

---

## Boas práticas

* Sempre defina mensagens de erro personalizadas.
* Use *defaultValues* para inicializar o formulário.
* Evite [`useState`](../Iniciando%20com%20React/8.1-useState.md) para controlar campos — o RHF já faz isso internamente.
* Prefira `Controller` apenas para componentes externos controlados.
* Valide com bibliotecas externas apenas quando necessário.

---

## Links úteis

* [Documentação oficial](https://react-hook-form.com)
* [HookForm + Yup Integration](https://react-hook-form.com/get-started#SchemaValidation)
* [React Hook Form no GitHub](https://github.com/react-hook-form/react-hook-form)

---

<p align="center">Made with :purple_heart:</p>

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="../../assets/global/footer-4noobs.svg" width="380">
  </a>
</p>
  