# type vs interface

`type` e `interface` fazem coisas parecidas para objetos. Na prática, a maioria dos times usa os dois — saber **quando** cada um encaixa melhor evita confusão.

## O que os dois fazem igual

Descrever objetos, propriedades opcionais, métodos, `readonly`:

```ts
type UserType = { name: string; age?: number };
interface UserInterface { name: string; age?: number; }
```

Para esse caso, tanto faz.

## O que só o `type` faz

**Union** — valor pode ser um tipo ou outro:

```ts
type Id = string | number;
type Status = "ativo" | "inativo";
```

**Composição com `&`** — juntar dois types:

```ts
type A = { a: string };
type B = { b: number };
type C = A & B; // { a: string; b: number }
```

**Apelido para primitivo:**

```ts
type Idade = number;
```

Interface não aceita union de primitivos nem alias simples de `number`/`string` sozinhos:

```ts
interface Id = string | number; // ❌ nem compila — interface não usa '='
```

## O que só a `interface` faz

**extends** — herança explícita:

```ts
interface Animal { nome: string; }
interface Cachorro extends Animal { raca: string; }
```

Com `type`, o equivalente é interseção: `type Cachorro = Animal & { raca: string }`.

**Declaration merging** — duas declarações com o mesmo nome se fundem:

```ts
interface Config { debug: boolean; }
interface Config { port: number; }
// Config = { debug: boolean; port: number }
```

Útil em casos avançados (extender tipos de bibliotecas). Com `type`, redeclarar o mesmo nome dá erro:

```ts
type Config = { debug: boolean };
type Config = { port: number }; // ❌ Duplicate identifier 'Config'
```

## `extends` vs `&` — conflito de tipos

Na aula de [interfaces](./07-interfaces.md), vimos que `extends` com propriedades incompatíveis **quebra na hora**. Com `&`, o compilador deixa passar, mas a propriedade conflitante vira `never` — impossível de preencher:

```ts
interface X { valor: string; }
interface Y { valor: number; }
interface Z extends X, Y {} // ❌ conflito na hora do extends

type A = { valor: string };
type B = { valor: number };
type C = A & B; // valor vira 'string & number' → never
```

Pegadinha real: parece que compilou, mas nenhum valor satisfaz `C`.

## Regra prática

| Situação | Prefira |
|---|---|
| Formato de objeto (API, props, entidade) | `interface` |
| Union, literal, tipos compostos | `type` |
| Apelido para primitivo | `type` |
| Estender objeto de biblioteca | `interface` |
| Declaration merging (mesmo nome se soma) | `interface` |

Não existe resposta única certa — muitos projetos usam `interface` para objetos e `type` para o resto. O importante é ser **consistente** no time.

---

[← Interfaces](./07-interfaces.md) · [Menu](../../README.md#roadmap) · [Próximo: null, undefined e optional →](./09-null-undefined-optional.md)
