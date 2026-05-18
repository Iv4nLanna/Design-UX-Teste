---
title: Renascimento Digital
date: 2026-05-17
style: renaissance
tags: [classical, museum, css-art, chiaroscuro, interactive]
techniques: [svg, css-animation, intersection-observer, clip-path, google-fonts, radial-gradient]
process_pattern: from-scratch
starting_point: scratch
ai_role: co-designer
iterations: 3
inspiration:
  - Pintura renascentista italiana (séc. XV–XVI)
  - Técnica chiaroscuro de Rembrandt
  - Fibonacci e a Divina Proporção
difficulty: 4/5
---

## Conceito

Galeria de 3 obras geradas em CSS/SVG puro — sem imagens externas. Arte clássica reinterpretada como código: espiral de Fibonacci, retrato com chiaroscuro geométrico, paisagem com perspectiva atmosférica. Cada obra em moldura dourada com placa de bronze. Interação: hover zoom + spotlight que segue o mouse, clique abre modo exame com painel de informações em latim e português.

## Briefing inicial

"Galeria de arte renascentista com 3 obras em SVG puro — sem imagens. Espiral de Fibonacci, retrato com chiaroscuro, paisagem clássica com coluna dórica. Fundo pergaminho com feTurbulence, molduras douradas, tipografia Cinzel Decorative + EB Garamond. Velas animadas. Scroll reveal com clip-path. Hover: zoom + spotlight. Clique: modo exame com painel informativo em latim."

## Prompts e iterações

### v1 — galeria base + obras em SVG

Resumo: parchment background com SVG filter inline, layout das 3 obras com molduras, SVGs básicos de cada obra (espiral, retrato, paisagem), placas douradas, tipografia clássica.

<details>
<summary>Prompt completo v1</summary>

"v1 do 06-renascimento-digital. Galeria com 3 obras SVG. Fundo pergaminho via feTurbulence inline. Google Fonts: Cinzel Decorative + EB Garamond. Molduras: gradient dourado. Obra I: espiral fibonacci com arcos SVG. Obra II: rosto geométrico chiaroscuro (radialGradient como luz Rembrandt). Obra III: paisagem com montanhas sobrepostas + coluna dórica em polygon. Placas douradas embaixo de cada obra. Velas simples no header. Footer com latim."

</details>

**O que faltou**: scroll reveal, velas animadas, obras mais detalhadas.

### v2 — scroll reveal + vela animada + obras melhoradas

Resumo: clip-path reveal com IntersectionObserver (sequência 250ms entre obras), candle flame com steps(1) flickering em dois ritmos, espiral fibonacci com retângulos dourados marcando a decomposição.

<details>
<summary>Prompt completo v2</summary>

"Adiciona ao v1: clip-path inset(100%→0%) com IntersectionObserver (stagger 250ms), candle flicker com steps(1) animation (2s e 1.7s independentes), hover na vela intensifica glow. Melhora espiral fibonacci: adiciona retângulos de decomposição + arcos mais precisos + texto 'Divina Proportione'."

</details>

**O que faltou**: hover spotlight, modo exame, cursor lupa.

### v3 — hover spotlight + modo exame + cursor lupa

Resumo: spotlight radial seguindo mousemove dentro do frame, clique abre overlay com SVG clone + painel informativo com texto em latim, cursor SVG de lupa dentro dos frames.

<details>
<summary>Prompt completo v3</summary>

"Adiciona ao v2: hover no frame — painting scale(1.08) + spotlight radial que segue o mouse (radial-gradient dinâmico via JS). Clique: overlay com SVG clonado + painel com title/year/desc/latin deslizando da direita (translateX). Esc ou click fora fecha. Cursor SVG lupa (circle + line) visível dentro dos frames, padrão fora. Dados descritivos das 3 obras hardcoded em EXAMINE_DATA."

</details>

**Resultado final**: galeria imersiva com arte gerada em código, interação rica e contexto cultural.

## Decisões de processo

- SVG puro ao invés de canvas: escalável, acessível via DOM, clonável para o modo exame.
- `feTurbulence` inline como data-URI: zero request extra para a textura de pergaminho.
- `steps(1)` para o flicker da vela: discreto como chama real, não suave como glow LED.
- `clip-path: inset()` para scroll reveal: mais performático que opacity/translate para elementos grandes.
- Spotlight via `radial-gradient` dinâmico no JS: 2 linhas de código, efeito dramático.

## Aprendizados transferíveis

- SVG `radialGradient` com centro off-center simula iluminação direcional convincente sem WebGL.
- `clip-path: inset(100% 0 0 0)` → `inset(0)` como scroll reveal: limpíssimo, sem translate/opacity.
- Cursor SVG via `position:fixed` + JS mousemove: mais flexível que `cursor: url()` (suporte melhor, sem restrições de tamanho).
- Clonar SVG com `.cloneNode(true)` para modo exame: sem re-renderizar, mantém todos os gradientes e filtros.
- feTurbulence como data-URI inline: textura sem request de rede, funciona com file:// também.
