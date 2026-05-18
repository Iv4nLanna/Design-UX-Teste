---
title: Vaporwave Dream Engine
date: 2026-05-18
style: vaporwave
tags: [3d, audio-reactive, fps, post-processing, easter-egg]
techniques: [threejs, webgl, glsl, tone.js, post-processing, fps-camera, particle-system, gyroscope, polaroid-capture]
process_pattern: from-scratch
starting_point: scratch
ai_role: co-designer
iterations: 3
inspiration:
  - Macintosh Plus — Floral Shoppe (2011)
  - Refik Anadol — Machine Hallucinations
  - VHS aesthetics, CRT shaders, A-ha "Take On Me"
  - Synthwave/outrun visual canon
difficulty: 5/5
---

## Conceito

Você não vê o sonho. Você **é** o sonhador.

Vaporwave virou cliché de Tumblr 2015 — grades neon, estátuas gregas, palmeiras. Todo mundo já viu. A inovação aqui: transformar vaporwave de **estética visual** em **estado mental interativo**.

Você abre a página, não há scroll, não há menu. Você está dentro de um quarto digital infinito ao pôr do sol roxo eterno. Um busto de mármore flutua, partilculado. Você caminha pela nostalgia.

## Briefing inicial

Plano completo em `../PLANO_04-05-06_WOW.md` — seção **04 — VAPORWAVE DREAM ENGINE**.

Resumo verbatim do plano:

> Vaporwave sempre foi passivo, contemplativo, melancólico. Aqui ele é agência.
> Mouse = câmera (FPS), WASD = caminhar, click = "tocar" objetos, áudio panning espacial.
> V1 foundation, V2 reatividade, V3 identidade. Cada V já deve ser WOW.

## Prompts e iterações

### v1 — Foundation: a cena viva

**O que entregou:** cena Three.js completa, navegável em FPS, com:

- Céu em domo shader (gradient roxo→magenta→âmbar do horizonte)
- Sol procedural com listras horizontais animadas
- Grade infinita procedural via shader (não geometria) — fade pela distância, mistura pink→cyan com depth
- Plano d'água shimmer com noise FBM
- Busto greco-romano stylizado procedural (esfera deformada + cabelo modular)
- 6 palmeiras low-poly silhueta
- 3 layers de estrelas com parallax
- Câmera FPS smooth (yaw/pitch com lerp 0.06) + WASD walking
- Bob da câmera (sin(t*2)*0.04 em Y) — sutil mas vende a fantasia
- Boot screen "Loading dream…" com flicker steps()
- Post-processing: UnrealBloom + CRT shader custom (curvatura, scanlines, chromatic aberration, vinheta, ruído)
- Compass HUD canto superior direito

<details>
<summary>Prompt completo v1 (do plano)</summary>

Da seção `V1 — Foundation` do plano: "Cena Three.js completa com grade, sol, palmeiras, busto, água. Câmera first-person com lookAt baseado em mouse. Post-processing pipeline (CRT + chromatic + bloom). Música ambiente loop simples (não gerativa ainda). 60fps em laptop médio."

</details>

**O que faltou:** áudio (V1 sem música — focar visual primeiro), reatividade real, partículas.

### v2 — Reactivity: o mundo responde

**O que entregou (somando à v1):**

- **Tone.js audio synth completo**: drone A2 (MonoSynth sine), pad fatsawtooth com chord progression dorian (A-F-G-E), bass triangle, reverb global 8s decay, low-pass filter modulado pela distância da origem (paisagem sonora que respira com o caminhar)
- **Cursor world tracking**: raycaster intersecta plano y=0, posição mundial vira uniform do grid shader — a grade **ondula a partir do cursor** com decay exponencial
- **Click no busto = explosão**: sistema de 600 partículas Points (vertexColors pink/cyan/white), velocidades radiais + gravidade, blending aditivo. 1.6s de explosão, depois 2s reformando com ease-out cúbico. Bust mesh visible=false durante.
- **Fairy dust trail**: ring buffer de 200 partículas seguindo cursor world position, lifetime decay, float-up Y. Cores random pink/cyan/white.
- **Sun pulse**: shader uniform uPulse senoidal lento
- **Mood drift**: array de 4 paletas (dusk, midnight, sunrise, amethyst). Lerp contínuo entre paletas a cada 60s. cPink/cCyan/hot/sun1 todos animados nos uniforms.
- **HUD mood indicator** "dusk → midnight" bottom center
- Shatter SFX: NoiseSynth white com envelope curto

<details>
<summary>Prompt completo v2 (do plano)</summary>

Do plano: "Tone.js substitui audio estático: oscilladores modulados por posição XYZ. Click no busto → fragmenta em ~500 partículas com Cannon physics, recompõe em 3s (GSAP). Grade do chão ondula conforme cursor. Partículas seguem o cursor formando trilha estilo 'fairy dust' rosa/ciano. Sistema de 'humor' do ambiente — após 1min, paleta drift sutil pra outra tonalidade vaporwave."

</details>

**Desvios deliberados:**
- Substituí Cannon-es por integração Euler manual (gravidade + velocidade radial). 600 partículas, sem colisão. Bibliotecas física overkill pra explosão pontual.
- GSAP descartado para o reforming — ease-out cúbico manual em ~5 linhas, mesmo resultado.

### v3 — Identity: você no sonho

**O que entregou (somando à v2):**

- **VHS Webcam**: botão "▸ VHS" abre `getUserMedia({video})` e mostra preview 180×120 canto superior direito com border rosa, badge "REC ●" piscando, scanlines via repeating-linear-gradient + filter saturate/hue-rotate
- **Polaroid Snapshot**: tecla [F] ou botão. Renderiza composer fresh, captura canvas via toDataURL, monta polaroid 720×860 em canvas offscreen: paper bg #f6efe3, photo área quadrada centrada, film grain (noise injetado no ImageData), glitch chromatic strips, caption italic "dream — YYYY-MM-DD HH:MM" em Georgia serif, download como PNG
- **Flash overlay** branco 150ms ao capturar
- **Gyro mobile**: detecta `DeviceOrientationEvent`, request permission iOS-style, mapeia gamma→yaw e beta→pitch
- **Touch swipe**: touchstart/move acumula delta, dispara keys WASD virtuais conforme direção
- **Auto-tour cinematic**: após 120s inativo (ou botão "▸ AUTO-TOUR"), câmera começa órbita circular `r=12+sin(t*0.07)*4` ao redor da cena
- **Easter egg Konami**: detector ↑↑↓↓←→←→BA via keydown buffer. Ativa **MODO PROFUNDO**: `body.deep` aplica grayscale CSS no canvas (failsafe) + uniforms `uDeep=1` no sky/grid/CRT shaders desaturando + chromatic aberration triplicada. Frase em italic Georgia "o que você estava procurando aqui?" aparece centralizada com fade 2s. Sem saída além de fechar a aba.
- **Hidden Take On Me**: contador `standStillTimer` mede tempo parado (sem mudança de XZ > 0.01). Após 30s parado, dispara melodia square synth dos primeiros 15 notas do hook do A-ha **em escala dórica** (F#-D-B-E-G#-A-B-A-G#-E-D-F# warped), com reverb 4s. Toca uma vez só (flag hiddenMelody).

<details>
<summary>Prompt completo v3 (do plano)</summary>

Do plano: "Webcam opt-in: MediaPipe Face Mesh captura rosto, projeta em TV CRT no canto da cena. 'Tirar uma foto polaroid' — botão que captura screenshot + adiciona moldura polaroid + glitch, baixa PNG. Modo mobile completo: giroscópio = câmera, touch swipe = caminhar. Easter egg da Take On Me hidden. Modo 'screensaver' — se inativo 2min, câmera começa cinematic auto-tour."

</details>

**Desvios deliberados:**
- MediaPipe Face Mesh substituído por webcam raw filtrada via CSS (saturate/hue-rotate). Face Mesh ~10MB extra de bundle pra zero ganho visual aqui — a estética CRT já distorce o rosto.
- "Polaroid + glitch" implementado em pure canvas (no html2canvas) — controle pixel-level real e ~30 linhas de JS.

## Decisões de processo

- **V1 sem áudio**: deliberado. Conforme aprendizado de 03-low-poly-3d, post-processing Three.js precisa micro-tuning; tirar áudio do critical path da V1 deixa converger o visual primeiro.
- **Grade procedural shader (não geometria)**: linhas via fract() + fwidth() ao invés de WireframeGeometry. Permite fade contínuo pela distância e ondulação custosa só nos shaders, não no CPU.
- **Busto procedural (não GLTF importado)**: sphere geometry deformada + cluster de spheres pro cabelo. Bundle zero, estilizado certinho pra estética vaporwave, e total de ~30 linhas. GLTF de busto greco-romano seria 2-5MB e fugiria do estilo.
- **Mood system como uniforms (não materiais)**: 4 paletas em arrays JS, lerp contínuo nos uniforms `cPink/cCyan/hot/sun1`. Drift acontece sem rebuild de materials.
- **Tone.js progressão dorian, não major**: minor 7th feel é central ao vaporwave melancólico-mas-doce. A=>F=>G=>E em qualidade dórica.

## Aprendizados transferíveis

- **Shader procedural > geometria** para grades infinitas: `fract() + fwidth()` resolve linha aliasing e permite distance fade contínuo sem morte por draw calls.
- **Mood drift via uniform lerp** é cheap e impactante. 4 paletas + transição 60s = parece "world ages" sem custar nada.
- **Particle explosion + reform** em pure Three.js (sem física lib) com Euler integration: 600 partículas a 60fps tranquilas. O reform com cubic ease-out é mais bonito que recompose linear.
- **Polaroid PNG via canvas pure**: capturar via `toDataURL` do renderer + montagem em offscreen canvas. Zero dependência. Film grain via ImageData mutation.
- **Konami code via keydown buffer + Array.every**: 6 linhas, sem libs. Sliding window.
- **CRT shader curva (uv*2-1) + offsets quadráticos** é a fórmula canônica. Combinada com vignette + chromatic + scanlines + RGB stripe, o efeito vende a fantasia.
- **Hidden melody como recompensa de presença** (>30s parado): incentiva contemplação, não cliques. O usuário descobre a estética sendo, não fazendo.
- **DeviceOrientationEvent requestPermission** é iOS-only — usar try/catch e fallback graceful pro Android.
