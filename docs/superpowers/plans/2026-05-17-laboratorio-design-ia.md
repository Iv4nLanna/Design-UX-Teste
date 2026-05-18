# Laboratório de Design Artístico com IA — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Criar o repositório Design-UX-Teste com estrutura de laboratório de processo + 3 exemplos seed (Brutalist Archive, Pixel 8-bit, Low-poly 3D) totalmente documentados e deployados no GitHub Pages.

**Architecture:** Repositório estático puro — HTML/CSS/JS standalone por pasta, sem build step. Cada exemplo é auto-contido com iterações salvas em `iterations/` e documentação de processo em `README.md`. Aprendizados transferíveis acumulam no `PROCESS.md` raiz. AGENTS.md orienta IAs futuras.

**Tech Stack:** HTML5, CSS3, vanilla JS, Three.js r160 (via importmap/CDN) para o exemplo 3D, Press Start 2P via Google Fonts, GitHub Pages (deploy automático via workflow).

---

## Mapa de arquivos

```
Criar:
  README.md                                    ← vitrine raiz
  AGENTS.md                                    ← briefing pra IA
  PROCESS.md                                   ← aprendizados acumulados
  .github/workflows/pages.yml                  ← deploy GitHub Pages
  _template/README.md                          ← template de exemplo
  _template/index.html                         ← HTML stub
  01-brutalist-archive/README.md               ← doc do experimento
  01-brutalist-archive/iterations/v1.html      ← 1ª iteração
  01-brutalist-archive/iterations/v2.html      ← 2ª iteração
  01-brutalist-archive/iterations/v3.html      ← 3ª iteração (final)
  01-brutalist-archive/index.html              ← cópia do v3
  02-pixel-8bit/README.md
  02-pixel-8bit/iterations/v1.html
  02-pixel-8bit/iterations/v2.html
  02-pixel-8bit/iterations/v3.html
  02-pixel-8bit/index.html
  03-low-poly-3d/README.md
  03-low-poly-3d/iterations/v1.html
  03-low-poly-3d/iterations/v2.html
  03-low-poly-3d/iterations/v3.html
  03-low-poly-3d/index.html
```

---

## Task 1: Skeleton do repositório

**Files:**
- Create: `README.md`
- Create: `AGENTS.md`
- Create: `PROCESS.md`
- Create: `.github/workflows/pages.yml`
- Create: `_template/README.md`
- Create: `_template/index.html`

- [ ] **Step 1.1: Criar README.md raiz**

```markdown
# Design-UX-Teste

Laboratório de processo — não uma galeria. O objetivo é descobrir o melhor
processo de fazer design artístico e conceitual em software usando IA (Claude).
Cada pasta é um experimento documentado: o briefing, as iterações, o que
funcionou e o que virou aprendizado transferível.

→ [Aprendizados acumulados de processo](PROCESS.md)

## Exemplos

| N° | Conceito | Estilo | Live Preview | Processo |
|----|----------|--------|--------------|----------|
| 01 | Brutalist Archive | brutalism | [abrir](https://iv4nlanna.github.io/Design-UX-Teste/01-brutalist-archive/) | [README](01-brutalist-archive/README.md) |
| 02 | Pixel 8-bit | pixel-art | [abrir](https://iv4nlanna.github.io/Design-UX-Teste/02-pixel-8bit/) | [README](02-pixel-8bit/README.md) |
| 03 | Low-poly 3D | low-poly | [abrir](https://iv4nlanna.github.io/Design-UX-Teste/03-low-poly-3d/) | [README](03-low-poly-3d/README.md) |

## Como adicionar um exemplo

```bash
cp -r _template/ NN-novo-conceito/
# edite _template/README.md com seu briefing
# itere com Claude — salve cada iteração significativa em iterations/vN.html
# copie a versão final pra index.html
# adicione linha na tabela acima
# desfile aprendizados pra PROCESS.md
git add . && git commit -m "feat: add NN-novo-conceito"
```

## Sobre este laboratório

- **Processo > artefato.** O index.html final é evidência; o README é o experimento.
- **Zero atrito.** HTML/CSS/JS puro, CDN only. Abre clicando.
- **Reprodutível.** Prompts completos preservados em `<details>` por iteração.
- Spec: [docs/superpowers/specs/](docs/superpowers/specs/)
```

- [ ] **Step 1.2: Criar AGENTS.md**

```markdown
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
```

- [ ] **Step 1.3: Criar PROCESS.md (esqueleto vivo)**

```markdown
# Processo de Design Artístico com IA — Aprendizados

Documento vivo. Cada exemplo finalizado contribui bullets aqui.
Organizado por tema, não por ordem cronológica.

## Sobre briefing inicial

_Nenhum aprendizado ainda. Será preenchido após os exemplos seed._

## Sobre referências visuais

_Nenhum aprendizado ainda._

## Sobre quando deixar o Claude liderar vs micro-gerenciar

_Nenhum aprendizado ainda._

## Sobre iteração e convergência

_Nenhum aprendizado ainda._

## Sobre limites técnicos (CSS, WebGL, animações)

_Nenhum aprendizado ainda._

## Sobre constraints estilísticos rígidos

_Nenhum aprendizado ainda._

---

_Exemplos contribuídos: nenhum ainda._
```

- [ ] **Step 1.4: Criar .github/workflows/pages.yml**

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: pages
  cancel-in-progress: false

jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/configure-pages@v4
      - uses: actions/upload-pages-artifact@v3
        with:
          path: '.'
      - id: deployment
        uses: actions/deploy-pages@v4
```

- [ ] **Step 1.5: Criar _template/README.md**

```markdown
---
title: TÍTULO DO EXPERIMENTO
date: YYYY-MM-DD
style: ESTILO
tags: []
techniques: []
process_pattern: from-scratch
starting_point: scratch
ai_role: co-designer
iterations: 1
inspiration: []
difficulty: ?/5
---

## Conceito

_Descreva a ideia visual e o ângulo conceitual._

## Briefing inicial

_Cole aqui o pedido original dado ao Claude, sem editar._

## Prompts e iterações

### v1 — primeira tentativa

Resumo: _o que pedi e o que recebi._

<details>
<summary>Prompt completo v1</summary>

_Prompt verbatim aqui._

</details>

**O que faltou:**
- ...

## Decisões de processo

- _Quando usei referência vs descrição textual_
- _Quando deixei o Claude propor vs executar_
- _O que precisei micro-gerenciar_

## Aprendizados transferíveis

- ...
```

- [ ] **Step 1.6: Criar _template/index.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>DESIGN EXPERIMENT</title>
  <style>
    body { margin: 0; background: #111; color: #eee; font-family: sans-serif;
           display: flex; align-items: center; justify-content: center; min-height: 100vh; }
    h1 { font-size: clamp(2rem, 8vw, 6rem); text-align: center; }
  </style>
</head>
<body>
  <h1>EXPERIMENT<br>STARTS HERE</h1>
</body>
</html>
```

- [ ] **Step 1.7: Commit do skeleton**

```bash
git add README.md AGENTS.md PROCESS.md .github/ _template/
git commit -m "feat: scaffold laboratorio de design — skeleton inicial"
```

Expected: commit criado, nenhum erro.

---

## Task 2: Exemplo 01 — Brutalist Archive

**Conceito:** Landing editorial brutalista anos 90. Helvetica gigante, grid quebrado de propósito, preto/branco + 1 acento neon (#ff2d00), cursor customizado, ASCII art com scroll reveal. Testa: composição tipográfica ousada e quebra intencional de grid com IA do zero.

**Files:**
- Create: `01-brutalist-archive/iterations/v1.html`
- Create: `01-brutalist-archive/iterations/v2.html`
- Create: `01-brutalist-archive/iterations/v3.html`
- Create: `01-brutalist-archive/index.html`
- Create: `01-brutalist-archive/README.md`

- [ ] **Step 2.1: Criar diretórios**

```bash
mkdir -p 01-brutalist-archive/iterations
```

- [ ] **Step 2.2: Criar v1.html — layout base**

`01-brutalist-archive/iterations/v1.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>BRUTALIST ARCHIVE — N°01</title>
  <style>
    *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }
    :root { --bk: #0a0a0a; --wh: #f0ede8; --ac: #ff2d00; }

    body { background: var(--wh); color: var(--bk);
           font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; cursor: none; }

    #cur { position: fixed; width: 14px; height: 14px; background: var(--bk);
           pointer-events: none; z-index: 9999; mix-blend-mode: difference; }

    /* Hero */
    .hero { min-height: 100vh; display: grid;
            grid-template-columns: 5rem 1fr 5rem;
            grid-template-rows: 1fr auto; border-bottom: 2px solid var(--bk); }
    .sidebar { border-right: 2px solid var(--bk); padding: 2rem 1rem;
               writing-mode: vertical-rl; font-size: .6rem;
               letter-spacing: .3em; text-transform: uppercase; }
    .title { padding: 3rem 2rem; font-size: clamp(5rem, 18vw, 16rem);
             font-weight: 900; line-height: .85; text-transform: uppercase;
             letter-spacing: -.04em; align-self: center; }
    .title .ac { color: var(--ac); }
    .num { border-left: 2px solid var(--bk); padding: 2rem 1rem;
           font-size: .6rem; text-align: right; }
    .bar { grid-column: 1 / 4; border-top: 2px solid var(--bk); padding: 1.5rem 2rem;
           font-size: .7rem; letter-spacing: .25em; text-transform: uppercase;
           display: flex; justify-content: space-between; }

    /* Grid section */
    .grid { display: grid; grid-template-columns: repeat(6, 1fr); }
    .cell { border-right: 2px solid var(--bk); border-bottom: 2px solid var(--bk);
            padding: 2rem 1.5rem; display: flex; flex-direction: column;
            justify-content: flex-end; min-height: 28vh; }
    .cell:nth-child(1) { grid-column: span 3; background: var(--bk); color: var(--wh); }
    .cell:nth-child(2) { grid-column: span 1; background: var(--ac); }
    .cell:nth-child(3) { grid-column: span 2; }
    .cell:nth-child(4) { grid-column: span 2; }
    .cell:nth-child(5) { grid-column: span 4; border-right: none; }
    .ct { font-size: clamp(1.8rem, 4vw, 4rem); font-weight: 900;
          line-height: .9; text-transform: uppercase; }
    .cm { font-size: .6rem; letter-spacing: .3em; text-transform: uppercase;
          margin-top: .75rem; opacity: .5; }

    /* ASCII section */
    .ascii { background: var(--bk); color: var(--wh); padding: 4rem 2rem;
             border-bottom: 2px solid var(--bk); overflow: hidden; }
    .ascii pre { font-family: 'Courier New', monospace;
                 font-size: clamp(.35rem, 1vw, .65rem); line-height: 1.2; white-space: pre;
                 opacity: 0; transform: translateY(30px);
                 transition: opacity .9s ease, transform .9s ease; }
    .ascii pre.vis { opacity: 1; transform: none; }

    /* Footer */
    footer { display: grid; grid-template-columns: 1fr 1fr 1fr; }
    .fc { padding: 2rem; border-right: 2px solid var(--bk); }
    .fc:last-child { border-right: none; }
    .fl { font-size: .6rem; letter-spacing: .3em; text-transform: uppercase; opacity: .4; margin-bottom: .5rem; }
    .fv { font-size: clamp(.9rem, 2vw, 1.5rem); font-weight: 800; text-transform: uppercase; }
  </style>
</head>
<body>
<div id="cur"></div>

<header class="hero">
  <div class="sidebar">Design Archive · Vol. 01 · 2026</div>
  <h1 class="title">BRU<br><span class="ac">TAL</span><br>ISM</h1>
  <div class="num"><p>N°01</p><p>2026</p></div>
  <div class="bar">
    <span>Editorial Web Design Lab</span>
    <span>Claude × Ivan Lanna</span>
    <span>HTML/CSS/JS</span>
  </div>
</header>

<section class="grid">
  <div class="cell"><p class="ct">Type<br>over<br>image</p><p class="cm">§001 — Grid</p></div>
  <div class="cell"><p class="ct">Acc</p><p class="cm">§002</p></div>
  <div class="cell"><p class="ct">White<br>space<br>is a lie</p><p class="cm">§003 — Tension</p></div>
  <div class="cell"><p class="ct">Sys<br>tem</p><p class="cm">§004 — Type</p></div>
  <div class="cell"><p class="ct">Break the grid<br>on purpose</p><p class="cm">§005 — Intent</p></div>
</section>

<section class="ascii" id="ascii">
  <pre id="apre">
██████╗ ██████╗ ██╗   ██╗████████╗ █████╗ ██╗     ██╗███████╗███╗   ███╗
██╔══██╗██╔══██╗██║   ██║╚══██╔══╝██╔══██╗██║     ██║██╔════╝████╗ ████║
██████╔╝██████╔╝██║   ██║   ██║   ███████║██║     ██║███████╗██╔████╔██║
██╔══██╗██╔══██╗██║   ██║   ██║   ██╔══██║██║     ██║╚════██║██║╚██╔╝██║
██████╔╝██║  ██║╚██████╔╝   ██║   ██║  ██║███████╗██║███████║██║ ╚═╝ ██║
╚═════╝ ╚═╝  ╚═╝ ╚═════╝    ╚═╝   ╚═╝  ╚═╝╚══════╝╚═╝╚══════╝╚═╝     ╚═╝
  </pre>
</section>

<footer>
  <div class="fc"><p class="fl">Process</p><p class="fv">From Scratch</p></div>
  <div class="fc"><p class="fl">AI Role</p><p class="fv">Co-Designer</p></div>
  <div class="fc"><p class="fl">Iteration</p><p class="fv">V.01</p></div>
</footer>

<script>
  const cur = document.getElementById('cur');
  document.addEventListener('mousemove', e => {
    cur.style.left = (e.clientX - 7) + 'px';
    cur.style.top  = (e.clientY - 7) + 'px';
  });
  new IntersectionObserver(entries => {
    if (entries[0].isIntersecting) document.getElementById('apre').classList.add('vis');
  }, { threshold: .2 }).observe(document.getElementById('ascii'));
</script>
</body>
</html>
```

- [ ] **Step 2.3: Verificar v1 no browser**

```bash
open 01-brutalist-archive/iterations/v1.html   # macOS
# Linux: xdg-open 01-brutalist-archive/iterations/v1.html
```

Verificar:
- [ ] Título "BRUTALISM" enorme com "TAL" em vermelho
- [ ] Sidebar vertical à esquerda
- [ ] Grid com célula preta, célula vermelha e células brancas
- [ ] Cursor customizado (bloco preto seguindo o mouse)
- [ ] Ao rolar até a seção ASCII, o bloco aparece com fade-in
- [ ] Console do browser: sem erros (F12 → Console)

- [ ] **Step 2.4: Criar v2.html — ticker + hover no grid + cursor expande**

`01-brutalist-archive/iterations/v2.html` (v1 + adições abaixo):

Copiar v1 inteiro e aplicar estas mudanças:

1. Adicionar no `<style>` antes de `</style>`:

```css
    /* Ticker */
    .ticker { overflow: hidden; background: var(--ac); padding: .5rem 0; }
    .ticker-inner { display: inline-block; white-space: nowrap;
                    font-size: .65rem; letter-spacing: .2em; text-transform: uppercase;
                    animation: tick 22s linear infinite; }
    @keyframes tick { from { transform: translateX(100vw); } to { transform: translateX(-100%); } }

    /* Grid hover */
    .cell { transition: background .15s, color .15s; }
    .cell:hover { background: var(--bk) !important; color: var(--wh) !important; cursor: none; }
    .cell:nth-child(2):hover { background: var(--bk) !important; }

    /* Cursor expand on headings */
    h1:hover ~ #cur, .ct:hover { cursor: none; }
    #cur.big { transform: scale(3); }
```

2. Adicionar `<div class="ticker"><span class="ticker-inner">★ BRUTALISM ★ EDITORIAL WEB DESIGN ★ CLAUDE × IVAN LANNA ★ DESIGN ARCHIVE VOL.01 ★ BREAK THE GRID ★ BRUTALISM ★ EDITORIAL WEB DESIGN ★</span></div>` imediatamente após `</header>`.

3. Substituir o bloco `<script>` por:

```html
<script>
  const cur = document.getElementById('cur');
  document.addEventListener('mousemove', e => {
    cur.style.left = (e.clientX - 7) + 'px';
    cur.style.top  = (e.clientY - 7) + 'px';
  });
  // Cursor expande sobre elementos grandes
  document.querySelectorAll('.ct, h1, .fv').forEach(el => {
    el.addEventListener('mouseenter', () => cur.classList.add('big'));
    el.addEventListener('mouseleave', () => cur.classList.remove('big'));
  });
  new IntersectionObserver(entries => {
    if (entries[0].isIntersecting) document.getElementById('apre').classList.add('vis');
  }, { threshold: .2 }).observe(document.getElementById('ascii'));
</script>
```

- [ ] **Step 2.5: Verificar v2 no browser**

Verificar (além do v1):
- [ ] Ticker vermelho rolando horizontalmente após o header
- [ ] Células do grid invertem pro preto ao passar o mouse
- [ ] Cursor vira 3× maior ao passar sobre títulos/textos grandes

- [ ] **Step 2.6: Criar v3.html — glitch no título + typewriter ASCII**

`01-brutalist-archive/iterations/v3.html` (v2 + adições):

1. Adicionar no `<style>` (substituir a animação do ASCII e adicionar glitch):

```css
    /* Glitch no título */
    @keyframes glitch {
      0%,94%,100% { text-shadow: none; transform: none; }
      95%  { text-shadow: 3px 0 var(--ac), -3px 0 #0ff; transform: translateX(2px); }
      97%  { text-shadow: -3px 0 var(--ac), 3px 0 #0ff; transform: translateX(-2px); }
    }
    .title { animation: glitch 6s steps(1) infinite; }

    /* ASCII typewriter — override transition anterior */
    .ascii pre { opacity: 0; transition: none; }
    .ascii pre.vis { opacity: 1; }
```

2. Substituir o bloco `<script>` inteiro por:

```html
<script>
  // Cursor
  const cur = document.getElementById('cur');
  document.addEventListener('mousemove', e => {
    cur.style.left = (e.clientX - 7) + 'px';
    cur.style.top  = (e.clientY - 7) + 'px';
  });
  document.querySelectorAll('.ct, .fv').forEach(el => {
    el.addEventListener('mouseenter', () => cur.classList.add('big'));
    el.addEventListener('mouseleave', () => cur.classList.remove('big'));
  });

  // ASCII typewriter
  const pre = document.getElementById('apre');
  const full = pre.textContent;
  pre.textContent = '';
  let idx = 0;
  function typeNext() {
    if (idx < full.length) {
      pre.textContent += full[idx++];
      setTimeout(typeNext, idx < 10 ? 0 : 4);
    }
  }
  new IntersectionObserver(entries => {
    if (entries[0].isIntersecting) {
      pre.classList.add('vis');
      typeNext();
    }
  }, { threshold: .15 }).observe(document.getElementById('ascii'));
</script>
```

- [ ] **Step 2.7: Verificar v3 no browser**

Verificar:
- [ ] Título pisca com glitch sutil (~a cada 6s)
- [ ] ASCII seção: ao entrar no viewport, caracteres aparecem progressivamente
- [ ] Console sem erros

- [ ] **Step 2.8: Promover v3 para index.html**

```bash
cp 01-brutalist-archive/iterations/v3.html 01-brutalist-archive/index.html
```

- [ ] **Step 2.9: Criar README do exemplo**

`01-brutalist-archive/README.md`:

```markdown
---
title: Brutalist Archive
date: 2026-05-17
style: brutalism
tags: [editorial, typography, monochrome, neon]
techniques: [css-grid, custom-cursor, ascii-animation, mix-blend-mode, intersection-observer]
process_pattern: from-scratch
starting_point: scratch
ai_role: co-designer
iterations: 3
inspiration:
  - Bloomberg Businessweek layout
  - Berlin gallery sites (König Galerie, Sprüth Magers)
difficulty: 3/5
---

## Conceito

Landing editorial brutalista anos 90: Helvetica gigante preenchendo a viewport,
grid CSS quebrado de propósito (células de spans assimétricos), paleta monocromática
com único acento neon (#ff2d00), cursor customizado usando mix-blend-mode:difference,
e bloco ASCII animado por typewriter ao rolar.

## Briefing inicial

"Cria uma landing page estilo editorial brutalista anos 90. Tipografia Helvetica
enorme, grid quebrado de propósito, preto e branco com 1 acento vermelho neon.
Cursor customizado. ASCII art aparecendo no scroll. Inspiração: Bloomberg Businessweek
e sites de galerias berlinenses."

## Prompts e iterações

### v1 — layout base

Resumo: pedi estrutura geral — hero, grid assimétrico, ASCII estático, footer.
Resultado: grid 6-colunas com spans variados, tipografia clamp, cursor via mousemove.
ASCII fade-in via IntersectionObserver.

<details>
<summary>Prompt completo v1</summary>

Cria uma landing page brutalist editorial em HTML/CSS/JS puro standalone.
Requisitos:
- Fonte Helvetica Neue system, peso 900, tamanho clamp(5rem, 18vw, 16rem) no hero
- Cor: #f0ede8 fundo, #0a0a0a texto, #ff2d00 acento
- Layout hero: grid 3 colunas (sidebar vertical | título | número), linha horizontal embaixo
- Seção grid CSS: 6 colunas, células de spans 3+1+2 na primeira linha, 2+4 na segunda
  - célula span-3: fundo preto, texto branco
  - célula span-1: fundo #ff2d00
  - demais: fundo off-white
- Cursor personalizado: div quadrada 14px preta com mix-blend-mode:difference
- Bloco ASCII com a palavra BRUTALISM em block chars, fade-in ao rolar via IntersectionObserver
- Footer 3 colunas com metadados do experimento

</details>

**O que faltou:**
- Grid hover sem feedback visual
- Nenhuma animação de ticker
- ASCII aparecia mas sem drama — transição muito suave

### v2 — ticker + hover no grid + cursor expande

Resumo: adicionei ticker vermelho logo após o header, hover nas células inverte pra
preto, cursor cresce 3x ao passar sobre textos grandes.

<details>
<summary>Prompt completo v2</summary>

Partindo do v1, adiciona:
1. Ticker rolando horizontalmente logo após o header, fundo #ff2d00, texto em loop
2. Células do grid: hover inverte pra fundo preto + texto branco (transition .15s)
3. Cursor: ao passar sobre .ct, h1 e .fv, adiciona classe .big que faz scale(3)
Tudo em CSS puro quando possível. Sem dependências novas.

</details>

**O que faltou:**
- ASCII fade-in ainda monótono
- Título sem personalidade — precisava de mais tensão

### v3 — glitch no título + typewriter ASCII

Resumo: título ganha glitch sutil (text-shadow deslocado + translateX) em loop de 6s.
ASCII muda de fade-in pra typewriter real: cada caractere aparece em sequência.

<details>
<summary>Prompt completo v3</summary>

Partindo do v2, adiciona:
1. CSS keyframe glitch no .title: em 95% e 97% de um ciclo de 6s, aplicar
   text-shadow com deslocamento ±3px em #ff2d00 e #0ff + translateX(±2px).
   Nos outros 94% do tempo: sem efeito. Usar steps(1).
2. ASCII typewriter: ao invés de fade-in, capturar o textContent do pre,
   esvaziar, e adicionar um caractere por vez com setTimeout(4ms).
   Sem transição CSS — aparecer instantâneo caractere a caractere.

</details>

**O que funcionou:** Glitch ficou cirúrgico (quase imperceptível no ritmo normal,
gritante quando aparece). Typewriter ASCII dá uma dimensão "terminal" que combina
com o estilo editorial frio.

## Decisões de processo

- Dei o briefing todo na primeira mensagem — funcionou bem porque o Claude tinha
  todos os constraints claros (paleta, grid, técnicas). Menos vai-e-vem do que
  briefings abertos que testei em outros contextos.
- Micro-gerenciei o grid CSS span (tive que especificar 3+1+2 explicitamente; a
  primeira versão fez spans iguais).
- Para o glitch deixei o Claude propor a implementação CSS — ficou melhor do que
  o que eu teria escrito manualmente.
- O typewriter JS precisou de 2 correções: velocidade inicial (estava muito devagar)
  e o índice de aceleração nos primeiros 10 chars.

## Aprendizados transferíveis

- **Briefings com constraints técnicos explícitos convergem mais rápido.** Quando
  dei paleta HEX, spans do grid e técnicas por nome, o v1 já estava 80% certo.
- **mix-blend-mode: difference** em cursores custom cria contraste automático em
  qualquer fundo — boa técnica pra reusar em outros experimentos.
- **CSS glitch com steps(1)** funciona melhor que transição suave: a descontinuidade
  é parte do efeito.
- **Grid spans assimétricos precisam ser especificados.** O Claude tende pra grids
  simétricos/regulares se não for explicitado.
```

- [ ] **Step 2.10: Atualizar PROCESS.md com aprendizados**

Abrir `PROCESS.md` e substituir as seções relevantes:

```markdown
## Sobre briefing inicial

- Briefings com constraints técnicos explícitos (paleta HEX, técnicas por nome,
  dimensões numéricas) convergem mais rápido — v1 já 80% correto.
  (visto em 01-brutalist-archive)

## Sobre quando deixar o Claude liderar vs micro-gerenciar

- Grid layouts assimétricos: micro-gerenciar. O Claude tende pra grids regulares.
  (visto em 01-brutalist-archive)
- Implementações CSS de efeitos conhecidos (glitch, blend-mode): deixar o Claude
  propor — tende a ser melhor do que uma spec manual.
  (visto em 01-brutalist-archive)
```

Atualizar também a linha `_Exemplos contribuídos: nenhum ainda._` para `_Exemplos contribuídos: 01-brutalist-archive._`

- [ ] **Step 2.11: Commit do exemplo 01**

```bash
git add 01-brutalist-archive/ PROCESS.md
git commit -m "feat: add 01-brutalist-archive"
```

---

## Task 3: Exemplo 02 — Pixel 8-bit

**Conceito:** Landing page de jogo fictício "DESIGN QUEST" em estética 8-bit/NES. Press Start 2P via Google Fonts, paleta NES (10 cores), scanlines CSS, menu navegável por teclado, progress bars de stats, ticker e dialog box. Testa: fidelidade do Claude a constraints estilísticos rígidos.

**Files:**
- Create: `02-pixel-8bit/iterations/v1.html`
- Create: `02-pixel-8bit/iterations/v2.html`
- Create: `02-pixel-8bit/iterations/v3.html`
- Create: `02-pixel-8bit/index.html`
- Create: `02-pixel-8bit/README.md`

- [ ] **Step 3.1: Criar diretórios**

```bash
mkdir -p 02-pixel-8bit/iterations
```

- [ ] **Step 3.2: Criar v1.html — estrutura base NES**

`02-pixel-8bit/iterations/v1.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>DESIGN QUEST</title>
  <link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap" rel="stylesheet">
  <style>
    :root {
      --bk:#000; --wh:#fff; --rd:#cc0000; --bl:#0000fc; --gr:#00a800;
      --yw:#fcbc04; --pu:#7c00fc; --cy:#00f8f8; --or:#fc7c00; --gy:#7c7c7c;
    }
    *, *::before, *::after { margin:0; padding:0; box-sizing:border-box; }
    body {
      background: var(--bk); color: var(--wh);
      font-family: 'Press Start 2P', monospace;
      image-rendering: pixelated; image-rendering: crisp-edges;
      min-height: 100vh; display: flex; align-items: center; justify-content: center;
    }
    /* CRT scanlines */
    body::after {
      content:''; position:fixed; inset:0; pointer-events:none; z-index:100;
      background: repeating-linear-gradient(0deg, transparent, transparent 2px,
        rgba(0,0,0,.18) 2px, rgba(0,0,0,.18) 4px);
    }
    .screen {
      width: min(680px, 96vw);
      border: 4px solid var(--gy);
      box-shadow: 0 0 0 2px #000, 0 0 28px rgba(0,252,0,.12);
      padding: 2rem;
    }
    /* Title */
    .title-area { text-align:center; border-bottom:4px solid var(--wh); padding-bottom:1.5rem; margin-bottom:1.5rem; }
    .game-title { font-size:clamp(.9rem,5vw,1.8rem); color:var(--yw); text-shadow:4px 4px 0 var(--or); animation:blink-slow 2s steps(1) infinite; }
    .subtitle { font-size:.45rem; color:var(--gy); letter-spacing:.15em; margin-top:.75rem; }
    /* Menu */
    .menu { list-style:none; margin-bottom:1.5rem; }
    .menu li { font-size:.6rem; padding:.75rem .5rem; border-bottom:2px solid rgba(255,255,255,.08);
               display:flex; gap:.75rem; align-items:center; cursor:pointer; }
    .menu li.sel { color:var(--yw); }
    .arr { color:var(--rd); opacity:0; }
    .menu li.sel .arr { animation:blink .5s steps(1) infinite; opacity:1; }
    /* Stats */
    .stats { display:grid; grid-template-columns:1fr 1fr; gap:1rem; margin-bottom:1.5rem; }
    .stat p { font-size:.45rem; color:var(--cy); margin-bottom:.35rem; }
    .bar { height:10px; background:var(--gy); }
    .bar-fill { height:100%; }
    .hp .bar-fill  { width:75%; background:var(--gr); }
    .xp .bar-fill  { width:40%; background:var(--bl); }
    .cr .bar-fill  { width:90%; background:var(--yw); }
    .it .bar-fill  { width:55%; background:var(--rd); }
    /* Press start */
    .ps { text-align:center; font-size:.5rem; animation:blink .9s steps(1) infinite; padding:1rem 0; }
    /* Ticker */
    .ticker { overflow:hidden; border-top:4px solid var(--wh); margin-top:1rem; padding:.5rem 0; }
    .ticker-inner { display:inline-block; white-space:nowrap; font-size:.45rem;
                    color:var(--yw); animation:scroll-t 18s linear infinite; }
    @keyframes blink      { 0%,49%{opacity:1} 50%,100%{opacity:0} }
    @keyframes blink-slow { 0%,59%{opacity:1} 60%,100%{opacity:.6} }
    @keyframes scroll-t   { from{transform:translateX(100vw)} to{transform:translateX(-100%)} }
  </style>
</head>
<body>
<div class="screen">
  <div class="title-area">
    <h1 class="game-title">DESIGN QUEST</h1>
    <p class="subtitle">© 2026 IVAN LANNA LABS · VER 0.1.0</p>
  </div>
  <ul class="menu" id="menu">
    <li class="sel"><span class="arr">▶</span>NEW GAME</li>
    <li><span class="arr">▶</span>CONTINUE</li>
    <li><span class="arr">▶</span>GALLERY</li>
    <li><span class="arr">▶</span>SETTINGS</li>
  </ul>
  <div class="stats">
    <div class="stat hp"><p>HP</p><div class="bar"><div class="bar-fill"></div></div></div>
    <div class="stat xp"><p>XP</p><div class="bar"><div class="bar-fill"></div></div></div>
    <div class="stat cr"><p>CREATIVITY</p><div class="bar"><div class="bar-fill"></div></div></div>
    <div class="stat it"><p>ITERATIONS</p><div class="bar"><div class="bar-fill"></div></div></div>
  </div>
  <p class="ps">PRESS ENTER TO START</p>
  <div class="ticker">
    <span class="ticker-inner">★ DESIGN QUEST ★ PIXEL ART MODE ★ 8-BIT ENGINE ★ CLAUDE × IVAN LANNA ★ CREATIVE LVL MAX ★ PRESS START ★&nbsp;&nbsp;&nbsp;</span>
  </div>
</div>
<script>
  const items = Array.from(document.querySelectorAll('#menu li'));
  let sel = 0;
  function moveSel(d) {
    items[sel].classList.remove('sel');
    sel = (sel + d + items.length) % items.length;
    items[sel].classList.add('sel');
  }
  document.addEventListener('keydown', e => {
    if (e.key === 'ArrowDown') { e.preventDefault(); moveSel(1); }
    if (e.key === 'ArrowUp')   { e.preventDefault(); moveSel(-1); }
  });
  items.forEach((li, i) => li.addEventListener('click', () => {
    items[sel].classList.remove('sel'); sel = i; li.classList.add('sel');
  }));
</script>
</body>
</html>
```

- [ ] **Step 3.3: Verificar v1 no browser**

```bash
open 02-pixel-8bit/iterations/v1.html
```

Verificar:
- [ ] Fonte "Press Start 2P" carregada (requer internet para Google Fonts)
- [ ] Scanlines visíveis sobre tudo
- [ ] Título "DESIGN QUEST" amarelo com sombra laranja piscando
- [ ] Seta ▶ piscando na opção selecionada
- [ ] Setas ↑↓ do teclado movem a seleção
- [ ] Click no item muda seleção
- [ ] Ticker rolando na base
- [ ] Console sem erros

- [ ] **Step 3.4: Criar v2.html — sprite ASCII + dialog box**

`02-pixel-8bit/iterations/v2.html` (v1 + adições):

1. Adicionar no `<style>` antes de `</style>`:

```css
    /* Sprite ASCII */
    .sprite-area { font-family:'Courier New',monospace; font-size:.7rem; line-height:1;
                   text-align:center; color:var(--wh); margin:1rem 0 1.5rem;
                   letter-spacing:.1em; }

    /* Dialog box */
    .dialog { display:none; border:4px solid var(--wh); padding:1rem;
              margin-top:1rem; font-size:.5rem; line-height:1.8; min-height:4rem; }
    .dialog.open { display:block; }
    .dialog-text { }
    .dialog-cursor { animation:blink .6s steps(1) infinite; }
```

2. Adicionar após `</ul>` (antes de `.stats`):

```html
  <div class="sprite-area">
    <pre>  ▄█▄  
 ██▀██ 
 ▀█▄█▀ 
  ▀█▀  
  █ █  </pre>
  </div>
```

3. Adicionar após `.stats` (antes de `.ps`):

```html
  <div class="dialog" id="dialog">
    <span class="dialog-text" id="dtxt"></span><span class="dialog-cursor">█</span>
  </div>
```

4. Substituir `<script>` inteiro por:

```html
<script>
  const items = Array.from(document.querySelectorAll('#menu li'));
  const dialog = document.getElementById('dialog');
  const dtxt   = document.getElementById('dtxt');
  const msgs   = {
    0: 'A new design quest begins...\nChoose your style wisely.',
    1: 'Loading saved experiments...\nIterations: 3  Difficulty: 3/5',
    2: 'Gallery mode.\n01 Brutalism  02 Pixel  03 Low-Poly',
    3: 'Settings:\n[SCANLINES: ON]  [CURSOR: BLOCK]  [SFX: OFF]'
  };
  let sel = 0;
  function moveSel(d) {
    items[sel].classList.remove('sel');
    sel = (sel + d + items.length) % items.length;
    items[sel].classList.add('sel');
  }
  function openDialog(i) {
    dialog.classList.add('open');
    dtxt.textContent = '';
    const text = msgs[i] || '';
    let j = 0;
    function type() { if (j < text.length) { dtxt.textContent += text[j++]; setTimeout(type, 35); } }
    type();
  }
  document.addEventListener('keydown', e => {
    if (e.key === 'ArrowDown')  { e.preventDefault(); moveSel(1); }
    if (e.key === 'ArrowUp')    { e.preventDefault(); moveSel(-1); }
    if (e.key === 'Enter')      { openDialog(sel); }
    if (e.key === 'Escape')     { dialog.classList.remove('open'); }
  });
  items.forEach((li, i) => {
    li.addEventListener('click', () => {
      items[sel].classList.remove('sel'); sel = i; li.classList.add('sel');
      openDialog(i);
    });
  });
</script>
```

- [ ] **Step 3.5: Verificar v2 no browser**

Verificar:
- [ ] Sprite ASCII do personagem visível entre título e menu
- [ ] Pressionar Enter abre caixa de diálogo com texto em typewriter
- [ ] Texto correto pra cada opção do menu
- [ ] Esc fecha a caixa
- [ ] Click nos itens também abre dialog

- [ ] **Step 3.6: Criar v3.html — Web Audio beeps + refinamento**

`02-pixel-8bit/iterations/v3.html` (v2 + adições):

1. Adicionar no `<style>` antes de `</style>`:

```css
    /* Hover nos itens do menu */
    .menu li:hover { color:var(--wh); background:rgba(255,255,255,.05); }
    /* Screen glow reforçado */
    .screen { box-shadow:0 0 0 2px #000, 0 0 40px rgba(0,252,0,.2), inset 0 0 60px rgba(0,0,0,.5); }
    /* Dialog aprimorado */
    .dialog { background:rgba(0,0,0,.9); position:relative; }
    .dialog::before { content:'▼ MESSAGE'; display:block; font-size:.4rem; color:var(--gy); margin-bottom:.5rem; }
```

2. Substituir `<script>` inteiro por:

```html
<script>
  // Web Audio — beeps retro
  const ctx = new (window.AudioContext || window.webkitAudioContext)();
  function beep(freq, dur, type = 'square') {
    const o = ctx.createOscillator();
    const g = ctx.createGain();
    o.type = type;
    o.frequency.value = freq;
    g.gain.setValueAtTime(.08, ctx.currentTime);
    g.gain.exponentialRampToValueAtTime(.001, ctx.currentTime + dur);
    o.connect(g); g.connect(ctx.destination);
    o.start(); o.stop(ctx.currentTime + dur);
  }

  const items = Array.from(document.querySelectorAll('#menu li'));
  const dialog = document.getElementById('dialog');
  const dtxt   = document.getElementById('dtxt');
  const msgs   = {
    0: 'A new design quest begins...\nChoose your style wisely.',
    1: 'Loading saved experiments...\nIterations: 3  Difficulty: 3/5',
    2: 'Gallery mode.\n01 Brutalism  02 Pixel  03 Low-Poly',
    3: 'Settings:\n[SCANLINES: ON]  [CURSOR: BLOCK]  [SFX: ON]'
  };
  let sel = 0;

  function moveSel(d) {
    items[sel].classList.remove('sel');
    sel = (sel + d + items.length) % items.length;
    items[sel].classList.add('sel');
    beep(220, .07);
  }
  function openDialog(i) {
    beep(440, .12); beep(550, .08);
    dialog.classList.add('open');
    dtxt.textContent = '';
    const text = msgs[i] || '';
    let j = 0;
    function type() {
      if (j < text.length) {
        dtxt.textContent += text[j++];
        beep(880 + Math.random() * 200, .02, 'sawtooth');
        setTimeout(type, 38);
      }
    }
    type();
  }
  document.addEventListener('keydown', e => {
    if (e.key === 'ArrowDown')  { e.preventDefault(); moveSel(1); }
    if (e.key === 'ArrowUp')    { e.preventDefault(); moveSel(-1); }
    if (e.key === 'Enter')      { openDialog(sel); }
    if (e.key === 'Escape')     { dialog.classList.remove('open'); beep(110, .15); }
  });
  items.forEach((li, i) => {
    li.addEventListener('mouseenter', () => beep(330, .04));
    li.addEventListener('click', () => {
      items[sel].classList.remove('sel'); sel = i; li.classList.add('sel');
      openDialog(i);
    });
  });
</script>
```

- [ ] **Step 3.7: Verificar v3 no browser**

Verificar:
- [ ] Som ao navegar com setas (pitch baixo ~220Hz)
- [ ] Som ao pressionar Enter (2 beeps rápidos)
- [ ] Som typewriter (ruído de sarda aleatório durante texto)
- [ ] Som ao Esc (tom grave)
- [ ] Hover nos itens faz som suave
- [ ] Screen glow mais pronunciado
- [ ] Console sem erros

Nota: browser pode bloquear AudioContext sem interação prévia. O primeiro beep pode não tocar — depois da primeira keydown tudo funciona.

- [ ] **Step 3.8: Promover v3 para index.html**

```bash
cp 02-pixel-8bit/iterations/v3.html 02-pixel-8bit/index.html
```

- [ ] **Step 3.9: Criar README do exemplo**

`02-pixel-8bit/README.md`:

```markdown
---
title: Pixel 8-bit — Design Quest
date: 2026-05-17
style: pixel-art
tags: [retro, 8-bit, game-ui, nes, crt]
techniques: [press-start-2p, css-scanlines, web-audio, pixel-art-ascii, keyframe-blink]
process_pattern: from-scratch
starting_point: scratch
ai_role: co-designer
iterations: 3
inspiration:
  - NES game title screens (Mega Man, Castlevania)
  - Itch.io retro game aesthetic
difficulty: 2/5
---

## Conceito

Landing page de um jogo fictício "DESIGN QUEST" em estética 8-bit NES. Paleta
limitada a 10 cores NES, tipografia Press Start 2P, scanlines CRT em CSS,
menu navegável por teclado, stats de personagem, e dialog box com typewriter +
beeps Web Audio.

## Briefing inicial

"Cria uma landing page estilo jogo 8-bit NES. Fonte Press Start 2P, paleta NES
(preto, branco, vermelho, azul, verde, amarelo). Scanlines CRT. Menu de jogo
(NEW GAME, CONTINUE, GALLERY, SETTINGS) navegável com setas do teclado."

## Prompts e iterações

### v1 — estrutura base

Resumo: estrutura completa no primeiro prompt — título, scanlines, menu com
teclado, stats, ticker, press-start piscando.

<details>
<summary>Prompt completo v1</summary>

Cria uma landing page estilo jogo 8-bit NES em HTML/CSS/JS puro.
Requisitos:
- Fonte: Press Start 2P via Google Fonts CDN
- Paleta: --bk:#000 --wh:#fff --rd:#cc0000 --bl:#0000fc --gr:#00a800
  --yw:#fcbc04 --pu:#7c00fc --cy:#00f8f8 --or:#fc7c00 --gy:#7c7c7c
- Efeito CRT: body::after com repeating-linear-gradient de scanlines
- Tela centralizada max-width:680px com borda 4px solid cinza e box-shadow verde
- Título "DESIGN QUEST" em amarelo com text-shadow laranja, animação blink-slow
- Menu: 4 itens (NEW GAME / CONTINUE / GALLERY / SETTINGS), seta ▶ vermelha
  piscando no item selecionado. Setas ↑↓ navegam. Click também seleciona.
- Stats: 4 barras (HP verde 75%, XP azul 40%, CREATIVITY amarelo 90%,
  ITERATIONS vermelho 55%)
- PRESS ENTER TO START piscando
- Ticker: texto rolando lentamente na base, amarelo

</details>

**O que faltou:** Sem personagem visual, sem reação ao Enter.

### v2 — sprite + dialog box

Resumo: sprite ASCII de personagem adicionado entre título e menu.
Enter abre dialog box com texto typewriter, Esc fecha.

<details>
<summary>Prompt completo v2</summary>

Partindo do v1, adiciona:
1. Sprite ASCII simples de personagem humanóide (5 linhas com chars ▄ █ ▀)
   centralizado entre título e menu
2. Dialog box (display:none por padrão, .open mostra) com:
   - Borda 4px branca, padding 1rem
   - Texto typewriter (caractere por caractere, 35ms cada)
   - Cursor piscante █ ao final
   - 4 mensagens diferentes por opção (0-3)
3. Enter abre dialog da opção selecionada. Esc fecha.
4. Click nos itens também abre dialog correspondente.

</details>

**O que faltou:** Silêncio — sem feedback sonoro. Hover sem reação.

### v3 — Web Audio beeps

Resumo: Web Audio API adicionando beeps retrô em todo feedback: navegação,
confirmação, typewriter, fechar. Screen glow mais pronunciado.

<details>
<summary>Prompt completo v3</summary>

Partindo do v2, adiciona:
1. Web Audio context: função beep(freq, dur, type='square')
2. Navegar com seta: beep(220, .07)
3. Enter/click: beep(440,.12) + beep(550,.08)
4. Cada char do typewriter: beep(880+random*200, .02, 'sawtooth')
5. Esc: beep(110, .15)
6. mouseenter em menu item: beep(330, .04)
7. Screen: reforçar box-shadow com inset shadow escuro
8. Dialog: fundo rgba(0,0,0,.9) + label "▼ MESSAGE" em cinza via ::before

</details>

**O que funcionou:** Som transformou a experiência completamente.
Uma paleta de 5 cores de beep já dá identidade sonora ao UI.

## Decisões de processo

- Constraints de paleta NES funcionaram perfeitamente — o Claude respeitou
  100% sem precisar corrigir.
- Sprite ASCII foi a única coisa que pedi pra Claude propor livremente
  (não dei referência). Resultado: simples mas funcional.
- Web Audio: Claude gerenciou bem a API. Tive que calibrar volumes (.08)
  porque a primeira versão estava alto demais.

## Aprendizados transferíveis

- **Constraints de paleta funcionam melhor quando dados como variáveis CSS nomeadas.**
  Claude respeita as vars e não inventa cores novas.
- **Web Audio API baixo volume** (gain .08) é o ponto de equilíbrio entre audível
  e não-irritante em UI retro.
- **Sprite ASCII simples > sprite CSS complexo** quando o estilo já é ASCII-heavy.
  Consistência supera fidelidade técnica.
```

- [ ] **Step 3.10: Atualizar PROCESS.md**

Adicionar bullets relevantes nas seções corretas:

```markdown
## Sobre constraints estilísticos rígidos

- Paleta NES como variáveis CSS nomeadas: Claude respeitou 100%, sem inventar
  cores fora da paleta. (visto em 02-pixel-8bit)

## Sobre limites técnicos (CSS, WebGL, animações)

- Web Audio API: Claude gerencia bem, mas volumes precisam calibração manual
  (ponto de equilíbrio: gain ~0.08 para UI sounds). (visto em 02-pixel-8bit)
```

Atualizar: `_Exemplos contribuídos: 01-brutalist-archive, 02-pixel-8bit._`

- [ ] **Step 3.11: Commit do exemplo 02**

```bash
git add 02-pixel-8bit/ PROCESS.md
git commit -m "feat: add 02-pixel-8bit"
```

---

## Task 4: Exemplo 03 — Low-poly 3D

**Conceito:** Cena Three.js com icosaedro low-poly faceted, paleta de 10 cores saturadas, flat shading, rotação automática + OrbitControls, overlay de texto. Testa: colaboração em código 3D com IA.

**Dependência técnica:** Este exemplo usa ES modules com importmap. Requer servidor HTTP — não funciona via `file://`. Use `python3 -m http.server 8080` ou `npx serve`.

**Files:**
- Create: `03-low-poly-3d/iterations/v1.html`
- Create: `03-low-poly-3d/iterations/v2.html`
- Create: `03-low-poly-3d/iterations/v3.html`
- Create: `03-low-poly-3d/index.html`
- Create: `03-low-poly-3d/README.md`

- [ ] **Step 4.1: Criar diretórios**

```bash
mkdir -p 03-low-poly-3d/iterations
```

- [ ] **Step 4.2: Criar v1.html — cena Three.js base**

`03-low-poly-3d/iterations/v1.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>LOW POLY 3D — N°03</title>
  <style>
    * { margin:0; padding:0; box-sizing:border-box; }
    body { background:#0c0c1a; overflow:hidden; }
    canvas { display:block; }
  </style>
  <script type="importmap">
  {
    "imports": {
      "three": "https://unpkg.com/three@0.160.0/build/three.module.js",
      "three/addons/": "https://unpkg.com/three@0.160.0/examples/jsm/"
    }
  }
  </script>
</head>
<body>
<script type="module">
  import * as THREE from 'three';
  import { OrbitControls } from 'three/addons/controls/OrbitControls.js';

  const palette = ['#FF6B6B','#4ECDC4','#45B7D1','#96E6A1','#DDA0DD',
                   '#FFD93D','#6BCB77','#FF8B94','#A8DADC','#F4A261'];

  const scene    = new THREE.Scene();
  scene.background = new THREE.Color('#0c0c1a');
  const camera   = new THREE.PerspectiveCamera(60, innerWidth / innerHeight, 0.1, 100);
  camera.position.set(0, 0, 5);
  const renderer = new THREE.WebGLRenderer({ antialias: true });
  renderer.setSize(innerWidth, innerHeight);
  renderer.setPixelRatio(devicePixelRatio);
  document.body.appendChild(renderer.domElement);

  function buildMesh(radius = 1.5) {
    const geo  = new THREE.IcosahedronGeometry(radius, 1);
    const pos  = geo.attributes.position;
    const cols = [];
    for (let i = 0; i < pos.count; i += 3) {
      const c = new THREE.Color(palette[Math.floor(Math.random() * palette.length)]);
      cols.push(c.r, c.g, c.b, c.r, c.g, c.b, c.r, c.g, c.b);
    }
    geo.setAttribute('color', new THREE.Float32BufferAttribute(cols, 3));
    const mat = new THREE.MeshPhongMaterial({ vertexColors: true, flatShading: true });
    return new THREE.Mesh(geo, mat);
  }

  const mesh = buildMesh();
  scene.add(mesh);
  scene.add(new THREE.AmbientLight('#334466', 0.9));
  const dir = new THREE.DirectionalLight('#ffffff', 1.4);
  dir.position.set(4, 6, 4);
  scene.add(dir);

  const controls = new OrbitControls(camera, renderer.domElement);
  controls.enableDamping    = true;
  controls.dampingFactor    = 0.06;
  controls.enableZoom       = false;
  controls.autoRotate       = true;
  controls.autoRotateSpeed  = 0.8;

  function animate() {
    requestAnimationFrame(animate);
    controls.update();
    renderer.render(scene, camera);
  }
  animate();

  window.addEventListener('resize', () => {
    camera.aspect = innerWidth / innerHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(innerWidth, innerHeight);
  });
</script>
</body>
</html>
```

- [ ] **Step 4.3: Iniciar servidor HTTP e verificar v1**

```bash
cd 03-low-poly-3d && python3 -m http.server 8080
# Em outra aba/terminal: abrir http://localhost:8080/iterations/v1.html
```

Verificar:
- [ ] Icosaedro faceted colorido girando na tela
- [ ] Faces diferentes com cores diferentes da paleta
- [ ] Drag do mouse orbita a câmera (OrbitControls)
- [ ] Console sem erros (erro de CORS se abrir via file://)

Fechar servidor com `Ctrl+C` quando terminar.

- [ ] **Step 4.4: Criar v2.html — wireframe ghost + overlay de texto**

`03-low-poly-3d/iterations/v2.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>LOW POLY 3D — N°03</title>
  <style>
    * { margin:0; padding:0; box-sizing:border-box; }
    body { background:#0c0c1a; overflow:hidden; }
    canvas { display:block; position:fixed; inset:0; }
    /* Overlay de texto */
    .overlay {
      position:fixed; inset:0; pointer-events:none; z-index:10;
      display:flex; flex-direction:column; justify-content:space-between; padding:2rem;
      font-family:'Helvetica Neue',Helvetica,Arial,sans-serif; color:rgba(255,255,255,.85);
    }
    .ov-top { display:flex; justify-content:space-between; align-items:flex-start; }
    .ov-title { font-size:clamp(.6rem,1.5vw,1rem); font-weight:700; letter-spacing:.3em; text-transform:uppercase; }
    .ov-num   { font-size:clamp(.6rem,1.5vw,1rem); font-weight:300; opacity:.5; }
    .ov-bottom { display:flex; justify-content:space-between; font-size:.65rem; opacity:.4;
                 letter-spacing:.2em; text-transform:uppercase; }
  </style>
  <script type="importmap">
  {
    "imports": {
      "three": "https://unpkg.com/three@0.160.0/build/three.module.js",
      "three/addons/": "https://unpkg.com/three@0.160.0/examples/jsm/"
    }
  }
  </script>
</head>
<body>
<div class="overlay">
  <div class="ov-top">
    <span class="ov-title">Low-Poly 3D</span>
    <span class="ov-num">N°03 / 2026</span>
  </div>
  <div class="ov-bottom">
    <span>Three.js · Icosahedron · Flat Shading</span>
    <span>Claude × Ivan Lanna</span>
  </div>
</div>
<script type="module">
  import * as THREE from 'three';
  import { OrbitControls } from 'three/addons/controls/OrbitControls.js';

  const palette = ['#FF6B6B','#4ECDC4','#45B7D1','#96E6A1','#DDA0DD',
                   '#FFD93D','#6BCB77','#FF8B94','#A8DADC','#F4A261'];

  const scene    = new THREE.Scene();
  const camera   = new THREE.PerspectiveCamera(60, innerWidth / innerHeight, 0.1, 100);
  camera.position.set(0, 0, 5);
  const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
  renderer.setSize(innerWidth, innerHeight);
  renderer.setPixelRatio(devicePixelRatio);
  renderer.setClearColor(0x0c0c1a, 1);
  document.body.appendChild(renderer.domElement);

  function buildMesh(radius = 1.5) {
    const geo  = new THREE.IcosahedronGeometry(radius, 1);
    const pos  = geo.attributes.position;
    const cols = [];
    for (let i = 0; i < pos.count; i += 3) {
      const c = new THREE.Color(palette[Math.floor(Math.random() * palette.length)]);
      cols.push(c.r, c.g, c.b, c.r, c.g, c.b, c.r, c.g, c.b);
    }
    geo.setAttribute('color', new THREE.Float32BufferAttribute(cols, 3));
    return new THREE.Mesh(geo, new THREE.MeshPhongMaterial({ vertexColors: true, flatShading: true }));
  }

  // Sólido colorido + wireframe ghost
  const solid = buildMesh(1.5);
  const wire  = new THREE.Mesh(
    new THREE.IcosahedronGeometry(1.52, 1),
    new THREE.MeshBasicMaterial({ color: '#ffffff', wireframe: true, transparent: true, opacity: .08 })
  );
  const group = new THREE.Group();
  group.add(solid, wire);
  scene.add(group);

  scene.add(new THREE.AmbientLight('#334466', 0.9));
  const dir = new THREE.DirectionalLight('#ffffff', 1.4);
  dir.position.set(4, 6, 4);
  scene.add(dir);

  const controls = new OrbitControls(camera, renderer.domElement);
  controls.enableDamping   = true;
  controls.dampingFactor   = 0.06;
  controls.enableZoom      = false;
  controls.autoRotate      = true;
  controls.autoRotateSpeed = 0.8;

  function animate() {
    requestAnimationFrame(animate);
    controls.update();
    renderer.render(scene, camera);
  }
  animate();

  window.addEventListener('resize', () => {
    camera.aspect = innerWidth / innerHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(innerWidth, innerHeight);
  });
</script>
</body>
</html>
```

- [ ] **Step 4.5: Verificar v2 no servidor**

```bash
cd 03-low-poly-3d && python3 -m http.server 8080
# Abrir http://localhost:8080/iterations/v2.html
```

Verificar:
- [ ] Overlay de texto "Low-Poly 3D / N°03" no canto superior
- [ ] Rodapé com técnicas à esquerda e autoria à direita
- [ ] Malha wireframe semitransparente sobre o icosaedro colorido
- [ ] Orbiting funciona normalmente

- [ ] **Step 4.6: Criar v3.html — múltiplos shapes + hover pulse**

`03-low-poly-3d/iterations/v3.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>LOW POLY 3D — N°03</title>
  <style>
    * { margin:0; padding:0; box-sizing:border-box; }
    body { background:#0c0c1a; overflow:hidden; }
    canvas { display:block; position:fixed; inset:0; }
    .overlay {
      position:fixed; inset:0; pointer-events:none; z-index:10;
      display:flex; flex-direction:column; justify-content:space-between; padding:2.5rem;
      font-family:'Helvetica Neue',Helvetica,Arial,sans-serif; color:rgba(255,255,255,.9);
    }
    .ov-top { display:flex; justify-content:space-between; align-items:flex-start; }
    .ov-title { font-size:clamp(.7rem,1.8vw,1.1rem); font-weight:800; letter-spacing:.35em; text-transform:uppercase; }
    .ov-num   { font-size:clamp(.7rem,1.8vw,1.1rem); font-weight:200; opacity:.45; letter-spacing:.2em; }
    .ov-desc  { max-width:260px; font-size:.65rem; line-height:1.7; opacity:.35;
                letter-spacing:.08em; margin-top:.75rem; }
    .ov-bottom { display:flex; justify-content:space-between; font-size:.6rem; opacity:.35;
                 letter-spacing:.25em; text-transform:uppercase; }
    .tag { border:1px solid rgba(255,255,255,.2); padding:.15rem .5rem; border-radius:2px; }
  </style>
  <script type="importmap">
  {
    "imports": {
      "three": "https://unpkg.com/three@0.160.0/build/three.module.js",
      "three/addons/": "https://unpkg.com/three@0.160.0/examples/jsm/"
    }
  }
  </script>
</head>
<body>
<div class="overlay">
  <div class="ov-top">
    <div>
      <div style="display:flex;justify-content:space-between;gap:3rem;">
        <span class="ov-title">Low-Poly 3D</span>
        <span class="ov-num">N°03</span>
      </div>
      <p class="ov-desc">Icosaedro faceted com vertex colors aleatórios da paleta, flat shading e wireframe ghost. Rotação auto + OrbitControls.</p>
    </div>
  </div>
  <div class="ov-bottom">
    <div style="display:flex;gap:.75rem;">
      <span class="tag">Three.js</span>
      <span class="tag">Low-Poly</span>
      <span class="tag">Flat Shading</span>
    </div>
    <span>Claude × Ivan Lanna · 2026</span>
  </div>
</div>
<script type="module">
  import * as THREE from 'three';
  import { OrbitControls } from 'three/addons/controls/OrbitControls.js';

  const palette = ['#FF6B6B','#4ECDC4','#45B7D1','#96E6A1','#DDA0DD',
                   '#FFD93D','#6BCB77','#FF8B94','#A8DADC','#F4A261'];

  const scene    = new THREE.Scene();
  const camera   = new THREE.PerspectiveCamera(60, innerWidth / innerHeight, 0.1, 100);
  camera.position.set(0, 0, 7);
  const renderer = new THREE.WebGLRenderer({ antialias: true });
  renderer.setSize(innerWidth, innerHeight);
  renderer.setPixelRatio(devicePixelRatio);
  renderer.setClearColor(0x0c0c1a, 1);
  document.body.appendChild(renderer.domElement);

  function buildGroup(radius, wireOpacity = .08) {
    const geo  = new THREE.IcosahedronGeometry(radius, 1);
    const pos  = geo.attributes.position;
    const cols = [];
    for (let i = 0; i < pos.count; i += 3) {
      const c = new THREE.Color(palette[Math.floor(Math.random() * palette.length)]);
      cols.push(c.r, c.g, c.b, c.r, c.g, c.b, c.r, c.g, c.b);
    }
    geo.setAttribute('color', new THREE.Float32BufferAttribute(cols, 3));
    const solid = new THREE.Mesh(geo, new THREE.MeshPhongMaterial({ vertexColors: true, flatShading: true }));
    const wire  = new THREE.Mesh(
      new THREE.IcosahedronGeometry(radius * 1.015, 1),
      new THREE.MeshBasicMaterial({ color: '#ffffff', wireframe: true, transparent: true, opacity: wireOpacity })
    );
    const g = new THREE.Group();
    g.add(solid, wire);
    return g;
  }

  // 3 meshes em posições diferentes
  const main  = buildGroup(1.5, .08);
  const left  = buildGroup(0.7, .12);
  const right = buildGroup(0.55, .15);
  left.position.set(-3.2, -0.5, -1);
  right.position.set(3.0, 0.8, -0.5);
  scene.add(main, left, right);

  // Niebla sutil
  scene.fog = new THREE.Fog('#0c0c1a', 8, 18);

  scene.add(new THREE.AmbientLight('#334466', 1.0));
  const dir = new THREE.DirectionalLight('#ffffff', 1.3);
  dir.position.set(4, 6, 4);
  scene.add(dir);

  // Luz colorida secundária
  const pointL = new THREE.PointLight('#4ECDC4', 1.2, 12);
  pointL.position.set(-3, 2, 2);
  scene.add(pointL);

  const controls = new OrbitControls(camera, renderer.domElement);
  controls.enableDamping   = true;
  controls.dampingFactor   = 0.05;
  controls.enableZoom      = false;
  controls.autoRotate      = true;
  controls.autoRotateSpeed = 0.5;

  // Hover pulse: raycaster no mesh principal
  const raycaster = new THREE.Raycaster();
  const mouse     = new THREE.Vector2();
  let hovered     = false;
  window.addEventListener('mousemove', e => {
    mouse.x =  (e.clientX / innerWidth)  * 2 - 1;
    mouse.y = -(e.clientY / innerHeight) * 2 + 1;
  });

  const clock = new THREE.Clock();
  function animate() {
    requestAnimationFrame(animate);
    const t = clock.getElapsedTime();

    // Órbitas independentes dos shapes secundários
    left.rotation.y  = t * 0.4;
    right.rotation.y = -t * 0.6;
    right.rotation.x = t * 0.3;

    // Raycaster hover pulse no main
    raycaster.setFromCamera(mouse, camera);
    const hits = raycaster.intersectObject(main.children[0]);
    if (hits.length > 0) {
      hovered = true;
    } else {
      hovered = false;
    }
    const targetScale = hovered ? 1.08 : 1.0;
    main.scale.lerp(new THREE.Vector3(targetScale, targetScale, targetScale), 0.08);

    controls.update();
    renderer.render(scene, camera);
  }
  animate();

  window.addEventListener('resize', () => {
    camera.aspect = innerWidth / innerHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(innerWidth, innerHeight);
  });
</script>
</body>
</html>
```

- [ ] **Step 4.7: Verificar v3 no servidor**

```bash
cd 03-low-poly-3d && python3 -m http.server 8080
# Abrir http://localhost:8080/iterations/v3.html
```

Verificar:
- [ ] 3 icosaedros em posições diferentes (1 grande central, 2 menores nas laterais)
- [ ] Os dois menores giram em velocidades e eixos diferentes
- [ ] Hover sobre o mesh central faz ele crescer levemente (scale lerp)
- [ ] Luz pontual ciano visível iluminando da esquerda
- [ ] Névoa sutil nas bordas
- [ ] Overlay com tags "Three.js", "Low-Poly", "Flat Shading" no rodapé
- [ ] Console sem erros

- [ ] **Step 4.8: Promover v3 para index.html**

```bash
cp 03-low-poly-3d/iterations/v3.html 03-low-poly-3d/index.html
```

- [ ] **Step 4.9: Criar README do exemplo**

`03-low-poly-3d/README.md`:

```markdown
---
title: Low-Poly 3D
date: 2026-05-17
style: low-poly
tags: [3d, threejs, interactive, colorful, geometric]
techniques: [threejs, icosahedron, flat-shading, vertex-colors, orbit-controls, raycaster]
process_pattern: from-scratch
starting_point: scratch
ai_role: co-designer
iterations: 3
inspiration:
  - Figma Config visuals
  - Bruno Simon portfolio (threejs.journey.com)
difficulty: 4/5
---

## Conceito

Cena Three.js com icosaedros low-poly faceted: vertex colors aleatórios de
uma paleta de 10 cores saturadas, flat shading (cada face uma cor sólida),
wireframe ghost semitransparente. 3 shapes em órbitas independentes + hover
pulse no shape central. Overlay tipográfico com tags de tecnologia.

## Briefing inicial

"Cria uma cena Three.js com um icosaedro low-poly usando vertex colors aleatórios
de uma paleta de 10 cores. Flat shading. Rotação auto com OrbitControls. Standalone
HTML, Three.js via importmap/CDN."

## Prompts e iterações

### v1 — cena base

Resumo: cena funcional com 1 icosaedro, vertex colors, flat shading, OrbitControls
autoRotate, resize handler.

<details>
<summary>Prompt completo v1</summary>

Cria uma cena Three.js standalone em HTML (sem build, importmap com unpkg).
Requisitos:
- Three.js 0.160.0 via importmap
- OrbitControls da mesma versão
- IcosahedronGeometry(1.5, 1) — detail level 1 pra manter faceted
- Vertex colors: a cada 3 vertices (= 1 face), atribuir mesma cor aleatória
  de: ['#FF6B6B','#4ECDC4','#45B7D1','#96E6A1','#DDA0DD','#FFD93D','#6BCB77','#FF8B94','#A8DADC','#F4A261']
- MeshPhongMaterial flatShading:true vertexColors:true
- Luz: AmbientLight('#334466', 0.9) + DirectionalLight branca (4,6,4)
- OrbitControls: enableDamping, dampingFactor .06, enableZoom false, autoRotate true speed .8
- Background: #0c0c1a
- Resize handler

</details>

**O que faltou:** Tela toda apenas 3D — sem contexto tipográfico, sem composição.

### v2 — wireframe ghost + overlay de texto

Resumo: adicionei wireframe ghost com opacity .08 sobre o sólido (escala 1.015x
pra evitar z-fighting). Overlay HTML fixo com título e rodapé de metadados.

<details>
<summary>Prompt completo v2</summary>

Partindo do v1, adiciona:
1. Wireframe ghost: segundo Mesh com IcosahedronGeometry(1.52, 1),
   MeshBasicMaterial wireframe:true transparent:true opacity:.08
   Agrupados com Group.
2. Overlay HTML: position:fixed inset:0 pointer-events:none z-index:10
   - Canto superior esquerdo: "Low-Poly 3D"
   - Canto superior direito: "N°03 / 2026"
   - Rodapé esquerdo: técnicas (Three.js · Icosahedron · Flat Shading)
   - Rodapé direito: "Claude × Ivan Lanna"
   Fonte Helvetica, letra-espaçamento, text-transform uppercase

</details>

**O que faltou:** Composição ainda monótona (1 shape). Sem profundidade.

### v3 — 3 shapes + hover pulse + névoa

Resumo: função buildGroup() extrai criação do mesh. 3 icosaedros posicionados:
central grande, dois menores nas laterais em órbitas independentes. Raycaster
detecta hover no central e aplica scale lerp. Névoa sutil. Luz pontual ciano.

<details>
<summary>Prompt completo v3</summary>

Partindo do v2, refatora pra buildGroup(radius, wireOpacity) e cria:
- main: buildGroup(1.5, .08) no centro
- left: buildGroup(0.7, .12) em (-3.2, -0.5, -1)
- right: buildGroup(0.55, .15) em (3.0, 0.8, -0.5)
left.rotation.y = t * 0.4 no animate
right.rotation.y = -t * 0.6, right.rotation.x = t * 0.3
Raycaster: intersectObject(main.children[0]) pra detectar hover.
Hover: scale lerp pra 1.08. Sem hover: lerp pra 1.0. Fator: 0.08.
Névoa: THREE.Fog('#0c0c1a', 8, 18)
Luz pontual: PointLight('#4ECDC4', 1.2, 12) em (-3, 2, 2)
Overlay v2 refinado: description text + tags com border no rodapé.

</details>

**O que funcionou:** Composição com 3 shapes deu profundidade imediatamente.
O scale lerp via Vector3.lerp ficou suave sem vibrar.
**Dificuldade real:** Z-fighting entre sólido e wireframe — resolveu com escala 1.015x no wireframe.

## Decisões de processo

- Three.js: micro-gerenciei mais do que nos outros exemplos. Tive que corrigir:
  a escala do wireframe (z-fighting), o fator de lerp (muito rápido na primeira vez),
  a posição das luzes (primeira versão deixava o shape escuro de um lado).
- Refatorar pra `buildGroup()` foi sugestão do Claude no v3 — boa call,
  evitou repetição.
- Raycaster em `main.children[0]` (o sólido): tive que especificar explicitamente,
  o Claude tentou primeiro com o Group inteiro (que não funciona com raycaster diretamente).

## Aprendizados transferíveis

- **Three.js precisa mais micro-gerenciamento** que CSS puro. Coisas como z-fighting,
  posição de luz, e detalhes de API (raycaster em Mesh vs Group) precisam ser
  corrigidos manualmente. (visto em 03-low-poly-3d)
- **Z-fighting wireframe+sólido**: resolver com scale 1.01-1.02x no wireframe.
  (visto em 03-low-poly-3d)
- **scale.lerp() com Vector3** é mais limpo que lerp manual — e o Claude sugere
  essa API naturalmente. (visto em 03-low-poly-3d)
- **Composição 3D melhora drasticamente** com múltiplos shapes em planos Z
  diferentes. Um shape único parece demo; três shapes parecem cena.
```

- [ ] **Step 4.10: Atualizar PROCESS.md**

Adicionar nas seções relevantes:

```markdown
## Sobre quando deixar o Claude liderar vs micro-gerenciar

- Three.js: micro-gerenciar mais do que CSS puro. API details (raycaster em Mesh
  vs Group, z-fighting wireframe) precisam correção manual.
  (visto em 03-low-poly-3d)
- Refatoração interna (ex: extrair buildGroup()): deixar o Claude propor — tende
  a ser boa call. (visto em 03-low-poly-3d)

## Sobre limites técnicos (CSS, WebGL, animações)

- Z-fighting wireframe+sólido: resolver com scale 1.01-1.02x no wireframe.
  (visto em 03-low-poly-3d)
- Composição 3D: mínimo de 3 shapes em planos Z diferentes pra parecer cena
  e não demo. (visto em 03-low-poly-3d)

## Sobre iteração e convergência

- 3 iterações costumam ser suficientes: v1 (estrutura), v2 (composição),
  v3 (refinamento + detalhes). (visto em 01, 02 e 03)
```

Atualizar: `_Exemplos contribuídos: 01-brutalist-archive, 02-pixel-8bit, 03-low-poly-3d._`

- [ ] **Step 4.11: Commit do exemplo 03**

```bash
git add 03-low-poly-3d/ PROCESS.md
git commit -m "feat: add 03-low-poly-3d"
```

---

## Task 5: Push e verificação do deploy

**Files:** nenhum novo arquivo — só push e verificação no GitHub Pages.

- [ ] **Step 5.1: Revisar estado do repo**

```bash
git log --oneline
```

Expected output (4 commits):
```
<hash> feat: add 03-low-poly-3d
<hash> feat: add 02-pixel-8bit
<hash> feat: add 01-brutalist-archive
<hash> feat: scaffold laboratorio de design — skeleton inicial
<hash> docs: incorporate findings from related repos into spec
<hash> docs: add design spec for AI design lab
```

- [ ] **Step 5.2: Push para o remote**

```bash
git push origin main
```

Expected: push aceito, sem erros de conflito.

- [ ] **Step 5.3: Habilitar GitHub Pages no repositório**

Abrir https://github.com/Iv4nLanna/Design-UX-Teste/settings/pages

- Source: **Deploy from a branch**
- Branch: `main` / `/ (root)`
- Save

O workflow `.github/workflows/pages.yml` vai disparar automaticamente depois do próximo push.

- [ ] **Step 5.4: Aguardar deploy e verificar URLs**

Aguardar ~2 minutos. Verificar as URLs:

- `https://iv4nlanna.github.io/Design-UX-Teste/01-brutalist-archive/` — brutalist carrega
- `https://iv4nlanna.github.io/Design-UX-Teste/02-pixel-8bit/` — pixel carrega
- `https://iv4nlanna.github.io/Design-UX-Teste/03-low-poly-3d/` — 3D carrega (sem erro CORS)

Verificar para cada URL:
- [ ] Página carrega sem tela branca
- [ ] Sem erros 404 nos recursos CDN
- [ ] Console do browser sem erros críticos

---

## Self-Review

**Spec coverage:**
- [x] README raiz com tabela → Task 1
- [x] AGENTS.md → Task 1
- [x] PROCESS.md (esqueleto + destilação) → Task 1 + Steps 2.10, 3.10, 4.10
- [x] .github/workflows → Task 1
- [x] _template → Task 1
- [x] 01-brutalist-archive (v1/v2/v3 + README + iterations/) → Task 2
- [x] 02-pixel-8bit (v1/v2/v3 + README + iterations/) → Task 3
- [x] 03-low-poly-3d (v1/v2/v3 + README + iterations/) → Task 4
- [x] Frontmatter padronizado → em cada README de exemplo
- [x] Três modos de partida documentados → em todos os README (starting_point: scratch)
- [x] Deploy GitHub Pages → Task 5
- [x] AGENTS.md inclui disciplina de commits → Step 1.2

**Placeholder scan:** nenhum TBD ou TODO no plano.

**Consistência:** `buildGroup()` introduzido no v3 do 03 — referenciado apenas dentro da Task 4 (não vaza). `beep()` introduzida e usada dentro da Task 3. Sem referências cruzadas entre tasks.
