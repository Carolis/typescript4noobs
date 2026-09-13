# null, undefined e optional

JavaScript trata `null` e `undefined` de forma solta. Com `strict` no `tsconfig`, o TypeScript passa a cobrar — e isso evita boa parte dos bugs clássicos.

## Propriedade opcional vs valor ausente

**Opcional (**`?`**)** — a propriedade pode **não existir** no objeto:

```ts
type User = {
  name: string;
  age?: number;
};

const a: User = { name: "Diego" };           // ok
const b: User = { name: "Diego", age: 30 };  // ok
```

`undefined` **explícito** — a propriedade existe, mas sem valor:

```ts
const c: User = { name: "Diego", age: undefined }; // ok com strictNullChecks
```



## Optional chaining (`?.`)

`?.` acessa uma propriedade **sem estourar erro em runtime** se o valor no caminho for `null` ou `undefined`. Importante: isso vale para propriedades **declaradas no tipo** — `?.` lida com "pode não ter valor", não com "essa propriedade nem existe no tipo".

```ts
type Pessoa = {
  firstName: string;
  animals?: { dog: string; cat?: string };
  company?: { name: string };
};

const person: Pessoa = {
  firstName: "Marcio",
  animals: { dog: "Eros" },
};

const dogName = person.animals?.dog;   // "Eros" — animals pode não existir
const catName = person.animals?.cat;   // undefined — cat é opcional, não quebra
const company = person.company?.name;  // undefined — company é opcional, não quebra
```

Se a propriedade **não está no tipo**, o TypeScript acusa erro na compilação — `?.` não esconde isso:

```ts
const errado = person.animals?.bird; // ❌ 'bird' não existe no tipo
```

Sem `?.`, se `animals` for `undefined` em runtime, `person.animals.dog` lançaria erro. Com `?.`, o resultado é `undefined` e o programa continua.

Funciona em cadeia:

```ts
type Usuario = {
  endereco?: { cidade?: string };
};

const usuario: Usuario = {};
const cidade = usuario?.endereco?.cidade; // undefined — ok, sem quebrar
```



## Nullish coalescing (`??`)

Define um valor padrão quando o lado esquerdo é `null` ou `undefined`:

```ts
const nome = usuario.nickname ?? usuario.name ?? "Anônimo";
```

Diferente de `||`, que trata `0` e `""` como falsy:

```ts
const contagem = valor ?? 0;   // usa 0 só se valor for null/undefined
const contagem2 = valor || 0;  // usa 0 também se valor for 0 ou ""
```



## strictNullChecks

Com `strict: true`, o TypeScript não deixa você usar `null`/`undefined` onde se espera `string` ou `number` sem tratar antes:

```ts
function tamanho(texto: string) {
  return texto.length;
}

let valor: string | undefined = buscarTexto();
tamanho(valor); // ❌ undefined não é string

if (valor !== undefined) {
  tamanho(valor); // ok — estreitou o tipo
}
```

Esse "estreitar" o tipo antes de usar é **narrowing** — tema do módulo Intermediário.

---

[← type vs interface](./08-type-vs-interface.md) · [Menu](../../README.md#roadmap) · [Próximo: any, unknown, never e void →](./10-any-unknown-never-void.md)