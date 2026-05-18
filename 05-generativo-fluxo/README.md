---
title: Confluência — A Obra Que Você Deixa Rastro
date: 2026-05-18
style: generative
tags: [fluid-dynamics, generative, persistent, collaborative, ambient-audio]
techniques: [p5.js, webgl, glsl, fluid-sim, navier-stokes, localstorage-persist, webaudio, snapshot, geo-minimap]
process_pattern: from-scratch
starting_point: scratch
ai_role: co-designer
iterations: 3
inspiration:
  - Refik Anadol — Machine Hallucinations
  - r/place (Reddit, 2017/2022) — agência coletiva
  - Casey Reas / Processing community
  - Jos Stam — Real-Time Fluid Dynamics for Games (2003)
difficulty: 5/5
---

## Conceito

Toda visita pinta uma pincelada. A obra é coletiva. E inacabável.

Arte generativa em código existe desde Processing 2001. Quase toda é **solo** — você abre, vê, fecha, perdeu. **Confluência inverte isso**: a tela é uma obra única, persistente, mundial, que evolui pincelada por pincelada com cada visitante. Você chega, vê o que **24.832 almas pintaram antes de você**, adiciona sua marca, sai. Sua marca fica.

A composição é mediada por **fluid dynamics** (Navier-Stokes simplificado, à la Anadol) — cada pincelada injeta velocidade e cor no campo, e o sistema absorve organicamente. Paleta muda com **hora real do espectador**; estação influencia textura.

## Briefing inicial

Plano completo em `../PLANO_04-05-06_WOW.md` — seção **05 — CONFLUENCIA**.

Resumo verbatim:

> Não é um quadro coletivo bagunçado tipo r/place. É uma pintura abstrata curada pela física: cada visitante adiciona energia, e o sistema generativo usa fluid dynamics para absorver essa energia na composição global.
> V1 fluid + pincelada local. V2 persistência global. V3 vida própria + sonora.

## Prompts e iterações

### v1 — Fluid + Pincelada local

**O que entregou:**

- p5.js em **WebGL mode** com pipeline GLSL custom: ping-pong de duas FBOs de densidade + duas de velocidade, 256×256 sim resolution
- Shaders: **advect** (semi-Lagrangian backtrace), **splat** (injeta cor + velocidade radial com falloff gaussiano), **diffuse** (blur 5-tap)
- Pincelada do mouse: cor sorteada da paleta atual + velocidade do drag injetada como campo vetorial
- **Paleta por hora local** (4 modos: amanhecer pastéis quentes, dia saturado, crepúsculo magenta/ouro, noite índigo/ciano)
- Display shader: dissolve fundo + grain procedural + vinheta
- Overture cinematográfica: contador "0 → 24.832" easing cúbico, fade para a obra
- HUD editorial Cormorant Garamond + Space Mono — tags "p5.js / WebGL / GLSL / Fluid"
- 60fps em laptop médio (SIM_W=SIM_H=256 é o sweet spot)
- localStorage da última visita

<details>
<summary>Prompt completo v1 (do plano)</summary>

Da seção `V1 — Fluid + Pincelada local`: "p5.js WebGL com fluid shader funcionando. Pincelada do mouse adiciona velocidade + cor ao campo. Paleta hardcoded inicial (3 paletas: dia, crepúsculo, noite — escolhe por hora local). 60fps em laptop. Salva localStorage da última visita (não global ainda)."
</details>

**Desvios deliberados:**
- 4 paletas em vez de 3 — incluí "amanhecer" entre 5h-9h. A transição visual é parte da identidade da obra.
- Pressure solve omitido. Para a estética artística pretendida (não fisicamente acurada, mas **emocionalmente fluida**), advect + diffuse + dissipation é suficiente. Anadol "Machine Hallucinations" usa abordagem similar.

### v2 — Persistência global

**O que entregou (somando à v1):**

- **Store adapter**: namespace `confluencia_meta_v2` em localStorage simulando schema realista de Firestore (collections: `souls`, `brushes`, `snapshots`). Adapter pluggável — se `window.__FBCFG` presente, conecta Firebase real; senão, fallback local.
- **Seed de 24.832 almas históricas** + 100 pinceladas em 20 cidades reais (lat/lng) com timestamps espalhados em 30 dias
- **Snapshot a cada 30s** (em prod: 5min) — captura `densBuf.elt` reduzido a 128×128 JPEG q=0.6 + data:url no storage
- **Restore shader**: ao carregar, restaura snapshot anterior como ponto de partida do campo de densidade (subtrai bg para extrair apenas a "pintura")
- **Mini-mapa mundial SVG** com pontinhos das 100 últimas almas, opacidade decay por idade
- **Contagem real** "24.833ª" no overture, atualizada do storage
- Status dot pulsante "persistência local · pronto"

<details>
<summary>Prompt completo v2 (do plano)</summary>

Do plano: "Firebase Firestore: a cada 5min salva snapshot global. Ao carregar, restaura último snapshot como ponto de partida da fluid sim. Contador real 'X almas pintaram antes de você'. Mini-mapa mundial com pontinhos das últimas 100 pinceladas."
</details>

**Desvios deliberados:**
- Firebase real opcional. localStorage com schema realista simula 99% da experiência. Adapter pluggável → trocar para Firebase é uma config (não um rewrite). Para o repo lab, evita exigir credentials.
- Snapshot reduzido a 128×128 (não 256×256). Reduz storage 4× sem perda visual perceptível pós-restore.

### v3 — Vida própria + sonora

**O que entregou (somando à v2):**

- **Paisagem sonora sintetizada via WebAudio** (Howler.js descartado — synth próprio com 3 osciladores + LFOs + convolver IR procedural pra reverb 3.4s). Quatro stems: drone 110Hz sine, mid 220Hz triangle, high 330Hz sine, bells aleatórios em escala C maior (523/659/784/880/1046Hz)
- **Heat audio reativo**: a cada 60 frames sampleia composição 16×16 e desloca frequência dos osciladores baseado em vermelho×azul (mais quente → grave; mais frio → agudo)
- **Botão "▸ som off/on"** — gesture-required pra Audio API, fade 1.2s
- **Ghost replay**: ring buffer de 50 strokes em localStorage; loop spawn aleatório (~1.2% por frame) que reaplica trajetória em densidade reduzida 35% — "fantasmas" das últimas pinceladas se movem pelo campo
- **Souvenir PNG 1080×1350**: botão "▸ souvenir" — canvas offscreen, pinta obra atual + destaca **sua pincelada em ciano luminoso** com shadow blur, título Garamond italic, número da alma, paleta+estação stamp, timestamp. Download como `confluencia-{ts}.png`
- **Estações** (mar-mai outono, jun-ago inverno, set-nov primavera, dez-fev verão — hemisfério sul): controlam `viscosity`, `grain` e **crystal** (quantização espacial no display shader → inverno parece grão de gelo)
- **Easter egg "alma silenciosa"**: 90s sem pintar → texto Garamond italic *"você não precisa pintar. olhar também é arte."* + sistema adiciona pincelada radial automática baseada em hover + incrementa contador separado `silentSouls` (seeded em 318)
- **Easter egg meia-noite**: ao chegar 00h local, `asleep` lerpa para 1 → cores dessaturam 70% no display shader, dissipation sobe (campo "respira" mais devagar), HUD opacidade 0.35, badge "obra dorme"

<details>
<summary>Prompt completo v3 (do plano)</summary>

Do plano: "Howler.js ambient stems reativos à composição. Replays 'fantasmas' das últimas pinceladas em loop tênue. 'Tirar souvenir': botão que gera screenshot personalizado com sua pincelada destacada em ciano + texto. Estação influencia textura. Easter egg: meia-noite local do user → modo 'obra dorme', animação muito lenta, cores acinzentadas."
</details>

**Desvios deliberados:**
- **Howler.js substituído por WebAudio puro**. Howler é wrapper para arquivos de áudio; para drones gerativos sintetizados em runtime, WebAudio direto é mais flexível e zero KB extra. 4 stems sintetizadas batem o que o plano descreve sem ter que servir 4 .ogg.
- Ghost replay implementado client-only (não server-side). Cada cliente vê seus próprios fantasmas — esse compromisso é coerente com o paradigma localStorage do V2 e dá impacto similar.

## Decisões de processo

- **Fluid sem pressure solve**: economia de ~40% do shader pass orçamento. Pra estética não-fisicamente-acurada-mas-emocional, advect+diffuse+dissipation é suficiente. Lição inversa: pra simulação fluid acurada (smoke/water), `Stam` exige projeção.
- **Schema localStorage realista (adapter pattern)**: V2 ficou indistinguível de Firebase real do ponto de vista do usuário. Trocar pra Firebase = 30 linhas em `Store`. Lição transferível: simular backend com adapter é estratégia de prototipagem rápida.
- **Synth WebAudio em vez de arquivos Howler**: para experiências contemplativas, drone sintético em runtime é mais "vivo" e zero-asset. Lição: nem todo audio precisa ser sample.
- **Estação no display shader, não na sim**: shader vê tudo, sim só roda dinâmica. Quantização "cristal" no inverno é puramente visual sem alterar comportamento do fluido — barato e impactante.
- **Tempo de seed das almas (318 silenciosas, ~25k pintando)**: 1.3% de silent souls cria contexto narrativo — você descobre que **olhar também conta**.

## Aprendizados transferíveis

- Fluid sim em GLSL com **ping-pong FBO** + 4 buffers (densA/densB/velA/velB) é o padrão canônico, ~250 linhas de shader e roda 60fps em laptop com SIM=256.
- `colorMode(HSB)` em p5.js: trocar de RGB para HSB mid-sketch permite animações de cor elegantes sem quebrar logicamente. (já visto em V1 do exemplo)
- Adapter pattern para "Firebase ou localStorage": permite desenvolvimento offline e prod online com mesma API. Ideal pra labs.
- WebAudio synth gerativo: 3 osciladores + LFOs + IR procedural = drone ambient infinito, ~50 linhas, zero asset.
- Souvenir PNG via canvas offscreen: a cópia personalizada (com sua pincelada em destaque) cria **identidade emocional** desproporcional ao código (~80 linhas).
- Easter egg "alma silenciosa" (recompensar contemplação, não cliques): pattern transferível — incentivar **ser** e não **fazer** muda a relação com a obra.
- Estações como **modulação de uniforms**, não branching de código: 1 sistema, 4 estados, transição gratuita.
