# 架构

**分析日期:** 2026-05-13

## 架构模式概览

**总体架构:** Agent 并行协调架构 (Multi-Agent Orchestration)

**关键特性:**
- 并行执行 6 个专业分析 Agent
- 使用统一的 code-analyzer Agent 处理不同分析领域
- 基于 Markdown 的 Agent 定义和模板系统
- 目标代码库的 .output/ 目录输出结构化文档

## 层级

**协调层 (Coordination Layer):**
- 用途: 协调并行执行多个分析 Agent，解析参数并管理输出
- 位置: `skills/analyze-codebase/SKILL.md`
- 包含: 协调逻辑、参数解析、Agent 启动配置
- 依赖: Claude Code 插件系统
- 被依赖: Claude Code 命令行接口

**Agent 层 (Agent Layer):**
- 用途: 根据 focus 参数执行特定领域的代码分析
- 位置: `agents/code-analyzer.md`
- 包含: Agent 角色定义、参数处理、探索命令模板、成功标准
- 依赖: 模板文件、目标代码库
- 被依赖: 被 SKILL.md 调用

**模板层 (Template Layer):**
- 用途: 定义输出文档的结构和格式规范
- 位置: `skills/analyze-codebase/assets/`
- 包含: 10 个 Markdown 模板文件
- 依赖: 无
- 被依赖: 被 code-analyzer Agent 读取使用

**输出层 (Output Layer):**
- 用途: 存储分析结果文档
- 位置: `{target-codebase}/.output/`
- 包含: 10 个分析报告文档
- 依赖: Agent 层生成内容

## 数据流

**主流程:**

1. 用户调用 `/analyze-codebase [目标目录]`
2. SKILL.md 解析目标目录参数（默认当前目录）
3. 创建 `{target}/.output/` 目录
4. 并行启动 6 个 code-analyzer Agent 实例
5. 每个 Agent 接收: focus 参数 + templates 参数
6. 各 Agent 探索目标代码库，读取模板，写入输出文档
7. 验证 10 个文档全部生成
8. 显示完成摘要

**Agent 并行执行映射:**

| Agent 序号 | focus | 模板 |
|-----------|-------|------|
| 1 | tech | STACK.md, INTEGRATIONS.md |
| 2 | arch | ARCHITECTURE.md, STRUCTURE.md |
| 3 | quality | CONVENTIONS.md, TESTING.md |
| 4 | concerns | CONCERNS.md |
| 5 | deps | DEPENDENCIES.md |
| 6 | flow | DATA-FLOW.md, FLOWCHARTS.md |

**状态管理:**
- 无持久状态，所有状态由 Claude Code 运行时管理
- Agent 间无状态共享，完全并行独立执行

## 关键抽象

**code-analyzer Agent:**
- 用途: 通用代码分析 Agent，根据 focus 参数执行不同领域的分析
- 示例: `agents/code-analyzer.md`
- 模式: 参数化 Agent 模式 (单一 Agent 文件处理多种分析场景)

**模板系统:**
- 用途: 标准化输出文档格式
- 示例: `skills/analyze-codebase/assets/ARCHITECTURE.md`
- 模式: 占位符替换模式 (使用 `[placeholder]` 标记待填充内容)

**协调器 SKILL:**
- 用途: 并行协调多个 Agent 完成分析任务
- 示例: `skills/analyze-codebase/SKILL.md`
- 模式: 工作流编排模式

## 入口点

**主入口:**
- 位置: `skills/analyze-codebase/SKILL.md`
- 触发: 用户运行 `/analyze-codebase [目标目录]`
- 职责: 解析参数、创建输出目录、并行启动 6 个 Agent、验证结果

**Agent 入口:**
- 位置: `agents/code-analyzer.md`
- 触发: 被 SKILL.md 并行调用，传入 focus 和 templates 参数
- 职责: 探索目标代码库、读取模板、写入分析文档

## 错误处理

**策略:** 验证驱动 + 分层处理

**模式:**
- SKILL 层: 验证 10 个文档是否全部生成
- Agent 层: 模板占位符未填充时使用 "未检测到" 或 "不适用"
- 系统层: 忽略禁止文件（.env、credentials 等）

## 横切关注点

**日志:** 无显式日志系统，由 Claude Code Agent 输出替代

**验证:** SKILL.md 包含验收标准检查

**认证:** 不适用 (无外部服务集成)

---

*架构分析: 2026-05-13*