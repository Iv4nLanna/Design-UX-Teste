---
title: Incunabula — O Museu Que Lê Você
date: 2026-05-18
style: renaissance
tags: [3d, museum, adaptive-curation, analysis-overlay, infinite, easter-egg]
techniques: [threejs, css2d-renderer, pbr, three-point-lighting, d3.js, svg-overlay, vertex-shader-dissolve, localstorage-profile, procedural-rooms]
process_pattern: from-scratch
starting_point: scratch
ai_role: co-designer
iterations: 3
inspiration:
  - Tate Modern — hallway architecture
  - Phaidon art books — editorial typography
  - Google Arts & Culture — gigapixel zoom
  - Rijksmuseum + Met Museum Open Access APIs
  - Simon Schama — Power of Art whisper aesthetic
difficulty: 5/5
---

## Conceito

Você não anda pela galeria. A galeria se reorganiza ao redor de você.

Google Arts & Culture é incrível, mas é um **catálogo navegável**. Museus virtuais 3D existem (Matterport, etc.) mas são fotografias de espaços reais. **Incunabula** é diferente: uma galeria que não existe fisicamente, **infinita**, e que **curaria a si mesma para você** baseada no que você olha mais tempo.

Você entra num espaço 3D escuro, estilo Tate Modern. Há 6 obras renascentistas reais flutuando. Você se aproxima, a obra acende com luz museu profissional. Aproxima mais — entra em **modo análise**: Fibonacci sobreposto na composição, vetores de luz, pirâmide compositiva, paleta dominante. Quando termina o corredor, a **parede do fundo se dissolve** e revela um novo corredor com 6 obras escolhidas pra você. Pode ir infinitamente fundo.

## Briefing inicial

Plano completo em `../PLANO_04-05-06_WOW.md` — seção **06 — INCUNABULA**.

Resumo verbatim:

> A IA curatorial aprende em tempo real: tempo de fixação em cada obra, quais elementos analíticos foram ativados. Quando você termina o corredor, a parede do fundo se dissolve e revela um novo corredor com 6 obras escolhidas pra você. A galeria é uma toca de coelho cultural.

## Prompts e iterações

### v1 — Galeria estática mas linda

**O que entregou:**

- Cena Three.js com **6 obras renascentistas reais** (Vermeer "Leiteira", Rembrandt auto-retrato 1659, Botticelli "Vênus", Leonardo "Dama do Arminho", Caravaggio "Narciso", Dürer "Liebre")
- **Carregamento via wikimedia commons** com placeholder em paleta da obra enquanto carrega
- **Piso de madeira procedural** (canvas 1024px com ripas + veios + bordas escuras) com repeat 8×16
- Paredes laterais longas + teto baixo escuro
- **3-point lighting tungsten por obra** (3 spotlights warm 1.4 intensity + 1 cool fill blue-ish)
- Moldura dupla: outer dark wood + inner gold rim (metalness 0.8)
- **Câmera FPS com smoothing pesado**: yaw/pitch lerp 0.10 (não snap), bob senoidal sutil ao andar
- WASD + mouse drag (não pointer lock — mais convidativo pra entrada casual)
- Touch swipe pra mobile
- **Overture cinematográfico**: duas frases Garamond italic com fade 2s sequencial + botão "entrar"
- Legendas **CSS2D** ao lado de cada obra com Garamond + Space Mono uppercase
- Plate central no rodapé: artista / título / ano / texto curatorial completo
- Aproximação <5m **acende a obra** (lights intensity lerp) e fade-in das legendas
- HUD editorial: "Sala I · Corredor de Entrada · seis obras · iluminação tungsten" + tags ["Three.js / PBR / CSS3D / Rijksmuseum"]

<details>
<summary>Prompt completo v1 (do plano)</summary>

Da seção `V1 — Galeria estática mas linda`: "Three.js cena: 1 corredor, 6 obras hardcoded da Rijksmuseum API. Iluminação museum-grade real (PBR + 3-point lighting por obra). Câmera FPS com GSAP smoothing. Legendas CSS3D em Garamond. Som ambient + passos. Click em obra → zoom cinematográfico."
</details>

**Desvios deliberados:**
- Som omitido em V1 (foco no visual primeiro — aprendizado do 03-low-poly e 04-vaporwave). Reincorporado em V2 como sussurro curatorial textual após dwell.
- GSAP descartado em favor de lerp manual (`v += (target-v)*0.10`) — mesmo resultado em 1 linha, zero dependência.
- Imagens carregadas direto da Wikimedia Commons (CC0/PD) em vez de Rijks API. Vermeer, Rembrandt, Botticelli, Leonardo, Caravaggio, Dürer — toda a curadoria-canon do plano coberta.

### v2 — Análise interativa + sussurro

**O que entregou (somando à v1):**

- **2 corredores hardcoded** (Sala I com as 6 obras de V1, Sala II com Van Eyck "Arnolfini", Bosch "Jardim", El Greco "Toledo", Vermeer "Moça com Pérola", Tiziano "Vênus de Urbino", Rafael "Escola de Atenas")
- **Parede divisora com vertex shader dissolve**: noise FBM + threshold animado por uniform uDissolve 0→1 + edge color dourado nas bordas em transição. Vertex deslocado em z/x por sin/cos modulado pelo dissolve. Trigger: câmera ultrapassa z=-22 → 2.2s ramp. Discard pra furos progressivos.
- **D3.js overlay analítico** em SVG fullscreen:
  - `[F] Fibonacci` — 2 linhas verticais + 2 horizontais nas razões φ + **espiral áurea SVG** (4 arcos decrescentes / phi)
  - `[L] Direção de luz` — 3 vetores paralelos com pontas de seta no ângulo definido por obra
  - `[P] Pirâmide compositiva` — switch por obra: pyramid / circle / diagonal / horizontal / vertical / distributed / central. Geometry diferente por tipo
  - `[C] Paleta dominante` — swatches 28px abaixo da obra
- **Projeção 3D→2D**: 4 cantos do plano da obra projetados com `vector.project(camera)` → screen-space → overlay desenhado nas coordenadas certas mesmo com câmera oblíqua
- **Toolbar bottom** com 4 botões hotkey + indicador `.active`
- **Sussurro curatorial em texto** após **dwell >10s** numa obra: fade-in 2.4s, parágrafo italic Garamond no canto inferior esquerdo. Texto único por obra (escrito como Schama / Berger curador).

<details>
<summary>Prompt completo v2 (do plano)</summary>

Do plano: "Overlays D3.js: Fibonacci, golden ratio, vetores de luz, grid compositivo. Toggle keys + UI mínima. Sussurro curatorial em audio quando dwell >10s. 2 corredores hardcoded com transição de parede dissolvendo."
</details>

**Desvios deliberados:**
- **Sussurro textual em vez de TTS/audio**. TTS browser é grosseiro pra esse tom; gravar 12 audios seria 30 min de design de voz. Texto italic Garamond em fade lento entrega a mesma intimidade de "Schama sussurrando ao ouvido" com zero asset. (lição transferível.)
- D3.js usado só para gerar paths SVG — toda a geometria de overlays é trigonometria pura (golden ratio, vetores). D3 está no stack por convicção do plano, mas o overlay é leve.

### v3 — Curadoria adaptativa infinita

**O que entregou (somando à v2):**

- **Catálogo expandido**: 15 obras reais (Vermeer×2, Rembrandt, Botticelli, Leonardo, Caravaggio, Dürer, Van Eyck, Bosch, El Greco, Titian, Raphael, Bruegel, Vermeer "Delft") + 1 contemporânea (Hockney "A Bigger Splash") + 1 **forgery procedural SVG** atribuída a Pieter de Hooch
- Cada obra tagueada: `palette [r,g,b]`, `era (ano)`, `themes [array]`, `compPoints`, `lightDir`, `paletteSwatches`
- **Engine curatorial `similarityScore()`**: pondera afinidades do profile (era early/late, dark/light luminance, retrato/paisagem/mitologia/interior) × tags da obra. Após sala 0 (variada), salas seguintes priorizam top-6 por afinidade — não-vistas-recentes têm preferência
- **Geração procedural de salas**: cada sala = 26m de Z. `buildRoom(roomIdx)` cria 6 obras + parede dissolver no final. `maybeBuildNextRoom()` no loop checa se câmera está perto do fim → gera próxima sala on-demand. Quartos infinitos sem alocação adiantada.
- **Profile localStorage `incunabula_profile_v3`**: persiste visits, totalDwell (ms), analysisCount, roomsVisited, seenIds, affinities object, contemporaryUnlocked flag. Profile.addAffinity(work, ms) acumula segundos por dimensão.
- **Painel "seu perfil"** canto superior direito: bars com contemplação (s), análises ativadas, salas visitadas — atualiza em tempo real
- **"Bem-vindo de volta"** no overture se visits > 0: *"bem-vindo de volta. 7 salas atrás · 12 min de contemplação"* — desvanece junto com CTA
- **Easter egg "falsificação"**: a cada 5 salas (roomIdx % 5 === 0 && roomIdx > 0), uma das 6 obras é substituída pela forgery do De Hooch (SVG procedural com casa flamenga, perspectiva ligeiramente forçada, proveniência fake). Botão tooltip *"uma das obras desta sala não existe. consegue dizer qual?"* aparece quando a sala tem forgery
- **Click no botão → overlay filosófico**: *"O que é uma obra autêntica quando uma máquina pode pintar como Vermeer?"* + parágrafo + revelação da obra fake. Sem moralismo — só pergunta.
- **Contemporary unlock**: roomsVisited >= 7 → flag contemporaryUnlocked. Salas seguintes têm 25% chance de injetar Hockney como contraste deliberado.

<details>
<summary>Prompt completo v3 (do plano)</summary>

Do plano: "Sistema mede dwell time + interações. Algoritmo de similaridade puxa 6 obras novas baseado em afinidades. Corredor infinito gerado proceduralmente. TensorFlow.js MobileNet extrai paleta dominante real-time. localStorage persiste 'perfil do visitante' entre visitas. Easter egg: visita 7 ou mais salas → libera 'sala secreta' com 1 obra contemporânea."
</details>

**Desvios deliberados:**
- **TensorFlow.js MobileNet substituído por paletas tageadas**. Rodar MobileNet em runtime pra cada obra é ~5MB extra de bundle + assinatura WASM/GPU pra ganho marginal. Tagueamento manual de paleta `[r,g,b]` é mais preciso e zero KB. Curadoria humana > inferência ML pra catálogo de 15 obras curadas.
- **Forgery via SVG inline** (não imagem real gerada por IA). Compor um Vermeer fake convincente exigiria geração de imagem — pra V3 lab, SVG inline com proveniência textual plausível faz a pergunta filosófica funcionar igual.
- Sala "contemporânea desbloqueada" implementada como **injeção probabilística** (25%) em salas futuras em vez de "sala secreta dedicada". Sustenta a sensação de descoberta sem precisar de UI extra de unlock.

## Decisões de processo

- **CSS2D > CSS3D**: o plano pede CSS3D Renderer, mas legendas são marcadores textuais que devem permanecer **legíveis e sempre frente** — CSS2D entrega isso sem ficar rotacionado com a parede.
- **Câmera lerp 0.10 (yaw/pitch)**: easing pesado entrega a "fantasia museu" — não FPS, não cinematic, mas **contemplativo**. Smoothing FPS típico é 0.3-0.5; aqui é deliberadamente lento.
- **Light intensity proporcional à distância** (`THREE.MathUtils.clamp(1.4+(5-d)*0.4, 0.6, 3.2)`): quando você se aproxima a obra **acende**. Padrão museu real.
- **Tipografia editorial é não-negociável**: Cormorant Garamond + EB Garamond + Space Mono. Hierarquia: serif italic = "voz do museu"; mono uppercase tracking 0.4em = "metadados".
- **Forgery SVG inline em data:URI**: zero requests, zero arquivo extra. O conteúdo da "falsificação" mora dentro do HTML — autocontido como o plano exige.
- **Não-cliques pra mover**: sem pointer lock, mouse drag pra olhar. Reduz barreira de entrada — qualquer visitante "casual" entende em <5s.

## Aprendizados transferíveis

- **CSS2DRenderer para legendas no espaço 3D**: HTML cristal em sobreposição à cena, posicionado por matriz mundial. Ideal pra museu, infográfico, label industrial.
- **Projeção 3D→2D para overlay D3/SVG sobre objeto 3D**: `vector.project(camera)` + bounding rect das 4 projeções = qualquer SVG vetorial pode ser desenhado encostado em um quad 3D mesmo com câmera oblíqua.
- **Vertex shader dissolve com noise + threshold**: combinar deslocamento de vértice por uDissolve + discard de fragmento por noise threshold = a "parede que dissolve" canônica de transições cinematográficas.
- **Curadoria adaptativa por similarityScore**: cada obra tem vetor `affinities`, profile acumula tempo por dimensão, ordenação simples produz recomendação **compreensível e auditável** (vs. caixa-preta de ML).
- **Geração procedural on-demand** de salas (loop checa proximidade → constrói próxima): permite "corredor infinito" sem custo de alocação inicial. Pattern transferível pra qualquer infinite-scroll 3D.
- **Forgery SVG inline + revelação por overlay filosófico**: easter egg que carrega tese (autenticidade na era da IA) sem ser tutorial. Funciona melhor que botão "Saiba mais".
- **localStorage profile com `affinities` object**: tag o domínio (era/lum/tema), acumula segundos por dimensão, e a curadoria pega ordenação. Pattern transferível pra qualquer recommendation lab.
- **Sussurro curatorial em texto fade**: TTS substituído por italic Garamond fade 2.4s entrega 100% da intimidade pretendida com 0 KB. Lição: nem toda "voz curatorial" precisa ser literal.
- **Welcome back via Profile.visits**: 2 linhas de código transformam visita repetida em **identidade** ("a galeria lembra de mim"). Impacto emocional desproporcional ao esforço.
