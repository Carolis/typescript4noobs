# Como usar este guia

Este material é uma trilha: do básico ao avançado. A ordem dos módulos importa — cada aula assume que você viu a anterior.

## Pré-requisito

Você precisa de **JavaScript básico**: variáveis, funções, objetos e arrays. O TypeScript não ensina a programar do zero; ele ensina a **tipar** o JavaScript que você já conhece.

## Como seguir

O roadmap do README está neste formato:

1. **Conteúdo** (módulo) — Introdução, Ambiente, Básico…
2. **Sub-conteúdo** (aula) — um arquivo por assunto
3. Seções dentro da aula — títulos `##` quando o tema se parte (como os tipos de tipagem)

Vá na ordem. Se pular, algum exemplo vai parecer mágica.

No fim de cada aula há links para **anterior**, **menu** e **próximo**.

## Versões deste guia

Os exemplos daqui usam:

- **TypeScript 7.x**
- **Node.js 20** ou superior (recomendado: 20 ou 22 LTS)

Para conferir na sua máquina:

```bash
node -v
npx tsc -v
```

Se um exemplo **não funcionar**, a primeira coisa a checar é a versão. Pode ser:

- uma **funcionalidade nova** (o seu TypeScript é mais antigo que o do guia)
- uma **funcionalidade depreciada ou removida** (o seu TypeScript é mais novo, ou o contrário)

A instalação passo a passo fica no módulo **Ambiente**. Se ainda não quiser instalar nada, use o playground.

## Onde testar os exemplos

Todos os trechos desta trilha podem ser colados no [playground oficial do TypeScript](https://www.typescriptlang.org/play).

No computador, o editor mais amigável para começar é o **VS Code**. Outros editores também funcionam se tiverem o servidor de linguagem do TypeScript (no Vim, por exemplo, [coc.nvim](https://github.com/neoclide/coc.nvim)). Extensões úteis — como Pretty TypeScript Errors — entram na aula de editores, no módulo Ambiente.

## Dúvidas e contribuições

Sentiu falta de algum conteúdo ou encontrou um erro? Abra uma [issue](https://github.com/Carolis/typescript4noobs/issues) neste repositório.

---

[← Formas de tipagem](./02-formas-de-tipagem.md) · [Menu](../../README.md#roadmap) · [Próximo: Instalação →](../02-ambiente/01-instalacao.md)
