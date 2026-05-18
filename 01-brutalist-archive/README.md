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
