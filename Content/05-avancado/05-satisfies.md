# satisfies

Tipar uma variável força tudo pro tipo declarado, mesmo quando o valor real era mais específico. Não tipar preserva o específico, mas perde qualquer checagem contra um formato esperado. `satisfies` resolve os dois ao mesmo tempo.

## O problema com anotação direta

```ts
interface RegrasDeCor {
  vermelho: string | [number, number, number];
  verde: string | [number, number, number];
  azul: string | [number, number, number];
}

const paleta: RegrasDeCor = {
  vermelho: [255, 0, 0],
  verde: "#00ff00",
  azul: [0, 0, 255],
};

paleta.verde.toUpperCase();
// ❌ Property 'toUpperCase' does not exist on type 'string | [number, number, number]'.
```

A anotação `: RegrasDeCor` garante que cada campo bate com o formato esperado, mas força o tipo de `verde` pra union inteira — o TypeScript esquece que, nesse objeto específico, `verde` é sempre uma string.

## O problema sem anotação nenhuma

```ts
const paletaSemTipo = {
  vermelho: [255, 0, 0],
  verde: "#00ff00",
  azul: 123, // deveria ser inválido — RegrasDeCor não aceita number
};
```

Sem anotação, o TypeScript infere o formato exato do que foi escrito e não reclama de nada: não existe nenhum contrato sendo checado, então `azul: 123` passa direto, mesmo sendo um erro de verdade.

## satisfies — os dois ao mesmo tempo

```ts
const paletaFinal = {
  vermelho: [255, 0, 0],
  verde: "#00ff00",
  azul: [0, 0, 255],
} satisfies RegrasDeCor;

paletaFinal.verde.toUpperCase(); // ok — TypeScript sabe que 'verde' é string aqui

const paletaInvalida = {
  vermelho: [255, 0, 0],
  verde: "#00ff00",
  azul: 123,
} satisfies RegrasDeCor;
// ❌ Type 'number' is not assignable to type 'string | [number, number, number]'.
```

`satisfies` checa o objeto contra `RegrasDeCor` (por isso `azul: 123` quebra, igual no exemplo anotado), mas o tipo de `paletaFinal` continua sendo o tipo inferido do próprio objeto literal — não `RegrasDeCor`. É por isso que `paletaFinal.verde` continua sendo `string`, não a union inteira.

---

Até aqui, todo tipo usado neste curso foi declarado dentro do próprio projeto TypeScript. A próxima aula lida com o cenário oposto: como tipar código que não tem tipo nenhum.

---

[← infer](./04-infer.md) · [Menu](../../README.md#roadmap) · [Próximo: Declaration files →](./06-declaration-files.md)
