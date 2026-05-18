# AGENTS.md — Briefing para IA

Este repositório é um **laboratório de processo**, não uma galeria.
Você será avaliado pelo processo documentado, não só pelo artefato final.

## Ao adicionar um exemplo novo

1. Crie a pasta: `cp -r _template/ NN-slug-novo/`
2. Preencha o frontmatter do README antes de começar a implementar.
3. Salve `iterations/v1.html` como primeiro snapshot — mesmo que imperfeito.
4. A cada mudança significativa de abordagem (layout, paleta, estrutura): novo `vN.html`.
   "Significativa" = mudou direção visual. Ajuste de cor isolado não conta.
5. Quando satisfeito com vN, copie pra `index.html` da pasta.

> **Nota sobre deploy:** as iterações (`iterations/vN.html`) ficam no repositório como
> documentação de processo — não são deployadas automaticamente. Só o `index.html` de
> cada pasta aparece no live preview do GitHub Pages.

## Estrutura obrigatória de cada exemplo

```
NN-slug/
├── README.md          ← frontmatter YAML + seções obrigatórias (veja abaixo)
├── index.html         ← versão final standalone
└── iterations/
    ├── v1.html
    ├── v2.html
    └── v3.html        ← (quantas forem necessárias)
```

## Frontmatter obrigatório (README.md do exemplo)

```yaml
---
title: Nome Legível
date: YYYY-MM-DD
style: brutalism | pixel-art | low-poly | glassmorphism | ...
tags: [tag1, tag2]
techniques: [css-grid, threejs, webgl, ...]
process_pattern: from-scratch | skill-driven | reference-driven | iterative-refinement
starting_point: scratch | skill:nome | reference:url
ai_role: co-designer | gerador | refinador | executor
iterations: N
inspiration:
  - Referência 1
difficulty: N/5
---
```

## Seções obrigatórias no README do exemplo

- `## Conceito` — parágrafo curto
- `## Briefing inicial` — o pedido cru, sem editar
- `## Prompts e iterações` — um sub-heading por versão com resumo + `<details>` com prompt verbatim
- `## Decisões de processo` — bullets sobre escolhas feitas
- `## Aprendizados transferíveis` — bullets que vão pro PROCESS.md raiz

## Convenção de commits

Commits atômicos, um por exemplo finalizado:
```
feat: add NN-slug-conceito
```

## Destilação pro PROCESS.md

Depois de finalizar um exemplo, abra `PROCESS.md` e adicione os
aprendizados transferíveis sob o tema correto.
Cite o exemplo: `(visto em NN-slug)`.
