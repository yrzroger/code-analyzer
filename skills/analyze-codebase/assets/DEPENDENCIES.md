# 代码依赖关系

**分析日期:** [YYYY-MM-DD]

## 模块依赖概览

**结构:** [层级数] 层， [模块数] 个核心模块

## 核心模块依赖

**[模块名称]:**
- 位置: `path/to/module`
- 导入: [moduleA, moduleB]
- 被导入: [moduleC, moduleD]

## 循环依赖

**状态:** [存在/不存在]

**[循环依赖链]:**
- `moduleA` → `moduleB` → `moduleC` → `moduleA`

## 孤立模块

**数量:** [N] 个

| 模块 | 路径 |
|------|------|
| ... | ... |

## 依赖层级

**最深链路:** [depth] 层

```
[module] → [module] → [module] → ...
```

---

*依赖分析: [date]*