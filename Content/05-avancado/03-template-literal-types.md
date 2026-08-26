# Template literal types

Template literal types criam tipos string literal combinando texto fixo com outro tipo, com a mesma sintaxe de um template string do JavaScript — só que rodando em tipos, não em valores.

## Sintaxe básica

```ts
type Evento = "click" | "hover" | "focus";

type NomeDoHandler = `on${Capitalize<Evento>}`;
// "onClick" | "onHover" | "onFocus"
```

`Capitalize` é outro utilitário embutido (junto de `Uncapitalize`, `Uppercase` e `Lowercase`) que transforma cada string literal de uma union. Como `Evento` entra "nu" dentro do template, o resultado distribui sobre a union — mesmo comportamento visto na aula de [Conditional types](./01-conditional-types.md).

## Combinando com key remapping

A cláusula `as` de um mapped type, vista na aula passada, costuma usar um template literal type para montar a nova chave:

```ts
type Handlers = {
  [E in Evento as `on${Capitalize<E>}`]: () => void;
};
// { onClick: () => void; onHover: () => void; onFocus: () => void }

const handlers: Handlers = {
  onClick: () => console.log("clicou"),
  onHover: () => console.log("passou o mouse"),
  onFocus: () => console.log("focou"),
};

const invalido: Handlers = {
  onClick: () => {},
  onHover: () => {},
  onFocus: () => {},
  onDblClick: () => {}, // ❌ 'onDblClick' não existe em Handlers
};
```

## Outros usos comuns

Rotas de API, chaves de CSS-in-JS, nomes de variável de ambiente — qualquer conjunto fechado de strings com um padrão fixo se beneficia:

```ts
type Recurso = "usuarios" | "produtos" | "pedidos";
type RotaApi = `/api/${Recurso}`;
// "/api/usuarios" | "/api/produtos" | "/api/pedidos"

function buscar(rota: RotaApi) {
  // ...
}

buscar("/api/usuarios");   // ok
buscar("/api/categorias"); // ❌ "/api/categorias" não é uma das rotas da union RotaApi
```

---

Template literal types e conditional types, juntos, abrem espaço pra extrair um pedaço específico de dentro de um tipo maior — é isso que a palavra `infer` faz, na próxima aula.

---

[← Mapped types](./02-mapped-types.md) · [Menu](../../README.md#roadmap) · [Próximo: infer →](./04-infer.md)
