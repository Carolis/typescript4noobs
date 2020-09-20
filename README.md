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
 
Aviso: Este projeto tem como intenção ser um apoio aos cursos de react desenvolvidos pelo projeto 4noobs, portanto, os exemplos aqui citados estarão preferencialmente inseridos nesse ecossistema.

## O que é o Typescript?

Typescript é considerado um **superset** da linguagem Javascript, dito isso, se você já sabe Javascript é muito fácil de começar a usá-lo já sabendo um pouco. 
Ele tem como  principal funcionalidade a capacidade de adicionar **tipagens estáticas** ao código. 
Um dos pontos positivos que vale a pena ser citado é a possibilidade de termos arquivos Typescript convivendo no mesmo projeto com arquivos Javascript já que no final das contas o Typescript é compilado para Javascript, ou seja, é uma ferramenta de **desenvolvimento**. Isso também permite que você adicione Typescript em qualquer momento do seu projeto, conforme necessidade e gosto pessoal.

## Por que usar Typescript?

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

Outra grande vantagem de usar o Typescript é o aumento da inteligência dentro do seu editor ou IDE, o famoso **[IntelliSense](https://code.visualstudio.com/docs/editor/intellisense)**. Além disso, as tipagens podem funcionar como uma mini documentação dentro do seu arquivo, facilitando futuras manutenções e fazendo com que todos esses fatores tragam uma camada a mais de segurança para o código.

## Por que não usar apenas PropTypes?

O PropTypes funciona de uma forma muito mais passiva dentro de um projeto, sendo passível de ser facilmente ignorado, o que não é o caso do Typescript que desfruta de uma série de ferramentas e arquivos de configuração (`.tsconfig`) para que você faça ele se comportar de uma forma mais ativa impedindo que você dê continuidade à execução ao se deparar com um erro.

## Como Contribuir

Contribuições fazem com que a comunidade open source seja um lugar incrível para aprender, inspirar e criar. Todas contribuições
são **extremamente apreciadas**

1. Realize um Fork do projeto
2. Crie um branch com a nova feature (`git checkout -b feature/featureBraba`)
3. Realize o Commit (`git commit -m 'Add some featureBraba'`)
4. Realize o Push no Branch (`git push origin feature/featureBraba`)
5. Abra um Pull Request

## Autores

- **Carolina Ale** - _Developer & Member of He4rt Developers_  - [Twitter](https://twitter.com/caroliscaroles) - [Github](https://github.com/Carolis)

<p align="center">Made with 💜</p>

---

<p align="center">
  <a href="https://github.com/he4rt/4noobs" target="_blank">
    <img src="./.github/images/footer_4noobs.svg" width="380">
  </a>
</p>