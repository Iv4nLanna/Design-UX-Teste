---
title: Low-Poly 3D
date: 2026-05-17
style: low-poly
tags: [3d, threejs, interactive, colorful, geometric]
techniques: [threejs, icosahedron, flat-shading, vertex-colors, orbit-controls, raycaster]
process_pattern: from-scratch
starting_point: scratch
ai_role: co-designer
iterations: 3
inspiration:
  - Figma Config visuals
  - Bruno Simon portfolio (threejs.journey.com)
difficulty: 4/5
---

## Conceito

Cena Three.js com icosaedros low-poly faceted: vertex colors aleatórios de
uma paleta de 10 cores saturadas, flat shading (cada face uma cor sólida),
wireframe ghost semitransparente. 3 shapes em órbitas independentes + hover
pulse no shape central. Overlay tipográfico com tags de tecnologia.

## Briefing inicial

"Cria uma cena Three.js com um icosaedro low-poly usando vertex colors aleatórios
de uma paleta de 10 cores. Flat shading. Rotação auto com OrbitControls. Standalone
HTML, Three.js via importmap/CDN."

## Prompts e iterações

### v1 — cena base

Resumo: cena funcional com 1 icosaedro, vertex colors, flat shading, OrbitControls
autoRotate, resize handler.

<details>
<summary>Prompt completo v1</summary>

Cria uma cena Three.js standalone em HTML (sem build, importmap com unpkg).
Requisitos:
- Three.js 0.160.0 via importmap
- OrbitControls da mesma versão
- IcosahedronGeometry(1.5, 1) — detail level 1 pra manter faceted
- Vertex colors: a cada 3 vertices (= 1 face), atribuir mesma cor aleatória
  de: ['#FF6B6B','#4ECDC4','#45B7D1','#96E6A1','#DDA0DD','#FFD93D','#6BCB77','#FF8B94','#A8DADC','#F4A261']
- MeshPhongMaterial flatShading:true vertexColors:true
- Luz: AmbientLight('#334466', 0.9) + DirectionalLight branca (4,6,4)
- OrbitControls: enableDamping, dampingFactor .06, enableZoom false, autoRotate true speed .8
- Background: #0c0c1a
- Resize handler

</details>

**O que faltou:** Tela toda apenas 3D — sem contexto tipográfico, sem composição.

### v2 — wireframe ghost + overlay de texto

Resumo: adicionei wireframe ghost com opacity .08 sobre o sólido (escala 1.015x
pra evitar z-fighting). Overlay HTML fixo com título e rodapé de metadados.

<details>
<summary>Prompt completo v2</summary>

Partindo do v1, adiciona:
1. Wireframe ghost: segundo Mesh com IcosahedronGeometry(1.52, 1),
   MeshBasicMaterial wireframe:true transparent:true opacity:.08
   Agrupados com Group.
2. Overlay HTML: position:fixed inset:0 pointer-events:none z-index:10
   - Canto superior esquerdo: "Low-Poly 3D"
   - Canto superior direito: "N°03 / 2026"
   - Rodapé esquerdo: técnicas (Three.js · Icosahedron · Flat Shading)
   - Rodapé direito: "Claude × Ivan Lanna"
   Fonte Helvetica, letra-espaçamento, text-transform uppercase

</details>

**O que faltou:** Composição ainda monótona (1 shape). Sem profundidade.

### v3 — 3 shapes + hover pulse + névoa

Resumo: função buildGroup() extrai criação do mesh. 3 icosaedros posicionados:
central grande, dois menores nas laterais em órbitas independentes. Raycaster
detecta hover no central e aplica scale lerp. Névoa sutil. Luz pontual ciano.

<details>
<summary>Prompt completo v3</summary>

Partindo do v2, refatora pra buildGroup(radius, wireOpacity) e cria:
- main: buildGroup(1.5, .08) no centro
- left: buildGroup(0.7, .12) em (-3.2, -0.5, -1)
- right: buildGroup(0.55, .15) em (3.0, 0.8, -0.5)
left.rotation.y = t * 0.4 no animate
right.rotation.y = -t * 0.6, right.rotation.x = t * 0.3
Raycaster: intersectObject(main.children[0]) pra detectar hover.
Hover: scale lerp pra 1.08. Sem hover: lerp pra 1.0. Fator: 0.08.
Névoa: THREE.Fog('#0c0c1a', 8, 18)
Luz pontual: PointLight('#4ECDC4', 1.2, 12) em (-3, 2, 2)
Overlay v2 refinado: description text + tags com border no rodapé.

</details>

**O que funcionou:** Composição com 3 shapes deu profundidade imediatamente.
O scale lerp via Vector3.lerp ficou suave sem vibrar.
**Dificuldade real:** Z-fighting entre sólido e wireframe — resolveu com escala 1.015x no wireframe.

## Decisões de processo

- Three.js: micro-gerenciei mais do que nos outros exemplos. Tive que corrigir:
  a escala do wireframe (z-fighting), o fator de lerp (muito rápido na primeira vez),
  a posição das luzes (primeira versão deixava o shape escuro de um lado).
- Refatorar pra `buildGroup()` foi sugestão do Claude no v3 — boa call,
  evitou repetição.
- Raycaster em `main.children[0]` (o sólido): tive que especificar explicitamente,
  o Claude tentou primeiro com o Group inteiro (que não funciona com raycaster diretamente).

## Aprendizados transferíveis

- **Three.js precisa mais micro-gerenciamento** que CSS puro. Coisas como z-fighting,
  posição de luz, e detalhes de API (raycaster em Mesh vs Group) precisam ser
  corrigidos manualmente. (visto em 03-low-poly-3d)
- **Z-fighting wireframe+sólido**: resolver com scale 1.01-1.02x no wireframe.
  (visto em 03-low-poly-3d)
- **scale.lerp() com Vector3** é mais limpo que lerp manual — e o Claude sugere
  essa API naturalmente. (visto em 03-low-poly-3d)
- **Composição 3D melhora drasticamente** com múltiplos shapes em planos Z
  diferentes. Um shape único parece demo; três shapes parecem cena.
