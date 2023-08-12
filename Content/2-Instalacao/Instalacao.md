# Instalando o TypeScript

PS: antes de seguir com a instalação do TypeScript é importante ter o **node** previamente instalado.

A instalação em si é super simples e pode ser feita com apenas esse comando abaixo:

`npm install -g typescript`

Para checar a versão instalada basta rodar `tsc -v`, assim teremos segurança de que ele realmente foi instalado.

Após instalado, é interessante rodarmos `tsc --init` no terminal para que um arquivo `tsconfig.json` seja gerado. Esse arquivo é responsável por ditar como o TypeScript irá se comportar no projeto: para qual versão do JavaScript ele vai compilar, quais diretórios ele deve jogar seus arquivos, se ele vai ser mais ou menos "chato" com os erros, etc.

---

# Extra: Instalação com Yarn

Você também pode inicializar seu projeto TypeScript usando o **Yarn** por questões de preferência.

Basta rodar:

`yarn init -y` para inicializar o Yarn em si no diretório

`yarn add -D typescript` para instalar o TypeScript

`yarn tsc --init` para gerar o arquivo `tsconfig.json`

# TypeScript + React

É possível inicializar um projeto react com um template para TypeScript de várias formas, uma delas se utilizando do vite com o template do TypeScript, usando os seguintes comandos:

#### yarn 
`yarn create vite my-tsreact-app --template react-ts`
#### npm 6.x 
`npm create vite@latest my-tsreact-app --template react-ts` 
#### npm 7.x 
`npm create vite@latest my-tsreact-app -- --template vue`

Exemplo de como fica um componente funcional com TypeScript:

```ts
import React, { FunctionComponent, useState } from 'react'

interface Props {
  message: string
}

const App: FunctionComponent<Props> = props => {
  const [hasMessage, setHasMessage] = useState<boolean>(false)
  return <p>{hasMessage ? props.message : 'Default Message'}</p>
}

export default App
```

# Typescript + React Native

Também é possível iniciar um projeto React Native com Typescript usando esse comando:
`npx react-native init MyApp --template react-native-template-typescript`

---

<p align="center">
  <a href="https://github.com/Carolis/typescript4noobs#roadmap">VOLTAR PARA O MENU PRINCIPAL</a>
</p>
