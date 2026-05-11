# Academic Presentation Skill

可移植的学术汇报 skill，用于把论文、poster 和 review 材料整理成最终可讲的 academic deck，并支持 Codex App 与 Claude CLI 使用。

## 适合谁

| 适合使用 | 不适合使用 |
| --- | --- |
| 把论文、poster 或已经整理好的 review 内容变成汇报 deck | 只需要底层 PowerPoint XML 修复 |
| 需要 seminar、conference、defense 或 review deck 的稳定预设 | 还没有 review 内容，需要从零做文献综述 |
| 希望同一个公开包同时支持 Codex App 和 Claude CLI | 只是解释某一页 slide 或一段文字 |

## 为什么需要它

- 把上游 review synthesis 和最终 deck authoring 分开。
- 把可复用的 presentation preset 放在 skill package 里。
- 让生成 deck 的 visual QA 预期更明确。

## 包含内容

| Component | 作用 |
| --- | --- |
| [`academic-presentation`](./academic-presentation) | 可安装的 Codex App skill package |
| [`academic-presentation/agents/openai.yaml`](./academic-presentation/agents/openai.yaml) | Codex App 界面 metadata |
| [`academic-presentation/references`](./academic-presentation/references) | 随包发布的公开 reference material |
| [`academic-presentation/test-prompts.json`](./academic-presentation/test-prompts.json) | trigger / non-trigger 示例 |
| [`claude-code-cli/CLAUDE.academic-presentation.md`](./claude-code-cli/CLAUDE.academic-presentation.md) | 可复制的 Claude CLI excerpt |
| [`CHANGELOG.md`](./CHANGELOG.md) | release history |
| [`LICENSE`](./LICENSE) | license |

## 安装 / 使用

### Codex App

- 从本 repo 的这个路径安装 skill：`academic-presentation`
- GitHub install target:
  - repo: `Mingdao007/academic-presentation-skill`
  - path: `academic-presentation`
- 安装后重启 `Codex App`，让新 skill 被重新发现。

## 工作流

```mermaid
flowchart LR
    A["源材料"] --> B["汇报触发"]
    B --> C["预设选择"]
    C --> D["Deck authoring"]
    D --> E["Rendered QA"]
```

## 覆盖范围

- conference、seminar、defense 和 review deck 路由
- oral talk 与 literature-review deck 的确定性 preset 选择
- paper-first presentation workflow 和公开 references
- rendered deck visual QA 与 report-class source-text scan guidance

## 预期结果 / 验证

| 检查项 | 预期结果 |
| --- | --- |
| 安装路径 | `academic-presentation` |
| GitHub target | `Mingdao007/academic-presentation-skill`，path 为 `academic-presentation` |
| Skill 入口 | 存在 `academic-presentation/SKILL.md` |
| 触发样例 | `academic-presentation/test-prompts.json` |
| 隐私检查 | 公开包不包含私人本机路径或 live user state |

## 触发示例

- `Make a literature-review deck from these papers.`
- `Turn this poster into a short talk deck.`
- `Prepare a seminar presentation from this paper.`

## 不应触发

- `Edit one existing .pptx template at the XML level.`
- `Do a full literature review from scratch.`
- `Only explain one slide or one paragraph.`

## 隐私边界

这个公开仓库只保留通用、可复用的 workflow。

- 示例保持通用，不包含私人项目、课程或导师上下文。
- 公开包不发布本机绝对路径、私人 workspace reference 或主机特定 private skill link。

## 仓库结构

| 路径 | 作用 |
| --- | --- |
| [`academic-presentation`](./academic-presentation) | 可安装的 Codex App skill package |
| [`academic-presentation/agents/openai.yaml`](./academic-presentation/agents/openai.yaml) | Codex App 界面 metadata |
| [`academic-presentation/references`](./academic-presentation/references) | 随包发布的公开 reference material |
| [`academic-presentation/test-prompts.json`](./academic-presentation/test-prompts.json) | trigger / non-trigger 示例 |
| [`claude-code-cli/CLAUDE.academic-presentation.md`](./claude-code-cli/CLAUDE.academic-presentation.md) | 可复制的 Claude CLI excerpt |
| [`CHANGELOG.md`](./CHANGELOG.md) | release history |
| [`LICENSE`](./LICENSE) | license |

English:

- [README.md](./README.md)
