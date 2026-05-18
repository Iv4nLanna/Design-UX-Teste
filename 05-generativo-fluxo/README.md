---
title: Campo de Fluxo Generativo
date: 2026-05-17
style: generative
tags: [generative-art, procedural, perlin-noise, interactive, flow-field]
techniques: [p5js, perlin-noise, particle-system, canvas, hsb-color]
process_pattern: from-scratch
starting_point: scratch
ai_role: co-designer
iterations: 3
inspiration:
  - Campos vetoriais matemáticos
  - Arte generativa de Vera Molnár e Casey Reas
difficulty: 3/5
---

## Conceito

Campo de fluxo vetorial com Perlin noise. 800 partículas nascem nas bordas, seguem vetores calculados pelo noise, acumulam trilha com fade lento — criando "fósseis" de movimento. Peso das linhas e velocidade variam pelo gradiente local do noise. Hue das cores desloca lentamente ao longo do tempo. O mouse atrai as linhas; clique dispara explosão. Design que nunca é o mesmo duas vezes.

## Briefing inicial

"Cria um campo de fluxo generativo com p5.js. 800 partículas seguem vetores de Perlin noise, deixando trilhas que se acumulam com fade lento. Mouse como atrator, clique como explosão. 5 paletas alternáveis com C, reset com R, pausa com Space. Linhas com peso variável pelo noise local. Hue shift lento ao longo do tempo. UI mínima no canto com os controles."

## Prompts e iterações

### v1 — campo de fluxo base

Resumo: p5.js, Particle class, noise field, 800 partículas, paleta oceano, acumulação por alpha baixo.

<details>
<summary>Prompt completo v1</summary>

"v1 do 05-generativo-fluxo. p5.js 1.9.0 CDN. Canvas fullscreen. Particle class com spawn nas bordas, steering por noise(x*0.003, y*0.003, t)*TWO_PI*4, maxAge 150-200, alpha fade. 800 partículas, noiseDetail(4, 0.5). Paleta oceano: ['#001220','#0077b6','#00b4d8','#90e0ef','#caf0f8']. background(0,8) por frame para fossils."

</details>

**O que faltou**: interação com mouse, paletas, controles de teclado.

### v2 — atrator + paletas + teclado

Resumo: mouse como atrator (raio 200px, força proporcional a 1/dist), clique spawna 200 partículas rápidas, C alterna 5 paletas, R reset com novo noiseSeed, Space pausa.

<details>
<summary>Prompt completo v2</summary>

"Adiciona ao v1: mouse attractor (força 0.4, raio 200px), mousePressed spawna 200 partículas rápidas (speed 2-5) no ponto do clique, keyPressed C alterna paletas (oceano/fogo/floresta/aurora/mono), R reset com noiseSeed aleatório, Space toggle pausa."

</details>

**O que faltou**: peso variável, HSL shift temporal, UI de controles.

### v3 — peso variável + HSL shift + UI

Resumo: strokeWeight de 0.2–2.5 baseado em noise local (segunda escala), hue desloca +0.05° por frame via colorMode(HSB), UI labels no canto inferior direito.

<details>
<summary>Prompt completo v3</summary>

"Adiciona ao v2: strokeWeight variável (noise em escala 2x, mapeado 0.2-2.5), speed variável por segundo octave de noise (0.7-1.5x), colorMode(HSB) com hueShift global incrementado +0.05 por frame, UI overlay com textSize 11 mostrando paleta atual e atalhos."

</details>

**Resultado final**: sistema vivo com variação de espessura, cor e velocidade — cada sessão única.

## Decisões de processo

- `background(0, 0, 0, 8)` ao invés de `clear()`: acumulação de trilhas é o efeito principal.
- Spawn nas bordas ao invés do centro: linhas percorrem a tela inteira antes de morrer.
- `noiseDetail(4, 0.5)`: 4 octaves com persistência 0.5 dá padrão visualmente rico sem ser caótico.
- HSB colorMode só durante o loop de partículas: evita conflito com os comandos de UI (RGB).

## Aprendizados transferíveis

- `noiseDetail(4, 0.5)` + escala 0.003: sweet spot para campos de fluxo que parecem orgânicos.
- Dois scales de noise independentes (0.003 para direção, 0.006 para espessura) criam variação sem correlação visual óbvia.
- colorMode(HSB) com hueShift global: forma simples de animar paletas sem redesenhar partículas.
- Spawn nas bordas + fade por alpha: partículas preenchem o espaço naturalmente, sem clustering.
