# 数据流分析

**分析日期:** [YYYY-MM-DD]

## 数据输入点

| 入口 | 类型 | Handler |
|------|------|---------|
| `/api/users` | REST API | `handlers/user.ts` |
| `cli.cmd` | CLI | `src/cli.ts` |

## 数据处理路径

### [处理流程名称]

**输入:** [数据源]
**输出:** [目标]

| 步骤 | 处理 | 文件 |
|------|------|------|
| 1 | 验证 | `services/validator.ts` |
| 2 | 转换 | `services/transformer.ts` |
| 3 | 存储 | `repos/user-repo.ts` |

## 数据存储操作

### 读取操作

| 数据 | 来源 | 读取方 |
|------|------|--------|
| User | PostgreSQL | `repos/user-repo.ts` |

### 写入操作

| 数据 | 目标 | 写入方 |
|------|------|--------|
| User | PostgreSQL | `repos/user-repo.ts` |

## 状态管理

**方案:** [Redux/Context/其他]

**状态流转:** `init` → `loading` → `ready` / `error`

---

*数据流分析: [date]*