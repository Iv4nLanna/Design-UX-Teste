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
