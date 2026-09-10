# Mapped types

Os tipos utilitários da aula de [Tipos utilitários](../04-intermediario/04-tipos-utilitarios.md) parecem mágica, mas não são: `Partial`, `Readonly` e `Pick` são, por baixo dos panos, mapped types — um jeito de gerar um tipo novo percorrendo as propriedades de um tipo existente.

## Sintaxe básica

```ts
interface Produto {
  id: number;
  nome: string;
}

type Copia<T> = { [K in keyof T]: T[K] };

type ProdutoCopia = Copia<Produto>; // { id: number; nome: string }
```

`[K in keyof T]` percorre cada chave de `T`, uma por uma, e `T[K]` (indexed access, da aula de [keyof, typeof e indexed access](../04-intermediario/05-keyof-typeof-e-indexed-access.md)) pega o tipo daquela chave específica.

## Reimplementando Partial

Adicionar `?` dentro do mapped type torna cada propriedade opcional — essa é, literalmente, a implementação real do `Partial` embutido do TypeScript:

```ts
type MeuPartial<T> = { [K in keyof T]?: T[K] };

const p1: MeuPartial<Produto> = { nome: "Caneca" }; // ok — todos os campos viram opcionais
const p2: MeuPartial<Produto> = { preco: 20 };      // ❌ 'preco' não existe em Produto
```

## Modificadores + e -

`?` e `readonly` também podem ser removidos dentro de um mapped type, com `-` na frente. `+` existe para o caso contrário, mas é o padrão — raramente é escrito à mão.

```ts
interface ConfigParcial {
  tema?: string;
  idioma?: string;
}

type SemOpcionais<T> = { [K in keyof T]-?: T[K] };

type ConfigCompleta = SemOpcionais<ConfigParcial>; // { tema: string; idioma: string }

const c1: ConfigCompleta = { tema: "escuro", idioma: "pt-BR" }; // ok
const c2: ConfigCompleta = { tema: "escuro" };                  // ❌ falta 'idioma'
```

```ts
type SoLeitura<T> = { readonly [K in keyof T]: T[K] };
type Editavel<T> = { -readonly [K in keyof T]: T[K] };

const travado: SoLeitura<ConfigCompleta> = { tema: "escuro", idioma: "pt-BR" };
travado.tema = "claro"; // ❌ tema é readonly

const liberado: Editavel<SoLeitura<ConfigCompleta>> = { tema: "escuro", idioma: "pt-BR" };
liberado.tema = "claro"; // ok — o -readonly desfez a trava
```

---

Mapped types também podem renomear cada chave durante a transformação, com uma cláusula `as` — e a forma mais comum de montar esse novo nome é com template literal types, que é a próxima aula.

---

[← Conditional types](./01-conditional-types.md) · [Menu](../../README.md#roadmap) · [Próximo: Template literal types →](./03-template-literal-types.md)
