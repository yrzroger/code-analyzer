# 代码库结构

**分析日期:** 2026-05-13

## 目录布局

```
[project-root]/
├── .claude-plugin/       # Claude Code 插件配置
├── agents/               # Agent 定义文件
├── skills/               # Skill 定义文件
│   └── analyze-codebase/
│       ├── SKILL.md      # 协调者 Skill (入口)
│       ├── code-analyzer.md  # Agent 核心实现
│       └── assets/       # 10 个分析文档模板
├── .output/              # 分析输出目录
├── .git/                 # Git 版本控制
└── README.md             # 项目说明
```

## 目录用途

**.claude-plugin/:**
- 用途: Claude Code 插件配置文件
- 包含: plugin.json, marketplace.json
- 关键文件: `.claude-plugin/plugin.json` - 插件注册配置

**agents/:**
- 用途: 存放 Agent 定义文件
- 包含: code-analyzer.md
- 关键文件: `agents/code-analyzer.md` - 通用分析 Agent 定义

**skills/:**
- 用途: 存放 Skill 定义文件和模板
- 包含: analyze-codebase 目录及其内容
- 关键文件: `skills/analyze-codebase/SKILL.md` - 协调者 Skill 入口

**skills/analyze-codebase/assets/:**
- 用途: 存放 10 个分析文档模板
- 包含: ARCHITECTURE.md, STRUCTURE.md, STACK.md, INTEGRATIONS.md, CONVENTIONS.md, TESTING.md, CONCERNS.md, DEPENDENCIES.md, DATA-FLOW.md, FLOWCHARTS.md
- 关键文件: 所有模板文件 - 供 Agent 读取并填充内容

**.output/:**
- 用途: 分析结果输出目录
- 包含: 10 个分析报告文档 (由 Agent 生成)
- 关键文件: 分析完成后生成的目标代码库分析结果

## 关键文件位置

**入口点:**
- `skills/analyze-codebase/SKILL.md`: 协调者 Skill，用户通过 `/analyze-codebase` 命令触发
- `agents/code-analyzer.md`: 实际执行分析的 Agent 定义

**配置:**
- `.claude-plugin/plugin.json`: Claude Code 插件配置
- `.claude-plugin/marketplace.json`: Marketplace 配置文件

**核心逻辑:**
- `skills/analyze-codebase/SKILL.md`: 并行协调 6 个 Agent 的逻辑
- `agents/code-analyzer.md`: 根据 focus 参数执行特定领域分析的逻辑

**测试:**
- 不适用 - 本项目无测试文件 (纯 Markdown 定义)

## 命名规范

**文件:**
- Agent 文件: `[name].md` 格式，如 `code-analyzer.md`
- Skill 文件: `[name].md` 格式，如 `SKILL.md`
- 模板文件: `[doc-name].md` 格式，如 `ARCHITECTURE.md`

**目录:**
- 技能目录: 使用连字符命名，如 `analyze-codebase`
- 配置文件目录: 使用点号前缀，如 `.claude-plugin`

## 新增代码位置

**新功能:**
- 主代码: 不适用 - 项目由 Markdown 文件定义，无可执行代码
- 测试: 不适用

**新组件/模块:**
- 新 Agent: 在 `agents/` 目录添加 `[name].md` 文件
- 新 Skill: 在 `skills/` 目录添加 `[skill-name]/SKILL.md` 文件
- 新模板: 在 `skills/analyze-codebase/assets/` 目录添加模板文件

**工具:**
- 共享辅助函数: 不适用 - 无可执行代码

## 特殊目录

**skills/analyze-codebase/assets/:**
- 用途: 存储分析文档模板
- 是否生成: 否 - 由项目提供
- 是否提交: 是 - 属于项目源代码

**.output/:**
- 用途: 存储分析结果，由运行分析命令时自动创建
- 是否生成: 是 - 由分析命令执行时创建
- 是否提交: 否 - 每次分析都会重新生成

**.git/:**
- 用途: Git 版本控制元数据
- 是否生成: 否 - 由 Git 管理
- 是否提交: 是 - Git 必需文件

---

*结构分析: 2026-05-13*