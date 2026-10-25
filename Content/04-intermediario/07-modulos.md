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

## Namespaces

Um `namespace` agrupa declarações relacionadas sob um nome. Você acessa seus membros com `NomeDoNamespace.membro`, evitando que cada nome ocupe diretamente o escopo global.

### Caso de uso: um script sem módulos

Imagine uma página antiga que carrega scripts sem `import`/`export`. Um namespace pode reunir os tipos e as funções de mensagens da página, reduzindo colisões com nomes de outros scripts:

```ts
namespace Mensagens {
  const saudacao = "Olá";

  export interface Usuario {
    nome: string;
  }

  export function boasVindas(usuario: Usuario): string {
    return `${saudacao}, ${usuario.nome}!`;
  }
}

const usuario: Mensagens.Usuario = { nome: "Ana" };

console.log(Mensagens.boasVindas(usuario)); // "Olá, Ana!"
```

O `export` **dentro** do namespace torna aquele membro acessível de fora, pelo nome do namespace. Ele não transforma o arquivo em um módulo. Sem `export`, a declaração fica acessível apenas dentro do bloco:

```ts
Mensagens.saudacao; // ❌ 'saudacao' não é exportada pelo namespace
```

A interface `Mensagens.Usuario` existe só durante a checagem de tipos. Já o namespace com a função `boasVindas` gera código JavaScript: neste exemplo, um objeto `Mensagens` com a função exportada. Compile o exemplo com TypeScript antes de executar o JavaScript; `namespace` não é sintaxe nativa do JavaScript.

### Namespace ou módulo?

Namespaces aparecem em projetos antigos e em arquivos de declaração de bibliotecas que expõem nomes globais. Para código novo, especialmente em React e Node.js, prefira os **módulos** com `import`/`export` apresentados nesta aula: cada arquivo já tem seu próprio escopo e declara suas dependências explicitamente.

Não é necessário envolver os exports de um módulo em um namespace. Se quiser acessar as funções de um módulo por um nome em comum, use `import * as`:

```ts
// main.ts — usando o matematica.ts do início da aula
import * as Matematica from "./matematica";

Matematica.somar(2, 3); // 5
```

Esse import agrupa os exports do módulo em `Matematica`; ele não declara um `namespace` do TypeScript.

Referências: [Namespaces](https://www.typescriptlang.org/docs/handbook/namespaces.html) e [Namespaces e módulos](https://www.typescriptlang.org/docs/handbook/namespaces-and-modules.html).

---

[← Classes](./06-classes.md) · [Menu](../../README.md#roadmap) · [Próximo: Exercícios →](./08-exercicios.md)
