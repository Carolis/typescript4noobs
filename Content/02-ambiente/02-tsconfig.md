# tsconfig.json

Depois de instalar o TypeScript, o próximo passo é dizer **como** ele se comporta no seu projeto. Isso vai no arquivo `tsconfig.json`, na raiz da pasta.

## Gerando o arquivo

Dentro do projeto:

```bash
npx tsc --init
```

O comando cria um `tsconfig.json` com opções padrão — muitas comentadas. Você não precisa entender tudo de uma vez; comece pelas que importam no dia a dia.

## O que o tsconfig faz

Pense nele como o "manual de regras" do compilador:

- quão **rigoroso** ele é com erros de tipo
- quais **pastas e arquivos** ele analisa
- para qual versão de **JavaScript** converter (quando ele emite código)
- se ele **só checa tipos** ou também **gera arquivos `.js`**

Sem esse arquivo, o `tsc` não sabe onde olhar. Com ele, o editor (VS Code, por exemplo) usa as mesmas regras — autocomplete e erros ficam alinhados com o que o compilador faria.

## Opções que você vai ver o tempo todo

Dois cenários comuns — e configs diferentes para cada um.

**Estudo ou Node simples** — o TypeScript gera o JavaScript:

```json
{
  "compilerOptions": {
    "strict": true,
    "target": "ES2022",
    "module": "NodeNext",
    "moduleResolution": "NodeNext",
    "rootDir": "./src",
    "outDir": "./dist"
  },
  "include": ["src"]
}
```

`NodeNext` é a opção recomendada para Node moderno — lida melhor com `import`/`export` e a mistura de módulos ESM e CommonJS que você ainda encontra por aí. Em tutoriais mais antigos, é comum ver `"module": "CommonJS"`; funciona, mas reflete o modelo antigo do Node.

**Vite, Next, webpack** — o bundler transforma o código; o TS só checa tipos:

```json
{
  "compilerOptions": {
    "strict": true,
    "target": "ES2022",
    "module": "ESNext",
    "noEmit": true
  },
  "include": ["src"]
}
```

Repare: no segundo exemplo não tem `outDir`. Com `noEmit: true`, o TypeScript **não gera nenhum arquivo** — `outDir` ficaria sem efeito.

| Opção | O que faz |
|---|---|
| `strict` | Liga o modo rigoroso — `null`/`undefined`, `any` implícito e outros checks extras. **Deixe ligado** em projeto novo. |
| `include` | Quais arquivos/pastas o TypeScript analisa. |
| `noEmit` | Só checa tipos, **não gera** `.js`. Use `true` quando um bundler cuida da transformação. |
| `target` | Versão do JavaScript na saída, quando o `tsc` gera código. |
| `module` | Sistema de módulos na saída (`NodeNext` no Node, `ESNext` com bundler). |
| `rootDir` | Pasta onde está o seu código TypeScript. |
| `outDir` | Pasta onde o JavaScript gerado vai parar — só faz sentido quando `noEmit` está desligado. |
| `exclude` | O que ignorar (padrão inclui `node_modules`). |

### `strict`: vale a pena?

Sim. Com `strict: true`, o TypeScript pega erros que passariam batido — variável `undefined`, parâmetro esquecido, propriedade que não existe.

Desde o **TypeScript 6**, o compilador assume `strict` ligado mesmo que você não coloque nada no `tsconfig`. O `tsc --init` também costuma deixar `"strict": true` explícito no arquivo gerado — mais clareza do que necessidade.

Se um projeto antigo estiver com `strict: false`, migrar para `true` pode gerar muitos erros de uma vez. Dá para ir ligando opções individuais (`strictNullChecks`, `noImplicitAny`…) aos poucos.

### `noEmit` vs emitir JavaScript

**Projeto simples (Node ou estudo):** o `tsc` gera o `.js` sozinho. `noEmit` fica `false` (ou omitido) e você usa `outDir`.

**Projeto com Vite, Next, webpack:** o bundler cuida da transformação. O TypeScript **só checa tipos** — `noEmit: true`. Sem isso, o TypeScript geraria `.js` que ninguém usa — o bundler já faz esse trabalho.

## Rodando o compilador

Para checar o projeto inteiro:

```bash
npx tsc
```

Com `noEmit: true`, ele só reporta erros. Sem, gera os arquivos em `outDir`.

Para compilar um arquivo avulso (sem tsconfig):

```bash
npx tsc arquivo.ts
```

Na prática, quase todo projeto usa `tsconfig.json` — é mais previsível.

## Ajustando aos poucos

O `tsconfig.json` gerado pelo `--init` traz dezenas de opções comentadas. Não precisa descomentar tudo. Comece com `strict`, `include` e `noEmit` (se usar bundler). O resto você descobre quando o projeto pedir — paths alias, `jsx` (se for usar React), `lib` para APIs do browser, etc.

Na próxima aula: onde testar código sem instalar nada, e extensões que deixam o dia a dia mais confortável.

---

[← Instalação](./01-instalacao.md) · [Menu](../../README.md#roadmap) · [Próximo: Playground e editores →](./03-playground-e-editores.md)
