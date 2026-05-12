---
name: code-analyzer
description: "Analyze codebase with parallel agents to produce .output/ documents"
argument-hint: "[optional: path to codebase, default is the current directory]"
---

## 目标

使用 6 个并行 analyzer agent 分析代码库，输出 10 个结构化文档到目标项目的 .output/ 目录。

**输出文档：**
1. STACK.md - 技术栈
2. INTEGRATIONS.md - 外部集成
3. ARCHITECTURE.md - 架构模式
4. STRUCTURE.md - 代码结构
5. CONVENTIONS.md - 编码规范
6. TESTING.md - 测试模式
7. CONCERNS.md - 问题与风险
8. DEPENDENCIES.md - 代码依赖
9. DATA-FLOW.md - 数据流
10. FLOWCHARTS.md - 流程图 (Mermaid)


## 前置条件

Target directory: $ARGUMENTS (可选，默认当前目录)
Output directory: {target}/.output/

## 架构设计

- 并行执行 6 个 agent
- 每个 agent 独立负责特定分析维度
- 输出文档到目标项目的 .output/ 目录


## 处理流程

1. 解析目标目录参数，默认当前目录 
2. 创建 {target}/.output/ 目录 
3. 并行启动 6 个 analyzer agent:  
   - Agent 1: tech-analyzer → STACK.md, INTEGRATIONS.md
   - Agent 2: arch-analyzer → ARCHITECTURE.md, STRUCTURE.md
   - Agent 3: quality-analyzer → CONVENTIONS.md, TESTING.md
   - Agent 4: concerns-analyzer → CONCERNS.md
   - Agent 5: deps-analyzer → DEPENDENCIES.md
   - Agent 6: flow-analyzer → DATA-FLOW.md, FLOWCHARTS.md
4. 等待所有 agent 完成
5. 验证 10 个文档已生成
6. 显示完成摘要


## 验收标准

- [ ] 处理流程无错误
- [ ] 10 个文档全部生成
- [ ] 并行 agent 全部完成
- [ ] 输出目录结构正确
- [ ] 文档内容符合模板要求
