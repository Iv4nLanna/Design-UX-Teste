# Design-UX-Teste

Laboratório de processo — não uma galeria. O objetivo é descobrir o melhor
processo de fazer design artístico e conceitual em software usando IA (Claude).
Cada pasta é um experimento documentado: o briefing, as iterações, o que
funcionou e o que virou aprendizado transferível.

→ [Aprendizados acumulados de processo](PROCESS.md)

## Exemplos

| N° | Conceito | Estilo | Live Preview | Processo |
|----|----------|--------|--------------|----------|
| 01 | Brutalist Archive | brutalism | [abrir](https://iv4nlanna.github.io/Design-UX-Teste/01-brutalist-archive/) | [README](01-brutalist-archive/README.md) |
| 02 | Pixel 8-bit | pixel-art | [abrir](https://iv4nlanna.github.io/Design-UX-Teste/02-pixel-8bit/) | [README](02-pixel-8bit/README.md) |
| 03 | Low-poly 3D | low-poly | [abrir](https://iv4nlanna.github.io/Design-UX-Teste/03-low-poly-3d/) | [README](03-low-poly-3d/README.md) |
| 04 | Vaporwave / Synthwave | vaporwave | [abrir](https://iv4nlanna.github.io/Design-UX-Teste/04-vaporwave-synthwave/) | [README](04-vaporwave-synthwave/README.md) |
| 05 | Campo de Fluxo Generativo | generative | [abrir](https://iv4nlanna.github.io/Design-UX-Teste/05-generativo-fluxo/) | [README](05-generativo-fluxo/README.md) |
| 06 | Renascimento Digital | renaissance | [abrir](https://iv4nlanna.github.io/Design-UX-Teste/06-renascimento-digital/) | [README](06-renascimento-digital/README.md) |

## Como adicionar um exemplo

```bash
cp -r _template/ NN-novo-conceito/
# edite _template/README.md com seu briefing
# itere com Claude — salve cada iteração significativa em iterations/vN.html
# copie a versão final pra index.html
# adicione linha na tabela acima
# desfile aprendizados pra PROCESS.md
git add . && git commit -m "feat: add NN-novo-conceito"
```

## Sobre este laboratório

- **Processo > artefato.** O index.html final é evidência; o README é o experimento.
- **DeepSeek << Claude.** Ao executar estes designs com DeepSeek (vs Claude),
  a qualidade do resultado foi muito inferior — menos precisão nas coordenadas
  SVG, interações mais pobres, e necessidade de muito mais micro-gerenciamento.
- **Zero atrito.** HTML/CSS/JS puro, CDN only. Abre clicando.
- **Reprodutível.** Prompts completos preservados em `<details>` por iteração.
- Spec: [docs/superpowers/specs/](docs/superpowers/specs/)
