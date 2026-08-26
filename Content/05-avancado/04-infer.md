# infer

`infer` só existe dentro de um conditional type — é a forma de capturar um pedaço do tipo que está sendo comparado, em vez de só aprovar ou rejeitar ele.

## Reimplementando ReturnType

A aula de [Tipos utilitários](../04-intermediario/04-tipos-utilitarios.md) usou `ReturnType<T>` como uma caixa-preta. Por dentro, é só um conditional type com `infer`:

```ts
type MeuReturnType<T extends (...args: any[]) => any> =
  T extends (...args: any[]) => infer R ? R : any;

function buscarProduto() {
  return { id: 1, nome: "Caneca" };
}

type Produto = MeuReturnType<typeof buscarProduto>; // { id: number; nome: string }
```

`infer R` declara uma variável de tipo nova: "seja lá o que estiver na posição de retorno dessa função, chame de `R`". O TypeScript resolve `R` sozinho, comparando `T` contra o formato de função à direita do `extends`.

## Reimplementando Parameters

O mesmo truque funciona para os parâmetros, só mudando onde o `infer` aparece:

```ts
type MeusParametros<T extends (...args: any) => any> =
  T extends (...args: infer P) => any ? P : never;

function criarProduto(nome: string, preco: number) {
  // ...
}

type ParametrosCriar = MeusParametros<typeof criarProduto>; // [string, number]
```

```ts
type Invalido = MeuReturnType<string>;
// ❌ Type 'string' does not satisfy the constraint '(...args: any[]) => any'.
```

O erro acontece antes mesmo de o conditional type rodar: `string` não bate com a restrição `extends (...args: any[]) => any` do generic, então o TypeScript nem chega a testar o `infer`.

## infer fora de funções

`infer` funciona em qualquer posição de um tipo, não só no retorno de função — por exemplo, para extrair o tipo de elemento de um array:

```ts
type ElementoDe<T> = T extends (infer U)[] ? U : T;

type A = ElementoDe<string[]>; // string
type B = ElementoDe<number>;   // number — não é array, cai no 'else'
```

---

Conditional types, mapped types e infer resolvem problemas de generalizar e extrair tipos. A próxima aula ataca um problema mais comum no dia a dia: validar um objeto contra um formato sem perder o tipo específico de cada valor.

---

[← Template literal types](./03-template-literal-types.md) · [Menu](../../README.md#roadmap) · [Próximo: satisfies →](./05-satisfies.md)
