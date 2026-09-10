# Instalação

Para rodar TypeScript na sua máquina, você precisa de duas coisas: **Node.js** e o pacote **typescript** dentro do projeto.

> **Versões deste guia:** TypeScript **7.x** e Node.js **20+**. Se algum exemplo não funcionar, confira `node -v` e `npx tsc -v` — pode ser recurso novo que sua versão ainda não tem, ou algo que foi depreciado.

## Node.js

Baixe em [nodejs.org](https://nodejs.org/). Para projetos novos com TypeScript 7, use Node **20** ou **22** LTS.

O requisito mínimo muda conforme a versão do TypeScript:

| TypeScript | Node.js mínimo |
|---|---|
| 7.x | 20.0+ |
| 6.x | 18.0+ |

Para checar o que você tem instalado:

```bash
node -v
```

Se estiver em um projeto legado preso no TS 6, Node 18 já resolve. Para qualquer coisa nova, vá de Node 20+.

## Instalar o TypeScript no projeto

A forma recomendada é instalar **dentro de cada projeto**, não globalmente. Assim todo mundo na equipe usa a mesma versão — e o CI também.

**1.** Crie uma pasta e inicialize o projeto (se ainda não tiver):

```bash
mkdir meu-projeto-ts
cd meu-projeto-ts
npm init -y
```

**2.** Instale o TypeScript como dependência de desenvolvimento:

```bash
npm install typescript --save-dev
```

O `--save-dev` (equivalente a `-D`) coloca o pacote em `devDependencies`. TypeScript é ferramenta de **desenvolvimento**: ele checa tipos e, se precisar, gera JavaScript — mas não vai para produção como dependência do app. Em runtime, quem roda é JS normal.

Com outros gerenciadores:

```bash
yarn add -D typescript
pnpm add -D typescript
```

**3.** Confira se instalou:

```bash
npx tsc -v
```

Deve aparecer algo como `Version 7.x.x`.

### Por que não instalar global?

`npm install -g typescript` até funciona, mas cada projeto pode precisar de uma versão diferente. Instalar local evita aquele "funciona na minha máquina" quando alguém está numa versão antiga do compilador.

## TypeScript 6 ou 7?

Para projeto novo, use sempre a **7.x** — é a versão atual e a que este guia assume.

```bash
npm install typescript --save-dev
```

Se o projeto legado exigir TS 6:

```bash
npm install typescript@6 --save-dev
```

A diferença prática: o TS 7 reescreveu o compilador em Go e ficou bem mais rápido. O TS 6 foi a última linha na arquitetura antiga e serve como ponte para projetos que ainda não migraram.

## E se eu usar Vite, Next ou outro framework?

Muitos templates já trazem TypeScript na instalação — você aceita quando o terminal pergunta e pronto. Mesmo assim, entender a instalação manual ajuda: você sabe o que está no `package.json` e consegue ajustar a versão quando precisar.

A configuração do compilador fica no `tsconfig.json` — na próxima aula.

---

[← Como usar este guia](../01-introducao/03-como-usar-este-guia.md) · [Menu](../../README.md#roadmap) · [Próximo: tsconfig →](./02-tsconfig.md)
