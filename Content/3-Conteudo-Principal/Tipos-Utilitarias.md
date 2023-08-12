## Tipos Utilitários

Várias tipos utilitários são fornecidos pelo TypeScript para facilitar as transformações de tipos comuns. 
Esses tipos são acessíveis em escala global.

Os mais conhecidos são Partial, Required, Readonly e NonNullable. 

Temos vários exemplos como:

- Partial
- Required
- Exclude
- Record
- Awaited
- Readonly
- Pick
- Omit
- Extract
- NonNullable
- Parameters
- ConstructorParameters
- ReturnType
- InstanceType
- ThisParameterType
- OmitThisParameter
- ThisType

### Partial

Cria um tipo com todas as propriedades de Type definidas como opcionais. Ao usar este utilitário, um tipo que representa todos os subconjuntos de um determinado tipo será retornado.

```ts
// declarando a interface Geladeira
interface Geladeira {
  nome: string;
  descricao: string;
  modelo: string;
  funcionalidades: string[]; 
}
```

Se eu quiser utilizar a interface Geladeira mas por algum motivo só quero utilizar parcialmente meu tipo sem ter que criar um novo ou colocar alguma propriedade como opcional

```ts
let modelo:Partial<Geladeira> = { modelo: "French Door" } 
```

Partial é projetado para interagir com interfaces ou tipos personalizados que são declarados como objetos, como nosso tipo de geladeira acima, assim como muitos outros tipos de utilitários no TypeScript. Portanto, não se aplica a coisas como variáveis.

### Required

Cria um tipo com todas as características de Tipo definidas como necessárias. Mesmo que o tipo original declare algumas das características como opcionais, ocasionalmente precisamos garantir que um objeto tenha essas características.

```ts
interface Veiculo {
  descricao?: string;
  marca?: string; 
  motor?: string;
  portas?: number;
}
```

Agora vamos a utilizar Veiculo pero precisamos de todas as informações num objeto.

```ts

let car:Required<Veiculo> = {
  descricao: 'Skyline azul com preto';
  marca: 'nissan'; 
  motor: '3.8 gasolina';
  portas: '2';
}
```

O tipo Required pode nos dar maior adaptabilidade, ao mesmo tempo que nos permite atender às necessidades de campo para utilidade específica em uma aplicação. Da mesma forma que outros tipos de utilitários, Required destina-se a trabalhar com um tipo opcional, semelhante ao tipo de Veiculo que caracterizamos anteriormente.

---

<p align="center">
  <a href="https://github.com/Carolis/typescript4noobs#roadmap">VOLTAR PARA O MENU PRINCIPAL</a>
</p>