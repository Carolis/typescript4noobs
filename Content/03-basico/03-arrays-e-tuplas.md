# Arrays e tuplas

## Arrays

Lista de valores do **mesmo tipo**. Duas formas equivalentes de escrever:

```ts
let numeros: number[] = [1, 2, 3];
let frutas: Array<string> = ["maçã", "laranja"];
```

A primeira (`number[]`) é a mais comum. A segunda usa a sintaxe genérica — você verá mais dela no módulo Intermediário.

Colocar um tipo errado no array gera erro:

```ts
let ids: number[] = [1, 2, "três"]; // ❌ string não entra em number[]
```

## Array vazio

Se começar vazio, o TypeScript precisa saber o tipo:

```ts
let lista: number[] = [];
lista.push(1); // ok
lista.push("dois"); // ❌ erro
```

## Tuplas

Tupla é um array com **posições fixas** e tipos definidos para cada uma:

```ts
let par: [string, number] = ["idade", 25];

par[0]; // string
par[1]; // number
```

Útil quando a ordem importa — coordenada `[x, y]`, par `[chave, valor]`, retorno `[dados, erro]`.

Tupla com tamanho errado ou tipo errado na posição:

```ts
let errado: [string, number] = ["só string"]; // ❌ falta o number
```

## Quando usar cada um

- **Array** — lista de itens do mesmo tipo (usuários, produtos, tags)
- **Tupla** — conjunto fixo com tipos diferentes por posição

---

[← Tipos primitivos](./02-tipos-primitivos.md) · [Menu](../../README.md#roadmap) · [Próximo: Funções →](./04-funcoes.md)
