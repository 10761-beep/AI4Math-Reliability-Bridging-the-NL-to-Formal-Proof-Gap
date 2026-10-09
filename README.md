
# AI4Math Reliability: Bridging the NL-to-Formal Proof Gap

围绕 AI4Math 可靠性框架的可投稿 LaTeX 学术论文项目。 | A submission-ready LaTeX paper on the reliability of AI for mathematics.

## 项目简介 / About

**EN**: This project delivers a submission-ready LaTeX paper that decomposes the natural-language-to-formal proof gap in LLM theorem proving into four layers — (L1) theorem formalization, (L2) proof planning, (L3) low-level tactic detail, (L4) search & repair — and re-reads them through the lens of intersemiotic translation (Jakobson, Nida, Venuti, Swales). Key finding: the state-of-the-art 73% pass@k on miniF2F overstates the LLM contribution — a Dafny empty-proof baseline solves 40.6%, so the true LLM increment is ≈54%. The paper argues for a layer-resolved evaluation protocol.

**中文**: 本项目交付一篇可投稿的 LaTeX 学术论文，将 LLM 定理证明中"自然语言 → 形式化证明"的鸿沟分解为四层（题面形式化、证明规划、低层 tactic 细节、搜索与修复），并以符际翻译理论（Jakobson、Nida、Venuti、Swales）重新解读。核心发现：miniF2F 上 SOTA 的 73% pass@k 高估了 LLM 贡献——Dafny 空证基线即可解 40.6%，LLM 真实增量约 54%。论文提出分层评估协议（layer-resolved evaluation protocol）。

## 仓库结构 / Structure

```
.
├── paper.tex          # 论文源文件（可编译）
├── references.bib     # 24 篇参考文献（BibTeX）
├── paper.pdf          # 编译产物（9 页）
├── AAR.md             # After Action Review 复盘
├── logs/
│   └── ai-log.md      # 完整 AI 使用日志（可追溯）
├── docs/
│   ├── outline.md     # 论文骨架（过程稿）
│   └── literature-map.md  # 文献地图（过程稿）
└── figures/           # 图（TikZ 内绘，无需外部资源）
```

## 编译方法 / Compile

```bash
pdflatex paper.tex
bibtex paper
pdflatex paper.tex
pdflatex paper.tex
```

需要 TeX Live 或 MiKTeX（含 `tikz`、`natbib`、`booktabs`、`amsmath`）。不依赖外部素材，离线可编译。

## 交付物与评分对照 / Deliverables vs. Rubric

| 交付物 | 对应评分项 |
|---|---|
| paper.tex + references.bib | researchRigor / technicalExecution |
| paper.pdf（可编译证明） | artifactCompleteness |
| logs/ai-log.md | aiUsage |
| AAR.md | reflectionQuality |

## License

MIT License. See [LICENSE](LICENSE).
