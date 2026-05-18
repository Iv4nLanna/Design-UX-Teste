# Processo de Design Artístico com IA — Aprendizados

Documento vivo. Cada exemplo finalizado contribui bullets aqui.
Organizado por tema, não por ordem cronológica.

## Sobre briefing inicial

- Briefings com constraints técnicos explícitos (paleta HEX, técnicas por nome,
  dimensões numéricas) convergem mais rápido — v1 já 80% correto.
  (visto em 01-brutalist-archive)

## Sobre referências visuais

_Nenhum aprendizado ainda._

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

## Sobre iteração e convergência

- 3 iterações costumam ser suficientes: v1 (estrutura), v2 (composição),
  v3 (refinamento + detalhes). (visto em 01, 02 e 03)

## Sobre limites técnicos (CSS, WebGL, animações)

- Web Audio API: Claude gerencia bem, mas volumes precisam calibração manual
  (ponto de equilíbrio: gain ~0.08 para UI sounds). (visto em 02-pixel-8bit)
- Z-fighting wireframe+sólido: resolver com scale 1.01-1.02x no wireframe.
  (visto em 03-low-poly-3d)
- Composição 3D: mínimo de 3 shapes em planos Z diferentes pra parecer cena
  e não demo. (visto em 03-low-poly-3d)

## Sobre constraints estilísticos rígidos

- Paleta NES como variáveis CSS nomeadas: Claude respeitou 100%, sem inventar
  cores fora da paleta. (visto em 02-pixel-8bit)

---

_Exemplos contribuídos: 01-brutalist-archive, 02-pixel-8bit, 03-low-poly-3d._
