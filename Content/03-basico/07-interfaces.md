# Interfaces

`interface` descreve a **forma de um objeto** — parecido com `type`, mas com algumas diferenças que veremos na próxima aula.

## Declarando uma interface

```ts
interface Geladeira {
  nome: string;
  descricao: string;
  modelo: string;
  funcionalidades?: string[];
}

const minha: Geladeira = {
  nome: "Brastemp Frost Free",
  descricao: "Geladeira bonita",
  modelo: "1231XHDDH",
};

const errada: Geladeira = {
  nome: "Consul",
  descricao: "Geladeira simples",
  // ❌ falta 'modelo'
};
```

`funcionalidades?` é opcional — pode omitir, como vimos com `type`.

## Estendendo com extends

Uma interface pode **herdar** outra:

```ts
interface Pessoa {
  nome: string;
  idade: number;
}

interface Aluno extends Pessoa {
  codigo: number;
}

const aluno: Aluno = {
  codigo: 1,
  nome: "Mateus",
  idade: 25,
};
```

`Aluno` tem tudo de `Pessoa` mais `codigo`.

Se duas interfaces estendidas tiverem a **mesma propriedade com tipos incompatíveis**, o `extends` quebra na hora:

```ts
interface A { valor: string; }
interface B { valor: number; }
interface C extends A, B {} // ❌ conflito — 'valor' não pode ser string e number ao mesmo tempo
```

## Métodos na interface

```ts
interface Pessoa {
  nome: string;
  falar(mensagem: string): string;
}

const ana: Pessoa = {
  nome: "Ana",
  falar(mensagem) {
    return `${this.nome} disse: ${mensagem}`;
  },
};
```

Cuidado ao **soltar** o método do objeto — `this` perde o contexto:

```ts
const falarSolta = ana.falar;
falarSolta("oi"); // this vira undefined em muitos contextos
```

Funciona enquanto você chama `ana.falar("oi")` direto; quebra se passar o método como callback ou desestruturar.

## readonly

Propriedade que não pode ser reatribuída:

```ts
interface Identidade {
  readonly rg: string;
  emissor: string;
}

const doc: Identidade = {
  rg: "0123456789",
  emissor: "SSP",
};

doc.emissor = "CREA"; // ok
doc.rg = "999";       // ❌ rg é readonly
```

## Mesmo nome, declarações que se somam

Interfaces com o **mesmo nome** se **fundem** automaticamente:

```ts
interface Pessoa {
  nome: string;
}

interface Pessoa {
  idade: number;
}

// Pessoa agora exige nome e idade
```

Isso só funciona com `interface`, não com `type` — um detalhe que entra na comparação da próxima aula.

---

[← Type aliases](./06-type-aliases.md) · [Menu](../../README.md#roadmap) · [Próximo: type vs interface →](./08-type-vs-interface.md)
