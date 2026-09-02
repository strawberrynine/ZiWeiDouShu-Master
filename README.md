# 紫微斗数 · 结构化解盘

## Zi Wei Dou Shu Master

<p align="center">
  <img src="assets/ziwei-wheel.svg" alt="紫微斗数十二宫关系图 / Zi Wei Dou Shu twelve-palace relationship map" width="820">
</p>

这是一个给 Codex 用的紫微斗数分析 Skill。把命盘资料交给它后，它会先检查数据，再看宫位关系、四化和限运，最后把依据、相反信号和可观察的现实问题写出来。

A Codex skill for traceable Zi Wei Dou Shu readings. It validates the chart first, follows palace relationships and timing layers, then keeps evidence, counter-signals, and practical observations visible.

> 这是分析工具，不是独立排盘应用，也不把传统术语写成确定预言。
>
> This package provides analysis guidance and references. It is not a standalone chart calculator or a deterministic prediction engine.

## 你可以拿它做什么 · What you can do

| 场景 | 可以问什么 | Relevant files |
| --- | --- | --- |
| 夫妻宫与关系 | “详细分析他的夫妻宫”“这段关系的磨合点在哪里？” | [`frameworks/relationship-analysis.md`](frameworks/relationship-analysis.md), [`frameworks/spouse-analysis.md`](frameworks/spouse-analysis.md) |
| 事业与财运 | “适合创业还是上班？”“收入的压力点是什么？” | [`frameworks/career-analysis.md`](frameworks/career-analysis.md), [`frameworks/wealth-analysis.md`](frameworks/wealth-analysis.md) |
| 时间窗口 | “哪一段大限适合换工作？”“某年会触发什么主题？” | [`frameworks/timing-analysis.md`](frameworks/timing-analysis.md) |
| 迁移与环境 | “异地发展有哪些机会和成本？” | [`frameworks/migration-analysis.md`](frameworks/migration-analysis.md) |
| 全盘与资料检查 | “这张截图能不能精断？”“请先校验命宫和身宫。” | [`frameworks/full-chart-analysis.md`](frameworks/full-chart-analysis.md), [`prompts/intake.md`](prompts/intake.md) |

The same routes cover relationship, career, wealth, migration, timing, and full-chart questions. When the input is incomplete, the skill lowers precision instead of filling in missing stars.

## 快速开始 · Quick start

### 安装 / Install

把仓库放进 Codex 的 skills 目录，确保 `SKILL.md` 位于目录根部。Windows PowerShell 示例：

```powershell
git clone https://github.com/strawberrynine/ZiWeiDouShu-Master.git "$env:USERPROFILE\.codex\skills\ziwei-doushu-master"
```

如果你使用了自定义 `CODEX_HOME` 或其他 skills manager，请把目标目录换成对应位置。

Clone the repository into your Codex skills directory, with `SKILL.md` at the package root. Use your local skill manager if it handles installation for you.

在 Codex 对话中显式调用：

```text
$ziwei-doushu-master
请根据下面的结构化命盘，分析 2026 年农历八月的事业和财运。
先列出已确认字段，再给出依据、反证、置信度和现实建议。
```

Call it in English if you prefer:

```text
$ziwei-doushu-master
Analyze career and wealth for lunar month 8 of 2026 from the chart below.
Validate the fields first, then show evidence, counterevidence, confidence, and practical questions.
```

输入可以是结构化命盘、出生资料或截图。结构化输入最可靠；截图只作三级证据，模糊字段会被列为待确认。时辰字段使用地支索引 `0–11`，不是 0–23 点的小时数。字段约定见 [`schemas/chart-schema.json`](schemas/chart-schema.json)。

## 使用案例 · Worked examples

### 1. 夫妻宫：先看关系结构

```text
$ziwei-doushu-master
这是完整结构化命盘。请分析他的夫妻宫，范围包括命宫、福德、迁移、官禄、三方四正、对宫、四化和吉煞。
请把“吸引方式、相处压力、需要观察的沟通问题”分开写；不要直接断言结婚、分手或出轨。
```

示例输出（只展示格式，不代表任何真实命盘结论）：

```text
已确认 / Confirmed
夫妻宫与命、福德、官禄的字段齐全；采用固定四化表，流派差异另列。

依据 / Evidence
[SOURCE] 夫妻宫本宫与对宫结构；[DERIVED] 三方四正形成的互动主题。

反证 / Counterevidence
[UNCERTAIN] 福德宫资料不足，长期情绪满足感不能精断。

置信度 / Confidence
Medium。可观察：冲突时是先解释需求，还是先回避？

建议 / Next step
把“想要被理解”改成一条具体请求，观察对方是否能回应。
```

### 2. 事业与财运：把象征落到选择

```text
$ziwei-doushu-master
请比较这张命盘在当前大限中“稳定工作”和“尝试副业”两条路线。
分别说明收入来源、现金流压力、可验证的现实信号；命理部分不替代投资或职业咨询。
```

The answer should compare the relevant palaces and timing layers, rather than map one star to one job. It should name the evidence, the downside, and what to check in an actual budget or work trial.

### 3. 模糊截图：先停在能确认的地方

```text
$ziwei-doushu-master
我只有一张模糊排盘截图。请先列出能读到和读不到的字段，说明哪些结论只能算 Low 置信度，不要补造星曜。
```

When dates, hour branches, or palace names cannot be read, the skill asks for a re-export or the missing fields. It does not turn OCR guesses into chart facts.

## 工作流与技术架构 · Workflow and architecture

<p align="center">
  <img src="assets/architecture.svg" alt="从输入到证据化输出的技术架构 / architecture from input to evidence-led output" width="100%">
</p>

| 层 | 做什么 | 目录 |
| --- | --- | --- |
| 输入与校验 / Input & validation | 识别结构化命盘、出生资料和截图；检查历法、时辰、命宫、身宫与十二宫。 | [`prompts/intake.md`](prompts/intake.md), [`schemas/`](schemas/) |
| 主题路由 / Topic routing | 把问题送到夫妻、事业、财富、迁移、时间或全盘框架。 | [`prompts/topic-router.md`](prompts/topic-router.md) |
| 知识 / Knowledge | 放置原典页码地图、宫位、星曜、四化、组合、格局和时间规则。 | [`knowledge/`](knowledge/) |
| 专题推理 / Frameworks | 将同一套证据顺序应用到关系、事业、财富等问题。 | [`frameworks/`](frameworks/) |
| 输出 / Output | 给出结论、依据、反证、置信度、时间范围和现实观察点。 | [`prompts/output.md`](prompts/output.md), [`schemas/analysis-schema.json`](schemas/analysis-schema.json) |
| 质量与边界 / Quality & guardrails | 用测试题检查取证和安全表达；不把象征写成医疗、法律、投资或宿命保证。 | [`tests/`](tests/), [`SKILL.md`](SKILL.md) |

The workflow stays visible in the files: validate the data, read the palace field, separate natal and timing layers, then state both support and friction.

## 证据怎么进入答案 · How evidence is used

分析时按这个顺序读取：

1. 命宫、身宫、目标宫、三方四正、对宫和限运。
2. 主星、亮度、四化，以及辅弼魁钺、昌曲、禄存、天马、羊陀火铃、空耗等会照。
3. 原典引用、流派差异、反向信号和资料缺口。

The labels in an answer have distinct jobs:

| 标签 | 含义 |
| --- | --- |
| `[SOURCE]` | 1994 年版《紫微斗数》及其页码/章节能直接支持的规则。 |
| `[FRAMEWORK]` | 本仓库的分析流程，不冒充古籍原文。 |
| `[DERIVED]` | 将多条规则组合后得到的中间判断。 |
| `[INTERPRETATION]` | 把古典术语翻成现代、可讨论的语言。 |
| `[INFERENCE]` | 结合当前命盘得出的推断，必须说明证据。 |
| `[UNCERTAIN]` | 字段不完整、截图不清或流派存在差异。 |

三个相互独立的一级结构都支持同一结论时，通常可写 `High`；有重要反证时降为 `Medium`；只靠单星或单宫时保持 `Low`。正反信号同时出现，就分别说明它们在什么条件下会出现。

## 数据契约 · Data contract

### 输入命盘 / Chart input

[`schemas/chart-schema.json`](schemas/chart-schema.json) 要求：

| 字段 | 说明 |
| --- | --- |
| `birthInfo` | 年、月、日、时辰地支索引和性别；地点/经度可选。 |
| `mingGongBranch` / `shenGongBranch` | 命宫、身宫所在地支索引。 |
| `palaces` | 12 个宫位；每个宫位至少有 `branch`、`stem`、`name`、`stars`。 |
| `daXians` | 大限数组；时间问题需要同时说明年龄口径。 |

### 输出分析 / Analysis output

[`schemas/analysis-schema.json`](schemas/analysis-schema.json) 固定 `method`、`question`、`summary`、`claims`、`limitations` 和 `advice`；每条 claim 可附 [`schemas/evidence-schema.json`](schemas/evidence-schema.json) 中的证据、反证、来源标签和时间层。

## 目录 · Repository map

```text
ziwei-doushu-master/
├── SKILL.md                         # 入口规则 / skill instructions
├── agents/openai.yaml               # Codex 界面元数据 / UI metadata
├── prompts/                         # 输入、路由、推理、输出 / routing and output
├── frameworks/                      # 主题分析框架 / topic frameworks
├── knowledge/                       # 原典与结构规则 / source and domain notes
├── schemas/                         # 输入、证据、输出契约 / JSON contracts
├── tests/                           # 测试题与评分规则 / evaluation suite
└── assets/                          # GitHub 预览图 / visual references
```

如果你要改分析口径，先看 [`SKILL.md`](SKILL.md) 和对应专题文件；如果要改输入或输出格式，先改 schema，再同步提示词和测试。

For a rule change, start with `SKILL.md` and the relevant framework. For a contract change, update the schema first, then check prompts and tests.

## 资料、版权与许可 · Sources, attribution, and license

主要资料是宋·希夷先生原著、云居山整理，《紫微斗数》，沈阳出版社，1994 年版。章节与印刷页码见 [`knowledge/source-book.md`](knowledge/source-book.md)；扫描或 OCR 不清的地方标为 `[UNCERTAIN]`。原始 PDF 不在本仓库内，README 和现代框架也不冒充古籍原文。

The repository also contains modern analysis frameworks and distilled notes. Keep their labels separate from quotations. Before redistributing the package or adding third-party material, check the source's terms and preserve attribution.

当前仓库没有附带许可证。公开发布前，请先确认 Skill 文档、原典蒸馏内容和第三方素材的权利，再选择许可证。

This repository currently ships without a license. Confirm the rights of the skill text, distilled source material, and any third-party assets before choosing one.

## 边界 · Boundaries

- 紫微斗数在这里是传统文化与自我观察的框架，不是事实预测器。
- 不提供医疗诊断、法律判断、投资建议或重大人生决定的替代方案。
- 不写“注定、必然、一定发财、必然分手”等确定断言。
- 桃花星只表示吸引力、社交或关系触发，不能直接等同出轨。
- 没有双方完整资料时，不做合盘结论。

This skill keeps uncertainty visible and leaves decisions with the user. Health, legal, financial, and relationship decisions still belong to qualified professionals and the people involved.

## 校验 · Validation

在仓库根目录运行：

```powershell
python <CODEX_HOME>\skills\.system\skill-creator\scripts\quick_validate.py .
git diff --check
```

如果未设置 `CODEX_HOME`，把路径替换为本机 `.codex\skills\.system\skill-creator\scripts\quick_validate.py` 的实际位置。测试场景见 [`tests/test-cases.md`](tests/test-cases.md)，评分规则见 [`tests/evaluation-rubric.md`](tests/evaluation-rubric.md)。

Run the validator after changing frontmatter or folder structure. It checks the package shape; it does not judge whether an interpretation is wise or well written.
