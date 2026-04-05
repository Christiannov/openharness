# GitHub Agent Harness 学习项目全景调研报告

> 调研时间：2026-04-05 | 覆盖 30+ 个项目 | 分 5 大类别

---

## 一、总览

"Agent Harness"（智能体线束/框架）是指包裹在 LLM 之外、使其成为可工作 Agent 的完整基础设施——包括工具调用、权限控制、记忆持久化、Agent Loop、多 Agent 协调等。

本报告从 **学习 Harness 架构** 的视角出发，将 GitHub 上的相关项目分为 5 个类别进行对比分析。

---

## 二、分类对比

### 第 1 类：Claude Code 逆向/教学项目

专门拆解 Claude Code 内部实现的教育类项目。

| 项目 | Stars | 语言 | 学习价值 | 一句话特点 |
|------|-------|------|----------|-----------|
| [shareAI-lab/learn-claude-code](https://github.com/shareAI-lab/learn-claude-code) | ~3k | Python/MD | ⭐⭐⭐⭐⭐ | 12 节课从 0 到 1 拆解 Harness 每个机制，"Bash is all you need" |
| [Yuyz0112/claude-code-reverse](https://github.com/Yuyz0112/claude-code-reverse) | ~2.3k | JS/HTML | ⭐⭐⭐⭐ | 用 mitmproxy 抓包可视化 Claude Code 的 API 交互 |
| [ComeOnOliver/claude-code-analysis](https://github.com/ComeOnOliver/claude-code-analysis) | ~1k | Markdown | ⭐⭐⭐⭐ | 最全面的 Claude Code 架构逆向文档（40+ 工具、100+ 命令） |
| [dadiaomengmeimei/claude-code-sourcemap-learning-notebook](https://github.com/dadiaomengmeimei/claude-code-sourcemap-learning-notebook) | ~500 | TS/MD | ⭐⭐⭐⭐ | 结构化笔记 + nano-claude-code，提炼 11 个可迁移模式 |
| [sanbuphy/learn-coding-agent](https://github.com/sanbuphy/learn-coding-agent) | ~500 | Markdown | ⭐⭐⭐ | 研究型笔记，覆盖 spawn 模式、swarm 模式、KAIROS 等高级话题 |
| [alejandrobalderas/claude-code-from-source](https://github.com/alejandrobalderas/claude-code-from-source) | ~200 | Markdown | ⭐⭐⭐ | 补充性逆向文档 |

**推荐**：
- **入门首选**：`shareAI-lab/learn-claude-code` — 渐进式课程，12 节课覆盖完整 Harness 机制
- **看真实 API 交互**：`Yuyz0112/claude-code-reverse` — 直观理解 Agent 与 LLM 之间到底传了什么
- **查架构全貌**：`ComeOnOliver/claude-code-analysis` — 当字典用

---

### 第 2 类：从零构建 Agent 的教学项目

手把手教你写一个 Coding Agent 的项目。

| 项目 | Stars | 语言 | 学习价值 | 一句话特点 |
|------|-------|------|----------|-----------|
| [rasbt/mini-coding-agent](https://github.com/rasbt/mini-coding-agent) | ~1k | Python | ⭐⭐⭐⭐⭐ | Sebastian Raschka 出品，纯 Python 零依赖，极致可读性 |
| [SWE-agent/mini-swe-agent](https://github.com/SWE-agent/mini-swe-agent) | ~2.7k | Python | ⭐⭐⭐⭐⭐ | 100 行代码在 SWE-bench 上跑出 74%+，证明核心 loop 极简 |
| [ghuntley/how-to-build-a-coding-agent](https://github.com/ghuntley/how-to-build-a-coding-agent) | ~500 | TS/JS | ⭐⭐⭐⭐⭐ | 渐进式 Workshop，从聊天机器人到完整 Agent |
| [owenthereal/build-your-own-coding-agent](https://github.com/owenthereal/build-your-own-coding-agent) | ~200 | Python | ⭐⭐⭐⭐ | 配套书籍，章节快照可运行，700 行构建完整 Agent |
| [eddmann/my-own-coding-agent](https://github.com/eddmann/my-own-coding-agent) | ~100 | Python | ⭐⭐⭐⭐ | 事件驱动架构，自举构建（Agent 用 Agent 写自己） |
| [gerred/building-an-agentic-system](https://github.com/gerred/building-an-agentic-system) | ~300 | Markdown | ⭐⭐⭐⭐ | 两本书系列，深度分析 Amp 的架构，覆盖从单机到多用户协作 |

**推荐**：
- **最小可行 Agent**：`rasbt/mini-coding-agent` + `mini-swe-agent` — 先理解"核心 loop 其实很简单"
- **动手造轮子**：`ghuntley/how-to-build-a-coding-agent` — Workshop 格式，一步步做
- **理解架构理论**：`gerred/building-an-agentic-system` — 概念层面最深入

---

### 第 3 类：开源 Claude Code 替代/重实现

可以和 Claude Code 对照学习的完整实现。

| 项目 | Stars | 语言 | 学习价值 | 一句话特点 |
|------|-------|------|----------|-----------|
| [HKUDS/OpenHarness](https://github.com/HKUDS/OpenHarness) | ~1-3k | Python | ⭐⭐⭐⭐⭐ | **44x 轻量**，11,733 行实现 98% 功能，专为学习设计 |
| [opencode-ai/opencode](https://github.com/opencode-ai/opencode) | ~130k | Go | ⭐⭐⭐ | 支持 75+ LLM，star 最多但侧重工具使用而非教学 |
| [openclaw/openclaw](https://github.com/openclaw/openclaw) | ~320k | TypeScript | ⭐⭐⭐ | 全平台（WhatsApp/Telegram/Slack），生态最大但过于庞大 |

**推荐**：
- **学习首选**：`OpenHarness` — 唯一明确定位为"学习 Harness 架构"的完整实现，代码量可控
- **对比参考**：`opencode` 看 Go 怎么实现同样的东西

---

### 第 4 类：知名开源 Coding Agent 框架

生产级项目，适合在理解基础后深入研究。

| 项目 | Stars | 语言 | 学习价值 | 核心特点 | 状态 |
|------|-------|------|----------|----------|------|
| [OpenHands/OpenHands](https://github.com/OpenHands/OpenHands) | ~70k | Python | ⭐⭐⭐⭐⭐ | SWE-bench 50%+，software-agent-sdk 可单独学习 | 活跃 |
| [openai/codex](https://github.com/openai/codex) | ~73k | Rust | ⭐⭐⭐⭐ | OpenAI 官方，Rust 实现，沙箱安全模型 | 活跃 |
| [cline/cline](https://github.com/cline/cline) | ~60k | TypeScript | ⭐⭐⭐⭐ | VS Code 扩展，人工审批每一步操作 | 活跃 |
| [google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli) | ~98k | TypeScript | ⭐⭐⭐ | Google 方案，1M token 窗口，免费层 | 活跃 |
| [Aider-AI/aider](https://github.com/Aider-AI/aider) | ~39k | Python | ⭐⭐⭐⭐ | Git 原生（每次改动自动 commit），repo map 机制独特 | 活跃 |
| [block/goose](https://github.com/block/goose) | ~36k | Rust/TS | ⭐⭐⭐⭐ | **MCP 原生**，学 MCP 扩展模式的最佳项目 | 活跃 |
| [RooCodeInc/Roo-Code](https://github.com/RooCodeInc/Roo-Code) | ~23k | TypeScript | ⭐⭐⭐ | Cline 分叉，多 Agent "开发团队"模式 | 活跃 |
| [stitionai/devika](https://github.com/stitionai/devika) | ~19.5k | Python | ⭐⭐⭐⭐ | 有 ARCHITECTURE.md，规划优先的 Agent 设计 | 停滞 |
| [kortix-ai/suna](https://github.com/kortix-ai/suna) | ~20k | TypeScript | ⭐⭐⭐ | 全栈 Agent（浏览器+文件+部署），模块化架构 | 活跃 |
| [SWE-agent/SWE-agent](https://github.com/SWE-agent/SWE-agent) | ~19k | Python | ⭐⭐⭐⭐ | 学术标杆，ACI（Agent-Computer Interface）概念 | 活跃 |
| [plandex-ai/plandex](https://github.com/plandex-ai/plandex) | ~15k | Go | ⭐⭐⭐ | 差异沙箱模式（AI 改动隔离直到人工批准） | 停止维护 |
| [openinterpreter/open-interpreter](https://github.com/openinterpreter/open-interpreter) | ~63k | Python | ⭐⭐⭐ | LLM + exec() 的极简模式 | 活跃 |
| [stackblitz-labs/bolt.diy](https://github.com/stackblitz-labs/bolt.diy) | ~19k | TypeScript | ⭐⭐⭐ | 浏览器内全栈 Web 应用生成器 | 活跃 |
| [continuedev/continue](https://github.com/continuedev/continue) | ~32k | TypeScript | ⭐⭐⭐ | IDE 集成层，模型无关路由 | 活跃 |
| [langchain-ai/open-swe](https://github.com/langchain-ai/open-swe) | ~2k | Python | ⭐⭐⭐ | 异步云端 Agent，LangGraph 模式 | 活跃 |

**学术/研究类（有论文）**：

| 项目 | Stars | 论文 | 学习价值 | 核心贡献 |
|------|-------|------|----------|----------|
| [AutoCodeRoverSG/auto-code-rover](https://github.com/AutoCodeRoverSG/auto-code-rover) | ~3k | ISSTA 2024 | ⭐⭐⭐⭐ | AST 感知的代码搜索 + LLM 修复 |
| [OpenAutoCoder/Agentless](https://github.com/OpenAutoCoder/Agentless) | ~2k | [arXiv:2407.01489](https://arxiv.org/abs/2407.01489) | ⭐⭐⭐⭐⭐ | **反 Agent 派**：证明简单 pipeline 可匹敌复杂 Agent |
| [SWE-agent/SWE-agent](https://github.com/SWE-agent/SWE-agent) | ~19k | NeurIPS 2024 | ⭐⭐⭐⭐ | Agent-Computer Interface 概念 |
| [OpenHands/OpenHands](https://github.com/OpenHands/OpenHands) | ~70k | NeurIPS paper | ⭐⭐⭐⭐⭐ | 软件 Agent SDK + 云端异步执行 |

---

### 第 5 类：资源聚合/Awesome 列表

| 项目 | 说明 |
|------|------|
| [walkinglabs/awesome-harness-engineering](https://github.com/walkinglabs/awesome-harness-engineering) | Harness 工程最全资源列表（文章、基准、工具） |
| [walkinglabs/learn-harness-engineering](https://github.com/walkinglabs/learn-harness-engineering) | 项目制课程，以 Electron 知识库应用为载体 |
| [Picrew/awesome-agent-harness](https://github.com/Picrew/awesome-agent-harness) | Agent Harness 工程资源列表 |
| [bradAGI/awesome-cli-coding-agents](https://github.com/bradAGI/awesome-cli-coding-agents) | CLI 编码 Agent 工具目录 |

---

## 三、核心维度对比矩阵

从 **学习 Harness 架构** 的角度，按 6 个关键维度打分：

| 项目 | 代码可读性 | 架构完整度 | 文档质量 | 上手难度 | 社区活跃 | 综合推荐 |
|------|-----------|-----------|---------|---------|---------|---------|
| OpenHarness | ★★★★★ | ★★★★★ | ★★★★ | ★★★★ | ★★★ | **A+** |
| learn-claude-code | ★★★★★ | ★★★★ | ★★★★★ | ★★★★★ | ★★★★ | **A+** |
| mini-coding-agent | ★★★★★ | ★★ | ★★★★★ | ★★★★★ | ★★★ | **A** |
| mini-swe-agent | ★★★★★ | ★ | ★★★ | ★★★★★ | ★★★★ | **A** |
| how-to-build-a-coding-agent | ★★★★ | ★★★ | ★★★★ | ★★★★★ | ★★★ | **A** |
| OpenHands | ★★★ | ★★★★★ | ★★★★ | ★★ | ★★★★★ | **A** |
| claude-code-analysis | ★★★★ | ★★★★★ | ★★★★★ | ★★★★ | ★★★ | **A** |
| Agentless | ★★★★ | ★★★ | ★★★★ | ★★★★ | ★★★ | **A-** |
| aider | ★★★★ | ★★★★ | ★★★ | ★★★ | ★★★★★ | **B+** |
| goose | ★★★ | ★★★★ | ★★★ | ★★★ | ★★★★ | **B+** |
| cline | ★★★ | ★★★★ | ★★★ | ★★ | ★★★★★ | **B** |
| codex CLI | ★★★ | ★★★ | ★★★ | ★★★ | ★★★★ | **B** |

---

## 四、推荐学习路径

```
阶段 1：理解核心 Loop（1-2 天）
 ├─ rasbt/mini-coding-agent        → 纯 Python 零依赖，理解 Agent 本质
 └─ SWE-agent/mini-swe-agent       → 100 行 = 74% SWE-bench，核心 loop 就这么简单

阶段 2：系统学习 Harness 理论（3-5 天）
 ├─ shareAI-lab/learn-claude-code   → 12 节课完整拆解 Harness 每个机制
 ├─ gerred/building-an-agentic-system → 架构理论深度分析
 └─ OpenAutoCoder/Agentless         → 反面教材：不用 Agent 也能做到，理解边界

阶段 3：动手造轮子（3-5 天）
 ├─ ghuntley/how-to-build-a-coding-agent → Workshop 格式渐进构建
 └─ owenthereal/build-your-own-coding-agent → 配套书，章节快照可运行

阶段 4：研究生产级架构（持续）
 ├─ HKUDS/OpenHarness              → ★ 11K 行读完整个生产级 Harness
 ├─ ComeOnOliver/claude-code-analysis → 对照真实 Claude Code 的差异
 └─ OpenHands/OpenHands             → software-agent-sdk 模式

阶段 5：专题深入（按兴趣选）
 ├─ block/goose                    → MCP 扩展模式
 ├─ Aider-AI/aider                 → Git 原生模式 + repo map
 ├─ cline/cline                    → IDE 集成 + 权限模型
 └─ SWE-agent/SWE-agent            → ACI 概念 + 学术基准
```

---

## 五、关键洞察

1. **核心 Loop 极简，Harness 才是关键**：`mini-swe-agent` 用 100 行就跑出 74%，证明 Agent 的核心就是 `while True: call_llm → parse_tools → execute → feed_back`。真正的复杂度在 Harness 层（权限、记忆、上下文压缩、多 Agent 等）。

2. **OpenHarness 的独特定位**：它是唯一一个明确为"学习 Harness 架构"设计的完整实现。11,733 行 vs Claude Code 512,664 行，98% 功能对等，这个比例使其成为最佳学习标的。

3. **学术 vs 工程两条线**：
   - 学术线：SWE-agent → Agentless → AutoCodeRover → OpenHands（都有论文）
   - 工程线：Claude Code → OpenHarness → aider → goose（侧重生产实践）

4. **Agentless 的反直觉贡献**：它证明简单的三阶段 pipeline（定位 → 修复 → 验证）可以用 $0.34/issue 匹敌复杂 Agent，迫使你思考"什么时候需要 Agent，什么时候不需要"。

5. **MCP 正在成为标准**：goose、OpenHarness、gemini-cli 都在拥抱 Model Context Protocol，学习 MCP 扩展模式是未来趋势。

---

*本报告基于 2026 年 4 月 GitHub 公开数据，star 数为近似值。*
