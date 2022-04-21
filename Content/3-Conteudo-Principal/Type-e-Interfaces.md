# Type e Interfaces

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

Caso um objeto de certo tipo não implemente corretamente o tipo definido, o compilador irá nos avisar.

Também podemos colocar funções nesses tipos, ou seja:

```ts
type Triangulo = {
  lado1: number;
  lado2: number;
  lado3: number;

  area(altura: number, base: number): number;
  // ou
  area: (altura: number, base: number) => number;
}

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

Interfaces são muito úteis quando queremos descrever um objeto. São parecidas com os types, porém possuem algumas diferenças, podendo ser por exemplo estendidas.

Algo muito interessante de se citar é a possibilidade de definirmos propriedades opcionais através do símbolo de `?`.

Exemplos:

```ts
// declarando a interface Geladeira
interface Geladeira {
  nome: string;
  descricao: string;
  modelo: string;
  funcionalidades?: string[]; // o símbolo de "?" demonstra que essa é uma propriedade OPCIONAL
}

// declarando um objeto do tipo Geladeira 
const Brastemp: Geladeira = {
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

---

<p align="center">
  <a href="https://github.com/Carolis/typescript4noobs#roadmap">VOLTAR PARA O MENU PRINCIPAL</a>
</p>
