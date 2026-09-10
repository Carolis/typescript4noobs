# Exercícios

Fixe o que você viu neste módulo. Teste no [playground](https://www.typescriptlang.org/play) ou num projeto local.

## 1. Enum de status

Crie um enum `StatusPedido` com `Pendente`, `Pago` e `Cancelado`. Depois reescreva o mesmo enum usando `as const` + `keyof typeof`. Qual das duas versões você prefere, e por quê?

## 2. Narrowing de union

Escreva uma função que recebe `string | number | boolean` e retorna uma descrição diferente para cada tipo, usando `typeof` para estreitar.

## 3. Generic de lista

Crie uma função `ultimo<T>(lista: T[]): T` que devolve o último item de qualquer array. Teste com um array de `number` e um de `string`, e confira que o tipo de retorno muda de acordo.

## 4. Tipos utilitários num cadastro

Dada:

```ts
interface Usuario {
  id: number;
  nome: string;
  email: string;
  senha: string;
}
```

Crie três tipos: um para atualização parcial de cadastro (`Partial`), um para devolver ao cliente sem expor a senha (`Omit`), e um só com `id` e `nome` para listagens resumidas (`Pick`).

## 5. keyof e indexed access

Para a mesma `interface Usuario` do exercício 4, crie `type ChaveUsuario = keyof Usuario` e uma função `pegarCampo` que devolve o valor daquele campo, com o tipo correto no retorno — por exemplo, `pegarCampo(usuario, "nome")` precisa ter tipo `string`, não a union de todos os campos de `Usuario` (dica: `chave: ChaveUsuario` sozinho não preserva o tipo específico de cada chave; você vai precisar combinar com um generic, como na aula de [Generics](./03-generics.md)).

## 6. Classe com encapsulamento

Crie uma classe `CarrinhoDeCompras` com uma lista `private` de itens (`string[]`), um método público `adicionar(item: string): void` e um método `total(): number` que devolve a quantidade de itens. Ninguém de fora da classe deve poder alterar a lista diretamente.

## 7. Separar em módulos

Pegue a classe do exercício 6 e separe em dois arquivos: `carrinho.ts` (exporta a classe) e `main.ts` (importa e usa). Use `export default` num dos dois arquivos e export nomeado no outro.

---

Quando terminar, siga para o módulo **[Avançado](../05-avancado/01-conditional-types.md)** (conditional types, mapped types, template literal types e mais).

---

[← Módulos](./07-modulos.md) · [Menu](../../README.md#roadmap) · [Próximo: Conditional types →](../05-avancado/01-conditional-types.md)
