---
name: analyze-codebase
description: "Analyze codebase with parallel agents to produce .output/ documents"
argument-hint: "[optional: path to codebase, default is the current directory]"
---

## 目标

使用 6 个并行 code-analyzer agent 分析代码库，每个agent根据focus参数执行特定领域的分析，输出 10 个结构化文档到目标项目的 .output/ 目录。

**输出文档：**
1. STACK.html - 技术栈
2. INTEGRATIONS.html - 外部集成
3. ARCHITECTURE.html - 架构模式
4. STRUCTURE.html - 代码结构
5. CONVENTIONS.html - 编码规范
6. TESTING.html - 测试模式
7. CONCERNS.html - 问题与风险
8. DEPENDENCIES.html - 代码依赖
9. DATA-FLOW.html - 数据流
10. FLOWCHARTS.html - 流程图 (Mermaid + 交互式)


## 前置条件

Target directory: $ARGUMENTS (可选，默认当前目录)
Output directory: {target}/.output/

## 架构设计

- 并行执行 6 个 analyze-codebase:code-analyzer agent 实例
- 每个 agent 接收参数: focus (专注领域) + templates (模板列表)
- 使用统一的 agent 文件: `agents/code-analyzer.md`
- 模板文件位于: `skills/analyze-codebase/assets/`


## 处理流程

1. 解析目标目录参数，默认当前目录
2. 创建 {target}/.output/ 目录
3. 并行启动 6 个 analyze-codebase:code-analyzer agent，每个传递不同参数:
   - Agent 1: focus=tech, templates=[STACK.html, INTEGRATIONS.html]
   - Agent 2: focus=arch, templates=[ARCHITECTURE.html, STRUCTURE.html]
   - Agent 3: focus=quality, templates=[CONVENTIONS.html, TESTING.html]
   - Agent 4: focus=concerns, templates=[CONCERNS.html]
   - Agent 5: focus=deps, templates=[DEPENDENCIES.html]
   - Agent 6: focus=flow, templates=[DATA-FLOW.html, FLOWCHARTS.html]
4. 等待所有 agent 完成
5. 验证 10 个文档已生成
6. 显示完成摘要


## 验收标准

- [ ] 处理流程无错误
- [ ] 10 个文档全部生成
- [ ] 并行 agent 全部完成
- [ ] 输出目录结构正确
- [ ] 文档内容符合模板要求