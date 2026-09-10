# keyof, typeof e indexed access

Três operadores que extraem tipos a partir de outros tipos ou valores, em vez de você escrevê-los à mão.

## keyof — as chaves de um tipo como union

```ts
interface Produto {
  id: number;
  nome: string;
  preco: number;
}

function pegarValor(produto: Produto, chave: keyof Produto) {
  return produto[chave];
}

pegarValor({ id: 1, nome: "Caneca", preco: 20 }, "preco"); // ok
pegarValor({ id: 1, nome: "Caneca", preco: 20 }, "cor");   // ❌ 'cor' não é chave de Produto
```

`keyof Produto` equivale a `"id" | "nome" | "preco"` — mas some sozinho se você adicionar ou remover uma propriedade de `Produto`, sem precisar atualizar a union à mão.

## typeof — o tipo de um valor que já existe

```ts
const configPadrao = {
  tema: "escuro",
  idioma: "pt-BR",
  notificacoes: true,
};

type Config = typeof configPadrao;

function aplicar(config: Config) {
  // ...
}

aplicar({ tema: "claro", idioma: "en-US", notificacoes: false }); // ok
aplicar({ tema: "claro" }); // ❌ faltam 'idioma' e 'notificacoes'
```

Em vez de declarar `interface Config` manualmente e correr o risco dela ficar dessincronizada de `configPadrao`, `typeof` extrai o formato direto do valor.

Repare que `tema` foi inferido como `string`, não como o literal `"escuro"` — a mesma regra de inferência de tipos vista lá no início do curso. Se você quisesse o literal exato (por exemplo, para restringir `tema` só a `"escuro" | "claro"`), combinaria `typeof` com `as const`, como no exemplo a seguir.

## keyof typeof — combinação comum

Retomando o `as const` da primeira aula do módulo, [Enums e as const](./01-enums-e-as-const.md):

```ts
const StatusPedido = {
  Pendente: "PENDENTE",
  Pago: "PAGO",
  Cancelado: "CANCELADO",
} as const;

type ChaveStatus = keyof typeof StatusPedido;                      // "Pendente" | "Pago" | "Cancelado"
type ValorStatus = (typeof StatusPedido)[keyof typeof StatusPedido]; // "PENDENTE" | "PAGO" | "CANCELADO"
```

`typeof StatusPedido` pega o tipo do objeto; `keyof` pega as chaves desse tipo. Juntos, viram um jeito comum de derivar uniões de string a partir de um objeto `as const`.

## Indexed access — Type["propriedade"]

Acessa o tipo de uma propriedade específica, do mesmo jeito que você acessaria o valor em runtime:

```ts
interface ProdutoCompleto {
  id: number;
  nome: string;
  preco: number;
  fornecedor: {
    razaoSocial: string;
    cnpj: string;
  };
}

type Fornecedor = ProdutoCompleto["fornecedor"];    // { razaoSocial: string; cnpj: string }
type Preco = ProdutoCompleto["preco"];              // number
type IdOuNome = ProdutoCompleto["id" | "nome"];     // number | string — também aceita union de chaves
type CampoQualquer = ProdutoCompleto[keyof ProdutoCompleto]; // union de todos os tipos de valor

const campo: CampoQualquer = 10; // ok — number é um dos tipos possíveis
const campoInvalido: CampoQualquer = true; // ❌ boolean não é nenhum dos tipos de ProdutoCompleto
```

---

[← Tipos utilitários](./04-tipos-utilitarios.md) · [Menu](../../README.md#roadmap) · [Próximo: Classes →](./06-classes.md)
