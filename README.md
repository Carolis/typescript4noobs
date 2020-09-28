<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="./.github/images/header_4noobs.svg">
  </a>
</p>

<p align="center">
  <h2 align="center">Typescript4noobs</h2>

  <p align="center">
    <a href="https://github.com/Carolis/typescript4noobs/issues">Report Bug</a>
    ·
    <a href="https://github.com/Carolis/typescript4noobs/issues">Request Feature</a>
  </p>
</p>

`Último update do projeto Typescript4noobs: 20/09/2020`

[Link para a documentação Oficial do Typescript](https://www.typescriptlang.org/docs)


# Introdução

Avisos:

Este projeto tem como intenção ser um apoio aos cursos de react desenvolvidos pelo projeto 4noobs, portanto, os exemplos aqui citados estarão preferencialmente inseridos nesse ecossistema.

Outro ponto é o fato de que editores como o **VSCode** são muito mais amigáveis ao Typescript e talvez seja uma boa ideia usá-lo caso você esteja iniciando. Porém você também pode usar o Vim, que possui uma ótima integração com Servidor da Linguagem por meio da extensão [coc.nvim](https://github.com/neoclide/coc.nvim).

Todos os exemplos citados nesse artigo podem ser testados no [playground online oficial](https://www.typescriptlang.org/play) caso não queira baixar nada.

### O que é o Typescript?

<p align="center">
  <a href="https://twitter.com/ianhunter/status/1258209274347638787" target="_blank">
    <img src="./.github/images/Toy.png">
  </a>
</p>

Typescript é considerado um **superset** da linguagem Javascript, dito isso, se você já sabe Javascript é muito fácil de começar a usá-lo já sabendo um pouco.
Ele tem como  principal funcionalidade a capacidade de adicionar **tipagens estáticas** ao código.
Um dos pontos positivos que vale a pena ser citado é a possibilidade de termos arquivos Typescript convivendo no mesmo projeto com arquivos Javascript já que no final das contas o Typescript é compilado para Javascript, ou seja, é uma ferramenta de **desenvolvimento**. Isso também permite que você adicione Typescript em qualquer momento do seu projeto, conforme necessidade e gosto pessoal.

### Por que usar Typescript?

O uso de Typescript traz segurança principalmente na detecção de **erros inesperados**. Um exemplo clássico seria o problema do operador `+` do Javascript que, dada uma soma com tipagens erradas poderia retornar erroneamente uma **concatenação** ao invés da soma propriamente dita.

```ts
function soma(x, y) {
    return x + y;
}
```

Chamando a função `soma(2,2)` o retorno seria `4`;

Chamando a função `soma('2','2')` o retorno seria `22`;

Esse problema seria facilmente evitado ao tiparmos as variáveis corretamente como números.


---

Outra grande vantagem de usar o Typescript é o aumento da inteligência dentro do seu editor ou IDE, o famoso **[IntelliSense](https://code.visualstudio.com/docs/editor/intellisense)** e a possibilidade de usar **parâmetros opcionais**. Além disso, as tipagens podem funcionar como uma mini documentação dentro do seu arquivo, facilitando futuras manutenções e fazendo com que todos esses fatores tragam uma camada a mais de segurança para o código.

### Por que não usar apenas PropTypes?

O PropTypes funciona de uma forma muito mais passiva dentro de um projeto, sendo passível de ser facilmente ignorado, o que não é o caso do Typescript que desfruta de uma série de ferramentas e arquivos de configuração (`tsconfig.json`) para que você faça ele se comportar de uma forma mais ativa impedindo que você dê continuidade à execução ao se deparar com um erro.

# Instalando o Typescript

PS: antes de seguir com a instalação do typescript é importante ter o **node** previamente instalado.

A instalação em si é super simples e pode ser feita com apenas esse comando abaixo:

`npm install -g typescript`

Para checar a versão instalada basta rodar `tsc -v`, assim teremos segurança de que ele realmente foi instalado.

Após instalado, é interessante rodarmos `tsc --init` no terminal para que um arquivo `tsconfig.json` seja gerado. Esse arquivo é responsável por ditar como o Typescript irá se comportar no projeto: para qual versão do Javascript ele vai compilar, quais diretórios ele deve jogar seus arquivos, se ele vai ser mais ou menos "chato" com os erros, etc.

---

### Extra: Instalação com Yarn

Você também pode inicializar seu projeto Typescript usando o **Yarn** por questões de preferência.

Basta rodar:

`yarn init -y` para inicializar o Yarn em si no diretório

`yarn add -D typescript` para instalar o Typescript

`yarn tsc --init` para gerar o arquivo `tsconfig.json`


# Mão na Massa

# 1) Tipos

Tipar variáveis é bem simples, como demonstrado no exemplo abaixo basta que você adicione `:tipo` depois de uma variável.

Exemplos:

```ts
let numero: number
numero = 3

let isTrue: boolean
isTrue = true
```

Para começar, vamos corrigir o exemplo da soma demonstrada no início desse artigo:

```ts
function soma(x: number, y: number) {
    return x + y;
}
```

Adicionando `:number` na frente das variáveis o problema da concatenação não desejada já seria facilmente eliminado.

<div align='center'>
  <img src='./.github/images/soma.gif'/>
</div>

---

Mas você já pensou em tipar uma função? Bem, não é exatamente isso, mas em TypeScript é possível tipar o retorno de uma função!

Isso permite ter a segurança que uma função irá retornar determinado tipo, por exemplo:

```ts
const somar10 = (n: number): number => n + 10;

function resposta(): string {
  return 'sim!';
}
```

Como demonstrado acima, tipar o retorno de uma função é parecido com tipar uma variável: apenas coloque um `:tipo`, porém depois dos parênteses.

Caso o tipo retornado não corresponda com o tipo do retorno:

<div align='center'>
  <img src='./.github/images/retorno-funcao.gif'/>
</div>

---

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

Podemos encaixar aqui todos os outros tipos que não consideramos **primitivos** (number, string, boolean, bigint, symbol, null, or undefined são considerados tipos primitivos).

```ts
let meuObjeto: object;

meuObjeto = {
  caracteristica1: "quadrado"
}
```

## Enums

O Enum serve para criarmos "apelidos" para os tipos e deixá-los num formato muito mais amigável conforme sua necessidade, definindo constantes que podem ser usadas para melhorar a legilibilidade do código.

## Enums Numéricos

Esses enums serão incrementados conforme a primeira definição, exemplo:

```ts
enum Direçao {
  Cima = 1,
  Baixo,
  Esquerda,
  Direita
}
```

Seguindo a ordem, `Baixo == 2`, `Esquerda == 3`, etc...Nesse caso poderíamos declarar apenas as constantes, pois os valores inicais começam do 0.

Segue mais um exemplo da utilização de um Enum Numérico:

```ts
enum Resposta {
  Sim = 1,
  Nao = 0
}

function responda(remetente: string, menssagem: Resposta): void {
  //...
}
```

## Enums String

Tambem é possível definir constantes, vulgo, Enums, com strings. Diferente dos numéricos, não há uma ordem de incremeto, logo, é necessário inicializar com um valor real, como:

```ts
enum Direcao {
  Cima = 'CIMA',
  Baixo = 'BAIXO',
  Esquerda = 'ESQUERDA',
  Direita = 'DIREITA'
}
```

## Enums com Expressões

Numa inicialização de uma constante tambem permite-se o uso de expressões, como mostra o código a seguir:

```ts
enum AcessarArquivo {
  Nada,
  Ler = 1 << 1,
  Escrever = 1 << 2,
  EscreverELer = Ler | Escrever,
  G = "123".length
}
```

# 3) Type e Interfaces

Vimos que podemos usar os tipos naturais da linguagem, porém, e se quisermos ir além? Definir nossos próprios tipos, tipar objetos e muito mais?

Não é só possível mas também é super simples, vejamos:

## Type

A forma mais simples de criar uma tipagem própria é com a palavra-chave `type`. Podemos usar o `type` como um apelido, assim como enums, porém esses não possuem auto-incremento:

```ts
type LadoQuadrado = number;
```

ou tipar objetos

```ts
type Triangulo = {
  lado1: number;
  lado2: number;
  lado3: number;
}

const triangulo: Triangulo = {
  lado1: 3,
  lado2: 4,
  lado3: 5,
};
```

caso um objeto de certo tipo não implemente corretamente o tipo definido, o compilador irá nos avisar.

Tambem podemos colocar funções nesses tipos, ou seja:

```ts
type Triangulo = {
  lado1: number;
  lado2: number;
  lado3: number;

  area(altura: number, base: number): number;
  // ou
  area: (altura: number, base: number) => number;

enum AcessarArquivo {
  Nada,
  Ler = 1 << 1,
  Escrever = 1 << 2,
  EscreverELer = Ler | Escrever,
  G = "123".length
}
```

Esse método permite usar constantes literais, como:

```ts
type Sim = 'sim';

let sim: Sim = 'sim';
// ERRO
sim = 'meu nome';

type Lado1 = 44.5;
let lado1: Lado1 = 44.5;
// O compilador aceita, porém não é recomendável
lado1 += 2;
```

## Interfaces

Já as interfaces, são como os types, porém possuem algumas diferenças:

* Interfaces podem ser extendidas;
* Interfaces podem ser unificadas;

Exemplos:

```ts
interface Pessoa {
  altura: number;
  falar(msg: string): string;
}

// essa interface criará uma interseção com a primeira
// ou seja, a interface Pessoa é a junção da primeira com essa
interface Pessoa {
  andar(passos: number): string;
}

// possui todos os métodos e atributos de Pessoa
interface Programador extends Pessoa {
  tomarCafe(): void;
}
```

# 4) Union Types (W.I.P)

# Como Contribuir com o 4noobs

Contribuições fazem com que a comunidade open source seja um lugar incrível para aprender, inspirar e criar. Todas contribuições
são **extremamente apreciadas**

1. Realize um Fork do projeto
2. Crie um branch com a nova feature (`git checkout -b feature/featureBraba`)
3. Realize o Commit (`git commit -m 'Add some featureBraba'`)
4. Realize o Push no Branch (`git push origin feature/featureBraba`)
5. Abra um Pull Request

# Autores

- **Carolina Ale** - _Developer & Member of He4rt Developers_  - [Twitter](https://twitter.com/caroliscaroles) - [Github](https://github.com/Carolis)

<p align="center">Made with 💜</p>

---

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="./.github/images/footer_4noobs.svg" width="380">
  </a>
</p>
