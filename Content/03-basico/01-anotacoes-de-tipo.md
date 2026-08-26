# Anotações de tipo

A forma mais direta de usar TypeScript é colocar o tipo **depois** do nome — com `:tipo`.

```ts
let idade: number = 25;
let nome: string = "Ana";
let ativo: boolean = true;
```

O compilador passa a saber o que cada variável guarda. Se você tentar atribuir outro tipo, ele avisa na hora.

Vamos ver isso na prática com um exemplo completo: primeiro em JavaScript, depois em TypeScript.

## JavaScript: calcular a idade

```js
function calcularIdade(anoNascimento, anoAtual) {
  return anoAtual - anoNascimento;
}

const usuario = {
  nome: "Diego",
  anoNascimento: "1990",
};

console.log(calcularIdade(usuario.anoNascimento, 2026));
// NaN — "1990" é string, não número
```

O código roda sem erro. Só que o resultado é `NaN`, porque o JavaScript concatenou/subtraiu tipos errados sem avisar.

Outro problema comum: passar o objeto inteiro sem checar se os campos existem.

```js
function idadeDoUsuario(usuario) {
  return 2026 - usuario.anoQueNasceu; // undefined se o campo tiver outro nome
}
```

Bug silencioso de novo.

## TypeScript: o mesmo exemplo, tipado

Começamos pelos parâmetros da função:

```ts
function calcularIdade(anoNascimento: number, anoAtual: number): number {
  return anoAtual - anoNascimento;
}

calcularIdade(1990, 2026);     // 36 ✓
calcularIdade("1990", 2026);   // ❌ erro: string não é number
```

Com `: number` nos parâmetros, a concatenação acidental some. O retorno `: number` garante que a função devolve um número — se você retornar texto por engano, o compilador barra.

Tipando o objeto:

```ts
type Usuario = {
  nome: string;
  anoNascimento: number;
};

const usuario: Usuario = {
  nome: "Diego",
  anoNascimento: 1990,
};

function idadeDoUsuario(usuario: Usuario): number {
  const anoAtual = 2026;
  return anoAtual - usuario.anoNascimento;
}
```

Se você escrever `anoQueNasceu` em vez de `anoNascimento`, o TypeScript aponta na hora — typo de propriedade, aquele erro clássico do JavaScript.

## Inferência: nem tudo precisa de anotação

Quando você inicializa a variável, o TypeScript **infere** o tipo:

```ts
let contador = 0;        // number
const mensagem = "oi";   // tipo: "oi" (literal — só aceita esse valor)
let saudacao = "oi";     // string (genérico — aceita qualquer texto)
```

Com `const`, o TypeScript estreita para o valor exato — o tipo literal `"oi"`, não `string`. Com `let`, ele generaliza para `string`, porque o valor pode mudar depois.

Anotação explícita faz sentido quando:

- a variável começa vazia e recebe valor depois
- o TypeScript não consegue adivinhar o tipo sozinho
- você quer deixar claro para quem lê
- o tipo inferido não é o que você quer

```ts
let idade: number;
idade = 25; // ok — sem valor inicial, precisa dizer o tipo
```

Caso clássico: array vazio. Depende de **onde** ele está.

Variável solta — o TypeScript usa **evolving array**: acompanha os `push` seguintes e ajusta o tipo sozinho:

```ts
let lista = [];
lista.push(1);         // ok — TS infere number[]
lista.push(2);         // ok
```

Isso vale para `let lista = []` e até `const lista = []` dentro de uma função. Não precisa anotar na hora — mas o tipo só fica claro **depois** do que você colocou dentro. Se der `push` de tipos mistos, o array aceita tudo:

```ts
let lista = [];
lista.push(1);
lista.push("dois");    // ok — vira (string | number)[], não number[]
```

Se você quer **só números**, anote desde o começo:

```ts
let numeros: number[] = [];
numeros.push(1);       // ok
numeros.push("dois");  // ❌ erro
```

Propriedade de objeto — aqui o evolving array **não** entra. O TypeScript trava em `never[]`:

```ts
const obj = { items: [] };
obj.items.push(1);     // ❌ Argument of type '1' is not assignable to parameter of type 'never'
```

Sem tipo explícito, `items` não evolui. Por isso objetos com array vazio costumam pedir anotação — veremos mais disso na aula de [objetos](./05-objetos.md).

## O padrão JS → TS

Nos próximos módulos, vamos repetir esse fluxo: código JavaScript com o bug → mesma ideia em TypeScript com tipos. Se você já entendeu JS, o TypeScript é só dizer **qual formato** cada dado deve ter.

---

[← Playground e editores](../02-ambiente/03-playground-e-editores.md) · [Menu](../../README.md#roadmap) · [Próximo: Tipos primitivos →](./02-tipos-primitivos.md)
