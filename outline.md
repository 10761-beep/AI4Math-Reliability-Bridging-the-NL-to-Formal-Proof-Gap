# 论文大纲 / Paper Outline

## 题目
Decomposing the Natural-Language-to-Formal Proof Gap:
A Four-Layer Analysis of Why LLM Formal Theorem Proving Stalls at 30–80%

## 作者占位
[你的名字] · [你的机构] · 2026

---

## 0. Abstract (~200 words)
- 现象：formal proof 是唯一理论上零幻觉的数学输出（proof checker 确定性）
- 矛盾：SOTA 在 miniF2F-test 上仍只到 ~73%（BFS-Prover, ACL 2025）；AlphaProof IMO 银牌但**题面人工翻译**
- 论点：端到端 pass@k 数字把四种不同性质的失败混在一起
- 贡献：(1) 提出四层鸿沟分解；(2) 用现有论文数字逐层定位瓶颈；(3) 指出 Dafny 空证 40.6% 这一被忽视的基线；(4) 提议分层评估协议

## 1. Introduction (~1 page)
- 1.1 为什么 formal proof 重要（可靠性 vs NL 推理幻觉）
- 1.2 现状数字快照（Table 位置）
- 1.3 问题：端到端数字为什么具有误导性
- 1.4 贡献列表（4 条）

## 2. Background (~1 page)
- 2.1 Proof assistants：Lean 4 / Coq / Isabelle/HOL / Dafny
- 2.2 Benchmarks：miniF2F (244 test) / ProofNet / Mathlib / TRIGO / OBT
- 2.3 LTP 范式：whole-proof generation (Baldur) vs tactic prediction (Lean Copilot) vs tree search (MCTS / BFS-Prover)

## 3. The Four-Layer Gap Framework (~1.5 pages) 【核心章节】
- **L1. Theorem Formalization Gap**：NL 题面 → 正确的 FL theorem statement
  - 证据：AlphaProof 2024 IMO 人工翻译题面；ProofBridge 2025 专门做这件事
  - 为什么难：变量名歧义、隐式域、定义依赖
- **L2. Proof Planning Gap**：高层策略分解（lemma 该怎么拆）
  - 证据：ProntoQA (Saparov & He, ICLR 2023)——单步演绎对，但多路径探索系统性失败
  - BC-Prover pseudo-steps 显式在补这一层
- **L3. Low-Level Tactic Detail Gap**：类型、unification、rewrite 方向、参数显式化
  - 证据：PALM (Lu et al., 2024)——520 个错误分析显示高层结构对但低层错
  - APRIL (Wang et al., 2026)——编译器反馈驱动的 repair
- **L4. Search & Repair Gap**：证明状态空间搜索、失败后回退
  - 证据：BFS-Prover 72.95% (ACL 2025)；Coq lemma extraction 66→79%
  - 这是已被 tree search 推到局部极限的一层

## 4. Evidence Mapping: Where Existing Systems Sit (~1.5 pages)
- Table 1：系统 × 四层覆盖 × miniF2F 数字
  | 系统 | 年份 | L1 | L2 | L3 | L4 | miniF2F-test |
  |---|---|---|---|---|---|---|
  | GPT-4 zero-shot | 2023 | ✗ | ~ | ~ | ✗ | 25.4% |
  | TheoremLlama | 2024 | bootstrapped | ~ | ✓ | ✗ | 33.6% |
  | Lean Copilot | 2024 | ✗ | ✓ | ✓ | ✗ | n/a (step) |
  | PALM | 2024 | ✗ | ~ | ✓(repair) | ~ | +76–180% |
  | BC-Prover | 2024 | ✗ | ✓(pseudo) | ~ | ✓ | SOTA 时 |
  | BFS-Prover | 2025 | ✗ | ~ | ~ | ✓(DPO) | 72.95% |
  | ProofBridge | 2025 | ✓(joint emb) | ~ | ✓ | ✓(repair) | 提升 SC +31% |
- 4.1 关键观察：**L1 几乎无人系统解决**；L4 已饱和；L3 是 generate-then-repair 主战场
- Figure 1：四层金字塔图（L1 在最顶端最难）

## 5. The Baseline Nobody Talks About (~1 page)
- miniF2F-Dafny (Bakšys et al., 2025)：**空证就能过 40.6% test**
- 含义：40.6% 的题目根本不需要 LLM，纯符号自动化可解
- 重新计算"LLM 真正增量"：(72.95 − 40.6) / (100 − 40.6) ≈ **54%** 的剩余差距被 LLM 填补
- 启示：未来论文必须同时报告"符号基线空证率"，否则数字不可比

## 6. Towards a Layer-Resolved Evaluation Protocol (~0.5 page)
- 定义每层 pass rate：p1, p2, p3, p4
- 端到端 ≠ 乘积，因为层间有信息泄漏（例：proof repair 可以跨层）
- 提议报告格式

## 7. Discussion & Limitations (~0.5 page)
- 我们没跑新实验；数字全部来自已发表论文
- miniF2F 本身偏本科数学；研究生级问题的层分布可能不同
- Lean 生态偏置（Mathlib 训练数据占绝对主导）

## 8. Conclusion (~0.25 page)
- 召回四层框架
- 下一个突破点预测：L1（自动形式化题面）+ L2（proof planning）

## 图表清单
- Figure 1: Four-layer pyramid（用 TikZ 或 matplotlib 画）
- Table 1: System-by-layer coverage
- Table 2: Failure mode taxonomy（L3 的错误类型，来自 PALM 的 520 错误分析）
