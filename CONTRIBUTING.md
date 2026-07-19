# 贡献你的技能到 LuomiNest

感谢你为 LuomiNest 社区贡献技能！本文档介绍如何添加新技能并通过审核流程。

## 技能 vs 插件

在贡献之前，请先确认你要贡献的是「技能」还是「插件」：

| 类型 | 复杂度 | 入口 | 仓库 |
|------|--------|------|------|
| 技能（Skill） | 简单 — 纯 Markdown 提示词 | `SKILL.md` / `manifest.json` | 本仓库（集合仓库） |
| 插件（Plugin） | 复杂 — Python 代码、工具、API 路由 | `main.py` + `manifest.json` | 独立仓库 `LuomiNest-cxp-<name>` |

如果你要贡献的是带 Python 代码的插件，请改为使用 [LuomiNest-cxp-plugin-template](https://github.com/luminous-ChenXi/LuomiNest-cxp-plugin-template) 创建独立仓库。

## 技能文件格式

### 推荐：SKILL.md

YAML frontmatter + Markdown body：

```yaml
---
id: my-skill                      # 必填，kebab-case，与目录名一致
name: 我的技能                     # 必填，中文名称
version: 1.0.0                    # 必填
description: 一句话描述技能功能     # 必填，20-80 字
author: YourName                  # 必填
license: MIT                      # 推荐 MIT
tags: [example, demo]             # 可选
category: productivity            # 可选：productivity / lifestyle / tool / integration
icon: Sparkles                    # 可选，lucide 图标名（PascalCase）
trigger_keywords: [关键词1, 关键词2]  # 可选，触发关键词
---

# 我的技能

## 触发条件
当用户提到「关键词1」或「关键词2」时，本技能会被激活。

## 能力
- 能力 1
- 能力 2

## 输出格式
...
```

### 兼容：manifest.json

```json
{
  "id": "my-skill",
  "type": "skill",
  "name": "我的技能",
  "version": "1.0.0",
  "description": "一句话描述技能功能",
  "author": "YourName",
  "license": "MIT",
  "category": "productivity",
  "tags": ["example"],
  "icon": "Sparkles"
}
```

## 字段规范

| 字段 | 必填 | 类型 | 说明 |
|------|------|------|------|
| `id` | ✅ | string | kebab-case，与目录名一致，避免与已有技能冲突 |
| `name` | ✅ | string | 人类可读名称（中文或英文） |
| `version` | ✅ | string | 语义化版本号 `MAJOR.MINOR.PATCH` |
| `description` | ✅ | string | 20-80 字一句话描述技能功能 |
| `author` | ✅ | string | 作者名（可附 GitHub URL） |
| `license` | 推荐 | string | 推荐 MIT，也可选 Apache-2.0 等 |
| `tags` | 可选 | string[] | 标签数组，便于分类搜索 |
| `category` | 可选 | string | productivity / lifestyle / tool / integration |
| `icon` | 可选 | string | lucide 图标名（PascalCase，如 `Sparkles`） |
| `trigger_keywords` | 可选 | string[] | 触发关键词数组 |

## 提交流程

```bash
# 1. Fork 本仓库到你的 GitHub 账户

# 2. 克隆 Fork 后的仓库
git clone https://github.com/<your-username>/LuomiNest-cxp-skills.git
cd LuomiNest-cxp-skills

# 3. 创建技能子目录
mkdir my-skill
# 编辑 my-skill/SKILL.md 或 my-skill/manifest.json

# 4. 本地测试（可选）
# 把 my-skill/ 复制到 LuomiNest 项目 backend/skills/ 下
# 启动 LuomiNest 后端，技能会自动加载

# 5. 提交并推送
git add my-skill
git commit -m "feat: add my-skill v1.0.0"
git push origin main

# 6. 在 GitHub 上发起 PR
# 标题格式：feat: add skill <skill-id> v<version>
```

## 审核标准

维护者会按以下标准审核 PR：

- [ ] `id` 符合 kebab-case 命名规范
- [ ] `name` 与 `description` 准确描述技能功能
- [ ] `version` 遵循语义化版本号
- [ ] 不包含 Python 代码（如有，请使用插件模板）
- [ ] 不包含敏感信息（密钥、token 等）
- [ ] 不包含版权侵权内容
- [ ] License 字段已填写（推荐 MIT）
- [ ] 目录名与 `id` 一致

## 发布 Release

PR 合并后，维护者会：

1. 为该技能创建 GitHub Release（tag: `skill-<id>-v<version>`）
2. 将技能目录打包为 `skill-<id>.zip` 作为 Release 资源
3. 更新 [LuomiNest-cxp-registry](https://github.com/luminous-ChenXi/LuomiNest-cxp-registry) 仓库的 `index.json` 添加新条目

之后所有 LuomiNest 用户都能在「插件市场」中看到并安装该技能。

## 联系

- 提 Issue 反馈问题或建议
- PR 讨论技能设计
