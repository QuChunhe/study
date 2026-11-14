

[hello agents](https://github.com/datawhalechina/hello-agents)


哥伦比亚大学的课程： 大语言模型中的算法
地址：edoliberty.com/algorithms-in-large-language-models/

本课程涵盖了现代LLM各部分的算法层面内容，重点关注有理论基础的思路。课程主要会介绍理论/形式计算框架，在这些框架中，人们可以推导特定问题的最优算法。课程的大部分内容将用于对算法进行数学分析。

LLM是由一系列阶段组成的流水线构建而成：数据收集与过滤、分词、检索、Transformer架构本身（尤其是注意力机制）、通过随机优化进行训练、压缩（量化、稀疏性）以及在内存/延迟预算下进行推理。每个阶段都隐藏着一个或多个算法问题。本课程的重点在于 为何，而非 是什么：不是罗列当前使用的技术，而是解释优质技术之所以呈现出现有形态的根本原因。 





datawhale和sglang团队合作的《从零手搓SGLang》项目完结啦~~~  配套视频差不多这个月底也都能上线
项目地址：github.com/datawhalechina/zero-to-sglang/
这个项目带你从推理的本质出发，手搓一个 mini-sglang，再吃透真实 SGLang 的源码。

大模型已经从「训练」卷到「推理」了。应用爆发之后，推理成本和延迟成了真正的瓶颈：同样一块卡，好的推理引擎能多扛好几倍的请求。但市面上讲推理引擎的教程不多，要么只讲概念不动手，要么直接让你啃 SGLang 源码，从哪儿下手都不知道。

这门课想补上这个缺口。前半部分，我们从推理最核心的问题讲起：KV Cache 为什么要有、prefill 和 decode 差在哪、compute-bound 和 memory-bound 到底是什么意思。中间部分，带着你从零手搓一个 mini-sglang：前向、生成、KV Cache、HTTP 服务、Continuous Batching、Paged KV Cache、RadixAttention，一样一样加上去。后半部分，回到真实的 SGLang，讲清楚它那些前沿优化具体是怎么做的，最后教你怎么给 SGLang 提第一个像样的 PR






datawhale和sglang团队合作的《从零手搓SGLang》项目完结啦~~~  配套视频差不多这个月底也都能上线
项目地址：github.com/datawhalechina/zero-to-sglang/
这个项目带你从推理的本质出发，手搓一个 mini-sglang，再吃透真实 SGLang 的源码。

大模型已经从「训练」卷到「推理」了。应用爆发之后，推理成本和延迟成了真正的瓶颈：同样一块卡，好的推理引擎能多扛好几倍的请求。但市面上讲推理引擎的教程不多，要么只讲概念不动手，要么直接让你啃 SGLang 源码，从哪儿下手都不知道。

这门课想补上这个缺口。前半部分，我们从推理最核心的问题讲起：KV Cache 为什么要有、prefill 和 decode 差在哪、compute-bound 和 memory-bound 到底是什么意思。中间部分，带着你从零手搓一个 mini-sglang：前向、生成、KV Cache、HTTP 服务、Continuous Batching、Paged KV Cache、RadixAttention，一样一样加上去。后半部分，回到真实的 SGLang，讲清楚它那些前沿优化具体是怎么做的，最后教你怎么给 SGLang 提第一个像样的 PR





Aman's AI Journal – AI Primers 是一个面向 AI 研究者和工程师的开源技术知识库，系统梳理了从机器学习、深度学习到LLM及 AI Agent 的核心理论与工程实践。
网址：aman.ai/primers/ai/

内容涵盖 Transformer、Attention、MoE、RAG、模型微调、推理优化、强化学习、多模态和模型评估等主题。其特点是兼顾数学原理、模型架构、代码实现与技术演进，通过公式推导、架构图解和技术对比，帮助读者理解不同方法的设计动机、实现机制及适用场景。
网站维护者Aman Chadha是Google DeepMind，领导 Gemini 模型后训练团队，研究方向涵盖强化学习、监督微调、模型评估及 AI Agent。




「把自己的编程代理使用记录，炼成一款更懂你的本地模型」drost-ai 开源的 tinker-ai-skill，做的不是常见那种“拿点对话数据就去 SFT”的简化教程，而是一条从 Claude Code 会话记录出发，走到 LoRA 训练、权重合并、GGUF 导出、最终用 llama.cpp 本地运行的完整流水线。它面向的也不只是 Claude Code，还兼容 Codex 和 OpenCode，核心价值在于把“你平时怎么写代码、怎么调工具、怎么排错”沉淀成可训练的数据资产。仓库把流程拆成九步：采集原始 transcript、标准化、匿名化、按真实上下文长度切片、为超长会话补上 compact 后的工作上下文、按会话粒度切分训练集，再到 Tinker 上训练、抽样验模、导出 GGUF。真正有分量的地方在细节：它强调每条训练样本都要带 system prompt 和工具定义， continuation slice 不能凭空续写，token 长度必须按真实渲染器和 tokenizer 计算，评估时更该看行为而不是只看 loss；连服务阶段如果聊天模板或采样参数不一致，都可能把一个本来不错的 checkpoint 跑坏。仓库还提供合成 transcript 生成器，5 分钟就能离线跑通一遍，先验证流程，再决定是否投入真数据和训练成本。说白了，这不是“帮你一键造模型”的噱头，而是把一套踩过坑的 agent fine-tuning 方法论开源出来，让个人和小团队第一次有机会系统地复刻“把自己的工作方式教给模型”这件事。GitHub：drost-ai/tinker-ai-skill






GPU 算子优化教程 Hello GPU：从 AMD GPU 架构、ROCm 工具链到 HIP/Triton 算子优化与单卡推理性能分析的实战教程。
项目地址：github.com/datawhalechina/hello-gpu
在线阅读：datawhalechina.github.io/hello-gpu/

本教程以消费级显卡 AMD Radeon RX 9070 XT 为实验平台，带你从理解 GPU 硬件如何执行出发，学会用 benchmark 与 profiling 找到性能瓶颈，再亲手把 Element-Wise、Reduction、Softmax、GEMM、Attention、RMSNorm 等经典算子从正确基线一步步优化，最终构建一个算子优化 Agent，自动完成性能分析、优化建议、代码修改、benchmark 和报告生成。



OpenSpec 适合用 AI 写代码的开发者，把需求、方案和任务先定清楚，再让 AI 按清单实现。 #OpenSpec #AI编程 #SpecDrivenDevelopment #contextengineering #PRD #SDD #开发效率




「一本把RLHF讲透，也把“后训练”边界重新画清的书」Nathan Lambert 这本《Reinforcement Learning from Human Feedback》表面上写的是 RLHF，实际覆盖的已经是更完整的 LLM 后训练路线：先解释 RLHF 为什么出现，再顺着经典流程讲指令微调、奖励模型、拒绝采样、强化学习、on-policy distillation、direct alignment，一路补到合成数据、工具使用、角色训练、评测和开放问题，适合有一定数理背景、想系统补全方法脉络的人读。它的价值不只在“把概念讲全”，还在于作者持续把书往“post-training 手册”方向推进：2026 年网页版补了 score centering、MOPD 和 agentic post-training 示例、agentic evaluation，也重写和梳理了奖励建模部分；章节结构上还把第 12 章改成《Synthetic Data & Distillation》，说明作者自己也意识到，如今行业讨论早已不止于狭义 RLHF，而是在转向更宽的后训练框架。配套生态也做得完整：有课程、代码库、模型输出对比工具和社区讨论入口，不只是一本书，更像一套可上手、可对照、可延展的学习资源。一个细节也很能说明它的状态——网站专门列出网页版与 2026 年 7 月纸书、10 月重印之间的勘误和增补，更新一直没停，这种“活文档”气质，对变化很快的对齐研究尤其重要。整体看，如果你想理解今天 LLM 后训练到底由哪些技术拼起来，这本书很值得读；如果作者未来真出第二版，把书名也正式改成 post-training，反而会比现在更准确。 rlhfbook.com




你是否用过coding agents。

1、如何定义Spec：AI能写代码但没判断力，需要人工明确技术栈，比如前端用React还是Vue，后端用Python还是JavaScript，数据库用SQL还是NoSQL。
2、如何执行Execution：有两种模式，一是Agent走一步问人类下一步，二是让它在循环里完全自动化运行。
3、如何评估Evaluation：这是多数候选人答不上来的。需要提前定义成功标准，比如在terminal-bench打分达到95分，在speed-bench上速度达标，在accuracy上loss降到多少，才能避免Agent提前终止训练。

三、总结
回答"是否用过代码智能体"要覆盖以上三点：定义Spec、进行执行、定义成功指标。前两个AI工程技能可以在他之前的视频里找到


斯坦福CS229中的统计学习基础：从MLE到偏差-方差权衡，机器学习背后的统计逻辑




斯坦福 Stanford CS329Z教程的中文翻译稿
地址：github.com/wanghao-SunSky/cs329z-chinese
 CS329Z是一套面向 Python 开发者的 AI 智能体（Agent）自学教程。
包括练习和配套代码架构导读也都有 ​​​




2026-10-31，DeepSeek刚开源的Super-agent，跨聊天和评论交互，始终在线、自动推进，高效并行、异常自恢复。
你不用回消息、不用跟进度，只审代码差异：通过，还是驳回。
架构思路也公开了，真是啥都往外掏啊！但注意，目前还是研究原型。你愿意让AI参与维护仓库吗？




tiny-llm ，一个从零实现大语言模型推理系统的实战课程，目标是让开发者理解 vLLM 这样的推理引擎如何工作。
地址：github.com/skyzh/tiny-llm

传统 vLLM 等项目拥有大量高度优化的 CUDA 内核和复杂的工程代码，学习门槛较高。tiny-llm 采用更容易理解的方式：基于 Apple Silicon（M 系列 Mac）、MLX 框架和 Qwen3 模型，从最基础的矩阵运算开始，用 Python、C++ 和 Metal 自己实现推理算子，逐步构建完整的推理服务。




从零手写 Agent」一套很适合系统入门 Agent 的中文教程：不空谈概念，直接从最小循环写起，一步步补齐工具系统、权限、上下文管理、Skills、聊天软件接入，以及定时任务与心跳，最后做成一个能常驻、能主动找你的 Agent。内容一共分三部分，前两部分共 11 课，先手写核心，再补上 MCP、子 Agent、多 Agent、计划、记忆这些主流能力；第三部分则把 Claude Code、Codex、Pi、Grok Bot、DeepSeek Harness、OpenClaw、Hermes 等主流 Agent 拆开来看，用同一套零件对照分析，特别适合想自己动手实现、又想看懂行业方案的人。配套代码已经开源，11 课各有独立目录，还带本地网页端，可以直接在浏览器里观察 Agent 每一步是怎么运行的，学习路径很清楚，既能上手写，也能建立完整框架感。 namiai.tech/agent


https://github.com/roberto-inf/building-llm-applications  AI Applications with LangChain



按职业阶段给你梳理一下这个视频的推荐：

1、学生：选 Nano vLLM 或 Mini SGLang，代码仓小、能完整实现一个 feature，简历上要写具体性能指标，比如吞吐量达到多少 tokens/s。

2、1-2 年工程师：选 FlashInfer，它是 VLLM、SGLang、TensorRT-LLM 背后共用的 kernel 算子库，贡献后可通用，维护者友好，不需要数据中心级显卡。

3、资深工程师转行：直接上手 VLLM、SGLang 或 TensorRT-LLM 满血代码仓，从 CI 单元测试切入，做 performance test 或 accuracy test，容易被合并




视频基于Andrew Ng的观点，分享了LLM应用领域的三个可执行学习资源：

一、了解大模型基础。搞懂推理机制、预训练、微调、后训练的区别，推荐读DeepSeek V3技术报告，理解不同模型的特长，比如DeepSeek擅长数学、Nemotron适合高性能场景。

二、制作RAG应用。把大模型接入真实业务数据，解决私有信息不在互联网上的问题。半导体、金融、生物公司愿意花重金请RAG工程师，把内部资料token化后存入向量数据库。上手推荐用LangChain做一个LLM加向量数据库的小应用。

三、制作Agent应用。重点是给大模型暴露合适的工具，比如物理模拟器或编程沙盒，让模型能调用外部能力。推荐查看vLLM的Agentic API，它可以保存工具调用状态，方便在Claude和Codex之间无缝切换。

最后总结就是三条路径：读一篇论文、做一个RAG小项目、部署一个本地模型跑Agent。




电子书 Efficient LLM Inference《高效大语言模型推理》
如何让已经训练好的模型运行得更快、成本更低、支持更多并发用户。
全书共 14 章，基本覆盖了现代 LLM Inference 的核心技术栈，可以分为四个层次。
内容发群里了（原地址在google drive）：AI群  ​​​


「几何深度学习，正在从论文热点走向系统教材」Bronstein、Bruna、Cohen 和 Veličković 合著的《Geometric Deep Learning》官网已经把草稿章节长期免费公开，完整主题直接写进副标题：Grids、Groups、Graphs、Geodesics、Gauges。它不是面向少数研究者的资料堆，而是一本给学生和实践者搭入口的教材：前半部分先补齐监督学习、等变深度学习和几何归纳偏置这些底层观念，后半部分再落到图、网格、齐性空间上的群卷积、几何图等具体对象，最后再把视野推向更远处。书的野心也很明确：不是只教你几种模型，而是试着用“对称性”这条主线，把深度学习里分散的方法重新串起来。官网还同步放出了 Oxford 和 Cambridge 课程对应的讲义，说明这套内容已经不只是研究叙事，而是在真实教学中反复打磨过。数学门槛上，它没有把读者挡在门外，但也坦率说明根基离不开向量微积分、微分几何、拓扑、泛函分析、谱理论和图论；如果想系统补课，站内还推荐了 2025 年的《Mathematical Foundations of Geometric Deep Learning》。版权方面，目前在线内容是 MIT Press 2026 年正式出版前的公开草稿版，可免费阅读；如果学术引用，官网建议先引用 2021 年的 arXiv proto-book。整体看，这个站点最有价值的地方，不只是“能免费看书”，而是它把几何深度学习从零散论文、课程视频和学术名词，整理成了一条可进入、可教学、可研究的清晰路径。 geometricdeeplearning.com/book