# Conditional types

Na aula de [Generics](../04-intermediario/03-generics.md) vimos `extends` como uma restrição: `T extends { length: number }` limita quais tipos `T` pode assumir. Um conditional type usa a mesma palavra para outra coisa — decidir qual tipo usar dependendo de outro tipo, como um `if/else` que roda em tempo de compilação.

## Sintaxe básica

```ts
type Mensagem<T> = T extends string ? "sim" : "não";

type Resultado1 = Mensagem<string>; // "sim"
type Resultado2 = Mensagem<number>; // "não"
```

Essa sintaxe é a mesma do operador ternário do JavaScript (`condição ? seVerdadeiro : seFalso`), só que aplicada a tipos em vez de valores:

- antes do `?` fica a condição: `T extends string` pergunta "o tipo `T` é atribuível a `string`?".
- logo depois do `?` fica o tipo usado quando a condição é verdadeira.
- depois do `:` fica o tipo usado quando a condição é falsa.

De forma geral, um conditional type segue o formato: `tipoTestado extends tipoDeComparação ? tipoSeVerdadeiro : tipoSeFalso`.

## Retorno que muda de acordo com a entrada

Sem conditional types, um retorno que muda de acordo com o tipo de entrada exige sobrecargas de função ou aceitar um tipo mais largo (`T | T[]`), que obriga quem chama a fazer narrowing de novo depois. Um caso comum: uma função que sempre devolve array, sem embrulhar de novo algo que já é array.

```ts
type GarantirArray<T> = T extends any[] ? T : T[];

type A = GarantirArray<string>;   // string[]
type B = GarantirArray<string[]>; // string[] — não vira string[][]
```

```ts
declare function paraArray<T>(valor: T): GarantirArray<T>;

const a = paraArray("oi");       // string[]
const b = paraArray(["a", "b"]); // string[] — o mesmo tipo, sem aninhar de novo

const invalido: GarantirArray<string> = "oi"; // ❌ 'string' não é atribuível a 'string[]'
```

## Distribuindo sobre union

Quando `T` é usado "nu" (sem estar embrulhado em outra coisa) dentro do `extends`, o conditional type distribui sobre cada membro de uma union em vez de tratá-la como um bloco só — comportamento que costuma surpreender:

```ts
type SoString<T> = T extends string ? T : never;

type Resultado = SoString<string | number | boolean>; // string
```

`SoString` roda separado para cada membro da union (`string`, `number`, `boolean`), e os resultados `never` somem quando a union volta a se juntar — sobra só `string`. Embrulhar `T` numa tupla desliga essa distribuição:

```ts
type SoStringNaoDistributivo<T> = [T] extends [string] ? T : never;

type Resultado2 = SoStringNaoDistributivo<string | number | boolean>; // never
```

Aqui `[T]` não é mais um tipo "nu": o TypeScript compara a union inteira de uma vez contra `[string]`, ela não é atribuível, e o resultado vira `never` — bem diferente do exemplo anterior, mesmo com a mesma union de entrada.

---

Enquanto conditional types decidem qual tipo usar, mapped types transformam cada propriedade de um tipo já existente — é o que vem a seguir.

---

[← Exercícios](../04-intermediario/08-exercicios.md) · [Menu](../../README.md#roadmap) · [Próximo: Mapped types →](./02-mapped-types.md)
