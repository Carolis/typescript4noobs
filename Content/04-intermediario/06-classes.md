# Classes

Em JavaScript, nada impede acesso ou reatribuição indevida às propriedades de uma classe:

```js
class ContaBancaria {
  constructor(saldo) {
    this.saldo = saldo;
  }

  sacar(valor) {
    this.saldo -= valor;
  }
}

const conta = new ContaBancaria(100);
conta.saldo = -9999;  // ninguém deveria poder fazer isso diretamente
conta.sacar("50");    // "50" devia ser number — sem aviso nenhum
```

TypeScript adiciona tipos e modificadores de acesso às classes:

```ts
class ContaBancaria {
  private saldo: number;

  constructor(saldoInicial: number) {
    this.saldo = saldoInicial;
  }

  sacar(valor: number): void {
    this.saldo -= valor;
  }

  consultarSaldo(): number {
    return this.saldo;
  }
}

const conta = new ContaBancaria(100);
conta.saldo = -9999;     // ❌ 'saldo' é private, só acessível dentro da classe
conta.sacar("50");       // ❌ 'valor' precisa ser number
conta.consultarSaldo();  // 100
```

## public, private e protected

| Modificador | Quem acessa |
|---|---|
| `public` (padrão) | qualquer lugar |
| `private` | só dentro da própria classe |
| `protected` | a própria classe e suas subclasses |

```ts
class Animal {
  protected nome: string;

  constructor(nome: string) {
    this.nome = nome;
  }
}

class Cachorro extends Animal {
  latir(): string {
    return `${this.nome} está latindo`; // ok — protected libera acesso para a subclasse
  }
}

const rex = new Cachorro("Rex");
rex.nome; // ❌ 'nome' é protected, não acessível fora da classe
```

## readonly

```ts
class Usuario {
  readonly id: number;
  nome: string;

  constructor(id: number, nome: string) {
    this.id = id;
    this.nome = nome;
  }
}

const usuario = new Usuario(1, "Ana");
usuario.nome = "Ana Paula"; // ok
usuario.id = 2;             // ❌ id é readonly
```

## Getters e setters — leitura e escrita controladas

Volta ao `ContaBancaria` do início da aula: `consultarSaldo()` funciona, mas é essencialmente um getter escrito à mão. Um `get` faz a mesma leitura controlada, só que com sintaxe de propriedade em vez de método — e um `set` permite validar antes de escrever:

```ts
class ContaBancaria {
  private saldo: number;

  constructor(saldoInicial: number) {
    this.saldo = saldoInicial;
  }

  get saldoAtual(): number {
    return this.saldo;
  }

  set saldoAtual(valor: number) {
    if (valor < 0) throw new Error("saldo não pode ser negativo");
    this.saldo = valor;
  }
}

const conta = new ContaBancaria(100);
conta.saldoAtual;       // 100 — chama o get, mas parece acesso direto a uma propriedade
conta.saldoAtual = 200; // chama o set, com a validação no meio
conta.saldoAtual = -50; // erro em runtime — o set rejeitou antes de atribuir
```

`get`/`set` combinam bem com `private`: a propriedade real (`saldo`) fica escondida, e todo acesso de fora passa pelo método — sem a sintaxe de chamada com `()`.

## static — pertence à classe, não à instância

Um campo ou método `static` existe uma única vez, na classe em si, em vez de uma cópia por instância:

```ts
class Contador {
  static total = 0;

  constructor() {
    Contador.total++;
  }
}

new Contador();
new Contador();
console.log(Contador.total); // 2 — contado na classe, não em cada instância
```

Dentro da própria classe, um membro `static` também se acessa pelo nome da classe (`Contador.total`), nunca por `this` — `this` aponta para a instância, e um membro `static` não pertence a nenhuma instância específica.

## Parâmetros de construtor com modificador de acesso

Declarar a propriedade e atribuí-la no construtor é comum o bastante para ter um atalho: adicionar o modificador direto no parâmetro cria a propriedade automaticamente.

```ts
class Produto {
  constructor(
    public nome: string,
    private preco: number,
    readonly id: number
  ) {}

  aplicarDesconto(percentual: number): number {
    return this.preco - (this.preco * percentual) / 100;
  }
}

const produto = new Produto("Caneca", 20, 1);
produto.nome;  // ok — public
produto.preco; // ❌ preco é private
```

## implements — a classe cumpre um contrato

```ts
interface Notificavel {
  notificar(mensagem: string): void;
}

class EmailService implements Notificavel {
  notificar(mensagem: string): void {
    console.log(`Enviando e-mail: ${mensagem}`);
  }
}

class SemMetodo implements Notificavel {} // ❌ falta implementar 'notificar'
```

`implements` não herda nada, só obriga a classe a ter a forma descrita na interface — quem quiser reaproveitar implementação usa `extends`. Uma classe também pode cumprir mais de um contrato ao mesmo tempo: `class X implements A, B { ... }`.

## Para ir além: classes abstratas

`implements` obriga a forma sem fornecer nenhuma implementação; `extends` herda uma implementação já pronta. `abstract` fica no meio dos dois: uma classe abstrata pode ter métodos já implementados e métodos que só declara a assinatura, deixando a implementação para quem estender:

```ts
abstract class FormaGeometrica {
  abstract calcularArea(): number;

  descrever(): string {
    return `Área: ${this.calcularArea()}`; // usa um método que essa classe nem implementa
  }
}

class Quadrado extends FormaGeometrica {
  constructor(private lado: number) {
    super();
  }

  calcularArea(): number {
    return this.lado ** 2;
  }
}

new Quadrado(4).descrever(); // "Área: 16"
new FormaGeometrica();       // ❌ classe abstrata não pode ser instanciada diretamente
```

---

[← keyof, typeof e indexed access](./05-keyof-typeof-e-indexed-access.md) · [Menu](../../README.md#roadmap) · [Próximo: Módulos →](./07-modulos.md)
