# Tipos utilitários

TypeScript vem com tipos prontos para **transformar** outros tipos — evitam reescrever a mesma interface várias vezes com pequenas variações.

## Partial — tudo opcional

Sem `Partial`, atualizar um único campo já obriga a passar todos os outros — mesmo numa função de update, onde faz sentido mandar só o que mudou:

```ts
interface Geladeira {
  nome: string;
  descricao: string;
  modelo: string;
}

// Sem Partial — cada campo de Geladeira é obrigatório em 'dados'
function atualizar(id: number, dados: Geladeira) {
  // ...
}

atualizar(1, { modelo: "French Door" }); // ❌ faltam 'nome' e 'descricao'
```

`Partial<Geladeira>` gera um novo tipo com os mesmos campos de `Geladeira`, todos opcionais — sem precisar reescrever a interface inteira com `?` em cada linha. Repare que este é outro exemplo, não uma segunda definição de `atualizar` no mesmo arquivo — colar os dois blocos juntos causaria "Duplicate function implementation":

```ts
// Com Partial — todos os campos de Geladeira viram opcionais em 'dados'
function atualizar(id: number, dados: Partial<Geladeira>) {
  // ...
}

atualizar(1, { modelo: "French Door" }); // ok — só o campo que mudou
```

## Required — tudo obrigatório

Propriedades opcionais (`?`) fazem sentido enquanto o dado ainda está incompleto, mas às vezes você precisa garantir que, naquele ponto do código, nada ficou de fora — por exemplo depois de validar um formulário. `Required<T>` é o inverso do `Partial`: gera um novo tipo com todos os campos de `T`, mas nenhum opcional.

```ts
interface Veiculo {
  descricao?: string;
  marca?: string;
  motor?: string;
  portas?: number;
}

const carro: Required<Veiculo> = {
  descricao: "Skyline azul com preto",
  marca: "Nissan",
  motor: "3.8 gasolina",
  portas: 2,
};

const incompleto: Required<Veiculo> = {
  descricao: "Civic branco",
  marca: "Honda",
  motor: "2.0 flex",
  // ❌ falta 'portas' — Required não deixa nada de fora
};
```

## Pick — só algumas propriedades

Quando só uma parte de uma interface interessa num contexto específico — por exemplo, uma listagem que mostra apenas nome e id, sem os outros campos — `Pick<T, K>` cria um novo tipo contendo só as chaves escolhidas em `K`:

```ts
interface Produto {
  id: number;
  nome: string;
  preco: number;
  estoque: number;
}

type ResumoProduto = Pick<Produto, "id" | "nome">;

const resumo: ResumoProduto = { id: 1, nome: "Caneca" };
const invalido: ResumoProduto = { id: 1, nome: "Caneca", preco: 20 }; // ❌ 'preco' não existe em ResumoProduto
```

## Omit — todas menos algumas

O oposto do `Pick`: em vez de escolher o que fica, você escolhe o que sai. Útil quando falta só um campo — por exemplo um `id` gerado pelo banco de dados, que o cliente nunca envia ao criar um registro:

```ts
type ProdutoSemId = Omit<Produto, "id">;

function criarProduto(dados: ProdutoSemId): Produto {
  return { id: Date.now(), ...dados };
}

criarProduto({ nome: "Caneca", preco: 20, estoque: 100 }); // ok, sem id
```

## Record — mapa de chave para tipo

Quando um objeto funciona como mapa — chaves que só se sabe em runtime, todas apontando para o mesmo tipo de valor — declarar cada chave manualmente numa interface não faz sentido. `Record<K, V>` tipa isso de uma vez: toda chave do tipo `K` mapeia para um valor do tipo `V`.

```ts
type Estoque = Record<string, number>;

const estoque: Estoque = {
  caneca: 100,
  camiseta: 30,
};

estoque.caneca = "cem"; // ❌ valor precisa ser number
```

Também funciona com um conjunto fechado de chaves, usando um literal union:

```ts
type EstoquePorCategoria = Record<"eletronicos" | "roupas" | "livros", number>;

const porCategoria: EstoquePorCategoria = {
  eletronicos: 10,
  roupas: 5,
  livros: 20,
};
```

## Readonly — trava reatribuição

Às vezes você quer garantir que um objeto não seja modificado depois de criado — uma constante de configuração, ou um valor recebido de fora que a própria função não deveria alterar. `Readonly<T>` marca toda propriedade de `T` como somente leitura:

```ts
const produto: Readonly<Produto> = {
  id: 1,
  nome: "Caneca",
  preco: 20,
  estoque: 100,
};

produto.preco = 25; // ❌ preco é readonly
```

A trava é só em tempo de compilação e só no primeiro nível: o objeto em si não vira imutável em runtime (nada como `Object.freeze`), e uma propriedade que seja objeto/array continua editável por dentro — `Readonly` não é recursivo.

## ReturnType — tipo de retorno de uma função

Quando o formato de um dado só existe implícito no retorno de uma função — sem uma interface separada declarada em algum lugar — `ReturnType<T>` extrai esse tipo em vez de você duplicá-lo à mão:

```ts
function buscarProduto() {
  return { id: 1, nome: "Caneca", preco: 20, estoque: 100 };
}

type ProdutoRetornado = ReturnType<typeof buscarProduto>;

const p: ProdutoRetornado = { id: 2, nome: "Copo", preco: 15, estoque: 50 };
```

Note que `ReturnType` recebe `typeof buscarProduto`, não `buscarProduto` sozinho — `typeof` aqui extrai o tipo da função (sua assinatura), que é o que `ReturnType` precisa para olhar o retorno. Sem o `typeof`, você estaria passando o valor da função para um lugar que espera um tipo. Vemos `typeof` em detalhe na próxima aula.

## Outros utilitários (resumo)

Menos comuns no dia a dia, mas úteis de saber que existem — cada um evita escrever manualmente algo que o compilador já consegue derivar:

| Utilitário | O que faz | Exemplo |
|---|---|---|
| `Exclude<T, U>` | remove de `T` os tipos atribuíveis a `U` | `Exclude<"a" \| "b" \| "c", "a">` → `"b" \| "c"` |
| `Extract<T, U>` | mantém só os tipos de `T` atribuíveis a `U` | `Extract<"a" \| "b" \| "c", "a" \| "b">` → `"a" \| "b"` |
| `NonNullable<T>` | remove `null` e `undefined` de `T` | `NonNullable<string \| null>` → `string` |
| `Parameters<T>` | tupla com os tipos dos parâmetros de uma função | `Parameters<(a: number, b: string) => void>` → `[number, string]` |
| `ConstructorParameters<T>` | tupla com os parâmetros do construtor de uma classe | `ConstructorParameters<typeof Date>` → parâmetros aceitos por `new Date(...)` |
| `InstanceType<T>` | tipo da instância criada por um construtor | `InstanceType<typeof Date>` → `Date` |
| `Awaited<T>` | tipo "desembrulhado" de dentro de uma Promise | `Awaited<Promise<string>>` → `string` |

---

[← Generics](./03-generics.md) · [Menu](../../README.md#roadmap) · [Próximo: keyof, typeof e indexed access →](./05-keyof-typeof-e-indexed-access.md)
