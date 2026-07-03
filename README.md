# Qoder + GitHub 全流程协作框架模板

> 基于 Qoder Pro + GitHub 的人+AI 协作开发框架，适用于中型新项目从调研到上线的全生命周期管理。

## 这是什么

一个 **GitHub 模板仓库**，提供开箱即用的协作开发基础设施：

- 8 个自动化工作流（需求细化 → Spec 生成 → Wiki 同步 → 代码审查 → 变更传播）
- 5 人专家团角色定义（架构师、售前需求、后端、前端、工程运维）
- 7 阶段开发流程（调研 → 地基 → Ultra Spec → 并行开发 → 三层评审 → 自动验证 → 发布）
- 文档版本管理 + 变更传播自动通知
- 标签体系 + Issue 模板

方法论对齐 [Qoder V1 400万行官方案例](https://qoder.com/zh/blog/qoder-v1-mega-rewrite)：**地基 → Ultra Spec → 专家团并行 → Ultra Review → 自愈飞轮**。

## 快速开始

### 1. 创建项目

点击仓库页面右上角 **「Use this template」→「Create a new repository」**，输入你的项目名称。

### 2. 初始化配置

`ash
git clone https://github.com/你的用户名/你的项目.git
cd 你的项目
`

**必填 Secret**（Settings → Secrets → Actions）：
- `QODER_PERSONAL_ACCESS_TOKEN`：在 [Qoder 设置](https://qoder.com/settings) 生成

**同步标签**（终端执行）：
`ash
gh label create "type:requirement" -d "功能需求" -c "0075ca"
gh label create "type:change-request" -d "需求变更" -c "e4e669"
gh label create "type:bug" -d "Bug报告" -c "d73a4a"
gh label create "type:task" -d "开发任务" -c "0e8a16"
gh label create "status:new" -d "新提交" -c "c5def5"
gh label create "status:refining" -d "AI细化中" -c "fbca04"
gh label create "status:done" -d "已完成" -c "0e8a16"
gh label create "doc:draft" -d "文档草稿" -c "e4e669"
gh label create "doc:approved" -d "文档已批准" -c "0e8a16"
# 完整标签列表见 .github/labels.yml
`

### 3. 填写项目信息

编辑 `AGENTS.md`，替换占位内容为你的项目实际信息（项目简介、技术栈、编码规范等）。

### 4. 分配团队角色

每人阅读自己的角色文件，了解职责和 Qoder 用法：

| 角色 | 文件 | 核心职责 |
|------|------|---------|
| A 架构师 | [docs/roles/team-lead.md](docs/roles/team-lead.md) | 统筹、终审、架构决策 |
| B 售前需求 | [docs/roles/requirements-analyst.md](docs/roles/requirements-analyst.md) | 需求、验收、变更管控 |
| C 后端专家 | [docs/roles/backend-expert.md](docs/roles/backend-expert.md) | 服务、数据库、接口 |
| D 前端专家 | [docs/roles/frontend-expert.md](docs/roles/frontend-expert.md) | 页面、交互、联调 |
| E 工程运维 | [docs/roles/engineering-expert.md](docs/roles/engineering-expert.md) | CI/CD、测试、安全 |

## 自动化工作流

| 工作流 | 触发条件 | 作用 |
|--------|---------|------|
| `issue-refine.yml` | Issue 添加 `type:requirement` | Qoder 自动细化需求 |
| `change-impact.yml` | Issue 添加 `type:change-request` | Qoder 评估变更影响 + 下游检测 |
| `docs-review.yml` | docs/ PR 提交 | Qoder 评审文档质量 |
| `spec-generation.yml` | 分析文档 PR 合入 | Qoder 生成 Ultra Spec |
| `wiki-update.yml` | Spec 合入 main | Qoder 更新 RepoWiki |
| `doc-change-notify.yml` | 文档目录变更合入 | Qoder 通知下游 Issue |
| `code-review.yml` | PR 提交 | Qoder 自动代码审查 |
| `auto-changelog.yml` | Release 创建 | 自动生成 Changelog |

## 核心开发流程

详见 [docs/workflow.md](docs/workflow.md)（7 阶段）和 [docs/pipeline.md](docs/pipeline.md)（自动化管线）。

**核心规则：Spec 未定稿，绝不允许写业务代码。**

`
调研(0-1天) → 地基(1-2天) → Ultra Spec(2-4天) → 并行开发(4-18天) → 三层评审 → 自动验证+夜间自愈 → 发布
`

## 文档管理

- **版本规范**：[docs/doc-standards.md](docs/doc-standards.md) — frontmatter 格式、状态流转、变更日志
- **文档模板**：[docs/templates/](docs/templates/) — 调研报告、Spec 文档模板
- **模型调度**：[docs/model-strategy.md](docs/model-strategy.md) — 高级/标准模型选择策略

## 目录结构

`
├── .github/
│   ├── ISSUE_TEMPLATE/     # 4 个 Issue 模板（需求/变更/Bug/任务）
│   ├── workflows/           # 8 个自动化工作流
│   └── labels.yml           # 标签体系定义
├── .qoder/agents/           # Qoder Agent 配置
├── docs/
│   ├── roles/               # 5 个角色定义文件
│   ├── templates/           # 文档模板（调研报告、Spec）
│   ├── doc-standards.md     # 文档版本管理规范
│   ├── workflow.md          # 7 阶段开发流程
│   ├── model-strategy.md    # 模型调度策略
│   └── pipeline.md          # 自动化管线说明
├── AGENTS.md                # 项目上下文（所有 Qoder 共享）
└── .gitignore
`

## 团队协作模式

每人独立 Qoder Pro 账号，各自在自己的分支开发，通过 GitHub 协同：

`
张三 (Qoder) → feat/12-ner-panel    → PR → 三层评审 → 合并
李四 (Qoder) → feat/15-batch-import → PR → 三层评审 → 合并
王五 (Qoder) → fix/20-status-bug    → PR → 三层评审 → 合并
`

不限人数，GitHub 处理并发，模板管流程，Qoder 管个人。

## 许可

MIT