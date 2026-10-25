# Learning Planner — 学习规划师

[English](#english) | [中文](#中文)

---

<a id="english"></a>

## 先用一次：输入学习目标，最后拿到什么

这是给AI助手使用的学习规划Skill，**不是打开网站就自动生成课程的服务**。

| 你提供什么 | 示例 | 助手接下来给什么 |
| --- | --- | --- |
| 学什么、想做到什么 | “Python自动化，8周后能整理Excel” | 确认领域与目标；随后出10至15题水平测评 |
| 可投入时间与限制 | “每天40分钟，预算为0，工作日学习” | 按约束调整的学习范围 |
| 你的测评答案 | 按题号回答，不会的写不会 | 薄弱点分析、阶段路线、练习与复习计划 |

### 一次完整交互

1. 按后文安装方法把包含SKILL.md、references和resources的整个目录装到支持Skill的AI助手中。实际Skill名称是 `learning-planner`，仓库名称多了后缀 `-skill`。
2. 显式调用该Skill，并发送：“我想用8周学Python自动化，每天40分钟，希望最后能批量整理Excel。我现在只写过简单脚本，请先测评，不要直接给计划。”
3. 先完成测评必做题，再把答案交回助手。Skill需要根据答案判断起点，你不作答时，下一步通常还是等待/补充测评，而不是已经完成了个性化计划。
4. 核对薄弱点与可投入时间，再让助手给阶段目标、每日任务、资源和复习节奏；需要可打印文件时明确提出Word或HTML交付。

**输出在哪里：**默认是会话中的测评、分析和计划；只有明确要求并且助手有文件工具时，才会额外生成DOCX、HTML清单等文件。日历建议不会自动替你创建提醒，需要实际日历/自动化工具和相应授权。

**独立Word模板：**`references/generate_test.py`是测评卷模板，不是自动分析你水平的模型程序。安装requirements后直接运行会生成脚本内置示例卷，输出在references目录；适配新领域要修改main里的题目数据。

Codex安装与显式调用方式可核对[官方Skills说明](https://learn.chatgpt.com/docs/build-skills)；已有同名Skill时先比较版本，避免重复目录。

## English

A Claude Code skill that designs personalized learning plans grounded in cognitive science. It starts with a **diagnostic quiz** to locate your current level, then builds a complete roadmap with evidence-based strategies — every task tagged with the science behind *why* it works.

### What It Does

| Without | With This Skill |
|---|---|
| "What's your level?" → you guess | Diagnostic quiz pinpoints exact strengths & gaps |
| "Do more practice" | Tasks tagged with specific science-backed strategies |
| Same methods for every subject | Strategy mix tailored to subject type |
| No progress tracking | Traffic-light system + metacognitive reflection |
| "You can do it!" | Honest: "Here's what to cut if time is tight" |

### Quick Start

```bash
cp -r learning-planner ~/.claude/skills/
```

Then in Claude Code:

```
/learning-planner
```

**Flow**: Tell what you want to learn → Take a diagnostic quiz (10-15 questions) → Get gap analysis (L1-L5) → Receive your personalized learning plan.

### 7-Step Workflow

```
1. Domain Confirmation      → Narrow down exactly what to learn
2. Diagnostic Quiz          → 10-15 questions: required (≈10 min) + optional (≈15-20 min)
3. Level Analysis           → L1 (zero) ~ L5 (near-advanced) + detailed gap report
4. Knowledge Mapping        → Prerequisites, core concepts, learning phases
5. Strategy Matching        → Evidence-based strategies per subject type
6. Resource Recommendation  → Curated free & paid resources per phase
7. Learning Plan Delivery   → Full roadmap with strategy tags & reflection prompts
```

### Theoretical Foundation

| Source | Key Contributions |
|---|---|
| **Barbara Oakley** (Learning How to Learn, A Mind for Numbers) | Focused/Diffuse modes, Chunking, Procrastination |
| **The Learning Scientists** (Smith & Weinstein) | 6 evidence-based strategies |
| **Anders Ericsson** (Peak) | Deliberate Practice framework |
| **Scott Young** (Ultralearning) | Self-directed intensive learning |
| **Craik & Tulving** (1975) | Depth of Processing theory |
| **UNC Learning Center** | Study Cycle, Environmental Management |

### Strategy Tag System

Every task in a plan carries a tag so users understand *why*:

| Tag (EN) | Tag (中文) | What It Means |
|---|---|---|
| `[Spaced Practice]` | `[间隔重复]` | Review at 1→3→7→14→30 day intervals |
| `[Retrieval Practice]` | `[提取练习]` | Close the book and recall, don't re-read |
| `[Feynman Technique]` | `[费曼技巧]` | Explain it like teaching a 10-year-old |
| `[Interleaving]` | `[交错练习]` | Mix different problem types, don't block |
| `[Elaboration]` | `[精细加工]` | Keep asking "why", connect to what you know |
| `[Dual Coding]` | `[双重编码]` | Combine text with diagrams/charts |
| `[Deliberate Practice]` | `[刻意练习]` | Target weak spots at the edge of your ability |
| `[Deep Processing]` | `[深度处理]` | Record audio, annotate code, draw comparisons |
| `[Diffuse Mode]` | `[发散模式]` | Walk away; let your brain work in the background |

### Metacognitive Prompts

Every phase ends with 3 questions:
1. Which learning method helped me improve the most?
2. Which tasks am I always procrastinating on? How can I adjust?
3. If I restarted this phase, what would I change?

### Level Rating

| Level | Score | Meaning | Starting Point |
|---|---|---|---|
| L1 | 0-20% | Complete beginner | Fundamentals from scratch |
| L2 | 20-40% | Heard of concepts | Quick fundamentals review → core |
| L3 | 40-60% | Some core knowledge | Skip basics, moderate difficulty |
| L4 | 60-80% | Good grasp, some gaps | Target weak spots + advanced |
| L5 | 80-100% | Solid foundation | Advanced topics and projects |

### Word Document Generator

`references/generate_test.py` produces print-friendly `.docx` assessments with auto-split required/optional sections, auto-calculated time estimates, and Chinese font anti-corruption. Dependency: `python-docx`.

### Optional Deliverables

- **Printable HTML checklist** with Gantt chart
- **Calendar study reminders**

### File Structure

```
learning-planner/
├── SKILL.md                          ← Main definition
├── README.md                         ← This file
├── LICENSE                           ← MIT
├── requirements.txt
├── references/
│   ├── generate_test.py              ← Word generator template
│   ├── learning-science.md           ← 12 science principles
│   ├── self-learning-framework.md    ← 5-step self-learning
│   ├── topic-mapping-guide.md        ← Knowledge graph guide
│   └── obstacles-troubleshooting.md  ← 7 obstacles + solutions
└── resources/
    └── resource-database.md          ← Curated resources by domain
```

### License

MIT

---

<a id="中文"></a>

## 中文

一个基于认知科学的 Claude Code 技能。**先用测评卷精准定位水平，再出个性化学习规划**——每个任务标注方法论标签，让你理解"为什么这样做"有效。

### 差异化定位

| 普通让 AI 出计划 | 本 Skill |
|---|---|
| "你什么水平？"→ 自己估计 | 出卷子测评，用题目精准定位 |
| "多做练习""找好资源" | 6大证据策略，有具体操作定义 |
| 所有主题同一套方法 | 按主题类型匹配不同策略组合 |
| 没有进度追踪 | 红绿灯法 + 元认知反思 |
| "你能做到！" | "这个不是必需品"，诚实的取舍建议 |

**核心壁垒**：把认知科学的抽象原理翻译成每天 40 分钟里可执行的具体动作。

### 快速开始

```bash
cp -r learning-planner ~/.claude/skills/
```

在 Claude Code 中输入：

```
/learning-planner
```

**流程**：告诉它你想学什么 → 收到一份测评卷（10-15题）→ 提交答案 → 获得水平分析（L1-L5）→ 收到个性化学习规划。

### 七步工作流

```
第一步：领域确认      → 明确具体学什么
第二步：水平测评      → 出卷子（必做≈10分钟 + 选做≈15-20分钟）
第三步：水平分析      → L1（零基础）~ L5（接近进阶）+ 薄弱点报告
第四步：知识图谱      → 前置知识、核心概念、学习阶段
第五步：策略匹配      → 按主题类型匹配科学策略
第六步：资源推荐      → 每个阶段精选免费/付费资源
第七步：生成学习计划  → 完整路线图 + 方法论标签 + 反思引导
```

### 理论基础

| 来源 | 核心贡献 |
|---|---|
| **Barbara Oakley**（Learning How to Learn） | 专注/发散模式、分块、拖延神经科学 |
| **The Learning Scientists**（Smith & Weinstein） | 六大证据策略 |
| **Anders Ericsson**（Peak 刻意练习） | 刻意练习框架 |
| **Scott Young**（Ultralearning 超速学习） | 高强度自学方法论 |
| **Craik & Tulving**（1975） | 深度处理理论 |
| **UNC Learning Center** | 学习循环、环境管理 |

### 方法论标签系统

学习计划中每个任务都标注方法论标签：

| 标签 | 含义 | 用户感知 |
|---|---|---|
| `[间隔重复]` | 按 1→3→7→14→30 天节奏复习 | "这不是随意安排，是科学节奏" |
| `[提取练习]` | 合上书本主动回忆 | "不用重读，用回忆来强化" |
| `[费曼技巧]` | 用教别人的方式解释 | "理解 = 能解释清楚" |
| `[交错练习]` | 混合不同类型题目 | "混合练习比集中刷题更有效" |
| `[精细加工]` | 追问"为什么"、建立联系 | "多问为什么，记忆更深" |
| `[双重编码]` | 文字 + 图表结合 | "画出来记得更牢" |
| `[刻意练习]` | 聚焦薄弱环节 | "专攻短板，不在舒适区重复" |
| `[深度处理]` | 录音、代码注释、跨领域类比 | "不是浅层浏览，是深度加工" |
| `[发散模式]` | 散步休息时让大脑后台处理 | "卡住时去散步，别死磕" |

### 元认知引导

每个阶段末尾提供 3 个反思问题：
1. **进步识别**：哪种学习方式让我进步最快？
2. **障碍觉察**：哪些任务我总是在拖延？怎么调整？
3. **策略迭代**：如果重新开始这个阶段，我会改变什么？

初期侧重"是否坚持"，中期侧重"方法是否有效"，后期侧重"如何应用和输出"。

### 水平定级

| 等级 | 得分 | 含义 | 学习起点 |
|---|---|---|---|
| 🟢 L1 | 0-20% | 完全零基础 | 从最基础开始 |
| 🟡 L2 | 20-40% | 略有耳闻 | 快速过基础后进入核心 |
| 🟠 L3 | 40-60% | 有一定基础 | 跳过基础，直接中等难度 |
| 🔴 L4 | 60-80% | 中等水平 | 针对性补短板 + 进阶 |
| 🟣 L5 | 80-100% | 接近进阶 | 直接进入高级主题与实战 |

### 测评卷 Word 生成器

`references/generate_test.py` 可生成可打印的 .docx 测评卷，自动分"必做/选做"区域、自动计算用时、中文防乱码。依赖：`pip install python-docx`。

### 附加交付物

学习计划完成后可索取：
- **可打印 HTML 进度清单**（带甘特图）
- **日历学习提醒**

### 文件结构

```
learning-planner/
├── SKILL.md                          ← 主定义文件
├── README.md                         ← 本文件（中英双语）
├── LICENSE                           ← MIT
├── requirements.txt
├── references/
│   ├── generate_test.py              ← Word 生成脚本模板
│   ├── learning-science.md           ← 12 大学习科学原理详解
│   ├── self-learning-framework.md    ← 五步自学方法论
│   ├── topic-mapping-guide.md        ← 知识图谱构建指南
│   └── obstacles-troubleshooting.md  ← 7 大自学障碍与解决方案
└── resources/
    └── resource-database.md          ← 按主题分类的学习资源库
```

### 场景覆盖

| 场景 | 处理方式 |
|---|---|
| 完全不知道学什么 | 引导问题找方向 |
| 学习遇到瓶颈 | 障碍诊断框架（8种症状 → 解决方案） |
| 时间极紧 | 80/20法则 + 碎片时间利用 |
| 需要自制课程 | 五步 DIY Syllabus 框架 |

### License

MIT
