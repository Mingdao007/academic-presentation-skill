# Academic Presentation Skill

面向学术演示文稿的可移植 skill，用于把论文、海报和综述材料整理成最终展示稿。

## 提供内容

- 可安装 skill: [`academic-presentation`](./academic-presentation)
- 公开 references: [`academic-presentation/references/`](./academic-presentation/references)

## 安装 / 使用

- `Codex App`：从本仓库路径 `academic-presentation` 安装
- GitHub 安装目标：
  - repo：`<owner>/academic-presentation-skill`
  - path：`academic-presentation`
- 安装后重启 `Codex App`，让新 skill 被发现。

## 覆盖范围

- 支持 conference、seminar、defense、review deck 等场景路由
- 在 oral-talk 和 literature-review 两类 preset 之间做确定性选择
- 提供 paper-first 的学术演示工作流和公开参考材料

## 触发示例

- `Make a literature-review deck from these papers.`
- `Turn this poster into a short talk deck.`
- `Prepare a seminar presentation from this paper.`

## 不触发示例

- `Edit one existing .pptx template at the XML level.`
- `Do a full literature review from scratch.`
- `Only explain one slide or one paragraph.`

## 隐私边界

这个公开仓库只保留可复用、可公开的工作流部分。

- Examples stay generic and omit private project, course, or advisor context.
- This package publishes no local absolute paths or private workspace references.

## 仓库结构

- `academic-presentation/`: installable `Codex App` skill
- `academic-presentation/references/`: bundled public references
- `CHANGELOG.md`: release history
- `LICENSE`: `MIT`

English:

- [README.md](./README.md)
