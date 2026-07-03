# 项目名称

> 一句话项目简介

## 项目简介

详细描述项目背景、目标和核心价值。

## 核心架构

- 技术栈说明
- 架构设计要点
- 目录结构说明

## 编码规范

- 语言和框架规范
- 命名约定
- 注释规范

## 审查重点

- 安全性要求
- 性能要求

## 团队角色

本项目采用5人专家团模式（可按项目规模调整），详见 docs/roles/：

| 角色 | 文件 | 核心职责 |
|------|------|---------|
| A 架构师 | docs/roles/team-lead.md | 统筹、架构、终审 |
| B 售前需求 | docs/roles/requirements-analyst.md | 需求、验收、变更管控 |
| C 后端专家 | docs/roles/backend-expert.md | 服务、数据库、接口 |
| D 前端专家 | docs/roles/frontend-expert.md | 页面、交互、联调 |
| E 工程运维 | docs/roles/engineering-expert.md | CI/CD、测试、安全 |

每位成员使用Qoder前应阅读自己的角色文件，了解职责、权限和模型调度策略。

## 开发流程

详见 docs/workflow.md（7阶段流程）和 docs/model-strategy.md（模型调度策略）。

核心规则：Spec未定稿，绝不允许写业务代码。

## 人+AI 协作开发流程

项目以 GitHub 为唯一中枢，Qoder 在每个环节增强自动化能力。完整流程详见 docs/pipeline.md。

### Issue 标签体系

类型标签: type:requirement / type:change-request / type:bug / type:task

状态流转:
- 需求: status:new -> status:refining -> status:confirmed -> status:analyzing -> status:spec-ready -> status:in-dev -> status:done
- 变更: status:pending-review -> status:impact-assessed -> status:approved / status:rejected

### 分支规范

- feat/<issue>-<desc> - 功能分支
- fix/<issue>-<desc> - Bug修复
- change/<issue>-<desc> - 需求变更
- release/v<ver> - 发布分支

### PR规范

- 标题: <type>: <description> (closes #<issue>)
- 必须关联Issue，合入前通过三层评审（自评 -> 交叉复审 -> 架构+售前双终审）

## 忽略的检查

- node_modules/ 和 dist/ 目录
- .qoder/ 目录下的自动生成文件
- docs/research/ 和 docs/analysis/ 中的原始调研材料