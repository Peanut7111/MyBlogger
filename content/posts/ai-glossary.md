---
title: "AI术语笔记"
date: 2026-04-05T18:23:59+08:00
tags: ["AI术语"]
categories: []
description: "记录AI领域常见的英文术语和缩写，便于理解和使用"
---

## AI 术语笔记

本文记录 AI 领域常见的英文术语和缩写，用简洁的语言解释概念。

---

## 核心概念

### LLM (Large Language Model)

**大型语言模型**。一种基于深度学习的神经网络，通过海量文本训练来预测下一个 token（词元）。"大"指的是参数数量（数十亿到万亿级别）和训练数据规模。

常见 LLM：GPT、Claude、Llama、DeepSeek 等。

### Token

**词元**。LLM 处理文本的最小单位。英文中 1 token ≈ 1 个单词或标点；中文中 1 token ≈ 1-2 个汉字。一个句子可能被切成几个 token，如 "Hello world" = 3 tokens。

### Context Window

**上下文窗口**。LLM 一次能处理的 token 总数上限，包括输入和输出。超过这个限制的内容会被截断或丢失。

例如：上下文窗口 128k 的模型表示最多能处理约 10 万汉字。

### Temperature

**温度参数**。控制输出随机性的参数：
- `temperature = 0`：输出几乎确定，适合精确问答
- `temperature = 0.7~1.0`：输出更多样，适合创意写作

### Hallucination

**幻觉**。LLM 生成看似合理但实际错误或不存在的信息。这是 LLM 的固有问题，而非 bug。

---

## RAG 相关

### RAG (Retrieval Augmented Generation)

**检索增强生成**。一种让 LLM 回答基于私有知识的技术：

```
用户问题 → 检索相关文档 → 拼入提示词 → LLM 生成答案
```

解决的问题：LLM 不知道私有数据（如你的笔记、企业文档）的问题。

### Vector Database

**向量数据库**。存储文本嵌入向量的数据库，通过语义相似度搜索内容。例如 Milvus、Pinecone、Chroma。

### Embedding

**嵌入/向量化**。把文本转换成数字向量的过程，相似文本有相似的向量，便于语义搜索。

### Chunking

**分块**。把长文档切成小的文本块（通常 500-1000 tokens），便于检索和高效处理。

---

## Agent 相关

### AI Agent

**AI 代理/智能体**。能够自主规划、使用工具、完成复杂任务的 AI 系统。

核心能力：
1. **感知** — 接收信息
2. **思考** — 推理和规划
3. **行动** — 调用工具执行

### MCP (Model Context Protocol)

**模型上下文协议**。Anthropic 提出的标准协议，让 AI 能安全地连接外部数据源和工具（如文件、数据库、API）。

类似 USB 接口 — 有了 MCP，AI 就像有了标准化的"接口"来访问各种外部资源。

### Tool Use

**工具调用**。LLM 通过生成特殊指令来调用外部工具（搜索、计算、API等），扩展其能力边界。

### Multi-Agent

**多智能体**。多个 AI 代理协同工作，各司其职（规划、执行、检查），完成复杂任务。

---

## Fine-tuning 相关

### Fine-tuning

**微调**。在预训练模型的基础上，用特定领域数据进一步训练，使模型适应特定任务或风格。

### LoRA (Low-Rank Adaptation)

**低秩适配**。一种高效微调技术，通过训练少量参数而不是整个模型，大幅降低微调成本。

### RLHF (Reinforcement Learning from Human Feedback)

**基于人类反馈的强化学习**。用人类偏好数据训练奖励模型，再通过强化学习优化 LLM 输出质量。

### Quantization

**量化**。把模型参数从高精度（FP32）转换为低精度（INT8/INT4），大幅减少内存占用，同时保持大部分性能。

---

## Prompt Engineering

### Prompt Engineering

**提示词工程**。设计和优化输入给 LLM 的提示词，以获得更好输出的实践。

### Few-shot / Zero-shot

**少样本/零样本学习**：
- **Zero-shot**：直接提问，不给示例
- **Few-shot**：给 1-3 个示例，帮助模型理解任务

### System Prompt

**系统提示词**。设置 AI 角色、行为规则和约束的顶层指令，通常在对话开始时输入。

---

## 模型相关

### Base Model vs Instruct Model

- **Base Model**：基础模型，能续写文本但不擅长对话
- **Instruct Model**：指令模型，经过微调能理解并执行指令

### Multimodal

**多模态**。能处理多种类型数据（文本、图片、音频、视频）的模型。

### Reasoning Model

**推理模型**。专门优化过推理能力（数学、代码、逻辑）的模型，如 GPT-o1、Claude 3.5 Sonnet。

### MoE (Mixture of Experts)

**混合专家模型**。一种模型架构，只有部分"专家"网络被激活处理每个输入，提高效率。

---

## Claude Code 相关

### Skill

在 Claude Code 中，**Skill** 是经过经验优化好的提示词文档，用于特定任务的执行代理。

一个 Skill 通常包含：
- **角色定义** — 这个 Skill 扮演什么角色（代码审查员、测试专家等）
- **执行流程** — 明确的步骤和检查点
- **输出格式** — 报告的结构、commit 格式等
- **触发条件** — 什么情况该用、什么情况不该用

通常存放于 `~/.claude/agents/` 或插件目录下，本质是一个优化好的 Markdown 提示词文件。

**Slash Commands (`/xxx`)** 是调用 Skill 的快捷入口，输入 `/skill-name` 即可触发对应的 Skill 代理执行任务。

### MCP (Model Context Protocol)

**模型上下文协议**。Anthropic 提出的标准协议，让 AI 能安全地连接外部数据源和工具（如文件、数据库、API）。

类似 USB 接口 — 有了 MCP，AI 就像有了标准化的"接口"来访问各种外部资源。

### Hooks (钩子)

**Hooks** 是 Claude Code 中的自动化机制，在特定生命周期事件触发时自动执行脚本或命令。

#### 12 个生命周期事件

| Hook 事件 | 触发时机 | 可阻止？ | 最佳用途 |
|-----------|----------|----------|----------|
| `SessionStart` | 会话开始/恢复 | 否 | 加载上下文、设置环境变量 |
| `UserPromptSubmit` | 提交提示词时 | 是 | 上下文注入、验证 |
| `PreToolUse` | 工具执行前 | 是 | 安全拦截、自动批准 |
| `PermissionRequest` | 权限请求时 | 是 | 自动批准/拒绝 |
| `PostToolUse` | 工具执行后 | 否 | 自动格式化、lint、日志 |
| `PostToolUseFailure` | 工具失败后 | 否 | 错误处理 |
| `SubagentStart` | 子代理启动时 | 否 | 子代理初始化 |
| `SubagentStop` | 子代理停止时 | 是 | 子代理验证 |
| `Stop` | Claude 停止响应时 | 是 | 任务强制完成 |
| `PreCompact` | 压缩前 | 否 | 记录备份 |
| `Setup` | `--init/--maintenance` 时 | 否 | 一次性设置 |
| `SessionEnd` | 会话终止时 | 否 | 清理、日志 |
| `Notification` | 发送通知时 | 否 | 桌面提醒、TTS |

#### Hook 类型

| 类型 | 说明 |
|------|------|
| **Command** | 运行 Shell 脚本 |
| **HTTP** | POST 到端点接收 JSON |
| **Prompt** | 使用 LLM 评估决策 |
| **Agent** | 启动带工具的子代理进行验证 |

#### 配置位置（优先级从高到低）

| 范围 | 位置 | 共享？ |
|------|------|--------|
| Managed | 系统目录 | IT 部署 |
| Local | `.claude/settings.local.json` | 否 |
| Project | `.claude/settings.json` | 是 |
| User | `~/.claude/settings.json` | 否 |

---

### Rules (规则)

**Rules** 是 Claude Code 中的提示词规则文件，定义工作流程和最佳实践。

#### Rules 文件位置

| 类型 | 位置 |
|------|------|
| 用户级 | `~/.claude/rules/*.md` |
| 项目级 | 项目根目录或 `.claude/` |

#### 内置 Rules 示例

你的 `~/.claude/rules/` 下可能已有：

- **agents.md** — Agent 编排规则，定义何时使用什么代理（planner、code-reviewer 等）
- **code-review.md** — 代码审查标准，什么时候必须审查、审查清单
- **coding-style.md** — 编码风格规范（不可变性、错误处理等）
- **git-workflow.md** — Git 工作流和 commit 格式
- **security.md** — 安全检查清单
- **testing.md** — 测试要求（80% 覆盖率等）

#### Rules 的本质

和 Skill 一样，Rules 也是经过经验优化的 Markdown 提示词文件，只是用途不同：

| | Skill | Rules |
|--|-------|-------|
| 用途 | 执行特定任务 | 定义工作流程和标准 |
| 触发 | Slash 命令 | 自动融入每次交互 |
| 内容 | 角色+流程+输出格式 | 规范+清单+检查点 |

#### Rules 工作方式

Claude Code 会在执行任务前自动读取相关 Rules 文件，把规则融入到系统提示词中。例如：
- 写代码前 → 读取 `coding-style.md`
- 提交前 → 读取 `git-workflow.md`
- 安全相关 → 读取 `security.md`

#### Hooks 与 Rules 协同工作

**Rules** = 工作标准和规范（告诉 Claude "应该怎么做"）
**Hooks** = 自动化执行机制（在特定时刻自动触发动作）

##### 配合实例

**场景：用户让 Claude 写一个新功能并提交**

| 阶段 | Rules（规范） | Hooks（自动化） |
|------|--------------|----------------|
| 写代码前 | 读取 `coding-style.md`（命名规范、不可变性） | — |
| 写代码时 | 读取 `testing.md`（要求 80% 覆盖率） | — |
| 写完代码 | 读取 `security.md`（检查敏感信息） | — |
| 代码完成后 | — | `PostToolUse`：自动运行 Prettier 格式化 |
| 提交前 | 读取 `git-workflow.md`（commit 格式） | — |
| 提交时 | — | `Stop`：检查测试覆盖率是否达标 |
| 发现问题 | — | Hook 阻止提交，要求修复 |

##### 工作流程示意

```
用户: "帮我写一个登录功能并提交"
         │
         ▼
┌─────────────────────────────────────────┐
│  阶段1: Rules 融入系统提示词             │
│  • coding-style.md → 代码规范          │
│  • testing.md → 必须有测试              │
│  • security.md → 不能暴露密码           │
└─────────────────┬───────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────┐
│  阶段2: Claude 执行任务                 │
│  • 按 Rules 写代码                      │
│  • 遵循命名规范、不可变模式            │
│  • 添加测试用例                        │
│  • 检查敏感信息                        │
└─────────────────┬───────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────┐
│  阶段3: Hooks 拦截检查                 │
│  • PostToolUse: 格式化代码            │
│  • PostToolUse: 运行 lint              │
│  • PostToolUse: 运行测试               │
│  • Stop: 验证覆盖率 ≥ 80%             │
└─────────────────┬───────────────────────┘
                  │
         ┌────────┴────────┐
         ▼                 ▼
    通过检查            未通过检查
    (Rules 遵守)       (有问题)
         │                 │
         ▼                 ▼
    提交成功         Hook 阻止提交
                   提示修复问题
```

##### 本质区别

| 组件 | 职责 | 性质 |
|------|------|------|
| **Rules** | 定义"目标是什么" | 指导原则，Claude 尽量遵循 |
| **Hooks** | 执行"如何确保达到目标" | 强制检查，可拦截操作 |

---

### CLAUDE.md

**CLAUDE.md** 是项目级的说明文件，供 AI 在该项目中快速了解上下文。

与 Rules 的区别：
- **CLAUDE.md** — 项目专属信息（项目结构、功能、使用方式）
- **Rules** — 通用的工作流程规范（适用于所有项目）

---

## 其他常见术语

| 术语 | 全称 | 解释 |
|------|------|------|
| **API** | Application Programming Interface | 程序接口 |
| **Tokens per Minute (TPM)** | — | API 调用速率限制单位 |
| **Guardrails** | — | 内容过滤，防止输出不当信息 |
| **Streaming** | — | 流式输出，边生成边显示 |
| **Benchmark** | — | 基准测试，评估模型性能的标准 |
| **Red Teaming** | — | 红队测试，故意找漏洞来改进安全 |

---

## 参考资料

- [AI/LLM Glossary: 82 Terms Every Developer Should Know](https://sph.sh/en/posts/ai-llm-glossary-developer-terms/)
- [The Glossary You Must Read If You Wanna Talk About AI](https://shiftmag.dev/the-glossary-you-must-read-if-you-wanna-talk-about-ai-8413/)
- [Google Generative AI Glossary](https://docs.cloudflare.com/docs/generative-ai-glossary/)
