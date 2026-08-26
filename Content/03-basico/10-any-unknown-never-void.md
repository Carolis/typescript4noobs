# any, unknown, never e void

Alguns tipos aparecem menos no dia a dia, mas vale saber o que cada um significa — e quando **evitar**.

## any — desliga a checagem

`any` aceita qualquer coisa. O compilador para de ajudar naquele ponto — como vimos na aula de [formas de tipagem](../01-introducao/02-formas-de-tipagem.md#typescript-estático-mas-gradual):

```ts
let a: any = "texto";
a = 10;               // ok, sem aviso
a.metodoQualquer();   // ok pro compilador — pode quebrar em runtime
```

Use só quando estiver migrando JS legado ou integrando algo sem tipos. Com `noImplicitAny` no `strict`, variável sem tipo inferível vira erro em vez de virar `any` silencioso.

## unknown — any com segurança

`unknown` também aceita qualquer valor, mas **obriga você a verificar** antes de usar. É a alternativa mais segura quando você não sabe o formato de entrada:

```ts
let u: unknown = buscarDado();
u.toUpperCase(); // ❌ precisa checar o tipo antes

if (typeof u === "string") {
  u.toUpperCase(); // ok — estreitou o tipo
}
```

### any vs unknown — o contraste direto

O mesmo código muda completamente de comportamento:

```ts
function processarAny(dado: any) {
  dado.toUpperCase(); // ok pro compilador — pode quebrar em runtime
}

function processarUnknown(dado: unknown) {
  dado.toUpperCase(); // ❌ 'dado' is of type 'unknown'

  if (typeof dado === "string") {
    dado.toUpperCase(); // ok — checou antes
  }
}
```

Prefira `unknown` a `any` quando a entrada for incerta — JSON de API, `localStorage`, dados de formulário.

## never — nunca retorna

Função que **nunca** termina normalmente — sempre lança erro ou entra em loop infinito:

```ts
function erro(msg: string): never {
  throw new Error(msg);
}
```

### Exaustividade em switch

O uso mais didático de `never` aparece em unions — garantindo que todos os casos foram tratados. Conecta com a [discriminated union](./06-type-aliases.md#union--mais-de-um-tipo-possível) da aula de type aliases:

```ts
type Status = "ativo" | "inativo";

function trata(s: Status) {
  switch (s) {
    case "ativo": return "ok";
    case "inativo": return "não ok";
    default:
      const _exhaustive: never = s; // se adicionar um novo Status, isso quebra aqui
      throw new Error("caso não tratado");
  }
}
```

Se amanhã `Status` ganhar `"pendente"`, o compilador aponta o `default` — você não esquece de tratar o caso novo.

## void — sem retorno útil

Função que não devolve valor para quem chama:

```ts
function log(msg: string): void {
  console.log(msg);
}
```

Não confunda com `undefined` — `void` diz "ignore o retorno", não "retorna undefined tipado".

## object — qualquer não-primitivo

`object` (minúsculo) aceita qualquer valor **não-primitivo**, mas não descreve formato nenhum:

```ts
let o: object = { x: 1 };
let o2: object = [1, 2];    // ok — array é object
o = "texto";                // ❌ string é primitivo, não entra em object
// o.x                     // ❌ object não garante propriedade x
```

Mesma pegadinha de `string` vs `String`: `Object` (maiúsculo) é o wrapper e aceita primitivos — evite:

```ts
let errado: Object = "texto"; // ⚠️ compila, mas não é o que você quer
```

Por isso a tabela diz "raramente" — na prática, descreva o formato com `type` ou `interface`.

## Resumo

| Tipo | Significado | Quando usar |
|---|---|---|
| `any` | qualquer coisa, sem checagem | evitar; migração legada |
| `unknown` | qualquer coisa, checar antes | entrada incerta |
| `never` | nunca retorna | erros, exaustividade em switch |
| `void` | sem retorno útil | funções side-effect |
| `object` | não-primitivo genérico | raramente; prefira type/interface |

---

[← null, undefined e optional](./09-null-undefined-optional.md) · [Menu](../../README.md#roadmap) · [Próximo: Exercícios →](./11-exercicios.md)
