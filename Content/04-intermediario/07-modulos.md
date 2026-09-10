# Módulos

Todo arquivo `.ts` que tem pelo menos um `import` ou `export` é tratado como um **módulo** — suas declarações ficam isoladas, ao contrário de um script solto onde tudo cai no escopo global.

## export nomeado

```ts
// matematica.ts
export function somar(a: number, b: number): number {
  return a + b;
}

export const PI = 3.14159;
```

```ts
// main.ts
import { somar, PI } from "./matematica";

somar(2, 3);
```

O nome usado no `import` precisa bater com o nome exportado (a não ser que você renomeie com `as`).

## export default

```ts
// calculadora.ts
export default class Calculadora {
  somar(a: number, b: number): number {
    return a + b;
  }
}
```

```ts
// main.ts
import Calculadora from "./calculadora";

const calc = new Calculadora();
```

Só existe **um** `export default` por arquivo, e quem importa pode dar qualquer nome a ele — diferente do export nomeado.

## export type — só o tipo, não o valor

```ts
// tipos.ts
export interface Usuario {
  id: number;
  nome: string;
}

export type Id = string | number;
```

```ts
import type { Usuario } from "./tipos";
// ou
import { type Usuario } from "./tipos";
```

`import type` deixa explícito que aquele import existe só em tempo de compilação — ele desaparece do JavaScript gerado, o que evita trazer código desnecessário para o bundle final só por causa de um tipo.

## Renomeando com as

```ts
import { somar as add } from "./matematica";

add(2, 3);
```

Útil para evitar colisão de nomes quando dois módulos exportam algo com o mesmo nome.

## Módulo vs script global

Um arquivo `.ts` sem nenhum `import`/`export` é tratado como **script global**: suas declarações (`interface`, `type`, `function`) ficam visíveis para todos os outros arquivos do projeto, sem precisar de import — o que pode causar colisão de nomes entre arquivos diferentes. Um `export {}` vazio no fim do arquivo força ele a virar módulo mesmo sem ter exports reais:

```ts
export {};
```

## Organização de arquivos

Uma convenção comum: um arquivo por responsabilidade (`tipos.ts`, `matematica.ts`, ...) e, quando a pasta cresce, um arquivo `index.ts` que reexporta tudo — o chamado *barrel file*:

```ts
// index.ts
export * from "./matematica";
export * from "./tipos";
```

Assim quem consome só importa da pasta (`import { somar } from "./utils"`), sem precisar saber em qual arquivo específico cada coisa está.

---

[← Classes](./06-classes.md) · [Menu](../../README.md#roadmap) · [Próximo: Exercícios →](./08-exercicios.md)
