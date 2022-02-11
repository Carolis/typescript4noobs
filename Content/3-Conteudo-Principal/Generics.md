# Generics no Typescript

## O que são Generics ?

Muito provavelmente você já se deparou com algum tipo de função ou método que pode receber qualquer tipo de variável como parâmetro não ?
Não é incomum no mundo do frontend você ter de consumir uma API na qual não tem certeza de que tipo de dado irá receber, ou então no backend
você precisar criar um método no qual deverá receber tipos genéricos de dados e então retornar algo.

No mundo do Javascript isso não seria tão complexo, afinal trata-se de uma linguagem fracamente tipada, porém isso gera problemas como abordados nos outros tópicos
desse repositório. O Typescript vem resolver essa questão, trazendo uma tipagem forte no runtime do desenvolvedor. Problema resolvido? Não exatamente.

Veja bem, as vezes precisamos criar métodos que precisam trabalhar com variáveis genéricas, ou seja algo **genérico**. Basta adicionarmos o type _any_ para a variável que queiramos trabalhar certo?

```javascript
function logger(variable: any): void {
  console.log(variable);
}

logger(' Hello WOrld');
logger(1234);
logger(null);
// Podemos receber QUALQUER coisa quando colocamos o tipo any, o que é um problema.
```

Todavia isso não é uma boa prática no mundo do Typescript e dependendo das configurações do seu compilador, sequer gerará o arquivo JS.

Se não podemos resolver usando o _any_, como podemos resolver? Para isso, foram criados os Genérics.

De forma sucinta, os genérics são uma anotação no método o qual sinaliza ao compilador que é possível receber qualquer tipo de variável naquele método. Porém isso não quer
dizer que o método não terá um tipo, apenas que devemos posteriormente definir o tipo daquela variável.

## Como usar os Generics ?

Vejamos abaixo a mesma função de antes, porém com o uso correto dos Generics.

```ts
function logger<T>(variable: T): void {
  console.log(variable);
}

logger<string>(' Hello WOrld');
logger<number>(1234);
```

É perceptível que o Generic cria um _"molde"_, o qual podemos definir para diversos tipos de variáveis e aumentar a componentização e flexibilização do nosso código
sem ferir os princípios do SOLID.

## Onde os Generics são usados ?

Generics não são novidade do Typescript, eles já são presentes em linguagens como Java ou C# faz um tempo. Porém, dentro do ecossistema do Javascript temos já algumas bibliotecas bem conhecidas que fazem uso desse recurso como por exemplo Axios.

Axios é uma biblioteca utilizada para realizar chamadas HTTP assincronas a alguma rota de uma API. No Javascript não precisariamos nos preocupar com a tipagem dessa chamada, todavia perderiamos a vantagem da segurança e legibilidade do código. Por outro lado, no Typescript, teriamos essas vantagens, entretanto como resolveriamos a questão de uma API poder devolver qualquer tipo de dado ?

Veja a resposta comparando os dois códigos.

```js
const Axios = require('axios');

const numbers = async () => await Axios.get('URL');

console.log(userList);

//Aqui estamos fazendo uma chamada para a API recebendo um array de numbers
```

```ts
import Axios from 'axios';

interface User {
  id: number;
  email: string;
}

const userList: User[] = async () => await Axios.get<User[]>('URL');

console.log(userList);

//Aqui estamos fazendo uma chamada para a API recebendo um Array de objs do tipo User.
```

Repare que no primeiro chamamos o método get do Axios para recuperar uma lista de números, no segundo usamos o **mesmo** método, porém agora conseguimos recuperar
uma lista de User, um tipo totalmente diferente de number. Desse modo, vemos que há uma flexibilidade do método get graças ao uso do Generic !

---

<p align="center">
  <a href="https://github.com/Carolis/typescript4noobs#roadmap">VOLTAR PARA O MENU PRINCIPAL</a>
</p>
