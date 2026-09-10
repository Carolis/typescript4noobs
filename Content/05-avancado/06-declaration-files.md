# Declaration files

Nem toda biblioteca JavaScript vem com tipos. Um arquivo `.d.ts` descreve o formato de algo — módulo, variável global, biblioteca externa — sem conter nenhuma implementação, só as assinaturas.

## Bibliotecas sem tipos

```ts
import { formatar } from "biblioteca-sem-tipos";
// ❌ Could not find a declaration file for module 'biblioteca-sem-tipos'.
```

Sem um `.d.ts` em algum lugar descrevendo esse módulo, o TypeScript não sabe o formato de `formatar` — e sem `strict`/`noImplicitAny`, ele viraria silenciosamente `any`. Criar o arquivo resolve:

```ts
// biblioteca-sem-tipos.d.ts
declare module "biblioteca-sem-tipos" {
  export function formatar(valor: string): string;
}
```

```ts
import { formatar } from "biblioteca-sem-tipos";

formatar("oi");  // ok
formatar(42);    // ❌ Argument of type 'number' is not assignable to parameter of type 'string'.
```

## @types e o DefinitelyTyped

Escrever um `.d.ts` à mão só é necessário quando ninguém já fez isso. Para a maioria das bibliotecas populares sem tipos embutidos, existe um pacote `@types/nome-da-lib` mantido pela comunidade no projeto DefinitelyTyped — por exemplo, `@types/lodash` para o `lodash`. Instalando o pacote (`npm install -D @types/lodash`), o TypeScript encontra os tipos sozinho em `node_modules/@types`, sem nenhuma configuração extra.

## declare module para outros formatos de arquivo

O mesmo `declare module` tipa importações que nem são JavaScript — como um `.svg` importado direto num projeto com bundler (Vite, webpack):

```ts
// arquivos.d.ts
declare module "*.svg" {
  const conteudo: string;
  export default conteudo;
}
```

```ts
import logo from "./logo.svg"; // ok — sem essa declaração, o TS não sabe o que é um '.svg'
```

## declare global

Para adicionar algo ao escopo global — como uma propriedade customizada em `window` — `declare global` funciona dentro de qualquer arquivo que já seja um módulo (com `import` ou `export`), inclusive um `.d.ts`. Um `export {}` vazio, como na aula de [Módulos](../04-intermediario/07-modulos.md), força esse contexto quando não há nenhum import/export real:

```ts
export {};

declare global {
  interface Window {
    minhaFlagCustomizada: boolean;
  }
}

window.minhaFlagCustomizada = true; // ok — o TS agora conhece essa propriedade
```

---

Isso fecha as ferramentas de tipo mais avançadas do TypeScript. Hora de praticar tudo o que o módulo cobriu.

---

[← satisfies](./05-satisfies.md) · [Menu](../../README.md#roadmap) · [Próximo: Exercícios →](./07-exercicios.md)
