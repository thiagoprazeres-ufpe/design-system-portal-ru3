# Portal RU3 Design System

Design system do **Restaurante Universitário da UFPE** (Portal RU3). Tokens DTCG canônicos, marca, ilustrações e padrões mosaico — fonte da verdade é o tema WordPress oficial.

> **RU-only.** Identidade visual independente. Brasão UFPE, selos e assinaturas institucionais ficam fora do escopo (uso restrito ao fluxo de autenticação).

## Produção

| Recurso | URL |
|---|---|
| Portal de docs | https://thiagoprazeres-ufpe.github.io/design-system-portal-ru3/ |
| Plugin Penpot (manifest) | https://thiagoprazeres-ufpe.github.io/design-system-portal-ru3/plugin/manifest.json |
| Repo GitHub | https://github.com/thiagoprazeres-ufpe/design-system-portal-ru3 |
| Mirror GitLab | https://gitlab.ufpe.br/thiago.prazeres/design-system-portal-ru3 |
| Portal RU em produção | https://ru.ufpe.br |
| Tema WordPress | `wp-content/themes/ru-ufpe-theme` |

## Stack

| Camada | Tecnologia |
|---|---|
| Tokens canônicos | W3C DTCG (`ru.tokens.json`) — fonte do tema `ru-ufpe-theme` |
| Build de tokens | Script vanilla (`packages/tokens/build.js`) → CSS / JS / TS / Penpot JSON |
| Implementação visual | [Penpot](https://design.penpot.app) |
| Sincronização | `@ru/penpot-plugin` |
| Portal de docs | Vite + `@preact/signals-core` |
| CI / Deploy | GitHub Actions + GitHub Pages |
| Tipografia UI | Geist Variable |
| Tipografia arte legada | Trebuchet MS (apenas em peças impressas históricas) |

## Estrutura (monorepo pnpm)

```
design-system-portal-ru3/
├── packages/
│   ├── tokens/             # W3C DTCG — paleta RU completa
│   └── penpot-plugin/      # @ru/penpot-plugin
├── apps/
│   └── docs/               # portal zeroheight-style
├── public/
│   ├── marca/              # logos RU (horizontal claro/escuro, vertical, mono, institucional)
│   ├── illustrations/      # frutas, sobremesas, talheres e pratos
│   └── patterns/           # mosaico canônico + faixa de marca
├── penpot/                 # rpc + scripts publish/snapshot
├── .github/workflows/      # deploy-pages.yml
└── ROADMAP.md
```

## Início rápido

```bash
corepack enable && corepack prepare pnpm@9 --activate
pnpm install

pnpm tokens:build                    # gera CSS/JS/TS/Penpot JSON
pnpm dev                             # docs em localhost:5173
pnpm dev:plugin                      # plugin em localhost:5174
```

## Tokens — consumo

### CSS direto

```css
@import '@ru/tokens/css';

.botao-ru {
  background: var(--ru-color-primary);
  color: var(--ru-color-primary-content);
  font-family: var(--ru-font-family-ui);
  padding: var(--ru-space-3) var(--ru-space-6);
  border-radius: var(--ru-radius-md);
}

.cardapio-segunda { border-left: 4px solid var(--ru-color-day-segunda); }
.cardapio-terca   { border-left: 4px solid var(--ru-color-day-terca); }
```

### JavaScript / ESM

```js
import { tokens } from '@ru/tokens';

tokens.ru.color.brand.amarelo;       // '#EEAB1E'
tokens.ru.color.day.segunda;         // → amarelo
tokens.ru.font.family.ui;            // 'Geist Variable, ...'
```

## Paleta RU

5 famílias cromáticas × 3 tons + laranja accent:

- **Amarelo Ovo** — energia, sociabilidade
- **Verde Alface** — saúde, natureza
- **Azul Frescor** — refrescância, higiene
- **Vermelho Melancia** — força, apetite
- **Cinza Panela** — seriedade, modernidade
- **Laranja** — destaque/accent

Cada cor mapeia a estados semânticos (primary/secondary/accent + success/warning/error/info) e a dias da semana (cardápio).

## Marca RU

6 variantes em `public/marca/`:

- `brand-light.svg` — horizontal, texto escuro (fundos claros)
- `brand-dark.svg` — horizontal, texto branco (fundos escuros)
- `logo-ru-vertical.svg` — vertical
- `ru-ufpe.svg` — institucional UFPE + RU
- `logo-monochrome-horizontal-light.svg` / `vertical-light.svg` — monocromático

## Deploy

GitHub Actions (`.github/workflows/deploy-pages.yml`) builda e publica em GitHub Pages a cada push em `master`. Sem secrets externos — usa o `GITHUB_TOKEN` automático.

## Git LFS

PDFs, PNGs e arquivos `.penpot` versionados via Git LFS (`.gitattributes`). Clone com:

```bash
git lfs install
git clone https://github.com/thiagoprazeres-ufpe/design-system-portal-ru3.git
```

## Licença

Uso restrito a membros da UFPE / equipe do Restaurante Universitário.

## Contribuir

Veja [ROADMAP.md](./ROADMAP.md) + issues abertas no [GitHub](https://github.com/thiagoprazeres-ufpe/design-system-portal-ru3/issues).
