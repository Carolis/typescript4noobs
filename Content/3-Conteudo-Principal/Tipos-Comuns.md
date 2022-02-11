# Tipos comuns

Tipos em Typescript podem ser separados em algumas categorias, começando por tipos **básicos**:

## Any

O tipo Any pode ser, como o nome sugere, qualquer coisa. Recomenda-se **evitar** ao máximo o uso desse tipo já que no final das contas usá-lo seria o mesmo que não usar Typescript.

Vale lembrar que é possível configurar seu tsconfig para que seu código não aceite tipagens com `any` para uma maior segurança. 

```ts
let qualquerCoisa
qualquerCoisa = 1
qualquerCoisa = "Qualquer coisa"
qualquerCoisa = [coisa1, coisa2]
```

## Boolean

Aceita os valores `true` e `false`. Sua tipagem é escrita como `:boolean`

```ts
let checkTrue: boolean = false;
```

## Number

Você pode tipar praticamente qualquer tipo de número, sejam eles decimais, octais, binários ou hexadecimais. Sua tipagem é escrita como `:number` ou `:bigInt`

```ts
let decimal: number = 6;
let hexadecimal: number = 0xf00d;
let binario: number = 0b1010;
let octal: number = 0o744;
let big: bigint = 100n;
```

## String

Strings podem ser declaradas usando aspas simples e duplas como já conhecemos e também usando aspas **invertidas** para que algumas operações lógicas sejam inseridas dentro da variável.

Sua tipagem é escrita como `:string`

```ts
let frase1: string
frase1 = "Eu amo geladeiras!"

let frase2: string
frase2 = `Olá, meu nome é ${meuNome} e eu terei ${idade + 1} anos no próximo mês`
```

## Array

Arrays podem ser tipados de duas formas diferentes:

```ts
let listaDeNumeros: number[] = [1, 2, 3];

let listaDePalavras: string[] = ["maçã", "laranja", "banana"];
```

ou com a notação **Generics**

```ts
let listaDeNumeros: Array<number> = [1, 2, 3];

let listaDePalavras: Array<string> = ["maçã", "laranja", "banana"];
```

## Tupla

Tuplas são bem parecidas com Arrays, a diferença é que sabemos previamente o qual será o tipo de cada elemento inserido ali dentro e eles podem ser diferentes entre si, por exemplo um par com uma string e um número como demonstrado abaixo:

```ts
let minhaTupla: [string, number];
minhaTupla = ["frase", 1];
```

## Void

O tipo `void`, geralmente utilizado no retorno de funções, significa que uma função não retorna nenhum valor em especifíco, ou seja, não retorna nada. Pode ser considerado o oposto do tipo `any`.

```ts
function lerArquivo(): void {
  // ler o arquivo
  // não retorna nenhum valor
}
```

## Never

Especialmente útil no gerenciamento de erros o tipo `never` serve para criarmos exceções que nunca irão retornar nada.

```ts
function error(): never {
  throw new Error("errrouuuu");
}

```

## Object

Podemos encaixar aqui todos os outros tipos que não consideramos **primitivos** (number, string, boolean, bigint, symbol, null, ou undefined são considerados tipos primitivos).

```ts
let meuObjeto: object;

meuObjeto = {
  caracteristica1: "quadrado"
}
```

---

<p align="center">
  <a href="https://github.com/Carolis/typescript4noobs#roadmap">VOLTAR PARA O MENU PRINCIPAL</a>
</p>
