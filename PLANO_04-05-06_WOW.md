# Plano: 04, 05, 06 — Experiências WOW

Filosofia: cada exemplo é uma **obra**, não uma demo. O espectador não "vê" — ele **habita**. A web é o medium; a IA é o pincel; o navegador é a galeria.

---

## 04 — VAPORWAVE DREAM ENGINE
### "Você não vê o sonho. Você é o sonhador."

### Conceito Disruptivo

Vaporwave virou cliché de Tumblr 2015 — grades neon, estátuas gregas, palmeiras. **Todo mundo já viu**. A inovação aqui: transformar vaporwave de **estética visual** em **estado mental interativo**.

Você abre a página. Não há scroll. Não há menu. Você está em **um quarto digital infinito** ao pôr do sol roxo eterno. Uma estátua de mármore flutua, partilculada, fragmentada. Há um VHS rolando no canto, tocando um clipe que **não existe** — é gerado em tempo real pela sua webcam (com permissão) filtrada em CRT scanlines + chromatic aberration. Você vira a cabeça (mouse/giroscópio do celular) e a câmera vira no mundo 3D. A música muda de frequência conforme você se aproxima de objetos — sintetizador modal reativo (Tone.js). 

O disruptivo: vaporwave sempre foi **passivo, contemplativo, melancólico**. Aqui ele é **agência**. Você caminha pela nostalgia.

### Tech Stack

- **Three.js** (r160+) — cena 3D principal, post-processing pipeline
- **GSAP + ScrollTrigger** — timing das transições narrativas
- **Tone.js** — síntese de áudio reativa, oscilladores modulados por posição
- **Postprocessing.js** (Three.js addon) — CRT shader, VHS noise, chromatic aberration, bloom intenso
- **Cannon-es** — física leve para partículas e fragmentos da estátua
- **MediaPipe Face Mesh** (opcional, V3) — webcam tracking para inserir rosto do user em texturas
- **Stats.js** — debug-only, removido em prod
- Assets: modelo de busto greco-romano CC0 (Sketchfab/Poly Haven), textura mármore, palmeiras low-poly

### Arquitetura Experiencial

**Onboarding (0-5s)**: tela preta. Texto rosa neon digita: *"LOADING DREAM..."*. Som de VHS rebobinando. Glitch. **Boom** — você está dentro.

**Mundo principal**: 
- Chão de grade infinita (shader procedural, não geometria) que reage ao mouse — ondulações sutis
- Sol gigante (sprite + shader) ao fundo com listras horizontais escuras animadas
- Busto grego flutuando ao centro, rotação lenta. Ao clicar/tocar, ele **explode em partículas** que se reorganizam após 3s
- 6 palmeiras low-poly em silhueta
- Plano d'água espelhada abaixo (CubeCamera reflection)
- Estrelas em parallax (3 layers de profundidade)

**Interação**:
- Mouse = câmera (FPS-like, sem clique pra mover, só olhar)
- WASD/setas/swipe = caminhar lentamente (velocidade dreamlike, não FPS)
- Click = "tocar" objetos, cada um tem reação (busto explode, palmeira vibra som, sol pulsa)
- Áudio panning espacial — Tone.js conectado a posição XYZ do mouse

**Easter egg do áudio**: ficar parado 30 segundos → começa uma "música oculta" baseada em A-ha "Take On Me" desafinada em escala dórica, sintetizador modular.

### Roadmap V1 → V2 → V3

**V1 — Foundation (a cena viva)**
- Cena Three.js completa com grade, sol, palmeiras, busto, água
- Câmera first-person com lookAt baseado em mouse
- Post-processing pipeline (CRT + chromatic + bloom)
- Música ambiente loop simples (não gerativa ainda)
- 60fps em laptop médio

**V2 — Reatividade (o mundo responde)**
- Tone.js substitui audio estático: oscilladores modulados por posição XYZ
- Click no busto → fragmenta em ~500 partículas com Cannon physics, recompõe em 3s (GSAP)
- Grade do chão ondula conforme cursor
- Partículas seguem o cursor formando trilha estilo "fairy dust" rosa/ciano
- Sistema de "humor" do ambiente — após 1min, paleta drift sutil pra outra tonalidade vaporwave

**V3 — Identidade (você no sonho)**
- Webcam opt-in: MediaPipe Face Mesh captura rosto, projeta em TV CRT no canto da cena
- "Tirar uma foto polaroid" — botão que captura screenshot + adiciona moldura polaroid + glitch, baixa PNG
- Modo mobile completo: giroscópio = câmera, touch swipe = caminhar
- Easter egg da Take On Me hidden
- Modo "screensaver" — se inativo 2min, câmera começa cinematic auto-tour

### Easter Egg / Surpresa

Konami code (↑↑↓↓←→←→BA) ativa **MODO PROFUNDO**: toda a cena vira preto-e-branco CRT, busto vira **liquefação em looping (vertex shader)**, audio vira drone ambient, e palavras flutuam pelo espaço: *"o que você estava procurando aqui?"*. Não há saída — só fechar a aba. Inquietante de propósito.

### Métrica de Sucesso WOW

- Pessoa fica >2min sem clicar em nada — apenas olhando
- Captura screenshot e posta em redes sem ser pedido
- Volta no dia seguinte
- Frase típica: *"isso roda no navegador?!"*

---

## 05 — CONFLUENCIA: A OBRA QUE VOCÊ DEIXA RASTRO
### "Toda visita pinta uma pincelada. A obra é coletiva. E inacabável."

### Conceito Disruptivo

Arte generativa em código existe desde Processing 2001 (Reas, Fry). Quase toda é **solo** — você abre, vê, fecha, perdeu. **Confluência inverte isso**: a tela é uma **obra única, persistente, mundial**, que evolui pincelada por pincelada com cada visitante anônimo do mundo. Você chega. Vê o que **24.832 pessoas pintaram antes de você** nas últimas semanas. Adiciona sua marca. Sai. Sua marca fica.

Não é um quadro coletivo bagunçado tipo r/place. É uma **pintura abstrata curada pela física**: cada visitante adiciona "energia" (um traço gestural com mouse/touch), e o sistema generativo usa **fluid dynamics** (estilo Navier-Stokes simplificado, à la Refik Anadol) pra absorver essa energia na composição global. Resultado: pintura sempre coerente, sempre evoluindo, sempre única no tempo, mas com **traço de cada alma que passou**.

Paleta muda com **hora real do espectador** — amanhecer = pastéis quentes, meio-dia = saturado, pôr do sol = magentas/ouros, noite = índigo profundo + ciano. Estação do ano influencia textura (inverno = grãos cristalinos; verão = orgânico fluido).

### Tech Stack

- **p5.js** + **WebGL mode** — engine principal, shaders custom
- **GLSL** — fluid simulation shader (advection + diffusion + pressure solve)
- **Firebase Firestore** (free tier) ou **Supabase** — persistir snapshots da obra a cada N minutos + lista de "almas" (anônimas, só timestamp + país via IP)
- **GSAP** — transições de abertura cinematográficas
- **Howler.js** — paisagem sonora ambient generativa baseada em densidade da pintura
- **Vanilla JS** para UI mínima

Dados:
- Snapshot da pintura salvo a cada 5min em Firestore como base64 reduzido (256x256)
- Contagem de "almas" + array de timestamps + geolocalização aproximada (cidade, não IP)

### Arquitetura Experiencial

**Abertura (0-8s)**: tela branca → fade-in de um número crescendo rápido: **"24,832 almas pintaram antes de você"**. Embaixo, texto pequeno: *"Você é a 24,833ª."*. Click → entra.

**A obra**: ocupa tela inteira. Pintura abstrata grande, em movimento sutil (fluid sim a 30fps). Não é estática — está respirando. Você vê **fantasmas tênues** se movendo — são "ecos" das últimas 50 pinceladas feitas por outras pessoas (replays sutis).

**Sua pincelada**:
- Mouse down = começa a "soltar tinta" — cor depende da hora local do user
- Arrastar = pincelada com pressão (tamanho varia com velocidade, GSAP smoothing)
- Mouse up = sua pincelada se **funde** no fluid sim e se torna parte da obra
- Mensagem: *"sua pincelada foi adicionada. ela ficará."*

**Mapa do mundo (canto inferior)**: pontinhos luminosos onde outras almas pintaram. Click → vê traço dela em replay tênue.

**Áudio**: paisagem sonora drone, frequências mudam com densidade de cor da obra. Mais vermelho = mais grave; mais azul = mais agudo. Howler.js cross-fading 4 stems.

### Roadmap V1 → V2 → V3

**V1 — Fluid + Pincelada local**
- p5.js WebGL com fluid shader funcionando
- Pincelada do mouse adiciona velocidade + cor ao campo
- Paleta hardcoded inicial (3 paletas: dia, crepúsculo, noite — escolhe por hora local)
- 60fps em laptop
- Salva localStorage da última visita (não global ainda)

**V2 — Persistência global**
- Firebase Firestore: a cada 5min salva snapshot global
- Ao carregar, restaura último snapshot como ponto de partida da fluid sim
- Contador real "X almas pintaram antes de você"
- Mini-mapa mundial com pontinhos das últimas 100 pinceladas

**V3 — Vida própria + sonora**
- Howler.js ambient stems reativos à composição
- Replays "fantasmas" das últimas pinceladas em loop tênue
- "Tirar souvenir": botão que gera screenshot personalizado com sua pincelada destacada em ciano + texto *"você foi a 24.833ª. esta foi sua marca."* — baixa como PNG
- Estação influencia textura (Date.now() → primavera/verão/outono/inverno modifica params do shader)
- Easter egg: meia-noite local do user → modo "obra dorme", animação muito lenta, cores acinzentadas

### Easter Egg / Surpresa

Se o user **não pintar nada** e ficar 90 segundos só olhando, aparece em fade lento: *"você não precisa pintar. olhar também é arte."* — e o sistema **adiciona automaticamente** uma pincelada sutil baseada no movimento do mouse dele durante a contemplação. Fica registrado como "alma silenciosa". Estatística separada conta quantos passaram em silêncio.

### Métrica de Sucesso WOW

- Pessoa fica >5min na primeira visita
- Volta semanas depois pra "ver como está"
- Compartilha link sem ser pedido
- Frase típica: *"deixei minha marca em algo permanente"*

---

## 06 — INCUNABULA: O MUSEU QUE LÊ VOCÊ
### "Você não anda pela galeria. A galeria se reorganiza ao redor de você."

### Conceito Disruptivo

Google Arts & Culture é incrível, mas é um **catálogo navegável**. Museus virtuais 3D existem (Matterport, etc) mas são **fotografias de espaços reais**. Incunabula é diferente: é uma **galeria que não existe fisicamente**, **infinita**, e que **curaria a si mesma para você** baseada no que você olha mais tempo.

Você entra num espaço 3D escuro estilo Tate Modern. Há 6 obras renascentistas reais flutuando (alta resolução, Rijksmuseum API + Met Open Access). Você se aproxima, a obra **acende com luz museu profissional** (3 luzes warm tungsten + 1 cool fill, modelo físico real). Aproxima MAIS — entra em **modo análise**: overlay vetorial mostra **Fibonacci/golden ratio sobreposto** na composição, mapa de **direção de luz** (vetores), análise de **piramidação compositiva** (Da Vinci style), legenda curatorial em tipografia editorial séria (estilo Phaidon book).

A IA curatorial **aprende em tempo real**: quanto tempo você olhou cada obra, quais elementos analíticos você ativou. Quando você termina o corredor, a parede do fundo **se dissolve** e revela um **novo corredor** com 6 obras escolhidas pra você — não algoritmo de recomendação ruim, mas baseado em afinidades estéticas (paleta, época, tema, composição). Pode ir infinitamente fundo. **A galeria é uma toca de coelho cultural.**

### Tech Stack

- **Three.js** (r160+) — espaço 3D, iluminação física (físically-based rendering)
- **CSS3D Renderer** (Three.js addon) — overlays HTML sobre o 3D para legendas tipográficas crispy
- **GSAP** — todo timing de câmera, transições entre salas, fade das obras
- **APIs reais**:
  - **Rijksmuseum API** (gratuita, sem auth) — Vermeer, Rembrandt, etc
  - **Met Museum Open Access** (CC0) — coleção massiva
  - **Art Institute of Chicago API** — alta resolução
- **D3.js** — overlay de análise compositiva (Fibonacci, vetores de luz, grids)
- **Howler.js** — paisagem sonora: passos em piso de madeira, ambient reverb de sala alta, sussurros distantes (museu real)
- **TensorFlow.js MobileNet** (opcional, V3) — análise visual real-time de obra pra extrair paleta dominante automática
- **localStorage** — persistir "preferências aprendidas" do visitante

### Arquitetura Experiencial

**Abertura (0-10s)**: tela preta. Fade-in MUITO lento de uma frase em serifa elegante (Cormorant Garamond ou EB Garamond): *"Você está prestes a entrar em um museu que não existe."*. Fade. Próxima: *"Cada sala foi feita para você. Mesmo que você ainda não saiba."*. Click → entra.

**Sala 1 — Corredor de Entrada**:
- Espaço 3D escuro, piso de madeira escura (textura PBR), parede com 6 obras dispostas em ritmo museológico (espaçamento real de curadoria)
- Iluminação ambient muito baixa. Cada obra tem 3 spotlights tungsten focados (luz museum-grade)
- Câmera FPS com easing pesado (não snap, GSAP smoothing 0.8s)
- Som: passos em madeira sincronizados com movimento, reverb de sala alta

**Aproximação de uma obra**:
- Distância >5m: obra é silhueta com glow tênue
- 5m-2m: obra acende em alta resolução (texture LOD), legenda surge em CSS3D ao lado em tipografia editorial
- <2m: **modo análise** ativa automaticamente — overlay D3.js vetorial sobrepõe composição
- Toggle keys: [F] Fibonacci, [L] direção de luz, [C] paleta, [P] pirâmide compositiva

**Sistema curatorial adaptativo**:
- Sistema mede tempo de fixação em cada obra (dwell time)
- Mede quais overlays analíticos foram ativados
- Ao chegar no fim do corredor, parede do fundo **dissolve em GSAP** (vertex shader displacement) revelando sala seguinte
- Sala seguinte: 6 obras escolhidas por afinidade — algoritmo simples mas eficaz (similaridade de paleta dominante + tag de tema + época)
- Pode continuar infinitamente

**Audio detail**: ao parar em frente a uma obra >10s, áudio sutil começa — não música, mas **sussurro curatorial** (TTS opcional ou audio gravado) lendo trecho do texto curatorial. Como ter Simon Schama ao seu ouvido.

### Roadmap V1 → V2 → V3

**V1 — Galeria estática mas linda**
- Three.js cena: 1 corredor, 6 obras hardcoded da Rijksmuseum API (Vermeer "Leiteira", Rembrandt, etc)
- Iluminação museum-grade real (PBR + 3-point lighting por obra)
- Câmera FPS com GSAP smoothing
- Legendas CSS3D em Garamond
- Som ambient + passos
- Click em obra → zoom cinematográfico

**V2 — Análise interativa**
- Overlays D3.js: Fibonacci, golden ratio, vetores de luz, grid compositivo
- Toggle keys + UI mínima
- Sussurro curatorial em audio quando dwell >10s
- 2 corredores hardcoded com transição de parede dissolvendo

**V3 — Curadoria adaptativa infinita**
- Sistema mede dwell time + interações
- Algoritmo de similaridade puxa 6 obras novas da API baseado em afinidades
- Corredor infinito gerado proceduralmente
- TensorFlow.js MobileNet extrai paleta dominante real-time para afinidade
- localStorage persiste "perfil do visitante" entre visitas (volta dias depois → galeria lembra)
- Easter egg: visita 7 ou mais salas → libera "sala secreta" com 1 obra contemporânea (Hockney, Bacon) com contraste deliberado

### Easter Egg / Surpresa

Em uma das salas (aleatoriamente uma a cada 5), uma das 6 obras é **uma falsificação sutil** — IA generativa estilo Vermeer mas obra que **não existe**. Legenda curatorial é convincente, com proveniência fake plausível. No fim da sala, micro-texto cinza claro embaixo: *"uma das obras desta sala não existe. consegue dizer qual?"*. Click pra revelar. Comentário filosófico sobre autenticidade na era da IA — sem moralismo, só pergunta.

### Métrica de Sucesso WOW

- Sessão média >8min
- Pessoa explora >3 salas sequenciais
- Volta com link salvo
- Frase típica: *"eu não sabia que entendia tanto de arte"* ou *"isso me fez sentir culto"*
- Compartilhamento espontâneo com screenshot de overlay Fibonacci

---

## Filosofia Comum aos Três

1. **Lentidão deliberada**: nenhum dos três tem pressa. Animações pesadas em easing (GSAP power3.out, 1-2s). Web hoje é frenética; estes são contemplativos.
2. **Sem onboarding tutorial**: você descobre interagindo. Confiança no usuário inteligente.
3. **Tipografia como protagonista**: Cormorant Garamond, EB Garamond, Space Mono. Nada de Inter genérico.
4. **Som não é trilha — é arquitetura**: cada experiência é incompleta no mute.
5. **Mobile-respeitoso, não mobile-first**: cada um tem fallback mobile honesto (touch + gyro), mas o **canonical experience** é desktop com mouse + áudio.
6. **Persistência**: 04 lembra sua última visita (localStorage), 05 é globalmente persistente, 06 aprende você ao longo do tempo. Web hoje é amnésica; estes têm memória.

---

## Stack Final

```
Comum aos três:
- GSAP 3.12+ (timing)
- Vite (build) ou vanilla ES modules (zero-build)

04: Three.js r160 + postprocessing + Tone.js + Cannon-es + MediaPipe (V3)
05: p5.js 1.9 + WebGL + GLSL custom + Firebase Firestore + Howler.js
06: Three.js r160 + CSS3DRenderer + D3.js + Rijks/Met APIs + Howler.js + TF.js MobileNet (V3)
```

Bundle size esperado: 04 ~800KB gzipped, 05 ~400KB, 06 ~1.2MB.

**Princípio**: Opus builder deve atacar V1 completo dos três antes de qualquer V2. V1 já deve ser WOW.
