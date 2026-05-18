# Laboratório de Design Artístico com IA — Design Spec

**Data**: 2026-05-17
**Repositório**: [Iv4nLanna/Design-UX-Teste](https://github.com/Iv4nLanna/Design-UX-Teste)
**Autor**: Ivan Lanna

## Propósito

Este repositório é um **laboratório de processo**, não uma galeria de artefatos. O objetivo é descobrir o melhor processo de fazer design em software de forma artística e conceitual usando IA (Claude). Cada exemplo é um experimento documentado: o que foi pedido, como foi iterado, o que funcionou, o que virou aprendizado transferível.

Função dupla:
- **Showcase público**: vitrine via GitHub Pages mostrando designs criativos e os processos por trás.
- **Laboratório pessoal**: registro acumulativo de padrões de colaboração com IA pra design visual.

## Princípios

1. **Processo > artefato.** O `index.html` final é evidência; o `README.md` do exemplo é o experimento.
2. **Zero atrito técnico.** HTML/CSS/JS puro, dependências via CDN. Abre clicando, sem build.
3. **Auto-contido.** Cada pasta é um experimento isolado, sem dependências cruzadas.
4. **Reprodutível.** Prompts integrais ficam preservados em `<details>` pra qualquer um repetir.
5. **Disciplina de versão.** Toda iteração visual significativa é salva como snapshot.
6. **Destilação contínua.** Aprendizados de cada experimento sobem pra um `PROCESS.md` raiz.

## Estrutura do repositório

```
Design-UX-Teste/
├── README.md                          # vitrine: lista de exemplos + links live
├── PROCESS.md                         # aprendizados acumulados sobre processo
├── .github/workflows/pages.yml        # deploy automático GitHub Pages
├── _template/                         # esqueleto pra novos exemplos
│   ├── README.md
│   └── index.html
├── 01-brutalist-archive/
│   ├── README.md                      # experimento documentado
│   ├── index.html                     # versão final
│   └── iterations/
│       ├── v1.html
│       ├── v2.html
│       └── v3.html
├── 02-pixel-8bit/
└── 03-low-poly-3d/
```

### Convenção de nomes

Pastas seguem `NN-slug-kebab`:
- `NN` = número sequencial de criação (01, 02, ...). Dá ordem cronológica visível.
- `slug-kebab` = nome curto e descritivo do conceito.

Pastas são auto-contidas, então renomear é trivial.

## Anatomia de um exemplo

### `index.html`

- Standalone. Tudo inline ou via CDN (Three.js, Google Fonts, etc).
- Zero `npm install`, zero etapa de build.
- Funciona ao abrir o arquivo direto no browser (sem servidor, salvo casos que exigem CORS).

### `README.md` do exemplo

Estrutura obrigatória:

```markdown
---
title: Brutalist Archive
date: 2026-05-17
style: brutalism
tags: [editorial, typography, monochrome]
techniques: [css-grid, custom-cursor, ascii-scroll]
process_pattern: iterative-refinement
ai_role: co-designer
iterations: 3
inspiration:
  - Bloomberg Businessweek
  - Berlin gallery sites
difficulty: 3/5
---

## Conceito
Parágrafo curto descrevendo a ideia visual e o ângulo conceitual.

## Briefing inicial
O pedido cru, do jeito que você deu pro Claude na primeira vez.

## Prompts e iterações

### v1 — primeira tentativa
Resumo: o que pedi e o que recebi.

<details>
<summary>Prompt completo v1</summary>

(prompt verbatim aqui)

</details>

**O que faltou**: bullets curtos.

### v2 — ajuste de X
Resumo: ...

<details>
<summary>Prompt completo v2</summary>

...

</details>

**O que faltou**: ...

### v3 — versão final
...

## Decisões de processo
- Quando usei referência visual vs descrição textual
- Quando deixei o Claude propor vs executar
- O que precisei micro-gerenciar

## Aprendizados transferíveis
- Aprendizado 1 (vai pra PROCESS.md)
- Aprendizado 2
```

### Pasta `iterations/`

- Toda iteração visualmente significativa salva como `vN.html`.
- "Significativa" = mudou abordagem, layout ou direção visual — não troca de cor isolada.
- Disciplina rígida desde o começo: melhor salvar demais que de menos.

## Frontmatter — campos padronizados

| Campo | Valores | Propósito |
|---|---|---|
| `title` | string livre | Nome legível do exemplo |
| `date` | ISO YYYY-MM-DD | Quando foi criado |
| `style` | brutalism, glassmorphism, claymorphism, pixel-art, low-poly, swiss, vaporwave, ... | Estilo visual principal |
| `tags` | array livre | Atributos descritivos |
| `techniques` | array livre | Tecnologias/técnicas usadas (css-grid, threejs, webgl, svg-animation, ...) |
| `process_pattern` | iterative-refinement, one-shot, reference-driven, conversational-design | Como o processo se desenrolou |
| `ai_role` | co-designer, gerador, refinador, executor | Papel do Claude nesse experimento |
| `iterations` | número | Quantas rodadas significativas |
| `inspiration` | array livre | Referências visuais externas |
| `difficulty` | 1/5 — 5/5 | Quão difícil foi chegar no resultado |

`process_pattern` é o eixo mais importante pro laboratório — é o que vamos cruzar pra encontrar padrões.

## README raiz

Estrutura:

1. **Hero curto** — uma frase explicando o que é o repo.
2. **Tabela de exemplos** — colunas: número, nome, estilo, link live preview, link README.
3. **Link pro PROCESS.md** — "Veja os aprendizados acumulados sobre processo".
4. **Como contribuir / replicar** — passos rápidos pra clonar um exemplo de template.

Atualizado à mão. Com volume baixo (~10-20 exemplos no horizonte), gerador automático seria over-engineering.

## PROCESS.md raiz

Documento vivo onde aprendizados transferíveis de cada exemplo são destilados em regras gerais. Organizado por temas, não cronologicamente:

```markdown
# Processo de Design Artístico com IA — Aprendizados

## Sobre briefing inicial
- ...

## Sobre referências visuais
- ...

## Sobre quando deixar o Claude liderar
- ...

## Sobre iteração
- ...

## Sobre limites técnicos (CSS, WebGL, etc)
- ...
```

Cada bullet pode citar exemplos: `(visto em 01-brutalist-archive, 03-low-poly-3d)`.

## Deploy

GitHub Pages, branch `main`, root do repositório. Workflow mínimo em `.github/workflows/pages.yml`. URLs ficam:

- `https://iv4nlanna.github.io/Design-UX-Teste/` → README/index (GitHub renderiza markdown)
- `https://iv4nlanna.github.io/Design-UX-Teste/01-brutalist-archive/` → exemplo live

## Workflow pra adicionar exemplo novo

1. `cp -r _template/ NN-novo-conceito/`
2. Preencher briefing inicial no README
3. Iterar com Claude — salvar cada `vN.html` significativa em `iterations/`
4. Atualizar README do exemplo: prompts (resumo + `<details>`), decisões, aprendizados
5. Promover versão final pra `index.html` da pasta
6. Adicionar linha na tabela do README raiz
7. Destilar aprendizados pro `PROCESS.md`
8. Commit atômico: `feat: add NN-novo-conceito`

## Seed inicial (3 exemplos)

### 01-brutalist-archive
Editorial brutalista anos 90: Helvetica gigante, grid quebrado de propósito, cores monocromáticas com 1 acento neon, cursor customizado, animações ASCII no scroll. Inspiração: Bloomberg Businessweek, sites de galerias berlinenses.

**Ângulo de processo**: testa quão bem o Claude lida com composição tipográfica ousada e quebra intencional de grid.

### 02-pixel-8bit
Estética 8-bit / pixel art. Fonte pixel (Press Start 2P via CDN), `image-rendering: pixelated`, paleta NES limitada (~16 cores), animações frame-by-frame em sprite sheets ou CSS keyframes discretas. Pode ser uma landing page de "jogo fictício" ou portfólio retrô.

**Ângulo de processo**: testa fidelidade do Claude a constraints estilísticos rígidos (paleta limitada, pixel-perfect).

### 03-low-poly-3d
Three.js via CDN, geometria facetada estilo origami, paleta saturada (8-10 cores), iluminação flat. Cena interativa girando lentamente, reage ao mouse. Vibe Figma Config / Notion.

**Ângulo de processo**: testa colaboração em código 3D — onde Claude geralmente precisa de mais micro-gerenciamento.

## Fora do escopo (YAGNI)

- Build system / bundler.
- Framework JS (React, Vue, etc).
- Gerador automático do README raiz.
- Testes automatizados.
- Sistema de comentários ou feedback.
- Tradução multi-idioma.

## Critério de sucesso

Em ~10 exemplos, o `PROCESS.md` deve conter regras que ajudem a chegar num design satisfatório com menos iterações que no primeiro. Se isso não estiver acontecendo, o formato do laboratório precisa ser revisto.
