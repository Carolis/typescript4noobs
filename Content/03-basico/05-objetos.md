# Objetos

Objetos agrupam dados. No TypeScript, você descreve **quais propriedades existem** e **de que tipo** cada uma é.

## Tipagem inline

Sem criar um `type` ainda — só descrever o formato na hora:

```ts
const usuario = {
  nome: "Diego",
  idade: 30,
};

// TypeScript infere: { nome: string; idade: number }
```

Se você tentar acessar uma propriedade que não existe:

```ts
console.log(usuario.emial); // ❌ typo — 'emial' não existe
```

## Anotação explícita

Quando o objeto começa vazio ou você quer fixar o formato:

```ts
let pessoa: { nome: string; idade: number };

pessoa = { nome: "Ana", idade: 25 }; // ok
pessoa = { nome: "Ana" };            // ❌ falta idade
```



## Propriedade a mais

Outro erro comum: passar **informação demais** num objeto literal. O TypeScript rejeita propriedades que não existem no tipo — regra chamada *excess property check*. Ela vale na atribuição direta de um literal, não quando o objeto vem de outra variável:

```ts
let pessoa: { nome: string; idade: number };
pessoa = { nome: "Ana", idade: 25, cidade: "SP" }; // ❌ 'cidade' não existe no tipo
```

## Propriedade opcional

Com `?`, a propriedade pode faltar:

```ts
let perfil: { nome: string; bio?: string };

perfil = { nome: "Ana" };              // ok — bio é opcional
perfil = { nome: "Ana", bio: "dev" };  // ok
```



## readonly

Propriedade que não pode ser reatribuída depois de criada:

```ts
let config: { readonly id: number; nome: string } = {
  id: 1,
  nome: "app",
};

config.nome = "outro"; // ok
config.id = 2;         // ❌ id é readonly
```

`readonly` é **raso** em objetos aninhados: `readonly endereco: { rua: string }` impede trocar `config.endereco` inteiro, mas não impede `config.endereco.rua = "outra"`. Aprofundamos isso em conteúdo mais avançado.

## Objetos aninhados

Um objeto dentro de outro — cada nível com seu tipo:

```ts
const usuario = {
  nome: "Diego",
  endereco: { rua: "Rua A", numero: 100 },
};

// TypeScript infere: { nome: string; endereco: { rua: string; numero: number } }

console.log(usuario.endereco.numero);  // ok — 100
console.log(usuario.endereco.cep);     // ❌ 'cep' não existe
usuario.endereco = "outra coisa";      // ❌ tipo errado
```

Repare: se você tivesse mais de um usuário, teria que repetir esse formato de `endereco` em cada um — é exatamente esse problema que a [próxima aula](./06-type-aliases.md) resolve, com `type` para nomear o formato uma vez e reutilizar.

---

[← Funções](./04-funcoes.md) · [Menu](../../README.md#roadmap) · [Próximo: Type aliases →](./06-type-aliases.md)