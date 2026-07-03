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

## 人+AI 协作开发流程

项目以 **GitHub 为唯一中枢**，Qoder 在每个环节增强自动化能力。完整流程详见 `docs/pipeline.md`。

### Issue 标签体系

**类型标签**: type:requirement / type:change-request / type:bug / type:task

**状态流转**:
- 需求: status:new -> status:refining -> status:confirmed -> status:analyzing -> status:spec-ready -> status:in-dev -> status:done
- 变更: status:pending-review -> status:impact-assessed -> status:approved / status:rejected

### 分支规范

- feat/<issue>-<desc> — 功能分支
- fix/<issue>-<desc> — Bug 修复
- change/<issue>-<desc> — 需求变更
- release/v<ver> — 发布分支

### PR 规范

- 标题: <type>: <description> (closes #<issue>)
- 必须关联 Issue，合入前通过 Code Review
