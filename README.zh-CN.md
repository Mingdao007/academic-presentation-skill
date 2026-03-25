# Academic Presentation Skill

面向学术演示文稿的可移植 skill，用于把论文、海报和综述材料整理成最终展示稿，同时支持 Codex App 和 Claude CLI。

## 提供内容

- 可安装 skill: [`academic-presentation`](./academic-presentation)
- Codex App 元数据: [`academic-presentation/agents/openai.yaml`](./academic-presentation/agents/openai.yaml)
- 公开 references: [`academic-presentation/references/`](./academic-presentation/references)
- Claude CLI excerpt: [`claude-code-cli/CLAUDE.academic-presentation.md`](./claude-code-cli/CLAUDE.academic-presentation.md)

## 安装 / 使用

### Codex App

- 从本仓库路径 `academic-presentation` 安装
- GitHub 安装目标：
  - repo：`<owner>/academic-presentation-skill`
  - path：`academic-presentation`
- 安装后重启 `Codex App`，让新 skill 被发现。

### Claude CLI

- 打开 [`claude-code-cli/CLAUDE.academic-presentation.md`](./claude-code-cli/CLAUDE.academic-presentation.md)
- 把整段 excerpt 复制到你的项目 `CLAUDE.md`
- 最好把它保留成一个独立章节，方便后续替换和比对
- 如果你的环境只在会话开始时读取 `CLAUDE.md`，更新后重启 Claude CLI 会话

## 覆盖范围

- 支持 conference、seminar、defense、review deck 等场景路由
- 在 oral-talk 和 literature-review 两类 preset 之间做确定性选择
- 提供 paper-first 的学术演示工作流和公开参考材料
- 包含 rendered-deck visual QA 和 report-class source-text scan 指引

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

- 示例保持通用，不包含私有项目、课程或导师上下文。
- 这个公开包不包含本地绝对路径、私有工作区引用或依赖你个人环境的私有 skill 链接。

## 仓库结构

- `academic-presentation/`: installable `Codex App` skill
- `academic-presentation/agents/openai.yaml`: `Codex App` interface metadata
- `academic-presentation/references/`: bundled public references
- `claude-code-cli/CLAUDE.academic-presentation.md`: 可直接复制的 `Claude CLI` excerpt
- `CHANGELOG.md`: release history
- `LICENSE`: `MIT`

English:

- [README.md](./README.md)
