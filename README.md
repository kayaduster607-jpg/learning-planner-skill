# Learning Planner · 先测评，再规划

给 AI 助手使用的学习规划 Skill。先用 10–15 道题判断起点，再按薄弱点、时间与目标组织学习路线，避免只凭“零基础”或“想进阶”生成一份泛化日程表。

适用于编程、语言、考试、数学、设计等主题。**仓库名是 learning-planner-skill，实际调用名是 learning-planner**。它是一套助手工作流与参考材料，不是独立网站。

[安装](#安装) · [一次完整使用](#一次完整使用) · [交付内容](#你会拿到什么) · [工作流](#规划依据如何组织) · [模板脚本](#单独生成-word-测评模板)

## 安装

把整个目录安装到助手支持的 Skill 路径，保留 SKILL.md、references 和 resources。

Codex 用户级安装，Windows PowerShell：

```powershell
$plannerSkillsRoot = Join-Path $env:USERPROFILE '.agents\skills'
New-Item -ItemType Directory -Path $plannerSkillsRoot -Force | Out-Null
git clone https://github.com/kayaduster607-jpg/learning-planner-skill.git (Join-Path $plannerSkillsRoot 'learning-planner')
```

Codex 中选择或输入 `$learning-planner`。已有同名目录时先比较版本；目录约定见 [官方 Skills 文档](https://learn.chatgpt.com/docs/build-skills)。Claude Code 可放入 `~/.claude/skills/learning-planner/`，按该客户端的 Skill 发现方式调用。

## 一次完整使用

直接给助手下面这类信息，而不是只说“帮我学 Python”：

```text
使用 learning-planner。
我想在8周后能用Python批量整理Excel。
现在只写过简单脚本，每个工作日能学40分钟，预算为0。
请先出水平测评，我作答后再规划。
最终希望获得每周目标、练习任务和复盘检查点。
```

1. 助手确认主题与目标，给出由基础到进阶的测评题，区分必做与选做。
2. 你按题号作答，不会的写“不会”，并说明实际时间约束。**作答是个性化判断的输入，不能跳过后直接声称已测出水平。**
3. 助手说明水平与薄弱点，整理前置知识和学习阶段。你确认目标是否合理，是否需要缩小范围。
4. 最后生成学习路线、阶段任务、练习方式、资源和复盘节奏；后续把练习结果交回，再调整计划。

## 你会拿到什么

| 阶段 | 你的输入 | 助手输出 |
| --- | --- | --- |
| 开始 | 目标、当前经验、时间和预算 | 领域确认与测评 |
| 诊断 | 逐题回答 | L1–L5 定位、具体薄弱点 |
| 规划 | 确认后的范围和约束 | 阶段路线、任务、资源、复习与检查点 |
| 复盘 | 做题或项目结果 | 对计划和难度的调整建议 |

默认输出在会话中。需要可打印测评卷或学习清单时，明确要求 Word / HTML 和保存位置，并确认助手具有文件工具。日历建议不等于已经创建提醒；这需要实际日历工具和相应授权。

## 规划依据如何组织

工作流包括领域确认、测评、水平分析、知识映射、策略匹配、资源选择和计划交付。参考材料提供间隔复习、检索练习、刻意练习等方法，以及不同主题的映射与常见障碍处理。

这些方法用于选择“怎么练、什么时候复习、如何检查”，不能替代你的测评证据，也不保证固定时间达到某级别。资源推荐应结合实际可访问性、价格和内容版本重新核对。

- [SKILL.md](SKILL.md)：助手执行规则。
- [学习科学参考](references/learning-science.md)：学习策略与依据。
- [知识映射](references/topic-mapping-guide.md)：从主题拆出前置知识。
- [学习障碍处理](references/obstacles-troubleshooting.md)：根据实际卡点调整。
- [资源库](resources/resource-database.md)：按领域组织的候选资源。

## 单独生成 Word 测评模板

`references/generate_test.py` 是可修改的文档模板，不是测评推理引擎。在已安装 Python 的环境中：

```bash
python -m pip install -r requirements.txt
python references/generate_test.py
```

脚本使用 main 中的内置示例题，在 references 目录写出 Word 文档。为自己的主题生成卷子，需要替换题目数据并检查输出；直接运行不会自动读取你的会话答案或生成个性化判断。

## English overview

This is an assistant skill for assessment-first learning plans. Provide a goal, baseline, available time and constraints; answer the diagnostic questions; then review the gaps and the proposed roadmap. The skill name is `learning-planner`. Documents are optional deliverables that require file tools, and calendar advice does not automatically schedule reminders.

许可见 [LICENSE](LICENSE)。
