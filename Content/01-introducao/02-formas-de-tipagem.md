# Formas de tipagem

Antes de escrever TypeScript de verdade, vale entender **como** uma linguagem trata tipos. JavaScript e TypeScript não fazem isso do mesmo jeito — e misturar os conceitos aqui costuma gerar confusão lá na frente.

Para classificar uma linguagem, duas perguntas simples resolvem quase tudo:

1. **Quando** o tipo é checado — enquanto o programa roda, ou antes dele rodar?
2. **A linguagem mistura tipos sozinha** — ou exige que você converta de propósito?

Vamos por partes.

## Quando o tipo é checado

### Tipagem dinâmica

Tipagem dinâmica é isto: você cria uma variável com um tipo e, em outro momento, **troca o tipo dela**.

```js
let nome = "Diego";
console.log(typeof nome); // "string"

nome = 10;
console.log(typeof nome); // "number"
```

Antes o conteúdo era o texto `"Diego"`. Depois a **mesma variável** passou a guardar um número. Isso é dinâmico porque o tipo pode mudar **em tempo de execução**.

Funciona. Só que nada garante o formato dos dados. Uma função espera texto, recebe número, e o bug só aparece quando aquele trecho realmente roda — às vezes já em produção.

Linguagens com tipagem dinâmica: **JavaScript**, **Python**, **Ruby**, **PHP**.

### Conferindo os dados enquanto o programa roda

Em linguagens dinâmicas, quando você quer mais segurança, acaba escrevendo validações — `if`, `throw`, bibliotecas como o Zod. A checagem acontece **enquanto o código executa**, por isso o nome **validação em runtime**.

Imagine que um usuário precisa ter o ano em que nasceu:

```js
const usuario = {
  nome: "Diego",
};

if (!("anoQueNasceu" in usuario)) {
  throw new Error("invalid");
}

// daqui pra frente, o campo existe
```

Cada regra nova vira mais um `if` no meio da lógica, e o erro só aparece quando o programa roda. O trabalho de garantir fica com você, não com o compilador.

Isso aparece o tempo todo com dados de fora — API, formulário, banco. Mesmo com TypeScript continua fazendo sentido; o compilador não sabe o que chegou pela rede. Validação em runtime não é um "tipo" de tipagem como dinâmica ou estática: é uma técnica que você usa dentro de uma linguagem dinâmica quando precisa compensar o que ela não garante sozinha.

### Tipagem estática

Outra abordagem é **evitar** o erro antes dele acontecer: não esperar a aplicação executar para descobrir que as informações estão indo de um lado para o outro do jeito errado.

É isso que o TypeScript traz para o JavaScript: **tipagem estática**. Você indica o formato de cada variável no código, e o compilador avisa possíveis erros na hora de escrever.

```ts
type Usuario = {
  nome: string;
  anoQueNasceu: number;
};

const usuario: Usuario = {
  nome: "Diego",
  // ❌ erro: falta anoQueNasceu
};
```

Sem `if`, sem `throw`. O TypeScript recusa o objeto incompleto antes de o código rodar.

Linguagens com tipagem estática: **TypeScript**, **Java**, **C#**, **Go**, **Rust**.

| | Tipagem dinâmica | Tipagem estática |
|---|---|---|
| Quando checa | em execução | antes de executar |
| Tipo da variável pode mudar | sim | não |
| Você descobre o erro | rodando o programa | escrevendo o código |
| Exemplos | JavaScript, Python, Ruby, PHP | TypeScript, Java, C#, Go, Rust |

## A linguagem mistura tipos sozinha?

A segunda pergunta é independente da primeira. Uma linguagem pode ser dinâmica **e** fraca, dinâmica **e** forte, estática **e** forte — são combinações diferentes.

**Tipagem fraca** converte tipos no automático. O clássico do JavaScript:

```js
console.log("2" + 2); // "22" — número virou texto e concatenou
console.log("2" - 2); // 0    — texto virou número e subtraiu
```

**Tipagem forte** não faz essa ginástica sem você pedir. Python é dinâmico **e** forte: `"2" + 2` estoura erro na hora.

| | Tipagem fraca | Tipagem forte |
|---|---|---|
| Converte tipos sozinha | sim | não, você precisa converter |
| `"2" + 2` | vira `"22"` | erro |

Na prática: Python é **dinâmico e forte**, JavaScript é **dinâmico e fraco**, Java é **estático e forte**.

## TypeScript: estático, mas gradual

TypeScript é **estático e forte** — mas com uma diferença importante em relação a Java ou Rust. Nessas linguagens, a tipagem estática vale para **tudo**. No TypeScript ela é **gradual**: você pode adotar aos poucos e, em trechos específicos, "desligar" a checagem com `any`:

```ts
let valor: any = "Diego";

valor = 10;        // ok
valor.qualquerCoisa(); // ok para o compilador — e possível erro em execução
```

Com `any`, aquele pedaço volta a se comportar como JavaScript puro. Útil para migrar um projeto legado; ruim se virar hábito, porque você perde justamente a proteção que foi buscar.

Vale lembrar também que TypeScript **não substitui** o JavaScript. Ele adiciona uma camada de tipos conferida durante o desenvolvimento e **desaparece** no código final. Em execução, quem roda é JavaScript — dinâmico e fraco como sempre foi. Por isso validação em runtime continua fazendo sentido para o que vem de fora do seu código.

Na próxima aula você vê como seguir este guia e quais versões de TypeScript e Node estamos usando.

---

[← O que é o TypeScript?](./01-o-que-e-typescript.md) · [Menu](../../README.md#roadmap) · [Próximo: Como usar este guia →](./03-como-usar-este-guia.md)
