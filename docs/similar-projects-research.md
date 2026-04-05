# GitHub 同类项目全面调研报告

> **目标**：全面调研 GitHub 上与 OpenHarness 同类的 Harness 学习/实现项目，对比各项目的特点与优劣，为后续学习提供指引。
>
> **更新时间**：2026-04-05

---

## 目录

1. [背景：什么是 Agent Harness？](#背景什么是-agent-harness)
2. [项目全景图](#项目全景图)
3. [A 类：Harness 架构学习教程（从零构建）](#a-类harness-架构学习教程从零构建)
   - [shareAI-lab/learn-claude-code（Python 原版）](#shareai-lablearn-claude-codepython-原版)
   - [sheng-jie/learn-cc-csharp（C# 移植版）](#sheng-jielearn-cc-csharpc-移植版)
   - [arrayadd/learn_claude_code_by_java（Java 移植版）](#arrayadlearn_claude_code_by_javajava-移植版)
4. [B 类：Claude Code 源码分析与逆向工程](#b-类claude-code-源码分析与逆向工程)
   - [dadiaomengmeimei/claude-code-sourcemap-learning-notebook](#dadiaomengmeimei-claude-code-sourcemap-learning-notebook)
   - [dadiaomengmeimei/nano-claude-code](#dadiaomengmeiminano-claude-code)
   - [ahmedk20/agentic-ai-from-claude-code](#ahmedk20agentic-ai-from-claude-code)
5. [C 类：生产级 Harness 实现（可直接使用）](#c-类生产级-harness-实现可直接使用)
   - [HKUDS/OpenHarness（本项目）](#hkudsopenharness本项目)
   - [AgentBoardTT/openharness（Harness Python SDK）](#agentboardttopenharness-harness-python-sdk)
   - [zhijiewong/openharness（TypeScript CLI）](#zhijiewongopenharnestypescript-cli)
6. [D 类：Harness 周边工具与扩展](#d-类harness-周边工具与扩展)
   - [amazinglvxw/enso-os（自进化 Hook 系统）](#amazinglvxwenso-os自进化-hook-系统)
   - [NeverSight/learn-skills.dev（技能库聚合平台）](#neversightlearn-skillsdev技能库聚合平台)
7. [横向对比矩阵](#横向对比矩阵)
8. [学习路径建议](#学习路径建议)
9. [总结与选择指南](#总结与选择指南)

---

## 背景：什么是 Agent Harness？

**Agent Harness（代理线束）** 是围绕 LLM 模型构建的完整基础设施，赋予模型"手"（工具执行）、"眼"（观察环境）、"记忆"（上下文管理）和"边界"（安全与权限）。

```
Harness = 工具（Tools）+ 知识（Knowledge）+ 观察（Observation）
        + 行动接口（Action Interfaces）+ 权限（Permissions）
```

**模型负责决策，Harness 负责执行。** 学习 Harness 工程，就是学习如何为智能模型构建高效、安全的"运行环境"。

---

## 项目全景图

| 项目 | 类型 | 语言 | ⭐ Stars | 核心定位 |
|------|------|------|---------|---------|
| [shareAI-lab/learn-claude-code](https://github.com/shareAI-lab/learn-claude-code) | 教程 | Python | ~2000+ | Harness 工程学习原版教程（12 课渐进式） |
| [sheng-jie/learn-cc-csharp](https://github.com/sheng-jie/learn-cc-csharp) | 教程移植 | C# | ~57 | learn-claude-code 的 .NET 移植版 |
| [arrayadd/learn_claude_code_by_java](https://github.com/arrayadd/learn_claude_code_by_java) | 教程移植 | Java | ~5 | learn-claude-code 的 Java 移植版 + 可视化 |
| [dadiaomengmeimei/claude-code-sourcemap-learning-notebook](https://github.com/dadiaomengmeimei/claude-code-sourcemap-learning-notebook) | 源码分析 | Markdown | ~163 | 逆向解析 Claude Code 512K 行 TS 源码 |
| [dadiaomengmeimei/nano-claude-code](https://github.com/dadiaomengmeimei/nano-claude-code) | 最小实现 | TypeScript | ~N/A | ~2300 行复刻 Claude Code 核心 |
| [ahmedk20/agentic-ai-from-claude-code](https://github.com/ahmedk20/agentic-ai-from-claude-code) | 学习指南 | TypeScript | ~113 | 10 周结构化学习路径（基于 Claude Code 源码） |
| [HKUDS/OpenHarness](https://github.com/HKUDS/OpenHarness) | 生产实现 | Python | N/A | 完整 Harness 生产实现（44x 更轻量） |
| [AgentBoardTT/openharness](https://github.com/AgentBoardTT/openharness) | 生产实现 | Python | ~5 | 含 SDK、Benchmark、企业教程的全功能 Harness |
| [zhijiewong/openharness](https://github.com/zhijiewong/openharness) | CLI 工具 | TypeScript | ~65 | 支持本地/云端任意 LLM 的轻量 CLI Harness |
| [amazinglvxw/enso-os](https://github.com/amazinglvxw/enso-os) | 周边扩展 | Shell | ~1 | 952 行 Shell Hook 驱动的自进化记忆系统 |
| [NeverSight/learn-skills.dev](https://github.com/NeverSight/learn-skills.dev) | 周边工具 | TypeScript | ~113 | Agent Skills 聚合搜索平台 |

---

## A 类：Harness 架构学习教程（从零构建）

### shareAI-lab/learn-claude-code（Python 原版）

**仓库**：https://github.com/shareAI-lab/learn-claude-code  
**语言**：Python | **定位**：Harness 工程学习首选教程

#### 项目简介

这是整个"Learn Harness"生态的源头项目。它以 Claude Code 作为参照物，通过 **12 个递进的 session（s01–s12）** 带领开发者从零构建一个完整的 AI Agent Harness。核心理念是：

> **"The model IS the agent. The code is the harness."**

不是训练模型，而是构建模型运行所需的环境。

#### 核心架构（12 课渐进）

```
s01 → 最简 Agent Loop（一个 while 循环 + Bash 工具）
s02 → 工具分派表（dispatch map）
s03 → TodoWrite 规划（让 AI 先列计划再执行）
s04 → Subagent（子代理隔离上下文）
s05 → Skills（按需加载知识文件 .md）
s06 → Context Compact（三层上下文压缩）
s07 → Task System（文件系统持久化任务图）
s08 → Background Tasks（守护线程异步执行）
s09 → Agent Teams（JSONL 邮箱多代理协作）
s10 → Team Protocols（request_id 握手协议）
s11 → Autonomous Agents（WORK/IDLE 自主认领任务）
s12 → Worktree Isolation（git worktree 目录隔离）
```

#### 核心代码模式

```python
def agent_loop(messages):
    while True:
        response = client.messages.create(
            model=MODEL, system=SYSTEM,
            messages=messages, tools=TOOLS,
        )
        if response.stop_reason != "tool_use":
            return
        results = [TOOL_HANDLERS[b.name](**b.input) for b in response.content if b.type == "tool_use"]
        messages.append({"role": "user", "content": results})
```

**每节课只在这个循环外加东西，循环本身从不改变。**

#### 优点

- ✅ **权威性强**：作为原版，被多个语言移植，社区最活跃
- ✅ **渐进式设计极佳**：每节课只加一个机制，学习曲线平滑
- ✅ **哲学深度**：从"什么是真正的 Agent"切入，建立正确心智模型
- ✅ **配套 Web 平台**：Next.js 可视化学习平台，有步进图示
- ✅ **多语言文档**：英文 / 中文 / 日文
- ✅ **范围清晰**：明确说明哪些内容被简化（如权限系统、完整 MCP），避免误导

#### 缺点

- ❌ **仅教学级代码**：不含完整权限体系、完整 MCP 运行时、会话恢复等生产功能
- ❌ **Python 依赖 Anthropic SDK**：使用 httpx 调用，对其他 LLM 提供商支持有限
- ❌ **无测试套件**：没有单元测试，仅靠运行验证

#### 适合人群

所有想学习 Harness 工程的开发者的**第一站**，不论语言背景。建议从 s01 开始，完整走完 12 课。

---

### sheng-jie/learn-cc-csharp（C# 移植版）

**仓库**：https://github.com/sheng-jie/learn-cc-csharp  
**语言**：C# (.NET 10) | **Stars**：~57

#### 项目简介

learn-claude-code 的 .NET 完整移植版，将原版 Python 异步风格（asyncio）用 C# Task/async/await 重写，使用 .NET 10 的最新语言特性（如 `required` 属性、record 类型等），同时保留原版 12 课的全部结构，并配套了每节课的深度技术文章（发布于微信公众号风格 Markdown）。

#### 核心差异

| 对比项 | Python 原版 | C# 版 |
|--------|-----------|-------|
| 异步模型 | asyncio | Task + async/await |
| HTTP 客户端 | httpx | HttpClient |
| 配置方式 | .env | appsettings.json |
| 文章深度 | 概念为主 | 含"上下文缓存经济学"等进阶文章 |

#### 优点

- ✅ **.NET 生态首选**：是目前 C# 版本中最完整的移植
- ✅ **配套文章质量高**：每课有对应深度文章，包含"为什么这样设计"的深层分析
- ✅ **支持国内代理**：明确说明支持智谱 GLM-4.7 等兼容模型，对国内开发者友好
- ✅ **与原版保持同步**：逻辑对齐，方便对照学习

#### 缺点

- ❌ **Stars 较少**：社区规模小，遇到问题较难找到支持
- ❌ **.NET 10 依赖**：部分旧环境不适用
- ❌ **无可视化平台**：相较 Java 版少了交互图表

#### 适合人群

.NET / C# 开发者，已了解 Python 原版概念、想用熟悉语言实践的开发者。

---

### arrayadd/learn_claude_code_by_java（Java 移植版）

**仓库**：https://github.com/arrayadd/learn_claude_code_by_java  
**语言**：Java 1.8 | **Stars**：~5

#### 项目简介

learn-claude-code 的 Java 1.8 移植版，**最大亮点是配套了 14 张交互式 SVG 架构图**，每节课一张，可在线浏览（无需克隆）：https://arrayadd.github.io/learn_claude_code_by_java/

全程零 AI SDK 依赖，只用 Gson + 原生 `HttpURLConnection`，极大降低了入门门槛。

#### 核心特色

- **Java 1.8 广兼容**：无 lambda，无 Stream API，适合各种 Java 环境
- **14 张交互式 SVG 图**：每节课一张，概念可视化程度最高
- **双语注释**：中文 + 英文，方便国际交流
- **每课独立 main()**：S01–S12 每个文件均可单独运行，无需理解全局

#### 优点

- ✅ **可视化最佳**：14 张交互式图表是所有移植版中独一无二的优势
- ✅ **零依赖启动**：`mvn compile` 后直接运行，不需要 pip/venv 等 Python 工具链
- ✅ **Java 企业生态**：对 Java 背景开发者极为友好
- ✅ **在线演示**：无需克隆即可查看课程图表

#### 缺点

- ❌ **Stars 极少**：社区几乎为零，维护不确定
- ❌ **Java 1.8 风格略显冗长**：相比 Python/TypeScript 版本代码更啰嗦
- ❌ **无文章配套**：深度解析文章较少

#### 适合人群

Java / Android / 大数据背景开发者，以及希望通过交互式图表辅助理解的视觉型学习者。

---

## B 类：Claude Code 源码分析与逆向工程

### dadiaomengmeimei/claude-code-sourcemap-learning-notebook

**仓库**：https://github.com/dadiaomengmeimei/claude-code-sourcemap-learning-notebook  
**语言**：Markdown | **Stars**：~163

#### 项目简介

基于 Claude Code 源码泄漏事件（npm source map 意外暴露了 512K 行 TypeScript 源码），对 Claude Code 进行深度逆向分析，提炼出**8 个章节、11 个可迁移设计模式、约 5.5 小时**的系统性学习内容。

#### 8 大章节

| 章节 | 主题 | 重点文件 | 学习时长 |
|------|------|---------|---------|
| 00 | 总览与索引 | — | 10 min |
| 01 | 全局架构 | main.tsx, App.tsx, QueryEngine.ts | 30 min |
| 02 | 工具系统 | Tool.ts, tools.ts | 45 min |
| 03 | 权限与安全 | permissions.ts, filesystem.ts | 45 min |
| 04 | Query Loop & API | query.ts, StreamingToolExecutor.ts | 50 min |
| 05 | 多代理系统 | AgentTool.tsx, runAgent.ts | 50 min |
| 06 | MCP、Skills、扩展 | mcp/client.ts, skills/ | 45 min |
| 07 | 提示词工程 | prompts.ts | 60 min |
| 08 | 语音与 Buddy | voiceStreamSTT.ts | 30 min |

#### 11 个可迁移设计模式

**来自 Query Loop（Ch.04）：**
1. Optimistic Recovery（乐观恢复）
2. Layered Degradation（分层降级）
3. State Machine + Transition Log（状态机 + 变迁日志）
4. Read-Write Lock Concurrency（读写锁并发）
5. Immutable Config Snapshot（不可变配置快照）
6. Hierarchical Cancellation（层级取消）

**来自 Multi-Agent（Ch.05）：**
7. Capability-based Security（能力型安全）
8. Cache-Friendly Forking（缓存友好 fork）
9. Deterministic Cleanup（确定性清理）
10. Star Topology Orchestration（星形拓扑编排）
11. Monotonic Permission Narrowing（单调权限收窄）

#### 优点

- ✅ **深度最高**：分析的是真实生产代码（512K 行），不是教学简化版
- ✅ **模式可迁移**：11 个设计模式有普适性（DB、K8s、微服务皆可用）
- ✅ **多学习路径**：提供快速入门、安全聚焦、代理研究、提示词研究等不同路径
- ✅ **姊妹项目 nano-claude-code**：可以运行代码验证理解

#### 缺点

- ❌ **依赖源码泄漏**：所分析的 Claude Code 源码非 Anthropic 官方开源，存在版权风险
- ❌ **TypeScript 强依赖**：需要有一定 TypeScript 基础才能深入
- ❌ **版本固化**：基于特定版本的泄漏代码，后续 Claude Code 迭代不会同步更新
- ❌ **纯阅读型**：无可运行代码，学习体验较被动

#### 适合人群

有 TypeScript 基础、想深入理解生产级 Harness 设计决策的中高级开发者。建议配合 nano-claude-code 一起学习。

---

### dadiaomengmeimei/nano-claude-code

**仓库**：https://github.com/dadiaomengmeimei/nano-claude-code  
**语言**：TypeScript | **Stars**：N/A（新项目）

#### 项目简介

sourcemap-learning-notebook 的配套实现项目，用约 2,300 行 TypeScript 复刻 Claude Code 的核心架构。同时提供 **6 个渐进式教程文件**（01–06），从 80 行最小实现到 210 行完整 6 工具代理。

#### 对比 Claude Code

| 指标 | Claude Code | nano-claude-code |
|------|-------------|-----------------|
| 源文件数 | ~1,900 | **19** |
| 代码行数 | 512,000+ | **~2,300** |
| 运行时依赖 | 50+ | **4** |
| 工具数 | 40+ | **7** |
| 运行时 | Bun | **Node.js ≥20** |

#### 6 个渐进教程

| # | 教程 | 行数 | 学到什么 |
|---|------|------|---------|
| 01 | Minimal Agent | 80 | 核心 while 循环 |
| 02 | File Tools + Streaming | 150 | 多工具 + 流式输出 |
| 03 | Permissions | 160 | 读自动/写询问安全模型 |
| 04 | Context Awareness | 170 | CLAUDE.md、Git 上下文组装 |
| 05 | REPL + Memory | 170 | 对话状态、/commands |
| 06 | Full Agent | 210 | 完整 6 工具代理 |

#### 优点

- ✅ **可运行验证**：`npx tsx tutorials/01-minimal-agent.ts` 即可跑起来
- ✅ **41 个测试**：有测试套件，覆盖 agent loop、工具、schema、compact
- ✅ **OpenAI 兼容**：支持 Kimi、DeepSeek 等 OpenAI-compatible 端点
- ✅ **教程 + 完整实现双轨**：渐进教程理解原理，src/ 模块化实现展示最佳实践

#### 缺点

- ❌ **Stars 未知**：项目较新，社区尚待建立
- ❌ **功能有限**：7 个工具 vs Claude Code 的 40+，多代理、MCP、技能系统均为简化版
- ❌ **TypeScript 门槛**：对非 JS 生态开发者不够友好

#### 适合人群

想用 TypeScript 实践、配合 sourcemap-notebook 加深理解的开发者。

---

### ahmedk20/agentic-ai-from-claude-code

**仓库**：https://github.com/ahmedk20/agentic-ai-from-claude-code  
**语言**：TypeScript | **Stars**：~113

#### 项目简介

同样基于 Claude Code 泄漏源码，提供一份 **10 周结构化学习计划**，分 5 个部分：基础（2 周）→ 工具系统（2 周）→ 代理编排（2 周）→ 高级模式（2 周）→ 实战项目（2 周+）。定位为大学课程 / 团队培训 / 自学的系统性指南。

#### 学习路径结构

```
Part 1: Fundamentals      (1-2 weeks) - 整体架构、核心概念
Part 2: Tool System       (2 weeks)   - 工具解剖、Zod 验证、权限
Part 3: Orchestration     (2 weeks)   - QueryEngine、流式处理、错误恢复
Part 4: Advanced Patterns (2 weeks)   - 多代理、上下文压缩、MCP、插件
Part 5: Practical         (2+ weeks)  - 动手项目，从零构建完整代理
```

#### 优点

- ✅ **结构化程度最高**：有明确时间表（全职 4-5 周 / 兼职 10-12 周 / 周末 12-15 周）
- ✅ **适合团队培训**：含团队学习安排（结对编程、代码审查、演讲环节）
- ✅ **适合课程使用**：明确支持大学课程（CS 毕业设计、软件工程、AI/ML 课程）
- ✅ **成果清单明确**：9 个可验证的学习成果

#### 缺点

- ❌ **本质是学习指南**：仓库本身无代码实现，主要是 Markdown 文档
- ❌ **依赖泄漏源码**：学习者需自行获取 Claude Code 源码（存在版权争议）
- ❌ **维护不确定**：Stars 约 113，但活跃度未知
- ❌ **时间成本高**：10 周投入较大，适合有专项学习计划的人

#### 适合人群

希望系统性、有计划地学习 Agent 架构的开发者；适合有明确时间安排的团队内训项目。

---

## C 类：生产级 Harness 实现（可直接使用）

### HKUDS/OpenHarness（本项目）

**仓库**：https://github.com/HKUDS/OpenHarness  
**语言**：Python + React/Ink | **Stars**：N/A（新项目）

#### 项目简介

本项目（OpenHarness）是 HKUDS 团队出品的 Claude Code 开源 Python 复刻版，43 个工具，覆盖 Claude Code 98% 的工具集，同时保留了完整的 Harness 架构（10 大子系统），并且比原版轻量 44 倍（11,733 vs 512,664 行代码）。

#### 10 大子系统

```
engine/       # 🧠 代理循环——流式工具调用、并行执行、指数退避重试
tools/        # 🔧 43 个工具——文件 I/O、Shell、搜索、Web、MCP
skills/       # 📚 技能系统——按需加载 .md 知识文件
plugins/      # 🔌 插件生态——兼容 claude-code/plugins（测试 12 个官方插件）
permissions/  # 🛡️ 权限控制——多级模式、路径规则、命令黑名单
hooks/        # ⚡ 生命周期——PreToolUse / PostToolUse 事件钩子
commands/     # 💬 54 个命令——/help, /commit, /plan, /resume...
mcp/          # 🌐 MCP——Model Context Protocol 客户端
memory/       # 🧠 记忆——持久化跨会话知识（MEMORY.md）
coordinator/  # 🤝 多代理——子代理孵化、团队协调
```

#### 与 Claude Code 对比

| 指标 | Claude Code | OpenHarness |
|------|-------------|------------|
| 代码行数 | 512,664 | **11,733** (44x 更轻) |
| 文件数 | 1,884 | **163** |
| 语言 | TypeScript | Python |
| 工具数 | ~44 | **43 (98%)** |
| 命令数 | ~88 | **54 (61%)** |
| Skills 兼容 | ✅ | ✅ anthropics/skills |
| Plugin 兼容 | ✅ | ✅ claude-code/plugins |
| 测试 | — | **114 单元 + 6 E2E 套件** |

#### 优点

- ✅ **完整度最高**：43 个工具、54 个命令、完整权限体系、完整 MCP 支持，生产可用
- ✅ **测试最完善**：114 个单元测试 + 多套 E2E，质量有保障
- ✅ **可读性强**：Python 实现（相比 TypeScript）更易于理解底层逻辑
- ✅ **插件生态兼容**：兼容 anthropics/skills 和 claude-code/plugins，可直接复用生态
- ✅ **React TUI**：与 Claude Code 相同的 React/Ink 终端 UI，交互体验完整

#### 缺点

- ❌ **新项目**：2026-04-01 发布，社区生态尚在建立
- ❌ **Python 栈**：前端（React/Ink）和后端（Python）双栈，本地安装稍复杂（需要 Node.js + Python + uv）
- ❌ **文档英文为主**：对纯中文用户有一定门槛

#### 适合人群

- 想要一个**可直接使用**的完整 Harness 实现
- 想深入阅读**清晰的 Python 代码**理解生产 Harness 架构
- 想在 OpenHarness 基础上开发自定义工具/插件/技能的开发者

---

### AgentBoardTT/openharness（Harness Python SDK）

**仓库**：https://github.com/AgentBoardTT/openharness  
**语言**：Python | **Stars**：~5

#### 项目简介

一个完整的 Harness CLI + Python SDK，支持 Claude、GPT、Gemini、Ollama 等所有主流提供商。自称在 Harness-Bench 上以 GPT-5.2 达到 100% 满分，速度比 Claude Code 快 2 倍。额外特色：**内置 SWE-bench 评测**、**异步 Steering Channel**（对话中实时注入消息）、**完整的 10 课企业教程系列**。

#### 特色功能

- **Python SDK**：可以 `import harness` 在代码中直接调用
- **Async Steering Channel**：代理执行时，可实时注入新消息改变方向
- **Harness-Bench / SWE-bench**：内置评测框架，可量化对比不同模型
- **10 课企业教程**：从入门到企业生产部署，含沙箱执行、合规审计、Policy-as-Code
- **多代理并行 API**：`spawn_parallel()` 同时运行多个子代理

#### SDK 示例

```python
import harness

async for msg in harness.run("Fix the bug in auth.py"):
    match msg:
        case harness.TextMessage(text=t, is_partial=False):
            print(t)
        case harness.Result(total_tokens=tok):
            print(f"Done ({tok} tokens)")
```

#### 优点

- ✅ **多 LLM 支持最全**：Claude / GPT / Gemini / Ollama / 任何 OpenAI 兼容端点
- ✅ **Python SDK 设计优雅**：`async for msg in harness.run(...)` 接口简洁
- ✅ **内置 Benchmark**：可量化验证代理性能（Harness-Bench + SWE-bench）
- ✅ **企业级教程完整**：10 课覆盖从入门到 CI/CD 集成、企业合规的全链路
- ✅ **Steering Channel 独特**：生产/研究场景中实时干预代理执行

#### 缺点

- ❌ **Stars 极少（~5）**：可信度存疑，Harness-Bench 100% 的声明需自行验证
- ❌ **Benchmark 自说自话**：Harness-Bench 是自定义 benchmark，非权威基准
- ❌ **维护不确定**：项目发布较新，长期维护存疑
- ❌ **文档偏英文**：对国内开发者有语言门槛

#### 适合人群

需要 **Python SDK 接口**的开发者；希望将 Harness 嵌入到更大应用中（而不仅是 CLI 使用）的工程师；以及需要 multi-provider 支持的场景。

---

### zhijiewong/openharness（TypeScript CLI）

**仓库**：https://github.com/zhijiewong/openharness  
**语言**：TypeScript | **Stars**：~65

#### 项目简介

一个轻量级 TypeScript Harness CLI，重点是**兼容任意 LLM（含本地 Ollama）**，附带独特的 **Cybergotchi**（赛博宠物）功能——一个像素风 Tamagotchi 伴侣，通过会话数据演化，增加学习趣味性。

#### 工具与命令

- **18 个工具**：涵盖 Bash、文件 I/O、Web、子代理等核心功能
- **18 个 /commands**：含 `/undo`（撤销 AI 提交）、`/cybergotchi`（养宠物）、`/model`（切换模型）
- **Git 自动提交**：每次 AI 文件修改自动 commit，附 `/undo` 一键回滚
- **Headless 模式**：`oh run "fix tests" --json` 适合 CI/CD 流水线

#### Cybergotchi 特色

```bash
oh init                    # 向导式初始化，含宠物孵化
/cybergotchi feed         # 饥饿值 +30
/cybergotchi pet          # 快乐值 +20
/cybergotchi rest         # 能量值 +40
```

18 种物种（鸭子、猫、猫头鹰、企鹅……），随会话数量进化到 Stage 2。

#### 优点

- ✅ **本地 LLM 支持好**：Ollama native，无 API key 即可启动
- ✅ **Git 集成优雅**：自动提交 + /undo 撤销，学习/实验场景非常实用
- ✅ **Cybergotchi 趣味**：独特的游戏化设计，增加持续使用动力
- ✅ **npm 一键安装**：`npm install -g @zhijiewang/openharness` 极低门槛
- ✅ **Stars 相对较高（65）**：社区较活跃

#### 缺点

- ❌ **工具数量少（18 vs 43）**：功能完整度不及 HKUDS/OpenHarness
- ❌ **Alpha 状态**：文档标注 Status: Alpha，稳定性待验证
- ❌ **功能相对基础**：无完整 MCP 运行时、无 Skills 深度整合、无完整权限规则引擎

#### 适合人群

想要**快速上手本地 LLM 代理**、喜欢趣味化学习体验的开发者；TypeScript / Node.js 背景的开发者进行工具探索。

---

## D 类：Harness 周边工具与扩展

### amazinglvxw/enso-os（自进化 Hook 系统）

**仓库**：https://github.com/amazinglvxw/enso-os  
**语言**：Shell | **Stars**：~1  
**核心定位**：952 行 Shell 驱动的代理自进化记忆系统

#### 项目简介

Enso 不是一个完整的 Harness 实现，而是一个**安装在 Claude Code（或任意 MCP 代理）上的 Hook 层**，专门解决"代理反复犯同样错误"的问题。它通过 10 个生命周期 Hook 捕获错误、蒸馏经验、注入记忆，让代理从失败中真正学习。

#### 四层架构

| 层 | Hook 数 | 功能 |
|----|---------|------|
| 🔒 Immutable Core | 3 | 物理文件验证、核心自保护、审计报告（永不演化） |
| 🧠 Learning Layer | 3 | Trace 发射、错误种子捕获、经验蒸馏（持续演化） |
| 💡 Memory Layer | 1 | 加载历史经验注入下次会话 |
| 🛡️ Guard Layer | 3 | 内存预算限制、安全扫描、维护修剪 |

#### DIKW 知识架构

```
Error → Data (error_seeds)
     → Information (raw lessons, info-layer.jsonl)
     → Knowledge (merged rules, knowledge.json)  ← 每日合并
     → Wisdom (permanent rules, wisdom.json)     ← 每周验证
```

#### 主动遗忘机制

| 机制 | 触发条件 |
|------|---------|
| Stale decay | 37 天未使用的经验自动删除 |
| LRU eviction | 超过 50 条经验时删除最旧的 |
| 容量检查 | >83% 容量时归档旧内容 |
| Trace 轮换 | 14 天以上的 trace 文件删除 |

#### 优点

- ✅ **独创性强**：自进化 Hook + DIKW 主动遗忘是该领域较新的研究方向
- ✅ **零依赖**：只需 bash + python3，兼容所有 MCP 代理
- ✅ **核心设计哲学深刻**："约束即代码，非提示词"（物理护栏 > 文字规则）
- ✅ **极轻量**：952 行 Shell，比任何框架都轻

#### 缺点

- ❌ **Stars 极少（1）**：尚处于极早期，稳定性完全未知
- ❌ **仅为 Hook 层**：不能独立使用，必须配合 Claude Code 等主 Harness
- ❌ **Shell 语言门槛**：修改/扩展需要 Shell 脚本能力
- ❌ **Benchmark 声明未验证**：README 中的"200 lines of hooks > 800 lines of prompt"等说法缺乏证据

#### 适合人群

对**代理记忆系统**和**自进化架构**有研究兴趣的开发者；想在现有代理（如 Claude Code）上叠加学习能力的工程师。

---

### NeverSight/learn-skills.dev（技能库聚合平台）

**仓库**：https://github.com/NeverSight/learn-skills.dev  
**语言**：TypeScript | **Stars**：~113  
**Web 平台**：https://www.learn-skills.dev

#### 项目简介

一个 **Agent Skills 聚合搜索平台**，从 skills.sh 等社区平台爬取 Skill 数据，生成每日更新的排行榜（全时 / 趋势 / 热门），并提供 RSS 订阅。兼容 Claude Code、Cursor、OpenClaw 等主流工具。

#### 优点

- ✅ **技能发现工具**：省去逐个搜索 GitHub 的时间
- ✅ **多语言支持**：README 支持 11 种语言
- ✅ **数据自动更新**：GitHub Actions 每日 0:00 UTC 自动爬取
- ✅ **可 self-host**：仓库包含完整爬虫代码，可自建实例

#### 缺点

- ❌ **非 Harness 本体**：仅是辅助工具，不涉及 Harness 架构学习
- ❌ **依赖第三方来源**：skills.sh 数据质量不完全可控
- ❌ **对学习帮助间接**：适合已有 Harness 基础后查找扩展技能，不适合入门

#### 适合人群

已掌握 Harness 基础、想快速找到高质量 Skills 扩展能力的开发者。

---

## 横向对比矩阵

### 功能完整度

| 功能 | learn-claude-code | nano-claude-code | HKUDS/OpenHarness | AgentBoardTT | zhijiewong |
|------|:-:|:-:|:-:|:-:|:-:|
| Agent Loop | ✅ | ✅ | ✅ | ✅ | ✅ |
| 工具系统 | ✅ (基础) | ✅ (7个) | ✅ (43个) | ✅ (10个) | ✅ (18个) |
| 权限系统 | ❌ (简化) | ✅ (简单) | ✅ (完整) | ✅ | ✅ (简单) |
| Skills | ✅ (s05) | ❌ | ✅ | ✅ | ✅ |
| Plugins | ❌ | ❌ | ✅ | ❌ | ❌ |
| MCP | ❌ (简化) | ❌ | ✅ (完整) | ✅ | ✅ (基础) |
| 多代理 | ✅ (s09-s12) | ✅ (SubAgent) | ✅ (完整) | ✅ | ✅ (基础) |
| 上下文压缩 | ✅ (s06) | ✅ | ✅ | ✅ | ✅ |
| 持久化记忆 | ✅ (s07) | ❌ | ✅ | ✅ | ✅ |
| Git 集成 | ❌ | ❌ | ✅ | ✅ | ✅ (自动提交) |
| 终端 UI | ❌ | ✅ (基础) | ✅ (React/Ink) | ✅ | ✅ (React/Ink) |
| 测试套件 | ❌ | ✅ (41个) | ✅ (114+个) | ✅ | ✅ |

### 学习价值对比

| 维度 | learn-claude-code | sourcemap-notebook | HKUDS/OpenHarness | AgentBoardTT | zhijiewong |
|------|:-:|:-:|:-:|:-:|:-:|
| 概念深度 | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ |
| 代码可读性 | ⭐⭐⭐⭐⭐ | N/A | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| 上手难度 (低=好) | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| 生产可用性 | ⭐ | N/A | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ |
| 社区活跃度 | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐ | ⭐ | ⭐⭐⭐ |
| 文档质量 | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| 中文友好度 | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐ |

---

## 学习路径建议

### 路径一：从零开始，系统学习 Harness 工程

```
Week 1-2：理论建立
  → 阅读 shareAI-lab/learn-claude-code README（建立核心心智模型）
  → 完成 s01–s04（核心循环 + 工具 + 规划 + 子代理）

Week 3-4：深化机制
  → 完成 s05–s08（技能、上下文压缩、任务系统、后台任务）

Week 5-6：多代理系统
  → 完成 s09–s12（团队、协议、自治代理、Worktree 隔离）
  → 对比阅读 HKUDS/OpenHarness 对应子系统的实现

Week 7-8：源码级理解
  → 阅读 dadiaomengmeimei/claude-code-sourcemap-learning-notebook
  → 运行 nano-claude-code 的 6 个教程，验证理解

Week 9+：生产实践
  → 在 HKUDS/OpenHarness 上开发自定义工具/技能/插件
  → 或基于 AgentBoardTT/openharness SDK 构建应用
```

### 路径二：有 Harness 基础，快速上手可用工具

```
Step 1：选择 Harness 实现
  - 需要完整功能 → HKUDS/OpenHarness（Python，最完整）
  - 需要多 LLM 支持 → AgentBoardTT/openharness 或 zhijiewong/openharness
  - 想用本地模型 → zhijiewong/openharness（Ollama native）

Step 2：找 Skills 扩展
  - 访问 learn-skills.dev 搜索所需领域技能
  - 兼容 anthropics/skills 格式，直接复制 .md 文件使用

Step 3：加深源码理解
  - 阅读 sourcemap-notebook 对应章节
```

### 路径三：特定语言学习

| 语言背景 | 推荐项目 | 原因 |
|---------|---------|------|
| Python | shareAI-lab/learn-claude-code → HKUDS/OpenHarness | 原版 + 生产实现同语言 |
| TypeScript/JS | nano-claude-code + sourcemap-notebook | 可运行 + 深度分析 |
| C# / .NET | sheng-jie/learn-cc-csharp | 唯一完整 .NET 移植 |
| Java | arrayadd/learn_claude_code_by_java | 可视化图表辅助 |
| 全栈 | 先 Python 版，再 sourcemap-notebook | 先建心智模型再看实现 |

### 路径四：研究方向（学术/系统设计）

```
1. 阅读 sourcemap-notebook 的 11 个设计模式
2. 研究 enso-os 的自进化 Hook + DIKW 记忆架构
3. 阅读 AgentBoardTT/openharness 的 Benchmark 设计
4. 深入 HKUDS/OpenHarness 的 coordinator/ 子系统（多代理协调）
```

---

## 总结与选择指南

### 一句话总结各项目

| 项目 | 一句话定位 |
|------|-----------|
| **shareAI-lab/learn-claude-code** | Harness 学习的"圣经"，任何人的第一站 |
| **sheng-jie/learn-cc-csharp** | .NET 开发者的完整移植，配套深度文章 |
| **arrayadd/learn_claude_code_by_java** | Java 移植 + 14 张交互图，视觉化学习最佳 |
| **dadiaomengmeimei/sourcemap-notebook** | 最深入的生产级源码分析，11 个迁移模式 |
| **dadiaomengmeimei/nano-claude-code** | 2300 行可运行最小实现，配合 sourcemap 使用 |
| **ahmedk20/agentic-ai-from-claude-code** | 10 周结构化学习计划，团队培训用 |
| **HKUDS/OpenHarness（本项目）** | 最完整的 Python 生产实现，43 工具 + 完整测试 |
| **AgentBoardTT/openharness** | Python SDK + 多 LLM + 企业教程，可嵌入应用 |
| **zhijiewong/openharness** | 最轻量 TypeScript CLI，本地 LLM + 赛博宠物 |
| **amazinglvxw/enso-os** | 代理自进化记忆系统的创新实验 |
| **NeverSight/learn-skills.dev** | Agent Skills 搜索发现平台 |

### 选择决策树

```
想学习 Harness 工程原理?
├─ 是 → shareAI-lab/learn-claude-code（先从 s01 开始）
│        ├─ 想要 .NET 版 → sheng-jie/learn-cc-csharp
│        ├─ 想要 Java 版 → arrayadd/learn_claude_code_by_java
│        └─ 学完后深入 → sourcemap-notebook + nano-claude-code
│
想要直接可用的 Harness 工具?
├─ 需要最完整功能（Python）→ HKUDS/OpenHarness
├─ 需要 Python SDK / 多 LLM → AgentBoardTT/openharness
├─ 需要本地模型 / 轻量 → zhijiewong/openharness
│
想研究特定方向?
├─ 代理记忆/自进化 → amazinglvxw/enso-os
├─ Skills 生态 → NeverSight/learn-skills.dev
└─ 生产架构深度分析 → sourcemap-notebook
```

---

> **推荐起点**：无论背景如何，建议从 [shareAI-lab/learn-claude-code](https://github.com/shareAI-lab/learn-claude-code) 的 `README.md` 开始阅读，建立正确的心智模型（"The model IS the agent"）后，再根据自己的语言背景和目标选择对应路径。
>
> **本项目（HKUDS/OpenHarness）的定位**：学完 learn-claude-code 的 12 课后，OpenHarness 是最好的"真实生产实现对照物"——通过阅读其 Python 代码，可以看到教程中每个机制如何在生产级代码中落地。
