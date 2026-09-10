# Generics

Às vezes uma função precisa funcionar com qualquer tipo de dado, mas sem perder a informação de qual tipo é. `any` resolve a primeira parte e destrói a segunda:

```ts
function primeiro(lista: any): any {
  return lista[0];
}

const x = primeiro([1, 2, 3]);
x.toUpperCase(); // ok pro compilador, quebra em runtime — 'any' apagou o tipo do array
```

Generics resolvem isso com uma variável de tipo (`T`, por convenção) que o compilador preenche a cada chamada:

```ts
function primeiro<T>(lista: T[]): T {
  return lista[0];
}

const numero = primeiro([1, 2, 3]); // T vira number
const texto = primeiro(["a", "b"]); // T vira string

numero.toUpperCase(); // ❌ number não tem toUpperCase — o tipo real foi preservado
```

`T` funciona como um "molde": você não fixa o tipo na definição da função, mas o compilador sabe exatamente qual foi usado em cada chamada.

## Mais de um parâmetro de tipo

```ts
function par<A, B>(a: A, b: B): [A, B] {
  return [a, b];
}

par(1, "um"); // [number, string]
```

## Generics em type e interface

```ts
interface Caixa<T> {
  conteudo: T;
}

const caixaDeNumero: Caixa<number> = { conteudo: 42 };
const caixaDeTexto: Caixa<string> = { conteudo: "oi" };

const invalida: Caixa<number> = { conteudo: "oi" }; // ❌ 'oi' não é number
```

## Constraints com extends

Às vezes o generic precisa aceitar "qualquer tipo, desde que tenha certa propriedade". `extends` limita isso:

```ts
function tamanho<T extends { length: number }>(valor: T): number {
  return valor.length;
}

tamanho("texto");    // ok — string tem length
tamanho([1, 2, 3]);  // ok — array tem length
tamanho(42);         // ❌ number não tem length
```

`{ length: number }` é uma restrição por formato, não por tipo nomeado: `T` pode ser qualquer coisa que tenha essa propriedade — `string`, `array`, ou até um objeto seu como `{ length: number, outraCoisa: boolean }`. É por isso que `tamanho([1, 2, 3])` funciona sem `T` nunca ter sido declarado como "array": array já nasce com `length: number`.

Combinado com `keyof`, generics ficam ainda mais precisos — por exemplo `function pega<T, K extends keyof T>(obj: T, chave: K): T[K]`, que restringe `chave` às chaves reais de `obj`. Veremos isso na aula de [keyof, typeof e indexed access](./05-keyof-typeof-e-indexed-access.md).

## Valor default do generic

```ts
interface Resposta<T = string> {
  status: number;
  corpo: T;
}

const r1: Resposta = { status: 200, corpo: "ok" };          // T vira string, o default
const r2: Resposta<number[]> = { status: 200, corpo: [1, 2] };
```

## Onde isso aparece na prática

Bibliotecas de HTTP como o Axios usam generics para tipar a resposta de uma chamada sem precisar de um método diferente para cada formato de dado:

```ts
import axios from "axios";

interface Usuario {
  id: number;
  email: string;
}

async function buscarUsuarios() {
  const resposta = await axios.get<Usuario[]>("/usuarios");
  resposta.data; // Usuario[], não any
}
```

O `await` precisa estar dentro de uma função `async` (ou em top-level de um módulo ESM) — aqui ele está dentro de `buscarUsuarios` de propósito, para o exemplo funcionar direto se você copiar. O mesmo método `get` serve para buscar `Usuario[]`, `number[]` ou qualquer outro formato — quem muda é o generic passado em cada chamada.

---

[← Narrowing](./02-narrowing.md) · [Menu](../../README.md#roadmap) · [Próximo: Tipos utilitários →](./04-tipos-utilitarios.md)
