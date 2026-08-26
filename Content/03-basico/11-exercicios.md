# Exercícios

Fixe o que você viu neste módulo. Teste no [playground](https://www.typescriptlang.org/play) ou num projeto local.

## 1. Tipar a função

Em JavaScript:

```js
function desconto(preco, percentual) {
  return preco - (preco * percentual) / 100;
}
```

Converta para TypeScript com tipos nos parâmetros e no retorno. O que acontece se passar `"100"` em vez de `100`?

## 2. Objeto de usuário

Crie um `type User` com:

- `name: string`
- `email: string`
- `age?: number` (opcional)

Crie dois objetos válidos: um com `age`, outro sem. Tente passar `age` como string e veja o erro.

## 3. Endereço aninhado

Crie `type Address` e use dentro de `type User` (como na aula de type aliases). `Address` deve ter `street: string` e `number: number`.

## 4. Interface vs type

Reescreva o `User` do exercício 2 como `interface`. Crie `interface Admin extends User` com `role: string`.

## 5. Optional chaining

Dado o objeto:

```ts
const pedido = {
  id: 1,
  cliente: {
    nome: "Ana",
  },
};
```

Acesse com segurança:

- o nome do cliente
- um campo `telefone` que não existe em `cliente`
- `pedido.endereco.cidade` quando `endereco` não existe

Use `?.` e `??` onde fizer sentido.

## 6. Evitar any

Esta função usa `any`:

```ts
function dobrar(valor: any) {
  return valor * 2;
}
```

Troque `any` por um tipo que aceite só números. O que muda se alguém chamar `dobrar("2")`?

---

Quando terminar, siga para o módulo **[Intermediário](../04-intermediario/01-enums-e-as-const.md)** (enums, generics, tipos utilitários).

---

[← any, unknown, never e void](./10-any-unknown-never-void.md) · [Menu](../../README.md#roadmap) · [Próximo: Enums e as const →](../04-intermediario/01-enums-e-as-const.md)
