# Narrowing

Narrowing é o processo de o TypeScript **estreitar** um tipo mais amplo (union, `unknown`) para um tipo mais específico, com base em checagens que você já escreveria de qualquer forma no código.

## typeof

```js
function formatar(valor) {
  return valor.toFixed(2); // quebra em runtime se valor for string
}

formatar("10"); // TypeError: valor.toFixed is not a function
```

```ts
function formatar(valor: string | number): string {
  if (typeof valor === "number") {
    return valor.toFixed(2); // aqui dentro, o TS sabe que valor é number
  }
  return valor.trim(); // aqui dentro, sabe que é string
}
```

Fora do `if`, `valor` continua sendo `string | number` — o estreitamento vale só dentro do bloco onde a checagem garante o tipo.

## instanceof

Funciona do mesmo jeito para diferenciar classes:

```ts
class ErroValidacao extends Error {}

function tratar(erro: Error) {
  if (erro instanceof ErroValidacao) {
    console.log("erro de validação:", erro.message);
  } else {
    console.log("erro genérico:", erro.message);
  }
}
```

Aprofundamos em classes na aula de [Classes](./06-classes.md).

## in — checando se a propriedade existe

Útil para diferenciar formatos de objeto que não compartilham uma propriedade em comum:

```ts
type Cachorro = { latir(): void };
type Gato = { miar(): void };

function fazerBarulho(animal: Cachorro | Gato) {
  if ("latir" in animal) {
    animal.latir();
  } else {
    animal.miar();
  }
}
```

`in` funciona mesmo quando os formatos não compartilham nenhuma propriedade em comum. Quando você controla o design dos tipos e pode adicionar uma propriedade só para isso, discriminated union (adiante) resolve o mesmo problema de outra forma.

## Truthiness

Um `if` comum já estreita `undefined`/`null` para fora do tipo:

```ts
function saudacao(nome?: string) {
  if (nome) {
    console.log(nome.toUpperCase()); // aqui, nome é string — não string | undefined
  }
}
```

Cuidado: valores falsy de verdade (`""`, `0`) também caem fora do `if`, mesmo sendo `string`/`number` válidos — se `""` for um caso legítimo, prefira `nome !== undefined`.

## Discriminated union — narrowing pela "etiqueta"

Retomando o `Resultado` da aula de [type aliases](../03-basico/06-type-aliases.md#union--mais-de-um-tipo-possível):

```ts
type Resultado =
  | { sucesso: true; dado: string }
  | { sucesso: false; erro: string };

function tratarResultado(r: Resultado) {
  if (r.sucesso) {
    console.log(r.dado); // TS sabe que aqui é a variante com 'dado'
  } else {
    console.log(r.erro); // e aqui, a variante com 'erro'
  }
}
```

A propriedade `sucesso` funciona como uma "etiqueta": ao checar seu valor, o TypeScript já estreita qual variante da union você está tratando.

## Exaustividade com never

A forma mais didática de garantir que todos os casos de uma union foram tratados usa `never`, como já vimos na aula de [any, unknown, never e void](../03-basico/10-any-unknown-never-void.md#never--nunca-retorna): se alguém adicionar um novo caso à union e esquecer de tratá-lo, o `default` deixa de aceitar `never` e o compilador aponta o erro ali mesmo — sem precisar rodar o código para descobrir.

```ts
type Resultado =
  | { sucesso: true; dado: string }
  | { sucesso: false; erro: string }
  | { sucesso: "pendente" }; // novo caso adicionado

function tratarResultado(r: Resultado) {
  if (r.sucesso === true) {
    console.log(r.dado);
  } else if (r.sucesso === false) {
    console.log(r.erro);
  } else {
    const _exaustivo: never = r; // ❌ agora quebra aqui — 'pendente' não foi tratado
  }
}
```

---

[← Enums e as const](./01-enums-e-as-const.md) · [Menu](../../README.md#roadmap) · [Próximo: Generics →](./03-generics.md)
