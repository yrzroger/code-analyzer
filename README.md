# Code Analyzer

Claude Code 插件，使用 6 个并行 agent 分析代码库，生成 10 个结构化文档。

## 功能

自动分析目标代码库，输出以下文档到 `.output/` 目录：

1. **STACK.md** - 技术栈（语言、框架、依赖）
2. **INTEGRATIONS.md** - 外部集成（API、数据库、服务）
3. **ARCHITECTURE.md** - 架构模式
4. **STRUCTURE.md** - 代码结构
5. **CONVENTIONS.md** - 编码规范
6. **TESTING.md** - 测试模式
7. **CONCERNS.md** - 问题与风险
8. **DEPENDENCIES.md** - 代码依赖
9. **DATA-FLOW.md** - 数据流
10. **FLOWCHARTS.md** - 流程图 (Mermaid)

## 安装

```bash
claude plugin install ./code-analyzer-plugin
```

或复制到插件目录：

```bash
cp -r code-analyzer-plugin ~/.claude/plugins/cache/claude-plugins-official/code-analyzer/1.0.0
```

## 使用

在任意项目目录下运行：

```
/code-analyzer [可选：目标目录路径]
```

默认分析当前目录。

## 分析的 Agent

- `tech-analyzer` - 技术栈和集成
- `arch-analyzer` - 架构和结构
- `quality-analyzer` - 代码质量和测试
- `concerns-analyzer` - 问题与风险
- `deps-analyzer` - 依赖分析
- `flow-analyzer` - 数据流和流程图