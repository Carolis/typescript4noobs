# Funções

Funções aceitam tipos nos **parâmetros** e no **retorno** — a mesma ideia das variáveis, só que depois dos parênteses.

## Parâmetros tipados

```ts
function soma(x: number, y: number) {
  return x + y;
}

soma(2, 2);       // 4 ✓
soma("2", "2");   // ❌ erro
```

Esse é o exemplo da introdução: no JavaScript, `"2" + "2"` vira `"22"`. Com tipos, o problema nem chega a compilar.

## Retorno tipado

```ts
function resposta(): string {
  return "sim!";
}

const somar10 = (n: number): number => n + 10;
```

O `: number` depois dos parênteses diz o que a função **deve** devolver. Se você retornar outro tipo, o compilador reclama.

```ts
function idade(ano: number): number {
  return "vinte"; // ❌ string não é number
}
```



## Retorno inferido

Na prática, muita gente omite o `: tipo` de retorno e deixa o TypeScript **inferir** — como na aula de [anotações de tipo](./01-anotacoes-de-tipo.md#inferência-nem-tudo-precisa-de-anotação). Anote explicitamente quando quiser deixar claro para quem lê, ou em funções exportadas de uma biblioteca.

```ts
function dobro(n: number) {
  return n * 2; // inferido como number
}
```



## void — função que não retorna valor

Quando a função só executa uma ação e não devolve nada útil:

```ts
function log(mensagem: string): void {
  console.log(mensagem);
}
```

`void` não significa "retorna undefined obrigatoriamente" — significa que você **não deve usar** o valor de retorno.

## Parâmetros opcionais

Com `?`, o parâmetro pode ser omitido:

```ts
function saudar(nome: string, titulo?: string) {
  return titulo ? `${titulo} ${nome}` : nome;
}

saudar("Ana");           // "Ana"
saudar("Ana", "Dra.");   // "Dra. Ana"
```

Dentro da função, `titulo` é `string | undefined` — se você omitir o argumento, precisa tratar o `undefined` (como no `titulo ?` acima).

## Valor padrão

Alternativa ao opcional — define um valor se nada for passado:

```ts
function saudar(nome: string, titulo: string = "") {
  return titulo ? `${titulo} ${nome}` : nome;
}

saudar("Ana");           // "Ana"
saudar("Ana", "Dra.");   // "Dra. Ana"
```

Com valor padrão, `titulo` é sempre `string` dentro da função — nunca `undefined`, porque o TypeScript já sabe que o padrão cobre o caso omitido.

## Ordem dos parâmetros

Parâmetros opcionais (`?`) e com valor padrão (`=`) precisam vir **depois** dos obrigatórios:

```ts
function errado(titulo?: string, nome: string) {} // ❌ obrigatório depois do opcional
function certo(nome: string, titulo?: string) {}  // ✓
```

Quem está aprendendo tromba nisso direto — o compilador não deixa passar.

## Arrow functions

A sintaxe muda, a tipagem não:

```ts
const multiplicar = (a: number, b: number): number => a * b;
```

---

[← Arrays e tuplas](./03-arrays-e-tuplas.md) · [Menu](../../README.md#roadmap) · [Próximo: Objetos →](./05-objetos.md)