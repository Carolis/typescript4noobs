# Optional Chaining

---
O Optional Chaining é um operador que permite fazer a verificação de um objeto de uma maneira mais curta/simples, somente adicionando um ``?.`` antes de acessar a propriedade a ser testada.

Por exemplo:

```typescript
  const person = {
    firstName: 'Marcio',
    lastName: 'Rodrigues',
    animals: {
      dog: 'Eros',
      cat: 'Felicia'
    },
    company:
  }


  const dogName = person.animals?.dog;
  const companyName = person?.company;
```

No exemplo acima, criamos um objeto ``person`` que recebeu as características demonstradas acima. Abaixo foram criadas duas constantes que recebem o nome do cachorro e o nome da empresa em que ele trabalha, essas constantes podem ser usadas para o que o usuário bem queira, o optional chaining facilita a nossa vida porque, caso o objeto não tenha uma das propriedades chamadas, ele retornará `undefined ` e não um erro de referencia, parando assim a execução do nosso programa. 

Por exemplo:

```typescript
  console.log(dogName)
  console.log(companyName)
   
```

No caso do primeiro console.log, ele retornará `'Eros'` porque é o nome atribuído a `dog` e no caso do segundo onde queremos mostrar o `companyName` ele retornará `undefined` e não irá parar o programa, ele simplesmente irá dar um "curto-circuito" e vai retornar `undefined` mas sem ser um erro de referência, assim fazendo nosso programa continuar a executar.

---

<p align="center">
  <a href="https://github.com/Carolis/typescript4noobs#roadmap">VOLTAR PARA O MENU PRINCIPAL</a>
</p>
