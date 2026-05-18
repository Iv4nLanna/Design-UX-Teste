---
title: Vaporwave / Synthwave
date: 2026-05-17
style: vaporwave
tags: [retro, neon, synthwave, parallax, chromatic-aberration]
techniques: [css-3d, css-animation, web-audio, clip-path, box-shadow-stars, custom-properties]
process_pattern: from-scratch
starting_point: scratch
ai_role: co-designer
iterations: 3
inspiration:
  - Estética visual dos anos 80
  - Capas de álbuns synthwave
difficulty: 3/5
---

## Conceito

Página de artista fictício "NEON PARALLAX". Grade 3D perspectiva com animação infinita, céu degradê roxo→laranja, sol semicírculo com listras, 80+ estrelas via box-shadow puro (zero JS), shapes geométricos flutuando. Retro-futurismo dos anos 80 como linguagem visual completa. Web Audio API para feedback sonoro em nota pentatônica aleatória.

## Briefing inicial

"Página de artista fictício estilo synthwave/vaporwave dos anos 80. Grade 3D perspectiva infinita, céu gradiente roxo para laranja, sol semicírculo, formas geométricas flutuando, texto neon com aberração cromática. Mouse cria paralaxe em camadas. Clique toca nota synth. Foco em interação, criatividade e detalhes profundos."

## Prompts e iterações

### v1 — estrutura visual base (CSS-only)

Resumo: sky gradient, perspectiva 3D da grade, sol com listras, estrelas via box-shadow, título com glow, scanlines.

<details>
<summary>Prompt completo v1</summary>

"Cria v1 do 04-vaporwave-synthwave. Página de artista fictício 'NEON PARALLAX'. Visual base CSS-only: sky gradient roxo→laranja, grade 3D perspectiva com animação infinita, sol semicírculo com listras horizontais, 80+ estrelas via box-shadow em elemento 1px (zero JS), título com neon glow cyan, subtítulo 'SYNTHWAVE · 1987' em neon pink, overlay de scanlines via ::after. Sem JS ainda — só visual estático."

</details>

**O que faltou**: interação, shapes, feedback de áudio.

### v2 — paralaxe + shapes + Web Audio

Resumo: adicionadas 3 shapes flutuantes (pirâmide, losango, triângulo), mouse parallax em 3 camadas, clique toca nota sawtooth pentatônica via Web Audio API.

<details>
<summary>Prompt completo v2</summary>

"Adiciona ao v1: 3 shapes flutuantes com animação float (pirâmide neon-pink, losango neon-cyan, triângulo neon-yellow), paralaxe no mousemove com 3 velocidades (grid lento, hero médio, shapes rápido), Web Audio API no click (oscilador sawtooth, frequência aleatória da escala pentatônica, envelope 300ms), aceleração da grade no scroll."

</details>

**O que faltou**: aberração cromática no título, glitch no hover.

### v3 — aberração cromática + glitch

Resumo: título decomposto em 3 spans sobrepostos (R/branco/C), glitch periódico a cada 8s via CSS keyframes com steps(1), glitch contínuo acelerado no hover.

<details>
<summary>Prompt completo v3</summary>

"Adiciona ao v2: aberração cromática no título com 3 spans (chroma-r, chroma-w, chroma-c). Glitch idle: offsets R/C aparecem por 4 frames a cada 8s (steps(1)). Glitch on hover: animação 0.4s rápida com offsets maiores. Diamond shape mantém rotação 45deg durante parallax."

</details>

**Resultado final**: visual completo com camadas de profundidade, interação sonora e efeito cromático.

## Decisões de processo

- Estrelas via box-shadow puro: evita JS, mantém performance. Custo: posições fixas (não aleatórias por sessão).
- Escala pentatônica para o audio: garante que qualquer nota soa bem independente do ritmo do clique.
- Glitch com `steps(1)`: simula mudança digital discreta, mais fiel à estética CRT que ease.
- 3 layers de parallax com multiplicadores 20px/12px/8+px: hierarquia de profundidade clara.

## Aprendizados transferíveis

- `steps(1)` em keyframes simula transição digital — essencial para glitch, pixel-art, CRT effects.
- box-shadow com 80+ pontos para estrelas: zero JS, boa performance, visual convincente.
- Escala pentatônica como constraint de áudio: qualquer frequência aleatória soa harmonioso.
- Parallax de 3 camadas com multiplicadores distintos cria ilusão de profundidade com ~10 linhas de JS.
