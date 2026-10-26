# Learning Planner · Assess First, Then Plan

[简体中文](README.md) | [English](README.en.md)

An assistant skill for learning plans. It uses 10–15 diagnostic questions to establish a starting point, then builds a learning route around gaps, time, and goals instead of producing a generic schedule from labels such as “beginner” or “advanced.”

Suitable for programming, languages, exams, mathematics, design, and other subjects. **The repository is named learning-planner-skill; the invocation name is learning-planner.** This is an assistant workflow and reference collection, not a standalone website.

[Install](#installation) · [Use it](#a-complete-session) · [Deliverables](#what-you-receive) · [Method](#how-planning-is-organized) · [Word template](#generate-a-word-assessment-template-separately)

## Installation

Install the entire directory in a skill location supported by your assistant, keeping SKILL.md, references, and resources together.

For a Codex user-level installation, use Windows PowerShell:

```powershell
$plannerSkillsRoot = Join-Path $env:USERPROFILE '.agents\skills'
New-Item -ItemType Directory -Path $plannerSkillsRoot -Force | Out-Null
git clone https://github.com/kayaduster607-jpg/learning-planner-skill.git (Join-Path $plannerSkillsRoot 'learning-planner')
```

Select or enter `$learning-planner` in Codex. Compare versions before replacing an existing same-name directory. See the [official Skills documentation](https://learn.chatgpt.com/docs/build-skills) for directory conventions. For Claude Code, use `~/.claude/skills/learning-planner/` and that client's skill-discovery mechanism.

## A complete session

Give the assistant information like the following rather than only “help me learn Python”:

```text
使用 learning-planner。
我想在8周后能用Python批量整理Excel。
现在只写过简单脚本，每个工作日能学40分钟，预算为0。
请先出水平测评，我作答后再规划。
最终希望获得每周目标、练习任务和复盘检查点。
```

1. The assistant confirms your subject and goal, then provides questions from basic to advanced, identifying required and optional questions.
2. Answer by question number, write “I don't know” where needed, and state your real time constraints. **Answers are evidence for personalization; skipping them does not justify claiming your level has been assessed.**
3. The assistant explains your level and gaps, prerequisite knowledge, and learning stages. Check whether the goal is reasonable or should be narrowed.
4. It produces a roadmap, stage tasks, practice methods, resources, and review cadence. Bring back exercise results to adjust the plan later.

## What you receive

| Stage | Your input | Assistant output |
| --- | --- | --- |
| Start | Goal, experience, time, and budget | Subject confirmation and diagnostic questions |
| Diagnosis | Answers to each question | L1–L5 positioning and specific gaps |
| Planning | Confirmed scope and constraints | Stages, tasks, resources, review, and checkpoints |
| Review | Exercise or project results | Suggested changes to the plan and difficulty |

The default deliverable is in the conversation. For printable assessments or checklists, explicitly request Word / HTML and a save location, and ensure the assistant has file tools. Calendar advice does not create reminders: that requires a real calendar tool and appropriate authorization.

## How planning is organized

The workflow covers subject confirmation, assessment, level analysis, knowledge mapping, strategy matching, resource selection, and delivery. References include spaced review, retrieval practice, deliberate practice, subject mappings, and ways to address common learning obstacles.

These methods guide how to practice, when to review, and how to check progress. They do not replace assessment evidence or guarantee a particular level within a fixed time. Recheck resource accessibility, prices, and content versions when recommending them.

- [SKILL.md](SKILL.md): assistant execution rules.
- [Learning science reference](references/learning-science.md): strategies and rationale.
- [Knowledge mapping](references/topic-mapping-guide.md): prerequisites for a subject.
- [Learning obstacles](references/obstacles-troubleshooting.md): adjustments for actual difficulties.
- [Resource database](resources/resource-database.md): candidate resources grouped by subject.

## Generate a Word assessment template separately

`references/generate_test.py` is an editable document template, not an assessment reasoning engine. In an environment with Python installed:

```bash
python -m pip install -r requirements.txt
python references/generate_test.py
```

The script uses built-in sample questions in `main` and writes a Word document into `references`. Replace the question data and inspect the output for your own subject. Running it directly does not read your conversation answers or produce a personalized assessment.

See [LICENSE](LICENSE) for licensing.
