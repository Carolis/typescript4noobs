# Tipos primitivos

Primitivos são os tipos básicos da linguagem — os blocos de construção antes de objetos, arrays e tipos customizados.

## Minúsculo, não maiúsculo

Para primitivos, use sempre **letra minúscula**: `string`, `number`, `boolean`.

`String`, `Number` e `Boolean` (maiúsculos) são os tipos *wrapper* de objeto do JavaScript — outra coisa:

```ts
let nome: string = "Ana";  // ✓ primitivo
let errado: String = "Ana"; // ⚠️ evite — wrapper, não primitivo
```

Sempre com letra minúscula — `String` (maiúsculo) é outra coisa, e o ESLint avisa se você usar sem querer. Quem vem de Java ou copia exemplos antigos cai nessa pegadinha com frequência.

## string

Texto. Aspas simples, duplas ou template literals:

```ts
let nome: string = "Ana";
let saudacao: string = `Olá, ${nome}`;
```

## number

Números inteiros, decimais, hex, binário, octal:

```ts
let idade: number = 25;
let preco: number = 19.99;
let hex: number = 0xf00d;
```

## boolean

Só `true` ou `false`:

```ts
let ativo: boolean = false;
```

## bigint

Para inteiros muito grandes (além do limite seguro de `number`):

```ts
let grande: bigint = 100n;
```

## symbol

Identificador único — aparece menos no dia a dia, mas existe:

```ts
const chave: symbol = Symbol("id");
```

## null e undefined

Representam ausência de valor. No JavaScript puro, você pode jogar `null` ou `undefined` em qualquer variável. Com `strict` no `tsconfig`, isso muda:

```ts
let nome: string = "Ana";
nome = null; // ❌ erro com strict ligado — string não aceita null

let vazio: null = null;
let indefinido: undefined = undefined;
```

Na aula de [null e optional](./09-null-undefined-optional.md) você vê como lidar com valores que podem faltar — `?`, `?.`, `??` e afins.

## Resumo rápido

| Tipo | Exemplo | Uso comum |
|---|---|---|
| **`string`** | `"texto"` | nomes, emails, mensagens |
| **`number`** | `42`, `3.14` | idade, preço, contagem |
| **`boolean`** | `true` / `false` | flags, condições |
| `bigint` | `100n` | inteiros enormes |
| `symbol` | `Symbol()` | chaves únicas |
| `null` | `null` | valor vazio intencional |
| `undefined` | `undefined` | ausência de valor |

Na maioria dos projetos, **`string`**, **`number`** e **`boolean`** cobrem quase tudo no começo.

---

[← Anotações de tipo](./01-anotacoes-de-tipo.md) · [Menu](../../README.md#roadmap) · [Próximo: Arrays e tuplas →](./03-arrays-e-tuplas.md)
