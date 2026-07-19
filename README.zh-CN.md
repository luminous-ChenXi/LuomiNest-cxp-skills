# LuomiNest CxPlugin 技能集合

[English](./README.md) | [简体中文](./README.zh-CN.md) | [日本語](./README.ja-JP.md)

LuomiNest 技能集合仓库 — 所有技能以子目录形式存放，社区可通过 PR 贡献新技能。

## 仓库职责

| 仓库 | 作用 |
|------|------|
| LuomiNest-cxp-registry | 中心索引注册表，维护 `index.json` |
| LuomiNest-cxp-plugin-template | 插件开发模板（fork 起始点） |
| **LuomiNest-cxp-skills**（本仓库） | 技能集合（每个技能一个子目录） |

与插件不同，技能只是 Markdown 文件（`SKILL.md`）或 manifest（`manifest.json`），没有复杂 Python 代码。因此采用集合仓库模式集中管理，无需每个技能独立仓库。

## 目录结构

```
LuomiNest-cxp-skills/
├── cooking-assistant/      ← 烹饪助手技能
│   └── manifest.json
├── skill-creator/          ← 技能创建助手（元技能）
│   └── SKILL.md
├── travel-planner/         ← 旅行规划技能
│   └── SKILL.md
├── README.md               ← 英文（默认）
├── README.zh-CN.md         ← 简体中文（本文件）
├── README.ja-JP.md         ← 日文
├── CONTRIBUTING.md
└── LICENSE
```

每个技能子目录名 = 技能 id（kebab-case）。

## 技能格式

### SKILL.md（推荐）

YAML frontmatter + Markdown body：

```yaml
---
id: travel-planner
name: 旅行规划
version: 1.0.0
description: 根据用户需求规划旅行行程
author: LuminousCX
license: MIT
tags: [travel, planning, lifestyle]
category: lifestyle
icon: Map
trigger_keywords: [旅行, 旅游, 出行, 行程]
---

# 旅行规划技能

当用户询问旅行相关问题时...
```

### manifest.json（兼容格式）

```json
{
  "id": "cooking-assistant",
  "type": "skill",
  "name": "烹饪助手",
  "version": "1.0.0",
  "description": "菜谱推荐、步骤指导、营养分析",
  "author": "LuminousCX",
  "license": "MIT",
  "icon": "ChefHat",
  "category": "lifestyle",
  "tags": ["community", "free"]
}
```

详细字段说明见 [docs/development/plugin-system.md](https://github.com/luminous-ChenXi/LuomiNest/blob/main/docs/development/plugin-system.md)。

## 现有技能

| 技能 ID | 名称 | 描述 | 格式 |
|---------|------|------|------|
| `cooking-assistant` | 烹饪助手 | 菜谱推荐（根据冰箱食材）、步骤指导、营养分析 | manifest.json |
| `skill-creator` | 技能创建助手 | 元技能，指导 AI 创建、修改、校验 SKILL.md 文件 | SKILL.md |
| `travel-planner` | 旅行规划 | 根据用户需求规划旅行行程，提供景点推荐、路线安排、交通住宿建议 | SKILL.md |

## 用户安装流程

```
用户在 LuomiNest 插件市场点击「安装技能」
  → 后端从本仓库下载对应技能子目录的 zip
  → 解压到本地 skills/{id}/
  → cx_skill_loader 自动加载
  → 技能注入 LLM Prompt
```

下载 URL 推导规则（由 LuomiNest 后端自动生成）：

```
https://github.com/luminous-ChenXi/LuomiNest-cxp-skills/releases/latest/download/skill-{id}.zip
```

因此每个技能发版时需在本仓库创建一个 Release，附上 `skill-{id}.zip` 资源。

## 贡献你的技能

详见 [CONTRIBUTING.md](./CONTRIBUTING.md)。简要流程：

1. Fork 本仓库
2. 在根目录创建新子目录 `<skill-id>/`
3. 编写 `SKILL.md`（推荐）或 `manifest.json`
4. 提交 PR
5. 合并后维护者会创建对应 Release 并更新 `LuomiNest-cxp-registry/index.json`

## License

MIT — 见 [LICENSE](./LICENSE)
