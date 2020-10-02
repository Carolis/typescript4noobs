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