# Enums e as const

Enum cria um conjunto nomeado de constantes relacionadas — direções, status, permissões. TypeScript oferece duas formas de fazer isso: a palavra-chave `enum` e o padrão `as const`, que usa só JavaScript puro.

## Enum numérico

Sem enum, é fácil usar números soltos e ninguém lembra o que cada um significa:

```js
function mover(direcao) {
  if (direcao === 1) return "subindo";
  if (direcao === 2) return "descendo";
}

mover(3); // undefined, silencioso — e "3" não diz nada sobre o que é
```

Com `enum`, os valores ganham nome e o compilador valida:

```ts
enum Direcao {
  Cima = 1,
  Baixo,
  Esquerda,
  Direita,
}

function mover(direcao: Direcao): string {
  switch (direcao) {
    case Direcao.Cima: return "subindo";
    case Direcao.Baixo: return "descendo";
    case Direcao.Esquerda: return "indo para a esquerda";
    case Direcao.Direita: return "indo para a direita";
  }
}

mover(Direcao.Cima);
mover(5); // ❌ 5 não é um valor válido de Direcao
```

Como só `Cima` recebeu um valor explícito, o resto é incrementado a partir dele: `Baixo = 2`, `Esquerda = 3`, `Direita = 4`.

Enum numérico também gera mapeamento reverso: em tempo de execução, `Direcao[1]` retorna `"Cima"` — o objeto compilado tem entradas nos dois sentidos (nome → valor e valor → nome). É um recurso de runtime, não uma proteção de tipo.

## Enum de string

Enums numéricos são difíceis de identificar num log ou no devtools — só aparece o número. Enums de string resolvem isso, mas cada membro precisa de um valor explícito (não há incremento automático):

```ts
enum StatusPedido {
  Pendente = "PENDENTE",
  Pago = "PAGO",
  Cancelado = "CANCELADO",
}

let status: StatusPedido = StatusPedido.Pago;
console.log(status); // "PAGO" — fácil de reconhecer, ao contrário de um número
```

## as const — a alternativa sem enum

`enum` gera um objeto extra no JavaScript compilado. Se você quer só a tipagem, sem esse código a mais em tempo de execução, `as const` sobre um objeto comum consegue o mesmo resultado:

```ts
const StatusPedido = {
  Pendente: "PENDENTE",
  Pago: "PAGO",
  Cancelado: "CANCELADO",
} as const;

type StatusPedido = (typeof StatusPedido)[keyof typeof StatusPedido];

let status: StatusPedido = StatusPedido.Pago;
let invalido: StatusPedido = "ENVIADO"; // ❌ "ENVIADO" não está na union
```

`typeof` e `keyof` aparecem aqui só para extrair o tipo do objeto — vemos os dois em detalhe na aula de [keyof, typeof e indexed access](./05-keyof-typeof-e-indexed-access.md).

## Quando usar cada um

| Abordagem | Vantagem | Cuidado |
|---|---|---|
| `enum` | sintaxe dedicada, leitura direta | gera objeto extra no JS compilado; em enum numérico, qualquer variável do tipo `number` passa despercebida onde se espera o enum, sem erro — um buraco de type-safety real (enum de string não tem esse problema) |
| `as const` | JavaScript puro, sem overhead em runtime | um pouco mais verboso para declarar |

---

[← Exercícios](../03-basico/11-exercicios.md) · [Menu](../../README.md#roadmap) · [Próximo: Narrowing →](./02-narrowing.md)
