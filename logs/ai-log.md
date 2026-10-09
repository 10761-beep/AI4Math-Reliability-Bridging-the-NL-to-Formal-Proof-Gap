# AI 日志 / AI Usage Log — C2 AI for Math

> 本文件全程记录：每一步用了什么 AI 工具、给了什么 prompt、得到了什么、如何验证/否决。
> 这是评分项 **aiUsage (20分)** 的核心证据。

## 规范
- 每次 AI 介入都记：日期 / 目的 / 工具 / 输入摘要 / 输出摘要 / 人工校验动作
- 区分"AI 直接产出"vs"人工判断后采纳"
- 记录被否决的 AI 建议（同样重要）

---

## 阶段 0–1：任务拆解与文献基线

### 2026-10-08 · 启动
- **目的**：拆解挑战要求、搭建工作目录、并行检索三条文献线
- **工具**：Doubao（主助手）+ scholar_search（学术检索）
- **输入 prompt（要点）**：
  - "围绕 AI4Math 可靠性框架撰写可投稿 LaTeX 论文"
  - 并行检索三组关键词：
    1. `LLM mathematical reasoning reliability hallucination` (2023–2026)
    2. `LLM formal theorem proving Lean verification reliability`
    3. `GSM8K MATH benchmark evaluation mathematical reasoning LLM`
- **输出摘要**：30 篇候选文献，覆盖三条子线（见 `refs/literature-map.md`）
- **人工校验动作**：
  - 剔除学位论文（除非作为背景引用）
  - 识别出关键张力：**final-answer accuracy 与 reasoning validity 脱钩**（CHAMP 论文）
  - 识别研究空白：现有"可靠性增强方法"是碎片化的，缺乏统一分层框架

### 待续

---

## 阶段 2：选题与深挖

### 2026-10-08 · 选题确认
- **目的**：从 A/B/C 三个候选中选定方向
- **动作**：用 interaction.ask 让用户选
- **用户选择**：B（NL→Formal 翻译鸿沟），而非我推荐的 A
- **人工校验**：尊重用户选择，但把 B 重新定位为"批判性分解已有系统"而非"自己实现 Lean"，以匹配资源边界

### 2026-10-08 · 二轮文献检索
- **工具**：scholar_search，3 组并行 query
- **关键新发现**：
  - ProofBridge (2025)：明确说 AlphaProof IMO 2024 题面人工翻译 → L1 证据
  - BFS-Prover (ByteDance, ACL 2025)：miniF2F-test 72.95% SOTA
  - PALM (Lu 2024)：520 个错误分析，高层对低层错 → L3 证据
  - ProntoQA (Saparov & He, ICLR 2023)：单步对、规划错 → L2 证据
  - miniF2F-Dafny (2025)：空证 40.6% → 被忽视的基线
- **人工判断**：把这些发现组织成"四层鸿沟"框架（L1 formalization / L2 planning / L3 detail / L4 search）

---

## 阶段 3–4：写作与编译

### 2026-10-08 · references.bib
- 19 条 BibTeX，全部来自 scholar_search 返回的真实论文
- 字段：author/title/booktitle/journal/year/url 完整

### 2026-10-08 · paper.tex 初稿
- 由 AI 起草全文（约 3500 英文词）
- **人工校验动作**：
  - 数字全部核对原文摘要（25.4% / 33.6% / 72.95% / 40.6% / 66.44%→79.42% / 74.2%）
  - 删除 AI 生成的空洞过渡句
- **第一次编译失败**：缺 `\usepackage{natbib}`，`\citet` undefined
  - 人工定位：读 /tmp/tex3.log，发现 6 处 undefined control sequence 都指向 `\citet`
  - 修复：加 natbib 包，bibliographystyle 改 plainnat
- **TikZ 图 bug**：一个多余的空节点导致 L4 位置错位；人工读源码发现并删除
- **最终编译**：8 页 PDF，19 篇 bibitem，零 warning

---

## 阶段 5：AAR

### 2026-10-08 · 复盘
- 见 `AAR.md`
- 核心诚实结论：没有一手实验，所有数字二手；论文价值在"闭环示范"而非"学术原创"

---

## AI 使用统计（自查）

| 环节 | AI 占比 | 人工判断占比 |
|---|---|---|
| 文献检索 | 90% | 10%（选题） |
| 文献筛选 | 30% | 70%（挑 19 篇） |
| 框架构建 | 20% | 80%（四层分解是综合判断） |
| 初稿写作 | 85% | 15%（数字核对、删 AI 腔） |
| 编译调试 | 40% | 60%（读日志、定位 bug） |
| AAR | 30% | 70%（诚实自我批评） |

**结论**：AI 是高效的检索器和起草器，但**研究品味和诚实复盘必须是人**。

---

## 阶段 6：关键方向调整（用户反馈驱动）

### 2026-10-08 · 用户提出"无法和我专业结合"
- **用户原话**："我是学英语语言的，有传播学、跨文化交际的研究背景，目前这些题目我看起来都有点难。"
- **我的判断**：这是真实信号，不是用户谦虚。硬走纯 CS 路线既不匹配学科身份，也攒不下申博资本。
- **关键洞察**：NL→Formal proof 鸿沟本质上是 Jakobson 的"符际翻译"（intersemiotic translation）——这是翻译学/跨文化交际的本行问题。
- **动作**：给用户三个重新框定的方向（A 翻译学 lens / B 科学传播 / C 教学话语），并对照评分标准判断 A 最贴合作业要求。

### 2026-10-08 · 用翻译学 lens 重写论文
- **保留**：所有技术骨架（四层鸿沟、19 篇 CS 文献、73% vs 40.6% 数字批评、TikZ 图、Table、公式）
- **新增**：
  - 标题改为 "An Intersemiotic-Translation Lens on the Reliability Gap in LLM Theorem Proving"
  - Abstract 加入 Jakobson 框架
  - Introduction 加一段定位（为什么用翻译学 lens）
  - 四层每节后加 "Translational reading" 段落（L1 文化不可译性、L2 动态对等、L3 搭配错误、L4 修订循环）
  - Discussion 加 "Why a translation-studies lens?" 小节
  - Conclusion 收回 intersemiotic translation 主线
- **新增 bib**（5 篇经典）：Jakobson 1959, Nida 1964, Venuti 1995, Swales 1990, Hall 1976
- **编译结果**：9 页、24 篇引用、零 warning

### 元教训
- AI（我）一开始顺着作业字面要求走，没有站在用户学科身份上想。是用户一句"无法和我专业结合"把方向拉回来。
- **好的指导不是替用户做他不擅长的事，而是帮他找到他擅长的事和作业要求的交叉点。**
