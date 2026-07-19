# LuomiNest CxPlugin スキル集

[English](./README.md) | [简体中文](./README.zh-CN.md) | [日本語](./README.ja-JP.md)

LuomiNest スキル集約リポジトリ — すべてのスキルはサブディレクトリとして保存、コミュニティは PR で新スキルを貢献できます。

## リポジトリの役割

| リポジトリ | 役割 |
|------------|------|
| LuomiNest-cxp-registry | 中心インデックスレジストリ、`index.json` を管理 |
| LuomiNest-cxp-plugin-template | プラグイン開発テンプレート（フォーク出発点） |
| **LuomiNest-cxp-skills**（本リポジトリ） | スキル集約（各スキルはサブディレクトリ） |

プラグインと異なり、スキルは Markdown ファイル（`SKILL.md`）またはマニフェスト（`manifest.json`）のみで、複雑な Python コードを含みません。そのため、スキルごとに個別リポジトリを立てず、集約リポジトリで一括管理します。

## ディレクトリ構成

```
LuomiNest-cxp-skills/
├── cooking-assistant/      <- 料理アシスタントスキル
│   └── manifest.json
├── skill-creator/          <- スキル作成アシスタント（メタスキル）
│   └── SKILL.md
├── travel-planner/         <- 旅行計画スキル
│   └── SKILL.md
├── README.md               <- 英語（デフォルト）
├── README.zh-CN.md         <- 簡体字中国語
├── README.ja-JP.md         <- 日本語（本ファイル）
├── CONTRIBUTING.md
└── LICENSE
```

各スキルのサブディレクトリ名 = スキル id（kebab-case）。

## スキル形式

### SKILL.md（推奨）

YAML フロントマター + Markdown 本文：

```yaml
---
id: travel-planner
name: 旅行計画
version: 1.0.0
description: ユーザーの要望に基づく旅行計画
author: LuminousCX
license: MIT
tags: [travel, planning, lifestyle]
category: lifestyle
icon: Map
trigger_keywords: [旅行, 旅, 旅程]
---

# 旅行計画スキル

ユーザーが旅行関連の質問をしたとき...
```

### manifest.json（互換形式）

```json
{
  "id": "cooking-assistant",
  "type": "skill",
  "name": "料理アシスタント",
  "version": "1.0.0",
  "description": "レシピ提案、ステップガイド、栄養分析",
  "author": "LuminousCX",
  "license": "MIT",
  "icon": "ChefHat",
  "category": "lifestyle",
  "tags": ["community", "free"]
}
```

完全なフィールド仕様は [docs/development/plugin-system.md](https://github.com/luminous-ChenXi/LuomiNest/blob/main/docs/development/plugin-system.md) を参照。

## 既存スキル

| スキル ID | 名前 | 説明 | 形式 |
|-----------|------|------|------|
| `cooking-assistant` | 料理アシスタント | レシピ提案（冷蔵庫の食材から）、ステップガイド、栄養分析 | manifest.json |
| `skill-creator` | スキル作成アシスタント | メタスキル、AI に SKILL.md ファイルの作成・修正・検証を指導 | SKILL.md |
| `travel-planner` | 旅行計画 | ユーザーの要望に基づく旅行計画、観光地提案、ルート計画、交通・宿泊提案 | SKILL.md |

## インストールフロー

```
ユーザーが LuomiNest プラグイン市場で「スキールをインストール」をクリック
  -> バックエンドが本リポジトリから対応スキルのサブディレクトリ zip をダウンロード
  -> ローカル skills/{id}/ に解凍
  -> cx_skill_loader が自動読み込み
  -> スキルを LLM プロンプトに注入
```

ダウンロード URL 導出ルール（LuomiNest バックエンドが自動生成）：

```
https://github.com/luminous-ChenXi/LuomiNest-cxp-skills/releases/latest/download/skill-{id}.zip
```

そのため各スキルのリリース時には本リポジトリで Release を作成し、`skill-{id}.zip` アセットを添付する必要があります。

## スキルの貢献

[CONTRIBUTING.md](./CONTRIBUTING.md) を参照。簡易フロー：

1. 本リポジトリをフォーク
2. ルートに新サブディレクトリ `<skill-id>/` を作成
3. `SKILL.md`（推奨）または `manifest.json` を作成
4. PR を提出
5. マージ後、メンテナーが対応する Release を作成し `LuomiNest-cxp-registry/index.json` を更新

## License

MIT — [LICENSE](./LICENSE) を参照
