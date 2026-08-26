# Exercícios

Fixe o que você viu neste módulo. Teste no [playground](https://www.typescriptlang.org/play) ou num projeto local.

## 1. Conditional type

Crie um conditional type `EhArray<T>` que resolve para `true` quando `T` é um array e `false` caso contrário. Teste com `EhArray<string[]>` e `EhArray<string>`.

## 2. Mapped type

Implemente seu próprio `MeuReadonly<T>` usando mapped type (sem usar o `Readonly` embutido). Teste que ele bloqueia reatribuição do mesmo jeito que o `Readonly<T>` da aula de [Tipos utilitários](../04-intermediario/04-tipos-utilitarios.md).

## 3. Template literal type

Dado `type Tamanho = "P" | "M" | "G"`, crie um template literal type `SkuTamanho` que gera `"SKU-P" | "SKU-M" | "SKU-G"`.

## 4. infer

Implemente `PrimeiroParametro<T>`, que extrai o tipo do primeiro parâmetro de uma função usando conditional type + `infer`. Teste com uma função que recebe `(nome: string, idade: number)` — o resultado esperado é `string`.

## 5. satisfies

Crie uma `interface Config` com pelo menos dois campos e um objeto validado com `satisfies Config`. Confirme que, depois, um campo específico mantém seu tipo literal — não o tipo mais largo declarado na interface.

## 6. Declaration file

Escreva um `.d.ts` que declara o módulo `"contador-simples"` (uma biblioteca fictícia sem tipos), exportando uma função `incrementar(valor: number): number`.

## 7. Combinando mapped type e template literal type

Dada:

```ts
interface Formulario {
  nome: string;
  idade: number;
}
```

Crie um tipo `FormularioComValidacao` que, para cada campo de `Formulario`, gera uma nova chave com o prefixo `validar` seguido do nome do campo capitalizado (`validarNome`, `validarIdade`), cujo valor é uma função `(valor: TipoDoCampo) => boolean`.

---

Este é o último módulo do curso. Continue praticando no [playground](https://www.typescriptlang.org/play) ou aplicando os conceitos num projeto real.

---

[← Declaration files](./06-declaration-files.md) · [Menu](../../README.md#roadmap)
