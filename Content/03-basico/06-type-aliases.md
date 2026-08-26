# Type aliases

`type` cria um **apelido** para um tipo. Em vez de repetir a mesma estrutura em vários lugares, você define uma vez e reutiliza.

## Apelido para primitivo

```ts
type Idade = number;
type Nome = string;

let idade: Idade = 25;
```

Útil quando o mesmo conceito aparece em muitos pontos — ou quando você quer deixar a intenção clara no código.

## Apelido para objeto

```ts
type Triangulo = {
  lado1: number;
  lado2: number;
  lado3: number;
};

const t: Triangulo = { lado1: 3, lado2: 4, lado3: 5 };
```

Se faltar um lado ou vier string no lugar de number, o compilador avisa.

## Um type dentro do outro

Você pode **compor** types — definir um e usá-lo dentro de outro:

```ts
type Endereco = {
  rua: string;
  numero: number;
};

type Usuario = {
  nome: string;
  idade?: number;
  endereco: Endereco;
};

const usuario: Usuario = {
  nome: "Diego",
  endereco: {
    rua: "Rua A",
    numero: 100,
  },
};
```

Repare no `idade?`: o `?` torna a propriedade **opcional**. Como `usuario` é uma constante e `idade` não foi informado, **não dá erro** — opcional significa que pode faltar.

Se `idade` existir, tem que ser `number`:

```ts
const invalido: Usuario = {
  nome: "Diego",
  idade: "trinta", // ❌ string não é number
  endereco: { rua: "Rua A", numero: 100 },
};
```

## Union — mais de um tipo possível

Quando um valor pode ser de tipos diferentes:

```ts
type Id = string | number;

let id1: Id = "abc-123";
let id2: Id = 42;
let id3: Id = true; // ❌ boolean não entra
```

Union fica ainda mais poderosa com objetos — por exemplo, um resultado de sucesso ou erro:

```ts
type Resultado =
  | { sucesso: true; dado: string }
  | { sucesso: false; erro: string };
```

Esse padrão (discriminated union) aparece o tempo todo na prática — aprofundamos em conteúdo mais avançado.

## Literal — valor fixo

Restringe a valores específicos:

```ts
type Resposta = "sim" | "não";

let r: Resposta = "sim";     // ok
let r2: Resposta = "talvez"; // ❌
```

Útil para status, direções, opções de menu — qualquer coisa com conjunto fechado de valores.

## Função no type

```ts
type Operacao = (a: number, b: number) => number;

const soma: Operacao = (a, b) => a + b;
const errado: Operacao = (a: string, b: number) => a + b; // ❌ tipo do parâmetro
```

---

[← Objetos](./05-objetos.md) · [Menu](../../README.md#roadmap) · [Próximo: Interfaces →](./07-interfaces.md)
