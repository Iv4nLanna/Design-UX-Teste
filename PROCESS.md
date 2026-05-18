# Processo de Design Artístico com IA — Aprendizados

Documento vivo. Cada exemplo finalizado contribui bullets aqui.
Organizado por tema, não por ordem cronológica.

## Sobre briefing inicial

- Briefings com constraints técnicos explícitos (paleta HEX, técnicas por nome,
  dimensões numéricas) convergem mais rápido — v1 já 80% correto.
  (visto em 01-brutalist-archive)
- Foco em interação, criatividade e detalhes profundos ao briefing acelera convergência:
  Claude prioriza camadas de detalhe desde a v1. (visto em 04, 05, 06)

## Sobre referências visuais

- Estética reconhecível (vaporwave, renascimento) funciona como referência implícita:
  Claude acessa o visual cultural sem precisar de URL. (visto em 04 e 06)

## Sobre quando deixar o Claude liderar vs micro-gerenciar

- Grid layouts assimétricos: micro-gerenciar. O Claude tende pra grids regulares.
  (visto em 01-brutalist-archive)
- Implementações CSS de efeitos conhecidos (glitch, blend-mode): deixar o Claude
  propor — tende a ser melhor do que uma spec manual.
  (visto em 01-brutalist-archive)
- Three.js: micro-gerenciar mais do que CSS puro. API details (raycaster em Mesh
  vs Group, z-fighting wireframe) precisam correção manual.
  (visto em 03-low-poly-3d)
- Refatoração interna (ex: extrair buildGroup()): deixar o Claude propor — tende
  a ser boa call. (visto em 03-low-poly-3d)
- Arte generativa (p5.js flow field): deixar o Claude propor o algoritmo inteiro
  da primeira vez. Resulta em elegância inesperada. (visto em 05-generativo-fluxo)
- SVG art complexa (chiaroscuro, espiral Fibonacci): micro-gerenciar as coordenadas
  e proporções — buscando acurácia visual. (visto em 06)

## Sobre iteração e convergência

- 3 iterações costumam ser suficientes: v1 (estrutura), v2 (composição),
  v3 (refinamento + detalhes). (visto em 01, 02 e 03)
- v1 CSS-only (sem JS) é boa estratégia para visual primeiro, depois adicionar
  interação. (visto em 04-vaporwave-synthwave)

## Sobre limites técnicos (CSS, WebGL, animações)

- Web Audio API: Claude gerencia bem, mas volumes precisam calibração manual
  (ponto de equilíbrio: gain ~0.08 para UI sounds). (visto em 02-pixel-8bit)
- Z-fighting wireframe+sólido: resolver com scale 1.01-1.02x no wireframe.
  (visto em 03-low-poly-3d)
- Composição 3D: mínimo de 3 shapes em planos Z diferentes pra parecer cena
  e não demo. (visto em 03-low-poly-3d)
- `steps(1)` é o modo correto para simular discretização digital (flicker, glitch):
  mais realista que easing suave. (visto em 04 e 06)
- colorMode(HSB) em p5.js: trocar de RGB para HSB mid-sketch permite animações de cor
  elegantes sem quebrar logicamente. (visto em 05-generativo-fluxo)
- SVG feTurbulence como data-URI inline: funciona em file:// e não requer request HTTP
  — otimização silenciosa. (visto em 06-renascimento-digital)

## Sobre constraints estilísticos rígidos

- Paleta NES como variáveis CSS nomeadas: Claude respeitou 100%, sem inventar
  cores fora da paleta. (visto em 02-pixel-8bit)
- Constraint cultural forte (vaporwave 80s, renascimento italiano) é suficiente como
  "paleta implícita" — Claude interpreta visualmente sem lista de cores. (visto em 04 e 06)
- Escala pentatônica como constraint de áudio: garante harmonia independente de ritmo,
  mesmo com notas aleatórias. (visto em 04-vaporwave-synthwave)

## Sobre interação e modos especiais (V3 lessons)

- Examine mode / overlay com trap focus: padrão dialog nativo (role="dialog", aria-modal)
  + ESC + clique fora + gestão de foco anterior — implementado sem libs em ~80 linhas JS.
  (visto em 06-renascimento-digital V3)
- stroke-dashoffset para animar paths SVG: idioma mais limpo que transformar element ou
  usar GSAP. Ideal para espirais, linhas de construção e trajetos técnicos. (visto em 06)
- localStorage para persistência de arte generativa: transforma demo em "obra que envelhece"
  — impacto emocional desproporcional ao esforço técnico. (visto em 05-generativo-fluxo V3)
- Easter eggs condicionados a gestos repetidos (3x click): recompensar exploração sem
  sinalização excessiva. Melhor que botões escondidos. (visto em 04-vaporwave-synthwave V3)
- Boot screen estilo terminal como loading: barata de implementar (setTimeout + classList),
  mas vende a fantasia do produto desde o primeiro frame. (visto em 04-vaporwave-synthwave V3)

---

_Exemplos contribuídos: 01-brutalist-archive, 02-pixel-8bit, 03-low-poly-3d, 04-vaporwave-synthwave, 05-generativo-fluxo, 06-renascimento-digital._
