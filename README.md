<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="./.github/images/header_4noobs.svg">
  </a>
</p>

<p align="center">
  <h2 align="center">Typescript4noobs</h2>

  --- 

  <h1 align="center"><img src="./.github/images/Typescript_logo_2020.png" alt="Logo do Typescript" width="120"></h1>

  <p align="center">    
    <br />
    <a href="https://www.typescriptlang.org/docs"><strong>Explore a documentação »</strong></a>
    <br />
    <br />
    <a href="https://github.com/Carolis/typescript4noobs/issues">Report Bug</a>
    ·
    <a href="https://github.com/Carolis/typescript4noobs/issues">Request Feature</a>
  </p>
</p>

# Sobre o Projeto

Este projeto tem como intenção ser um apoio aos cursos de react desenvolvidos pelo projeto 4noobs, portanto, os exemplos aqui citados estarão preferencialmente inseridos nesse ecossistema.

O material é pensado para que você consiga dar um pontapé inicial no seu projeto se utilizando de um ambiente preparado para o Typescript. Se você sentir falta ou necessidade de algum conteúdo sinta-se livre para abrir uma issue sinalizando isso.

Outro ponto é o fato de que editores como o **VSCode** são muito mais amigáveis ao Typescript e talvez seja uma boa ideia usá-lo caso você esteja iniciando. Porém você também pode usar o Vim, que possui uma ótima integração com Servidor da Linguagem por meio da extensão [coc.nvim](https://github.com/neoclide/coc.nvim).

Todos os exemplos citados nesse artigo podem ser testados no [playground online oficial](https://www.typescriptlang.org/play) caso não queira baixar nada.

# Roadmap


# Mão na Massa

# Tipos

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

Podemos encaixar aqui todos os outros tipos que não consideramos **primitivos** (number, string, boolean, bigint, symbol, null, ou undefined são considerados tipos primitivos).

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

## Type e Interfaces

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

Interfaces são muito úteis quando queremos descrever um objeto. São parecidas com os types, porém possuem algumas diferenças, podendo ser por exemplo extendidas.

Algo muito interessante de se citar é a possibilidade de definirmos propriedades opcionais através do símbolo de `?`.

Exemplos:

```ts

//declarando a interface Geladeira
interface Geladeira {
  nome: string;
  descricao: string;
  modelo: string;
  funcionalidades?: string[]; // o símbolo de  "?" demonstra que essa é uma propriedade OPCIONAL
}

//declarando um objeto do tipo Geladeira 
const Brastemp: Geladeira {
  nome: "Brastemp Frost Free",
  descricao: "Geladeira bonita",
  modelo: "1231XHDDH"
}

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

// utilizamos readonly para propriedades que são apenas para leitura
// elas disparam erro quando se tenta atualizá-las após definida

interface Identidade {
	readonly rg: string;
        emissor: string;
}

const minhaIdentidade: Identidade = {
	rg: "0123456789",
        emissor: "SSP"
}

minhaIdentidade.emissor = "CREA";
minhaIdentidade.rg = "9876543210" // dispara erro

// Quando queremos omitir algumas propriedades K de uma interface T podemos utilizar o Omit:
interface Veiculo {
    descricao: string;
    marca: string; 
    motor: string;
    portas: number;
}

type Bicicleta = Omit<Veiculo, 'motor' | 'portas'>;

const minhaBike: Bicicleta = {
    descricao: 'Bike que ganhei de presente',
    marca: 'Monark'
};

// e quando queremos pegar algumas propriedades K de uma interface T podemos utilizar o Pick:
type BicicletaComPick = Pick<Veiculo, 'descricao' | 'marca'>;

const minhaSegundaBike: BicicletaComPick = {
    descricao: 'Bike que comprei',
    marca: 'Monark'
};

```

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
