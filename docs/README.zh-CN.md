[English](../README.md) | **简体中文** | [日本語](README.ja.md) | [한국어](README.ko.md)

# career-mind

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE) [![Version](https://img.shields.io/badge/version-0.7.0-green.svg)](../.claude-plugin/marketplace.json)

面向 AI 编程 Agent 的职业能力管理工具。从任意来源采集能力信息，评估信息质量，为任意场景生成职业文档——简历、绩效评审、晋升案例等。

**不虚构成就。所有输出均可追溯到你的真实经历。**

## 快速开始

```bash
git clone https://github.com/ClawEnable/career-mind.git
cp -r career-mind/skills/* ~/.claude/skills/   # 或你的 Agent 的 skill 路径
```

然后在 Agent 中运行 `/career-mind:cm-init` 即可开始。

## 兼容 Agent

| Agent | Skill 路径 | 安装方式 |
|-------|-----------|---------|
| Claude Code | `~/.claude/skills/` | 插件市场或手动复制 |
| Codex | `~/.agents/skills/` | `$skill-installer` 或手动复制 |
| Cursor | `~/.agents/skills/` 或 `~/.cursor/skills/` | GitHub 远程导入或手动复制 |
| OpenCode | `.opencode/skills/` | 手动复制 |
| OpenClaw | `<workspace>/skills/` | `openclaw skills install` |

## 安装

### Claude Code

插件市场安装（推荐）：

```
/plugin marketplace add ClawEnable/career-mind
/plugin install career-mind@career-mind
```

或手动安装：

```bash
git clone https://github.com/ClawEnable/career-mind.git
cp -r career-mind/skills/* ~/.claude/skills/
```

### OpenClaw

```bash
openclaw skills install career-mind
```

### 其他 Agent

克隆并将 `skills/` 目录复制到你的 Agent 的 skill 路径（见上表）：

```bash
git clone https://github.com/ClawEnable/career-mind.git
cp -r career-mind/skills/* ~/.agents/skills/   # Codex、Cursor、OpenCode
```

## 技能列表

| 命令 | 说明 |
|------|------|
| `/career-mind:cm-init` | 初始化职业上下文——扫描文档、收集个人信息、导入已有材料 |
| `/career-mind:cm-capture` | 通过领域感知的选项式交互采集能力：导入后分析、主动描述、会话回顾或文档导入 |
| `/career-mind:cm-assess` | 评估信息质量，提供诊断洞察和可操作建议 |
| `/career-mind:cm-craft` | 生成职业文档：简历、绩效评审、晋升案例、技能地图 |
| `/career-mind:cm-interview` | 面试准备：技术题、行为题、协作题，以及结构化模拟练习 |
| `/career-mind:cm-status` | 查看当前状态并获取下一步建议 |

## 工作原理

插件采用领域优先的交互模型，专为有经验的从业者设计：

- **领域推断**——先理解你的技术内容再提问，不会让你解释通用做法
- **选项式采集**——生成带有估算值的精炼陈述选项，由你确认或修正，而非从零开始撰写
- **顾问式推荐**——附带理由推荐选项，而非仅展示选项让你选择
- **职业阶段适配**——根据你的职业阶段调整策略：应届生、职业中期、资深、转行
- **动态视角**——分析根据你的目标角色调整；对架构师而言关键的差距，对高级工程师可能只是次要问题
- **迭代精炼**——每次选择揭示新线索，通过结构化多轮对话收敛到准确陈述

```
cm-init → cm-capture ⇄ cm-assess → cm-craft（任意场景） → cm-interview（可选）
                   ↑              │
                   └──────────────┘  (cm-assess 发现差距 → cm-capture 补充)
```

根据你的需求从任意步骤开始：

- 什么都没有 → `/career-mind:cm-init`
- 想描述你的经历 → `/career-mind:cm-capture`
- 想评估现有内容 → `/career-mind:cm-assess`
- 需要特定文档 → `/career-mind:cm-craft`
- 准备面试 → `/career-mind:cm-interview`
- 不确定 → `/career-mind:cm-status`

## 数据存储

所有数据存储在当前工作目录的 `.career/` 中：

```
.career/
├── profile.md       # 姓名、联系方式、教育背景（可持续丰富）
├── context.md       # 跨技能状态（YAML frontmatter）
├── entries/         # 能力库（project、signal、achievement 条目）
└── outputs/         # 生成的文档（简历、评估报告等）
```

## 隐私

**所有个人数据存储在项目目录的 `.career/` 中。** 你的个人信息、条目和生成的文档不会离开本地设备，除非你主动分享。如不希望被 Git 追踪，请将 `.career/` 添加到 `.gitignore`。

## 反虚构

插件强制执行严格的来源追溯：

- `/career-mind:cm-craft` 生成的每个文档要点均可追溯到已验证来源（记录在独立的 `.meta.md` 文件中）
- 来源仅限于：条目库、个人信息或用户原话
- 不编造指标、不夸大技能、不虚构成就
- 限定性上下文与成就一并保留——不选择性引用证据来夸大感知范围

## 贡献

请参阅 [CONTRIBUTING.md](../CONTRIBUTING.md) 了解添加技能、评估维度和输出场景的指南。

## 许可证

[MIT](../LICENSE) © 2026 ClawEnable
