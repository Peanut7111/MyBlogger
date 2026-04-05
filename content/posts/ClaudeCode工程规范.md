---
title: "如何规范地使用 Claude Code 开发工程"
date: 2026-04-05
tags: ["Claude Code", "工作流程"]
categories: []
description: "总结一套模板化的工程开发流程，让 Claude Code 的使用更加规范高效"
---

## 背景


本文总结我自己的 Claude Code 工程开发规范，核心观点：**模版化的文件架构 + 标准化的开发流程 = 高质量的工程**。

---

## 一、核心原则

### 1. Rules 是基础，Hooks 是保障

| 组件 | 作用 | 性质 |
|------|------|------|
| **Rules** | 定义工作标准和规范 | 指导性 |
| **Hooks** | 自动化执行和检查 | 强制性 |

两者配合：Rules 告诉 Claude "应该怎么做"，Hooks 确保"真的做到了"。

### 2. 每个工程都应该有 CLAUDE.md

`CLAUDE.md` 是项目的"说明书"，包含：
- 项目用途和结构
- 技术栈说明
- 目录组织方式
- 注意事项和坑点
- 当前状态 / 未完成的事
- 相关文档链接

### 3. 标准化的工作流程

```
需求 → 规划 → 执行 → 审查 → 提交
```

---

## 二、工程目录结构规范

### 通用项目模板

```
项目名称/
├── .claude/                    # Claude Code 配置
│   ├── rules/                 # 项目级规则（可选，覆写用户级）
│   │   ├── coding-style.md    # 编码规范
│   │   ├── git-workflow.md    # Git 流程
│   │   └── security.md        # 安全规范
│   ├── agents/                # 项目专用 Agent
│   └── settings.json           # 项目配置
├── docs/                       # 文档
│   ├── ARCHITECTURE.md        # 架构设计
│   ├── API.md                 # 接口文档
│   └── DEPLOY.md              # 部署说明
├── src/                        # 源代码
├── tests/                      # 测试
├── scripts/                    # 脚本
├── CLAUDE.md                   # 项目说明（必须）
├── README.md                   # 入口文档
├── .gitignore
└── package.json
```

### Hugo 博客项目模板

```
博客名称/
├── .claude/
│   ├── rules/                 # 博客专用规则
│   └── settings.json
├── archetypes/                 # 内容模版
│   └── default.md
├── content/                   # 文章内容
│   ├── posts/
│   ├── about/
│   └── archive/
├── layouts/                   # 模板文件
│   ├── _default/
│   ├── partials/
│   └── index.html
├── static/                    # 静态资源
│   ├── css/
│   ├── icons/
│   └── images/
├── docs/                      # GitHub Pages 发布目录
├── config.yaml
├── CLAUDE.md
└── README.md
```

---

## 三、开发流程规范

### 阶段 1：项目初始化

```
1. 创建项目目录结构
2. 初始化 .claude/ 和 CLAUDE.md
3. 从 ~/.claude/rules/ 中获取 common rules 作为基础
4. 根据工程需要添加其他专用 rules
5. 创建 README.md
6. 初始化 Git 仓库
```

**必须包含的基础 Rules（来自 ~/.claude/rules/）**：

| 规则 | 必须？ | 说明 |
|------|--------|------|
| agents.md | ✅ | Agent 编排，什么时候用什么 agent |
| code-review.md | ✅ | 代码审查标准 |
| coding-style.md | ✅ | 编码风格（不可变性、错误处理等） |
| git-workflow.md | ✅ | Git 提交规范 |
| hooks.md | ✅ | Hook 系统说明 |
| patterns.md | 建议 | 设计模式 |
| performance.md | 建议 | 性能优化 |
| security.md | 建议 | 安全检查清单 |
| testing.md | 建议 | 测试要求 |
| development-workflow.md | 建议 | 开发流程 |

**为什么必须包含 common rules？**

确保在**任何环境下**（即使没有配置过 rules 的新机器）都能有统一的开发标准。Common rules 是开发规范的基础，必须先确保它们存在。

**CLAUDE.md 必须包含**：
```markdown
# 项目名称

## 基本信息
- 技术栈
- 目录结构
- 关键配置路径

## 开发规范
- 代码风格
- Git 工作流
- 测试要求

## 常见问题
- 已解决的坑
- 注意事项

## 当前状态 / 未完成的事
- 当前状态(最新完成的三件事，每次更新覆盖)
- 未完成的事(用于重启对话后快速理解上下文)

## 参考资料
- 相关文档链接
```

### 阶段 1.5：项目需求文档

```
6. 创建 项目需求.md
```

**项目需求.md** 是需求的集中管理文档，用于在开发阶段快速理解项目背景和需求。

**必须包含的内容**：
```markdown
# 项目名称 - 需求文档

## 项目背景
- 项目目标
- 目标用户
- 核心价值

## 需求概述
- 已完成的需求
- 进行中的需求
- 计划中的需求

## 详细需求
- [ ] 需求1：描述
- [ ] 需求2：描述

## 技术约束
- 技术栈限制
- 性能要求
- 安全要求
```

**使用方式**：
1. 开发新功能前 → 先读 `项目需求.md` 理解需求背景
2. 理解需求后 → 使用 `/plan` 指令进行需求补充和分解
3. 每次需求变更 → 更新 `项目需求.md`

### 阶段 2：功能开发

```
1. 明确需求（写清 user story）
2. 规划实现步骤（使用 planner agent）
3. 遵循 Rules 执行
   - coding-style.md
   - testing.md
   - security.md
4. Hooks 自动检查
   - 格式化
   - lint
   - 测试
5. 代码审查
```

### 阶段 3：提交与部署

```
1. 确保所有 Hooks 检查通过
2. 遵循 git-workflow.md 规范提交
3. Commit 消息格式：
   <type>: <description>
   [optional body]
4. 推送后检查 CI/CD
```

---

## 四、Rules 与 Hooks 的配合模式

### 场景：写代码

| 步骤 | Rules | Hooks |
|------|-------|-------|
| 开始前 | 读取 coding-style.md | — |
| 编写中 | 遵循不可变性、错误处理规范 | — |
| 完成后 | — | PostToolUse: 格式化 |
| 提交前 | 读取 git-workflow.md | — |
| 提交时 | — | Stop: 检查测试覆盖率 |

### 场景：修复 Bug

| 步骤 | Rules | Hooks |
|------|-------|-------|
| 分析时 | 使用 tdd-guide agent | — |
| 编写测试 | 测试覆盖率 ≥ 80% | — |
| 修复代码 | 遵循规范 | — |
| 验证 | — | PostToolUse: 运行测试 |
| 提交 | 遵循 commit 规范 | — |

---

## 五、我当前的配置

### 用户级 Rules（`~/.claude/rules/`）

| 规则 | 用途 |
|------|------|
| agents.md | Agent 编排 |
| code-review.md | 代码审查 |
| coding-style.md | 编码风格 |
| development-workflow.md | 开发流程 |
| git-workflow.md | Git 规范 |
| hooks.md | Hook 系统 |
| patterns.md | 设计模式 |
| performance.md | 性能优化 |
| security.md | 安全检查 |
| testing.md | 测试要求 |

### 项目级覆写

如需在特定项目中覆写用户级规则，在 `.claude/rules/` 下创建同名文件即可。

### Hooks 配置

常用 Hooks：
- `PostToolUse` → 自动格式化
- `PreToolUse` → 安全拦截
- `Stop` → 任务完成验证

---

## 六、持续改进

### 记录踩坑

每次遇到新问题并解决后，立即更新到项目的 CLAUDE.md：
```markdown
## 常见问题
- ❌ 问题描述 → ✅ 解决方法
```

### 优化 Rules

当发现现有规范不足时：
1. 更新 `~/.claude/rules/` 中的通用规则
2. 或在项目级 `.claude/rules/` 添加专用规则

### 复用成功模式

成功的开发模式应该被记录和复用：
- 最佳实践 → 更新到 rules
- 高效工具配置 → 记录到 CLAUDE.md
- 好用的脚本 → 放到 `scripts/`

---

## 七、总结

规范使用 Claude Code 的核心：

```
模版化的目录结构     → 快速启动
标准化的开发流程     → 质量保证
Rules 定义规范       → 统一标准
Hooks 强制执行       → 落实规范
CLAUDE.md 记录上下文 → 知识沉淀
```

**目标**：每次新建工程都能快速进入状态，每次遇到问题都能在 CLAUDE.md 中找到答案，每次提交都符合规范。

---

## 相关阅读

- [AI术语笔记](/posts/ai术语笔记/) — 相关术语解释
