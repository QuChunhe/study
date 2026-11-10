
AI.Agents.and.Harnesses.Foundations.2026.9.pdf


成熟智能体，指的是拥有完整开箱即用能力的智能体，例如多智能体协作、Skill 与 MCP 接入、Agent Loop 等各种功能。大家常见的 Claude Code、Codex、Hermes，以及国内的 Qoder、Trae 等，都属于这一类。

eepSeek Harness的底座是Cordis微内核。

开放式无边界复杂推理、深度自主思考 → Deep Agents

https://agentic.ai/best/coding-agents

git clone git@github.com:langchain-ai/langchain.git

Retrieval-Augmented Generation (RAG)

Low-Rank Adaptation (LoRA)


LLM fine-tuning

RAG and fine-tuning: RAG provides dynamic context at runtime (reducing costs and retraining needs), while fine-tuning embeds domain
knowledge into the model (improving efficiency for specialized tasks).

Instruction models  reasoning models

 Chain of Thought (CoT)


[](https://github.com/Dante-dan/pi-agent-book#1)

https://learn.shareai.run/en/  https://github.com/shareAI-lab/learn-claude-code

OpenClaude

OpenSpec

opencode

https://github.com/cordiverse/cordis

https://github.com/deepseek-ai/deepseek-harness

标准循环（也是它内部的工作方式）：
1. 探查：glob/grep/read 摸清项目结构和现有约定
2. 计划：多步任务会先列 todo
3. 实现：write/edit 改文件
4. 验证：pwsh 跑构建/测试/lint，失败了读报错再改
5. 交付：给你 diff 和验证结果

```
目标：在 <项目路径> 里加 <功能>。
验收：`<测试/构建命令>` 通过；<具体行为，如 接口返回 200 且含字段 x>。
约束：先读 <目录> 再动手；不要改 <某文件>；沿用现有代码风格。
```

```
~/.dsh/profiles/desktop/
├── package.json        # 声明 bundles：dsh-base + dsh-web-app
├── cordis.yml          # 根层，空的，别动
└── cordis.patch.yml    # ← 你的层：改模型、改 UI、开关插件都写这里
```


[Spec 开发模式：完整技术指南](https://niziming.github.io/2026/03/24/Spec%E6%A8%A1%E5%BC%8F%E5%BC%80%E5%8F%91/)

Spec 开发模式（Specification-Driven Development） 是一种以"规格说明文档"（Spec）为核心驱动力的软件开发方法论。


Spec（Specification）是 Spec 开发模式中的核心产物。它是一份结构化的文档，精确描述了一个功能、模块或系统的行为、约束和验收标准。

Spec 驱动开发的核心原则

原则一：Spec First（规格先行）。在编写任何代码之前，必须先有对应的 Spec。


原则二：Spec as Contract（规格即合约）
Spec 是人类与 AI 之间的正式合约。


原则三：Incremental Specification（增量式规格定义）
Spec 不需要一次性完美，可以逐步细化。


原则四：Verifiable Specification（可验证的规格）

每一条 Spec 都必须是可验证的。

    避免模糊性描述（“系统应该很快”）
    使用具体的量化指标（“API 响应时间 < 200ms”）
    定义明确的验收标准（Given-When-Then 格式）

原则五：Context is King（上下文为王）

Spec 必须包含足够的上下文，使 AI 无需猜测。


OpenSpec

```
### Scenario: 有效凭据
- GIVEN 用户具有有效凭据
- WHEN 用户提交登录表单
- THEN 返回 JWT 令牌
- AND 用户被重定向到仪表板
```