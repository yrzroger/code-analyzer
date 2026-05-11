---
name: code-analyzer
description: "分析代码库的技术架构、技术栈、代码结构、流程等，输出 10 个结构化文档"
argument-hint: "[optional: 要分析的代码库路径，默认当前目录]"
allowed-tools:
  - Read
  - Bash
  - Glob
  - Grep
  - Write
  - Task
---

<objective>
使用 6 个并行 mapper agent 分析代码库，输出 10 个结构化文档到目标项目的 output/ 目录。

Output: 10 个 Markdown 文档 (STACK, INTEGRATIONS, ARCHITECTURE, STRUCTURE, CONVENTIONS, TESTING, CONCERNS, DEPENDENCIES, DATA-FLOW, FLOWCHARTS)
</objective>

<context>
Target directory: $ARGUMENTS (可选，默认当前目录)
Output directory: {target}/output/

基于 gsd-map-codebase 架构:
- 并行执行 6 个 agent
- 每个 agent 独立负责特定分析维度
- 输出文档到目标项目的 output/ 目录
</context>

<process>
1. 解析目标目录参数，默认当前目录
2. 创建 {target}/output/ 目录
3. 并行启动 6 个 mapper agent:
   - Agent 1: tech focus → STACK.md, INTEGRATIONS.md
   - Agent 2: arch focus → ARCHITECTURE.md, STRUCTURE.md
   - Agent 3: quality focus → CONVENTIONS.md, TESTING.md
   - Agent 4: concerns focus → CONCERNS.md
   - Agent 5: deps focus → DEPENDENCIES.md
   - Agent 6: flow focus → DATA-FLOW.md, FLOWCHARTS.md
4. 等待所有 agent 完成
5. 验证 10 个文档已生成
6. 显示完成摘要
</process>

<success_criteria>
- [ ] 10 个文档全部生成
- [ ] 并行 agent 全部完成
- [ ] 输出目录结构正确
- [ ] 文档风格与现有 gsd-map-codebase 一致
</success_criteria>