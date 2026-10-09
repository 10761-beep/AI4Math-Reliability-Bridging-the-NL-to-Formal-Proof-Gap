# 文献地图 / Literature Map

> 三条子线 × 关键论文 × 在本论文中的角色

## 子线 A：自然语言数学推理的可靠性缺陷

| 论文 | 年份/会议 | 核心发现 | 对本论文的用途 |
|---|---|---|---|
| Frieder et al., "Mathematical Capabilities of ChatGPT" (GHOSTS) | NeurIPS 2023 | GPT-4 本科数学可用，研究生水平远不及格；媒体报道存在选择偏差 | 论据：能力边界随抽象层级骤降 |
| Collins et al., CheckMate / MathConverse | arXiv 2023 | 正确性与"用户感知有用性"经常背离；模型代数易错 | 论据：交互式评估≠静态 benchmark |
| Mao et al., CHAMP | ACL Findings 2024 | **模型常通过错误推理步骤得到正确最终答案**；多数模型无法自检 | **核心痛点**：right for wrong reasons |
| Stolfo et al., Causal Framework for Robustness | ACL 2023 | 模型依赖表面模式而非深层推理；鲁棒性不随规模单调提升 | 论据：prompt 扰动下的脆弱性 |
| Gambardella et al. | ACL 2024 | LLM 能算对难乘法首位数，却常错易乘法末位（进位错误） | 论据：信心与正确性脱钩 |
| Imani et al., MathPrompter | ACL 2023 | 多路径（代数/Python）交叉验证可提升置信 | 方法层：multi-path verification |
| Li et al., DiVERSE | ACL 2023 | 逐步验证器比整链投票更可靠 | 方法层：step-level verifier |
| Arora et al., JEEBench | EMNLP 2023 | GPT-4 在 IIT JEE 级 <40%；无法评估负分风险 | 论据：长程+领域知识的失败模式 |

## 子线 B：形式化证明（Lean / Coq / Isabelle）

| 论文 | 年份 | 核心发现 | 对本论文的用途 |
|---|---|---|---|
| Song et al., Lean Copilot | arXiv 2024 / PMLR | LLM 作为 Lean copilot 自动化 74.2% 证明步（AESOP 仅 40.1%） | 论据：形式化校验"不可幻觉" |
| Wang et al., TheoremLlama | EMNLP 2024 | MiniF2F-test 33.6%，超过 GPT-4 25.4% | 论据：formal 覆盖率仍低 |
| Prasad (Harvard thesis), Coq lemma extraction | 2024 | GPT-4 整体证明 66.4%→79.4%（lemma 递归抽取） | 论据：失败点可分解 |
| First, Baldur (Isabelle) | 2023 | 整证明生成范式 | 背景：whole-proof generation |

## 子线 C：工具增强与基准

| 论文 | 年份 | 核心发现 | 对本论文的用途 |
|---|---|---|---|
| Yu et al., MetaMath | ICLR 2024 | 数据引导自举；GSM8K 66.5% / MATH 19.8% (7B) | 背景：训练侧改进 |
| Tang et al., MathScale | arXiv 2024 | 概念图驱动的 200 万题合成 | 背景：数据规模 |
| Das et al., Math Sensei | NAACL 2024 | 工具（Bing/Python/Wolfram）对难题增益大，对简单题增益小 | **关键方法**：tool-as-verifier |
| Agrawal et al., Hints | NeurIPS 2024 | 提示可提升，但对抗性提示会误导 | 论据：辅助信息的双刃性 |

---

## 核心张力（论文的"靶子"）

1. **指标欺骗**：final-answer accuracy ≠ reasoning validity（CHAMP 直接证据）
2. **信心错位**：模型在简单算题上过度自信、在难题上校准差（Gambardella, Frieder）
3. **两条技术路线的可靠性不对称**：
   - NL 推理：灵活但有幻觉（覆盖率高，certifiability 低）
   - Formal proof：零幻觉但覆盖率低（certifiability 高，覆盖率 30–80%）
4. **方法碎片化**：CoT / self-consistency / verifier / tool-use / formal-tactic 各自为战，**没有统一框架**说明"在什么场景该用哪一层保障"

## 候选研究空白（待选）
- [ ] **选题 A**：提出一个分层可靠性框架（答案层/推理步层/工具层/形式化层），用证据对照各层的 cost/certifiability/coverage
- [ ] **选题 B**：聚焦 NL→Formal 的翻译鸿沟，分析 Lean/Coq 工作流为何仍是 30–80% 而非 100%
- [ ] **选题 C**：聚焦"right for wrong reasons"现象的度量与检测方法
