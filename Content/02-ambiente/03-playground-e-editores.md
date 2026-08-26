# Playground, editores e extensões

Você não precisa instalar nada para começar a testar TypeScript. Mas, no dia a dia, um editor configurado faz diferença.

## Playground oficial

O [TypeScript Playground](https://www.typescriptlang.org/play) roda no navegador: você cola código, vê erros na hora e compara o JavaScript gerado ao lado.

Útil para:

- testar um trecho das aulas sem montar projeto
- entender o que o compilador **remove** ou **transforma** na saída
- compartilhar um exemplo (dá para gerar link)

Se ainda não instalou Node, dá para acompanhar boa parte da trilha só por aqui.

## VS Code

O [Visual Studio Code](https://code.visualstudio.com/) é o caminho mais simples para quem está começando. Ele já traz suporte a TypeScript embutido — autocomplete, sublinhado de erro, ir para definição.

Abra a pasta do projeto (a que tem o `tsconfig.json`) e o editor passa a usar as regras daquele arquivo.

### Extensão: Pretty TypeScript Errors

Erros do TypeScript podem ser longos e difíceis de ler no terminal. A extensão [Pretty TypeScript Errors](https://marketplace.visualstudio.com/items?itemName=YoavBls.pretty-ts-errors) reformata a mensagem no editor — fica mais claro **o que** está errado e **onde**.

Não é obrigatória, mas recomendamos instalar cedo. Você vai ver muitos erros de tipo enquanto aprende; ler eles com calma acelera o processo.

Para instalar: abra a aba Extensions no VS Code, busque `Pretty TypeScript Errors` e instale.

### Outras extensões (opcional)

- **Error Lens** — mostra o erro na linha, sem precisar passar o mouse
- **ESLint** — regras de qualidade de código (complementa o TypeScript, não substitui)

## Outros editores

Qualquer editor com **Language Server** do TypeScript funciona — Neovim com [coc.nvim](https://github.com/neoclide/coc.nvim), JetBrains, Zed, etc. O que importa é o projeto ter `tsconfig.json` e o editor enxergar a pasta certa.

---

Com ambiente pronto, partimos para o código: tipar variáveis, funções e objetos no módulo **Básico**.

---

[← tsconfig](./02-tsconfig.md) · [Menu](../../README.md#roadmap) · [Próximo: Anotações de tipo →](../03-basico/01-anotacoes-de-tipo.md)
